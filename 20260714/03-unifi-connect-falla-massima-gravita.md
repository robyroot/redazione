---
title: "Se hai dispositivi UniFi in casa o in ufficio, aggiornali subito: falla di gravità massima in UniFi Connect"
rilevanza: "MEDIA"
fonte: "https://www.bleepingcomputer.com/news/security/ubiquiti-warns-of-new-max-severity-unifi-os-vulnerability/"
data_notizia: "2026-07-14"
tags: ["cybersecurity", "vulnerabilità", "iot", "rete domestica", "ubiquiti"]
livello: "beginner"
nota_editoriale: |
  Angolo per RobyRoot: UniFi è molto diffuso tra smanettoni, homelabber e piccole
  imprese che leggono blog come questo (router, access point, videocamere Protect).
  Meno enterprise di Oracle, più "vicino a casa": il pezzo dovrebbe rassicurare senza
  allarmismo (serve accesso di rete, non è sfruttabile da internet nella maggior
  parte dei setup) ma spingere comunque all'azione concreta: aggiornare il
  controller. Buona occasione per il solito discorso su IoT e superficie d'attacco
  che cresce ad ogni dispositivo smart aggiunto in casa.
---

Se in casa o in ufficio hai un router, un access point o una telecamera Ubiquiti (i famosi dispositivi UniFi, molto amati da chi ama sistemare la propria rete domestica in modo un po' più serio del solito), c'è un aggiornamento che ti conviene fare oggi stesso, non "quando hai tempo".

Ubiquiti ha rilasciato un bollettino di sicurezza — il numero 066 — che corregge in un colpo solo **25 vulnerabilità** sparse in tutto l'ecosistema UniFi. Tra queste ce n'è una particolarmente seria: **CVE-2026-50746**, con il punteggio di gravità più alto possibile, 10 su 10.

## Il problema, in parole semplici

La falla riguarda **UniFi Connect**, l'applicazione che Ubiquiti mette a disposizione per gestire da un'unica interfaccia impianti più complessi di una semplice rete domestica: illuminazione LED intelligente, colonnine di ricarica per veicoli elettrici, automazioni di edifici commerciali. Il problema è un controllo degli accessi fatto male: chi si trova già sulla stessa rete del dispositivo (quindi non serve essere su internet, basta essere "dentro" la LAN) può iniettare comandi arbitrari sul sistema, senza bisogno di alcuna password.

In gergo tecnico si chiama "command injection non autenticata", e nella pratica significa che un intruso che riesce ad accedere alla tua rete Wi-Fi — magari sfruttando un altro dispositivo IoT più debole già collegato — potrebbe usare questa falla come trampolino per prendere il controllo del sistema UniFi Connect e, da lì, potenzialmente di altri apparecchi collegati.

## Non è la sola: altre sei vulnerabilità critiche

L'advisory 066 non si limita a questa falla: risolve anche altre sei vulnerabilità critiche che toccano UniFi Talk (i telefoni VoIP), UniFi Access (i controlli di accesso fisico, tipo serrature e badge), UniFi Protect (le videocamere di sorveglianza) e il sistema operativo UniFi OS in generale. Sei di queste sette falle possono essere sfruttate con attacchi a bassa complessità e **senza alcuna interazione da parte della vittima** — niente click su link, niente password da rubare: basta la presenza sulla rete giusta al momento giusto.

Per un ecosistema che gestisce contemporaneamente la tua rete internet di casa, le telecamere di sicurezza e magari anche la serratura della porta, è un mix di vulnerabilità che vale la pena prendere sul serio.

## Chi rischia davvero

Va detto con chiarezza: questa non è una falla sfruttabile a caso da internet contro chiunque abbia un router UniFi. Serve, nella maggior parte dei casi, un accesso alla rete locale — quindi il rischio concreto riguarda soprattutto ambienti dove la rete non è ben segmentata: uffici con ospiti che si collegano al Wi-Fi, edifici commerciali con impianti gestiti da UniFi Connect esposti a reti condivise, o abitazioni dove magari un dispositivo smart di scarsa qualità (una lampadina, una presa intelligente di marca sconosciuta) fa già da porta d'ingresso per un attaccante.

Detto altrimenti: più dispositivi smart aggiungi in casa, più cresce la superficie d'attacco complessiva della tua rete, anche se il singolo dispositivo Ubiquiti in sé è ben progettato. È la stessa vecchia lezione dell'IoT: la sicurezza di una rete domestica è forte quanto il suo anello più debole, non quanto il suo dispositivo più costoso.

## Cosa fare adesso

Se usi UniFi Connect, aggiorna subito all'applicazione alla versione **3.4.20 o successiva** (le versioni fino alla 3.4.16 sono vulnerabili). Se gestisci un controller UniFi OS più in generale, vale la pena controllare il pannello di amministrazione e applicare tutti gli aggiornamenti disponibili collegati all'advisory 066, non solo quello per Connect. Un buon momento anche per fare due cose che non costano nulla: separare la rete "smart home"/IoT da quella dei dispositivi personali usando una VLAN o una rete guest dedicata (molti router UniFi lo permettono nativamente), e dare un'occhiata a quanti device sconosciuti compaiono nell'elenco dei client connessi — a volte la sorpresa più grande non è la vulnerabilità del produttore serio, ma il gadget da quattro soldi che nessuno ricordava di aver collegato due anni fa.
