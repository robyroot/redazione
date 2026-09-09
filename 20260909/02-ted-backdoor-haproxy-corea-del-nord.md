---
title: "«ted»: la backdoor nordcoreana che si nasconde dentro HAProxy"
rilevanza: "ALTA"
fonte: "https://www.rapid7.com/blog/post/tr-dprk-apts-ted-backdoor-curlrat-target-south-korean-media-automotive-sectors/"
data_notizia: "2026-09-09"
tags: ["cybersecurity", "linux", "apt", "supply-chain", "haproxy"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato: non fare cronaca dell'APT, ma usare il caso per parlare di
  fiducia nel software che gira sui nostri server di frontiera. Il punto forte per
  RobyRoot e' il tema "compilare da sorgente non basta": build riproducibili,
  firma dei pacchetti, monitoraggio dell'integrita' del filesystem. Chiudere con
  consigli pratici per chi ha HAProxy esposto. Collegabile al pezzo sui CVE del
  kernel per il filo conduttore "di chi ci fidiamo".
---

Ogni tanto salta fuori una storia di sicurezza che vale la pena raccontare non per l'allarme immediato, ma per la lezione che lascia. E' il caso di "ted", una backdoor per Linux scoperta dai ricercatori di Rapid7 Labs e usata in una campagna di spionaggio contro aziende sudcoreane dei settori automotive e media.

La parte interessante e' dove si nasconde. "ted" non e' un processo separato che gira di fianco al software legittimo: e' un plugin scritto per HAProxy, il popolarissimo load balancer open source, e viene compilato direttamente dentro il codice sorgente di HAProxy 2.8.12. Usa le API native del programma, il sistema dei filtri, la gestione della memoria, lo scheduler degli eventi, per intercettare il traffico HTTP mentre il bilanciamento del carico continua a funzionare perfettamente. Dall'esterno, il server sembra sanissimo. La backdoor si sveglia solo quando vede passare una richiesta verso un URL preciso, che funziona da parola d'ordine, e da quel momento accetta comandi dall'operatore.

Perche' proprio HAProxy? Perche' su molte architetture il load balancer e' il punto in cui termina la cifratura TLS: decifra ogni connessione HTTPS prima di girarla ai server applicativi dietro di lui. Chi controlla quel punto vede tutto in chiaro, sessioni, credenziali, cookie, e puo' anche modificare al volo le risposte, iniettando script nelle pagine o forzando il download di file. Gli attaccanti hanno trasformato un componente di infrastruttura in una cimice perfetta.

Un dettaglio da sottolineare: non c'e' nessuna vulnerabilita' in HAProxy. Il progetto non e' stato bucato. Gli operatori sono riusciti in qualche modo a ottenere l'esecuzione di codice sui server di frontiera delle vittime e hanno sostituito l'eseguibile legittimo di HAProxy con una versione modificata, ricompilata da loro a partire dalla stessa 2.8.12 rilasciata a fine novembre 2024. E' un attacco alla catena di fiducia, non a un bug.

Il resto del kit e' altrettanto curato. Ci sono versioni trojanizzate di demoni di sistema comuni, crond, agetty, atd, polkitd, sshd, che ospitano curlRAT, un trojan di accesso remoto basato su libcurl. curlRAT interroga il server di comando e controllo a intervalli regolari, puo' aprire una shell interattiva, scaricare ed eseguire payload, aggiornare la propria configurazione. C'e' poi un keylogger per SSH che cattura le password in chiaro e le salva cifrate sotto /var/lib/sshd/, e uno "stager" che decide quali componenti installare in base al profilo della macchina e che si preoccupa di cancellare selettivamente le tracce nei log.

Per l'attribuzione, Rapid7 parla di "confidenza media" verso un gruppo legato alla Corea del Nord, in particolare per sovrapposizioni con l'infrastruttura di comando e controllo gia' associata ad APT37 e per il modello di attacco "watering hole" documentato in operazioni precedenti. La campagna sarebbe attiva almeno dall'inizio del 2025: nove o dieci mesi di spionaggio prima della scoperta pubblica.

La morale, per chi gestisce infrastruttura, e' scomoda ma chiara: i componenti di frontiera, load balancer, reverse proxy, gateway TLS, vanno trattati con lo stesso livello di paranoia dei server applicativi piu' critici. Non basta guardare i log del componente stesso, perche' un impianto ben fatto quei log li ripulisce. Servono controlli di integrita' indipendenti sui binari, cioe' confrontare l'hash di HAProxy e dei demoni di sistema con quelli attesi dalla distribuzione, monitoraggio del comportamento in memoria e correlazione a livello di rete che non dipenda dalla macchina compromessa.

C'e' anche un tema piu' generale che a RobyRoot ci sta a cuore: la fiducia nel software che compili tu stesso. Compilare da sorgente non e' di per se' una garanzia di sicurezza, se il sorgente, il toolchain o il binario finale possono essere manomessi lungo il percorso. E' qui che entrano in gioco le build riproducibili, la firma dei pacchetti e il monitoraggio dell'integrita' del filesystem con strumenti come AIDE o Tripwire. Non sono argomenti sexy, ma sono esattamente le difese che avrebbero fatto la differenza contro "ted".

Se usi HAProxy 2.8.12 su un server esposto, vale la pena come minimo verificare l'integrita' dell'eseguibile e reinstallarlo dai repository ufficiali. E, piu' in generale, chiediti quanti dei tuoi componenti di frontiera riusciresti a riconoscere come compromessi se qualcuno li avesse toccati sei mesi fa.
