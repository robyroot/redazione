---
title: "Bad Epoll (CVE-2026-46242): il bug nel kernel Linux che regala i permessi di root"
rilevanza: "ALTA"
fonte: "https://thehackernews.com/2026/07/new-bad-epoll-linux-kernel-flaw-lets.html"
data_notizia: "2026-07-04"
tags: ["sicurezza", "linux", "kernel", "vulnerabilità", "CVE", "privilege-escalation"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: Spiegare la vulnerabilità in modo accessibile con comandi pratici per aggiornare, evidenziando che colpisce desktop, server e Android. Ottimo per sensibilizzare il pubblico Linux sulla patch immediata.
---

# Bad Epoll (CVE-2026-46242): il bug nel kernel Linux che regala i permessi di root

Se usi Linux su desktop, server o su uno smartphone Android, c'è una notizia di sicurezza che merita attenzione immediata. Si chiama **Bad Epoll**, è catalogata come **CVE-2026-46242**, e permette a qualunque utente senza privilegi speciali di diventare root su un sistema Linux. La cosa concreta è che esiste già un exploit pubblico con un tasso di successo del 99%.

## Cos'è successo

La vulnerabilità è stata scoperta dal ricercatore Jaeyoung Chung nell'ambito del programma **kernelCTF** di Google. Il bug risiede nel sottosistema **epoll** del kernel Linux — il meccanismo che gestisce le notifiche degli eventi I/O asincroni, usato praticamente da ogni applicazione moderna: server web, database, container, browser.

Tecnicamente si tratta di una **race condition combinata con un use-after-free**: due parti del kernel cercano di liberare lo stesso oggetto in memoria esattamente nello stesso momento. In quella brevissima finestra di collisione — appena sei istruzioni di CPU — un attaccante può corrompere la memoria del kernel e scalare da utente normale a **root**, il massimo dei privilegi.

Tradotto: chiunque abbia accesso locale a una macchina vulnerabile (anche come semplice utente guest) può prenderne il controllo completo.

## Quanti sistemi sono esposti

Le versioni del kernel Linux dalla **5.10 alla 6.11** sono confermate vulnerabili. Questo copre anni di installazioni: praticamente tutte le distribuzioni Linux moderne sono state esposte in un certo periodo. Anche Android è incluso, perché usa il kernel Linux.

Il PoC (proof-of-concept) è ospitato pubblicamente su GitHub e funziona con una affidabilità del 99% su kernel 6.12. Al momento della divulgazione pubblica non risultava ancora sfruttato attivamente — non era nella lista CISA KEV — ma con un exploit così affidabile e pubblico la situazione potrebbe cambiare rapidamente.

## Come proteggersi subito

La buona notizia è che la patch è già disponibile. Il bug è stato segnalato privatamente a **febbraio 2026**, corretto upstream il **24 aprile** e divulgato pubblicamente il **30 maggio**. Le principali distribuzioni hanno già rilasciato gli aggiornamenti.

Prima di tutto, controlla la versione del tuo kernel:

```bash
uname -r
```

Poi aggiorna con il gestore pacchetti della tua distribuzione:

```bash
# Debian/Ubuntu e derivate
sudo apt update && sudo apt upgrade

# Fedora/RHEL/CentOS Stream
sudo dnf update

# Arch Linux
sudo pacman -Syu

# openSUSE
sudo zypper update
```

Dopo l'aggiornamento è necessario **riavviare** per caricare il nuovo kernel:

```bash
sudo reboot
```

Se vuoi verificare che stai usando il kernel corretto dopo il riavvio, consulta gli advisory di sicurezza della tua distribuzione (Debian Security, Ubuntu Security Notices, Red Hat CVE Database, ecc.) per sapere quale versione include la patch.

## Un dettaglio tecnico curioso

La vulnerabilità è interessante anche dal punto di vista della ricerca. Il bug era nascosto in un'area del kernel analizzata di frequente, ma nessuno degli strumenti di auditing automatizzato — inclusi quelli basati su AI che diversi progetti open source stanno adottando — lo aveva individuato. Solo un ricercatore umano con esperienza specifica nel subsistema epoll ha trovato la seconda delle due race condition che compongono il bug.

Questo evidenzia quanto sia complessa la sicurezza di un kernel da decine di milioni di righe di codice: gli strumenti automatici aiutano, ma non sostituiscono l'analisi manuale approfondita.

## La questione Android

Chi ha uno smartphone Android non aggiornato da tempo è potenzialmente esposto. Il problema è che l'aggiornamento del kernel dipende dal produttore e dall'operatore, non da Google direttamente. Se il tuo dispositivo ha smesso di ricevere aggiornamenti di sicurezza, questa vulnerabilità è un ulteriore motivo per valutare un firmware alternativo come **LineageOS** o per considerare l'acquisto di un dispositivo supportato a lungo termine.

## Conclusione

Bad Epoll è uno di quei bug che ricordano quanto sia delicato mantenere un sistema operativo usato da miliardi di dispositivi. La risposta della community è stata rapida e la patch è già disponibile. Se non aggiorni regolarmente il kernel, questo è il momento giusto per farlo — è l'azione più semplice e più efficace che puoi fare oggi per proteggere la tua macchina Linux.
