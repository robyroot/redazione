---
title: "Januscape: la falla KVM che fa scappare le macchine virtuali (e minaccia il cloud)"
rilevanza: "ALTA"
fonte: "https://thehackernews.com/2026/07/16-year-old-linux-kvm-flaw-lets-guest.html"
data_notizia: "2026-07-22"
tags: ["linux", "kvm", "virtualizzazione", "cloud", "sicurezza"]
livello: "intermediate"
nota_editoriale: |
  Angolo utile per RobyRoot: pubblico homelab/Proxmox oltre che sysadmin cloud — molti
  lettori del blog fanno girare VM in nested virtualization per test e non pensano al
  rischio finché non gli si spiega in concreto cosa significa "guest-to-host escape".
---

Se GhostLock (di cui parliamo in un altro articolo di oggi) è una minaccia per chi condivide un server, Januscape (CVE-2026-53359) alza la posta e punta dritto al cuore del cloud computing: le macchine virtuali. Anche questa è una falla vecchia — sedici anni, dal commit di agosto 2010 nel kernel 2.6.36 — e resta nascosta nel codice "shadow MMU" di KVM, l'hypervisor open source integrato nel kernel Linux che fa girare gran parte delle VM del pianeta, da AWS a Google Cloud fino al tuo homelab con Proxmox.

Spiegazione semplice: quando una VM gira sopra KVM, l'hypervisor tiene traccia della sua memoria tramite delle "pagine ombra" (shadow page), una sorta di mappa che tiene sincronizzata la memoria virtuale del guest con quella fisica dell'host. Il problema sta in come queste pagine vengono riutilizzate: il sistema le abbina guardando solo l'indirizzo di memoria, ignorando completamente di che tipo di pagina di tracciamento si tratta. È come se un magazziniere rimettesse a posto uno scatolone guardando solo lo scaffale e non l'etichetta: prima o poi mischia il contenuto.

Questo mix-up corrompe lo stato delle shadow-page nel kernel host, causando uno scrambling dei record su chi possiede cosa. A seconda di come viene sfruttato, il risultato può essere "solo" un kernel panic — il proof-of-concept pubblico si ferma a questo punto — oppure, in teoria, esecuzione di codice con privilegi root sull'host: un guest malevolo che scappa dalla sua VM e prende il controllo della macchina fisica che la ospita. Non è un dettaglio da poco: è la differenza tra "il mio sito è andato giù" e "qualcuno ha appena messo le mani su tutte le VM dei miei vicini di hosting".

La particolarità di Januscape è che colpisce sia i sistemi Intel che AMD con lo stesso comportamento, rendendolo — a detta del ricercatore che l'ha scoperto — il primo exploit guest-to-host verificato su entrambe le architetture x86. Per essere sfruttata servono due condizioni: accesso root all'interno della VM guest e la virtualizzazione annidata (nested virtualization) attiva sull'host. Questo restringe un po' il bersaglio, ma non abbastanza da stare tranquilli: molti provider cloud e piattaforme CI abilitano la nested virtualization proprio per permettere ai clienti di far girare a loro volta VM o container dentro le VM che affittano. E su alcune distribuzioni come RHEL, dove il device `/dev/kvm` ha permessi 0666 (accessibile a chiunque), la falla diventa sfruttabile anche come semplice escalation di privilegi locale, senza bisogno di essere dentro una VM.

Chi l'ha trovata è Hyunwoo Kim, ricercatore di sicurezza che l'ha segnalata attraverso kvmCTF, il programma di bug bounty di Google che funziona un po' come una CTF permanente e paga fino a 250.000 dollari per una fuga completa guest-to-host. Non è la sua prima scoperta dell'anno: è la terza in due mesi, dopo Dirty Frag a maggio e ITScape su ARM64 a giugno — segno che il codice di virtualizzazione del kernel sta ricevendo un'attenzione, decisamente giustificata, senza precedenti.

La buona notizia è che il fix è già arrivato, con l'aggiunta di un controllo extra nella funzione `kvm_mmu_get_child_sp()` che verifica anche il "ruolo" della pagina, non solo il suo indirizzo. Le versioni stabili corrette dal 4 luglio 2026 includono 7.1.3, 6.18.38, 6.12.95, 6.6.144, 6.1.177, 5.15.211 e 5.10.260. Se non puoi aggiornare subito, la mitigazione temporanea è disabilitare la nested virtualization con `kvm_intel.nested=0` o `kvm_amd.nested=0`, a seconda della CPU.

Se gestisci un host KVM — che sia un server di produzione, un cluster Proxmox o anche solo una macchina di test con virtualizzazione annidata attiva per provare qualche distro dentro un'altra VM — questo è uno di quegli aggiornamenti da non rimandare al mese prossimo.
