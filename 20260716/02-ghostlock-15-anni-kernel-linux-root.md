---
title: "GhostLock: il bug del kernel Linux vecchio 15 anni che dà root in 5 secondi (e buca anche i container)"
rilevanza: "ALTA"
fonte: "https://thehackernews.com/2026/07/15-year-old-ghostlock-flaw-enables-root.html"
data_notizia: "2026-07-16"
tags: ["linux", "kernel", "cybersecurity", "vulnerabilita", "container", "docker"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato: puntare sul fatto "15 anni nascosto" e sulla scoperta tramite AI (Nebula
  Security con il tool VEGA) come spunto per parlare di come l'IA sta cambiando la ricerca di
  vulnerabilita. Molto rilevante per chi usa Docker/container in produzione, quindi vale la pena
  dedicare una sezione pratica a chi gestisce ambienti containerizzati o server condivisi.
  Da menzionare insieme a Bad Epoll (altro articolo della giornata) come "settimana nera" per il
  kernel Linux, ma senza creare inutile allarmismo: nessuno sfruttamento noto in the wild.
---

C'è qualcosa di quasi assurdo in questa storia: un bug capace di trasformare qualsiasi utente normale di un sistema Linux in root — l'amministratore con accesso totale — è rimasto silenziosamente nel codice del kernel per **15 anni**, dal 2011 fino a oggi. Si chiama **GhostLock**, è catalogato come **CVE-2026-43499**, ed è una di quelle scoperte che ti fanno chiedere quanti altri scheletri simili dormano ancora nei sistemi operativi che usiamo ogni giorno.

## Il bug, spiegato senza tecnicismi

GhostLock vive in una parte del kernel che si occupa di gestire le **priorità dei processi** quando più task competono per una stessa risorsa "bloccata" (in gergo, un lock). Quando un'operazione di questo tipo fallisce, il kernel deve fare pulizia — ma in GhostLock questa pulizia scatta nel momento sbagliato, e finisce per cancellare il riferimento al processo sbagliato. Il risultato è che il kernel resta con un puntatore che punta a memoria già riutilizzata per qualcos'altro: la classica **use-after-free**, lo stesso tipo di errore che abbiamo visto anche nella vulnerabilità "Bad Epoll" scoperta nella stessa settimana.

I ricercatori di **Nebula Security** hanno dimostrato che concatenando pochi passaggi è possibile forzare il kernel a eseguire codice come utente root — in circa **cinque secondi**. Non serve nessun permesso speciale, nessuna configurazione strana, nessuna connessione di rete: basta essere un normalissimo utente loggato sulla macchina, con un account "senza privilegi" come ne esistono milioni.

## Chi è a rischio (spoiler: quasi tutti)

Il bug è stato introdotto nel kernel Linux nel **2011** (versione 2.6.39) e da allora è rimasto presente in **praticamente ogni distribuzione mainstream**: Ubuntu 20.04, 22.04, 24.04 LTS, e a cascata tutte le derivate, oltre a Debian, RHEL, AlmaLinux, CloudLinux e chi più ne ha più ne metta. In sostanza, se non hai aggiornato il kernel di recente, il tuo sistema è probabilmente vulnerabile.

La parte più preoccupante riguarda i **container**: l'exploit funziona anche dall'interno di un container Docker o simili, permettendo di "evadere" verso il sistema host. Questo è un incubo per chiunque gestisca ambienti multi-tenant, hosting condiviso, runner di CI/CD o infrastrutture cloud dove più clienti o processi condividono lo stesso kernel fisico. Una escalation di privilegi "locale" diventa così un problema molto più serio, soprattutto se combinata con altre falle — i ricercatori citano ad esempio uno scenario in cui GhostLock, unito a un bug separato di Firefox (CVE-2026-10702), potrebbe trasformarsi in una compromissione avviabile da remoto.

## Come è stato scoperto: entra in scena l'IA

Un dettaglio interessante di questa vicenda è il metodo di scoperta: Nebula Security ha trovato GhostLock usando **VEGA**, un proprio strumento di analisi del codice basato su intelligenza artificiale. È un altro segnale di come la ricerca di vulnerabilità stia cambiando pelle: strumenti automatizzati riescono a scovare bug rimasti invisibili all'occhio umano per più di un decennio. Google ha riconosciuto la scoperta tramite il programma kernelCTF con un bounty di oltre 92mila dollari — una cifra che dice molto sulla gravità del problema.

## Cosa fare, concretamente

Il kernel è già stato corretto a monte (commit `3bfdc63936dd`, disponibile da aprile 2026), quindi la priorità assoluta è aggiornare:

- **Verifica la tua distribuzione**: non basta prendere la prima build "patchata" che trovi, controlla l'advisory ufficiale (Ubuntu, Debian, Red Hat, AlmaLinux hanno tutti pubblicato bollettini dedicati) e installa la versione di pacchetto corretta.
- **Dai priorità alle macchine più esposte**: server cloud, host di container, sistemi con più utenti reali, runner CI/CD. Sono gli ambienti dove un attacco di questo tipo fa più danni.
- Se non puoi riavviare subito per applicare il nuovo kernel, esistono mitigazioni parziali come `RANDOMIZE_KSTACK_OFFSET` e `STATIC_USERMODE_HELPER`, ma **non eliminano il rischio**, lo riducono soltanto. Non sono un sostituto della patch.

Al momento non risultano exploit usati attivamente contro sistemi reali, ma il codice proof-of-concept è pubblico e funzionante, quindi il margine di tempo per aggiornare non è infinito. Con Bad Epoll scoperta nella stessa settimana, è chiaro che il kernel Linux sta attraversando un periodo di scrutinio intenso — un bene per la sicurezza a lungo termine, ma un promemoria concreto che "è vecchio quindi è stabile" non è sempre sinonimo di "è sicuro".
