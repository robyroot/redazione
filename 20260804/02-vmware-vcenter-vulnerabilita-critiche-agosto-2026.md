---
title: "vCenter nel mirino: tre falle critiche VMware permettono di bypassare il login e scappare dalla VM"
rilevanza: "ALTA"
fonte: "https://thehackernews.com/2026/07/three-critical-vmware-flaws-allow-auth.html"
data_notizia: "2026-08-04"
tags: ["cybersecurity", "vmware", "vulnerabilità", "virtualizzazione", "CVE"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato: molti lettori RobyRoot non gestiscono infrastrutture VMware enterprise, ma tanti hanno un homelab con ESXi. Vale la pena tagliare il pezzo su due livelli: allarme per chi amministra vCenter in azienda, e promemoria più leggero per gli homelabber ("controlla la versione del tuo ESXi"). Buon gancio anche per parlare di segmentazione di rete e perché il "network access" da solo non deve mai bastare per fidarsi di un servizio di gestione.
---

Se in azienda (o nel vostro homelab più ambizioso) gestite infrastrutture virtualizzate con VMware, questa è una di quelle notizie da non scrollare via distrattamente. Broadcom ha rilasciato patch per tre vulnerabilità critiche che riguardano vCenter Server ed ESXi, e la combinazione dei tre problemi è particolarmente sgradevole: si va dal bypass completo dell'autenticazione fino alla fuga da una macchina virtuale verso l'host fisico.

Partiamo dal capire perché questa notizia conta. **vCenter** è il pannello di controllo centrale con cui si gestiscono interi cluster di server virtualizzati: chi ne prende il controllo, in pratica, prende il controllo di tutta l'infrastruttura che ci gira sopra — macchine virtuali, storage, rete, backup. Non è un dettaglio da poco.

## Le tre vulnerabilità

**CVE-2026-59309** è un bypass di autenticazione nel VMware Directory Service, il componente che gestisce identità e permessi dentro vCenter. Il punteggio CVSS è 9.8 su 10, il massimo della scala per severità pratica: un attaccante con semplice accesso di rete a vCenter — senza nemmeno credenziali valide — può aggirare i controlli di autenticazione e ottenere accesso non autorizzato al sistema. Broadcom è chiara: non esistono workaround, l'unica difesa è applicare la patch.

**CVE-2026-59310**, sempre con CVSS 9.8, è una vulnerabilità di directory traversal che, combinata con l'accesso ottenuto tramite la prima falla, permette l'esecuzione di codice arbitrario da remoto. In pratica, le due vulnerabilità possono essere incatenate: prima si entra senza credenziali, poi si esegue codice a piacere sul server.

**CVE-2026-47876** è leggermente diversa nella meccanica ma non meno seria: è una scrittura fuori dai limiti (out-of-bounds write) nell'adattatore di rete virtuale **VMXNET3** usato da ESXi, con CVSS 9.3. Qui serve già un accesso con privilegi amministrativi dentro una macchina virtuale, ma da lì un attaccante può sfruttare il bug per "scappare" dalla VM ed eseguire codice direttamente sull'host ESXi sottostante — quello che in gergo si chiama VM escape, uno degli incubi peggiori per chi fa virtualizzazione, perché rompe il presupposto stesso di isolamento tra macchine virtuali diverse.

## Chi è a rischio e cosa fare

I prodotti coinvolti includono VMware Cloud Foundation, vSphere Foundation, vCenter Server, ESXi, oltre alle varianti Telco Cloud Platform e Telco Cloud Infrastructure. Le versioni corrette sono:

- vCenter/Cloud Foundation/vSphere Foundation 9.1.x → fix in 9.1.0.0300
- versioni 9.0.x → fix in 9.0.2.0100
- vCenter 8.0 → fix in Update 3k
- Cloud Foundation 5.x → patch asincrona verso 8.0 U3k
- ESXi → build 9.1.0.0200-25557999, 9.0.2.0100-25595025 o ESXi80U3k-25595708 a seconda della versione

Broadcom ha classificato l'aggiornamento come "emergency change requiring immediate action", la categoria più alta di urgenza che usano per le patch. Al momento non risultano exploit attivi in circolazione né scansioni di massa che sfruttino queste falle, ma con un CVSS 9.8 e senza workaround disponibili, è solo questione di tempo prima che qualcuno ci provi: vulnerabilità di questo tipo, una volta pubblico il dettaglio tecnico, vengono tipicamente reverse-engineerate ed exploitate nel giro di giorni, non settimane.

## Il consiglio pratico

Se gestite vCenter in produzione, la priorità è patchare subito, senza aspettare la prossima finestra di manutenzione ordinaria — non è la classica vulnerabilità "da mettere in coda". Nel frattempo, se per qualche motivo non potete aggiornare immediatamente, limitate il più possibile l'esposizione di rete di vCenter: nessuna interfaccia di gestione di questo tipo dovrebbe mai essere raggiungibile da reti non fidate o, peggio, da internet.

E se avete un homelab con ESXi per giocare con macchine virtuali o testare distro Linux, non pensate "tanto sono solo io": anche un'istanza esposta per comodità su una porta forwardata dal router è un bersaglio valido. Controllate la versione installata e aggiornate quando potete: la sicurezza della virtualizzazione, in fondo, vale anche a scala di un armadietto con dentro un mini-PC.
