---
title: "Bad Epoll: la falla nel kernel Linux che regala privilegi di root (e colpisce anche Android)"
rilevanza: "ALTA"
fonte: "https://thehackernews.com/2026/07/new-bad-epoll-linux-kernel-flaw-lets.html"
data_notizia: "2026-07-15"
tags: ["linux", "kernel", "sicurezza", "cve", "android"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato: spiegare in modo semplice cos'è epoll (per non spaventare i lettori meno tecnici)
  e insistere sul fatto pratico "aggiorna il kernel adesso". Buon gancio anche per chi usa Android,
  visto che il bug tocca pure lì. Evitare toni allarmistici: nessun exploit è stato visto in the wild,
  ma la severità e la facilità di sfruttamento meritano attenzione. Possibile CTA: controllare la versione
  del proprio kernel con "uname -r".
---

Un'altra settimana, un'altra falla nel kernel Linux con un nome che sembra uscito da un film di spionaggio. Questa volta si chiama **Bad Epoll**, è identificata come **CVE-2026-46242**, e il problema è serio: permette a un utente qualunque, anche senza permessi speciali, di diventare root sulla macchina. Il bello (si fa per dire) è che non riguarda solo server e desktop Linux, ma anche Android.

## Cos'è epoll e perché è così importante

Se non mastichi il gergo kernel, epoll è uno dei meccanismi fondamentali con cui Linux gestisce migliaia di connessioni di rete contemporaneamente senza impazzire. È il motore silenzioso dietro software che usi ogni giorno senza saperlo: nginx, Apache, Node.js, i database, e persino il ciclo di eventi di Android. Insomma, non è un angolo oscuro e poco usato del kernel: è ovunque. Questo significa che la superficie d'attacco di Bad Epoll è enorme.

## Il problema tecnico, in parole povere

Bad Epoll è quella che i tecnici chiamano una "race condition" combinata con un "use-after-free". Tradotto: due parti del kernel provano a "ripulire" lo stesso pezzetto di memoria nello stesso istante. Una lo libera, l'altra ci scrive sopra credendo sia ancora valido. Il risultato è corruzione della memoria del kernel, che un attaccante esperto può trasformare in un'escalation di privilegi fino a root.

La finestra temporale per sfruttare questo bug è ridicolmente stretta — si parla di appena una manciata di istruzioni macchina. Non è il tipo di bug che chiunque può sfruttare da un giorno all'altro. Ma il ricercatore Jaeyoung Chung, che ha scoperto la falla e l'ha sottoposta al programma kernelCTF di Google (quello che paga bounty a partire da 71.337 dollari per exploit funzionanti sul kernel Linux), ha costruito un proof-of-concept che allarga quella finestra e ritenta l'attacco senza mandare in crash il sistema. Risultato: un tasso di successo del **99%** nei test.

## Chi è a rischio

I kernel interessati vanno dalla versione 6.4 in su. Curiosamente, i kernel basati su 6.1 (compresi alcuni telefoni Pixel 8) sono al sicuro, perché il bug è stato introdotto proprio con il passaggio alla 6.4. Ma per il resto, la lista dei sistemi coinvolti è lunga: desktop Linux, server, e appunto Android.

Su Android la faccenda si fa particolarmente delicata: un attaccante con accesso di livello app o tramite ADB shell può ottenere il controllo completo del dispositivo, compreso l'accesso al secure element, al keystore delle credenziali e il bypass del sandboxing delle applicazioni. In pratica, il tipo di isolamento che rende Android relativamente sicuro anche quando un'app è compromessa va a farsi benedire.

C'è anche un dettaglio interessante per chi si occupa di sicurezza del browser: la falla è sfruttabile persino dall'interno della sandbox del renderer di Chrome, il che significa che in teoria una pagina web malevola combinata con un altro bug potrebbe fungere da trampolino verso il sistema operativo.

## Cosa fare adesso

La cattiva notizia è che non esiste un modo per "disattivare" epoll come mitigazione temporanea — è troppo centrale nell'architettura del kernel. L'unica strada percorribile è applicare la patch. Il fix ufficiale è già stato integrato a monte con il commit `a6dc643c6931` e sta arrivando (o è già arrivato) nelle varie distribuzioni tramite gli aggiornamenti del kernel.

Quindi, se gestisci server Linux, il consiglio pratico è: controlla la versione del kernel con `uname -r`, verifica se la tua distro ha già rilasciato il pacchetto aggiornato, e applica l'aggiornamento appena possibile — non aspettare la prossima finestra di manutenzione programmata. Per chi usa Android, tieni d'occhio gli aggiornamenti di sicurezza mensili del produttore del telefono.

La buona notizia, per ora, è che non ci sono evidenze di sfruttamento reale "in the wild": il bug è stato scoperto da un ricercatore responsabile, non da un gruppo criminale. Ma la storia recente del kernel Linux (pensiamo a Dirty Pipe o Dirty COW) insegna che, una volta che un proof-of-concept pubblico circola, il tempo a disposizione prima che qualcuno lo trasformi in un'arma si misura in giorni, non mesi.

Bad Epoll si aggiunge a una lista già lunga di falle "storiche" scoperte quest'anno nel kernel Linux, e conferma un trend: più la community investe in strumenti automatizzati di analisi del codice (fuzzing, AI-assisted code review), più questi bug vecchi di anni vengono a galla. Non è necessariamente una brutta notizia — significa che li stiamo trovando prima che lo facciano gli attaccanti — ma richiede a chi amministra sistemi Linux di essere più reattivo che mai sugli aggiornamenti di sicurezza.
