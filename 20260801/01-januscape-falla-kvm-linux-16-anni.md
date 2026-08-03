---
title: "Januscape: la falla KVM che dorme nel kernel Linux da 16 anni (e ora è stata svegliata)"
rilevanza: "ALTA"
fonte: "https://thehackernews.com/2026/07/16-year-old-linux-kvm-flaw-lets-guest.html"
data_notizia: "2026-08-01"
tags: ["linux", "kernel", "kvm", "cybersecurity", "virtualizzazione", "cloud"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: puntare sul contrasto tra l'età del bug (introdotto nel 2010, quando avevamo ancora Windows XP diffuso) e la sua estrema attualità nel 2026, epoca di cloud multi-tenant e nested virtualization ovunque. Buon gancio anche per un pezzo "come proteggere il tuo homelab/server KVM" collegato. Vale la pena spiegare bene cos'è lo shadow paging per i lettori meno esperti, senza scendere troppo nei tecnicismi del codice.
---

Se gestisci anche solo una manciata di macchine virtuali su Linux con KVM, questa è una di quelle notizie da leggere fino in fondo. Si chiama **Januscape**, ha un nome che sembra uscito da un film di spionaggio, ed è una vulnerabilità che si nascondeva nel kernel Linux da **sedici anni** — dal lontano agosto 2010, quando venne introdotto il commit che l'ha causata. Il CVE ufficiale è **CVE-2026-53359**.

## Cosa fa, in parole povere

KVM (Kernel-based Virtual Machine) è il sistema di virtualizzazione integrato nel kernel Linux, quello che sta dietro a mezzo cloud del pianeta: se hai mai avviato una VM su un server Linux con QEMU/KVM, l'hai usato senza saperlo. Per far funzionare la virtualizzazione annidata (una VM dentro un'altra VM, tecnica comune nei cloud provider e in certi setup di sviluppo), KVM tiene una sorta di "copia ombra" delle tabelle di memoria della macchina guest, per tracciare cosa punta dove. È il cosiddetto **shadow paging**.

Il problema è che, quando queste pagine ombra vengono riutilizzate, KVM le abbinava soltanto guardando l'indirizzo di memoria, **ignorando il tipo di pagina**. Risultato: in certe condizioni, il kernel finisce per confondersi su cosa sia realmente in memoria in quel punto. Nella maggior parte dei casi il kernel se ne accorge e va in panic per proteggersi — fastidioso, ma non catastrofico, "solo" un denial of service. Nel caso peggiore, però, un attaccante che ha già accesso root **dentro** la macchina virtuale guest riesce a scrivere in un'area di memoria che il kernel host crede libera, aprendo la strada all'esecuzione di codice arbitrario **sull'host**. Tradotto: da dentro una VM si può, in teoria, prendere il controllo del server fisico che la ospita e di tutte le altre VM che ci girano sopra.

Il ricercatore che l'ha scovata, **Hyunwoo Kim**, l'ha dimostrata come zero-day dentro kvmCTF, il programma di bug bounty di Google che per una fuga completa da VM offre fino a 250.000 dollari. Non è nemmeno la sua prima scoperta di questo tipo negli ultimi due mesi: prima di Januscape c'erano già state Dirty Frag e ITScape, segno che c'è del lavoro sistematico di scavo nel codice legacy di KVM.

## Chi rischia davvero

Per essere chiari: questa non è una falla che chiunque può sfruttare da remoto senza credenziali. Serve **accesso root dentro una VM guest** e la **virtualizzazione annidata attiva** sull'host. Questo restringe il bersaglio principale a due categorie: i **cloud provider multi-tenant** che ospitano macchine virtuali di clienti diversi sullo stesso hardware fisico, e chiunque offra ambienti "VM dentro VM" (pensa a certi laboratori di sicurezza, servizi CI/CD cloud, o piattaforme di hosting che permettono di girare hypervisor annidati). Se hai un paio di VM personali sul tuo NAS o homelab senza nested virtualization abilitata, il rischio pratico è decisamente più basso — ma vale comunque la pena aggiornare.

## La patch e cosa fare

La buona notizia è che il fix è già arrivato, ed è sorprendentemente piccolo: **una sola riga di codice** aggiunta alla funzione che decide se riutilizzare una pagina ombra, che ora controlla anche il tipo di pagina (`role.word`) oltre all'indirizzo. Il commit è stato integrato nel mainline il 19 giugno 2026, e le versioni stabili patchate — 7.1.3, 6.18.38, 6.12.95, 6.6.144, 6.1.177, 5.15.211 e persino la vecchissima 5.10.260 — sono uscite il 4 luglio. Debian ha rilasciato il proprio avviso di sicurezza (DSA-6381-1) il giorno dopo.

Cosa fare, in ordine di priorità:

1. **Aggiorna il kernel** appena possibile sugli host che eseguono KVM con nested virtualization, specialmente se sono cloud multi-tenant.
2. Se non puoi patchare subito, **disabilita la virtualizzazione annidata** come mitigazione temporanea: basta impostare `kvm_intel.nested=0` (Intel) o `kvm_amd.nested=0` (AMD) e ricaricare il modulo.
3. Se gestisci un'infrastruttura cloud o offri hosting KVM a terzi, trattala come una **priorità di patching altissima**: esiste già un proof-of-concept pubblico capace di causare un crash affidabile dell'host in pochi secondi o minuti di "gara" (race condition), usando solo un modulo kernel caricabile dentro la guest.

Il fatto che un bug del genere sia rimasto silenzioso per sedici anni in uno dei sottosistemi più critici e più controllati del kernel Linux dice molto su quanto sia difficile, anche per un progetto maturo come Linux, stanare tutti i fantasmi nel codice legacy. Buon motivo in più per tenere sempre aggiornati i propri host di virtualizzazione, anche quando "tanto funziona da anni".
