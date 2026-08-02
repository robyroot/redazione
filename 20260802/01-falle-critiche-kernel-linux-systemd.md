---
title: "Allarme kernel Linux: due falle da CVSS 9.8 e 9.4 mettono a rischio quasi ogni sistema (e c'è pure systemd)"
rilevanza: "ALTA"
fonte: "https://www.techveda.live/2026/07/25/linux-kernel-cves-25-jul-2026/"
data_notizia: "2026-08-02"
tags: ["linux kernel", "sicurezza", "cve", "systemd", "vulnerabilità"]
livello: "intermediate"
nota_editoriale: |
  Angolo per RobyRoot: spiegare bene perché una vulnerabilità IPv6/RPL riguarda anche chi non ha
  mai sentito parlare di reti mesh IoT (il codice è compilato di default in quasi ogni kernel
  generico). Buona occasione per un mini-tutorial "come controllare la propria versione del kernel
  e capire se sei esposto" e per ricordare l'importanza degli aggiornamenti automatici su desktop
  Linux, non solo sui server. Taglio pratico, poco allarmistico.
---

Se pensavi che Linux fosse "quello sicuro" e potessi rimandare gli aggiornamenti all'infinito, questa settimana ti tocca ricrederti un attimo. Nell'ultimo giro di patch del kernel sono spuntate due vulnerabilità davvero serie, con punteggi CVSS che fanno venire i brividi: 9.8 e 9.4 su 10. E come se non bastasse, anche systemd — il "cuore" che avvia praticamente ogni distribuzione moderna — ha il suo bel bug da sistemare.

Partiamo dalla più inquietante: **CVE-2026-63984**, un buffer overflow nel decompressore dell'header RPL (Routing Protocol for Low-power and lossy networks) di IPv6, con CVSS 9.8. RPL è il protocollo pensato per le reti mesh a basso consumo, tipo quelle usate da sensori IoT e dispositivi 6LoWPAN. Il problema è che il supporto RPL è compilato di default in quasi tutti i kernel generici delle distribuzioni mainstream, anche se non hai mai configurato una rete IoT in vita tua. Questo significa che il tuo sistema elabora comunque gli header RPL in arrivo — e un pacchetto IPv6 malformato può bastare per corrompere la memoria del kernel, senza bisogno di autenticazione né di alcuna azione da parte tua. Bug di questo tipo, in gergo, si chiamano "zero-click" e sono i più temuti perché non serve che l'utente clicchi o apra nulla: basta essere raggiungibili in rete.

Poco dietro c'è **CVE-2026-64024**, una falla nello stack TCP con CVSS 9.4, anche questa sfruttabile da remoto e applicabile praticamente a ogni host connesso a Internet. A completare il quadro c'è **CVE-2026-63938**, un bug nella gestione delle VM con AMD SEV (Secure Encrypted Virtualization) su KVM, con CVSS 9.3: qui il rischio riguarda soprattutto chi gestisce infrastrutture cloud o virtualizzate, dove una macchina virtuale malevola potrebbe in teoria "scappare" verso l'host.

E poi c'è il capitolo systemd. **CVE-2026-29111** riguarda udev, il componente che gestisce l'hardware e i device node: in certe condizioni, un dispositivo malevolo collegato al sistema può inviare dati che udev interpreta male, arrivando — nei casi peggiori — all'esecuzione di codice arbitrario come root. Sulle versioni più vecchie di systemd (v249 e precedenti) il problema si traduce in un vero e proprio stack overwrite con contenuto controllato dall'attaccante; sulle versioni più recenti, nella peggiore delle ipotesi il sistema va in crash (un classico denial of service). Ubuntu ha già rilasciato le patch per 22.04, 24.04 e 25.10.

Perché dovrebbe interessarti tutto questo, anche se non gestisci un server esposto su Internet? Perché la superficie d'attacco è più ampia di quanto sembri: router, NAS, dispositivi embedded, macchine WSL2 su Windows, VM su Azure e qualunque cosa giri un kernel Linux relativamente recente con lo stack di rete abilitato è potenzialmente coinvolta. E il bug systemd tocca anche l'uso quotidiano su desktop, dato che udev gestisce ogni volta che colleghi una chiavetta USB o un dispositivo qualsiasi.

**Cosa fare, in pratica.** Prima cosa: aggiorna. Se usi una distro con supporto attivo (Ubuntu, Fedora, Debian stable, openSUSE, Arch), i pacchetti del kernel e di systemd con le patch sono già in arrivo o disponibili nei repository ufficiali — basta un classico `sudo apt update && sudo apt upgrade` o l'equivalente della tua distro. Se gestisci server o infrastrutture critiche, non aspettare la prossima finestra di manutenzione: qui parliamo di CVSS vicini al massimo, roba da patchare appena possibile. Su router e dispositivi IoT con firmware Linux personalizzato, invece, spesso l'unica soluzione è aspettare (e sollecitare) l'aggiornamento del produttore — un altro promemoria di quanto sia fragile l'ecosistema IoT quando si parla di manutenzione a lungo termine.

Nel frattempo, Linux 7.2 sta arrivando in versione stabile ad agosto (siamo già alla rc3), e la buona notizia è che gran parte di questi fix per la sicurezza di rete sono già stati integrati nel ramo di sviluppo. Restare aggiornati, insomma, non è mai stato un'opzione: è la prima linea di difesa.
