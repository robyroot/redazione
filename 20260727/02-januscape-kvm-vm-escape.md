---
title: "Januscape: il bug KVM che permette di scappare dalla virtual machine (e dormiva da 16 anni)"
rilevanza: "MEDIA"
fonte: "https://thecyberexpress.com/cve-2026-53359-januscape/"
data_notizia: "2026-07-27"
tags: ["linux", "kvm", "virtualizzazione", "cloud", "sicurezza"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato: pubblico più tecnico (sysadmin, chi usa Proxmox/hosting
  KVM in self-hosting). Vale la pena spiegare bene la differenza tra "host
  crash" (il worst case pubblico documentato) e "guest-to-host escape" (lo
  scenario peggiore in teoria possibile), per non generare allarmismo
  ingiustificato ma comunque spingere a patchare gli hypervisor.
---

Chi si occupa di self-hosting con **Proxmox**, KVM o QEMU ha probabilmente già sentito parlare di **Januscape**, la vulnerabilità che negli ultimi giorni ha tenuto svegli parecchi sysadmin. Il nome tecnico è **CVE-2026-53359** e riguarda un pezzo di codice del kernel Linux condiviso da Intel e AMD nella gestione della virtualizzazione: la **shadow MMU** di KVM. E anche qui, come per altri bug di cui abbiamo parlato di recente, il problema si nascondeva da un'eternità: circa **16 anni**.

## Come funziona l'attacco

Per capire Januscape serve un minimo di contesto su come funziona la virtualizzazione hardware. Quando una macchina virtuale gira su un host KVM, il kernel deve tradurre gli indirizzi di memoria "visti" dal guest in indirizzi fisici reali sull'host, tramite delle strutture chiamate "shadow page". Per efficienza, KVM tiene una cache di queste pagine e le riusa quando può.

Il bug sta proprio qui: in certe condizioni, KVM riutilizza una shadow page già in cache **senza verificare che il suo "ruolo" corrisponda ancora** alla mappatura che sta effettivamente costruendo. Un guest malevolo può sfruttare questa disattenzione per convincere KVM a riusare una pagina che punta a memoria che nel frattempo è stata liberata — di nuovo, una use-after-free, lo stesso pattern di bug che sta emergendo con sorprendente frequenza nel kernel negli ultimi mesi.

Il risultato documentato e riproducibile pubblicamente è, nella peggiore delle ipotesi confermate, un **crash dell'host**. Ma la ricerca che ha portato alla scoperta del bug descrive anche uno scenario ben più serio: una **guest-to-host escape** completa, cioè codice eseguito dentro una macchina virtuale malevola che finisce per girare **come root sull'host** che la ospita. È lo scenario da incubo per chiunque offra hosting VPS o servizi cloud multi-tenant: un cliente con una VM potrebbe, in teoria, prendere il controllo dell'intera macchina fisica e di tutte le altre VM che ci girano sopra.

## Chi l'ha scoperta e quanto vale

A trovare Januscape è stato il ricercatore **Hyunwoo Kim** (noto come @v4bel), che l'ha dimostrata come zero-day nell'ambito del programma **KVMCTF** di Google — lo stesso tipo di bug bounty che per una guest-to-host escape completa arriva a pagare fino a **250.000 dollari**. Il bug colpisce sia sistemi **Intel che AMD** su architettura x86, il che lo rende trasversale rispetto al tipo di hardware usato.

La patch principale è stata integrata nel kernel mainline a giugno 2026 (commit 81ccda30b4e8), ma c'è un dettaglio tecnico che vale la pena sottolineare: **serve anche una seconda correzione**, relativa a un bug collegato (CVE-2026-46113, anch'esso nella shadow paging di KVM/x86, con CVSS 8.8), perché la sola patch di Januscape non chiude completamente il problema. Chi aggiorna solo parzialmente rischia di sentirsi al sicuro senza esserlo davvero.

## Cosa fare se gestisci host KVM

Se hai un hypervisor Proxmox, una piattaforma KVM/QEMU casalinga per homelab, o gestisci VM su infrastrutture basate su Linux:

- **Aggiorna il kernel host** all'ultima versione stable o LTS della tua distribuzione, assicurandoti che includa entrambe le patch (Januscape e la CVE-2026-46113 collegata).
- Se usi **Proxmox**, controlla il changelog degli ultimi aggiornamenti del kernel PVE: diversi provider e la community hanno già documentato campagne di patching su larga scala proprio per questo bug.
- **Non fidarti solo dell'isolamento delle VM**: se ospiti VM di terzi (o comunque non completamente fidate), questo genere di bug è esattamente il motivo per cui l'hypervisor va tenuto aggiornato con la stessa priorità di un server esposto su internet.
- Monitora i log per crash anomali delle VM: anche solo il "worst case documentato" (host crash) è un problema serio per la disponibilità del servizio.

Januscape non fa notizia quanto un ransomware, ma per chi vive di virtualizzazione è probabilmente uno dei bug più rilevanti dell'anno: un promemoria che anche i pilastri più "maturi" dell'infrastruttura Linux, come KVM, possono nascondere sorprese vecchie di un decennio e mezzo.
