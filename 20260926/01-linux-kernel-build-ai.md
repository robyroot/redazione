---
title: "Il kernel Linux compila il 70% più veloce grazie all'AI (e al codice \"orrendo\" che genera)"
rilevanza: "ALTA"
fonte: "https://www.phoronix.com/news/Linux-Kbuild-Faster-v3"
data_notizia: "2026-09-23"
tags: ["linux", "kernel", "AI", "performance", "sviluppo", "kbuild"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: storia perfetta per chi ama sia Linux che l'AI. L'ironia del codice "orrendo" generato dall'AI ma funzionante è un ottimo hook. Mostra come l'AI sta entrando nel cuore dello sviluppo kernel senza sostituire gli sviluppatori umani (che devono ancora rivedere e riscrivere molto).
---

# Il kernel Linux compila il 70% più veloce grazie all'AI (e al codice "orrendo" che genera)

Se compili il kernel Linux regolarmente — o semplicemente ti chiedi come si sviluppa il software più critico del pianeta — questa settimana è arrivata una notizia interessante. Lorenzo Stoakes, ingegnere di ARM e sviluppatore kernel di lungo corso, ha pubblicato il 23 settembre la quarta revisione di una serie di 22 patch per il sottosistema **kbuild** che promette di far volare i tempi di compilazione.

I numeri sono notevoli: build complete fino al **36% più veloci**, build incrementali fino al **70% più veloci**, e le "noop build" (quando non c'è nulla da ricompilare) addirittura fino al **90% più veloci**. Su un server dual-socket AMD EPYC 9575F, una build x86_64 defconfig pulita è scesa da 22 secondi a 15 secondi.

## Come ha funzionato il processo

La parte interessante è il *come* Stoakes ha trovato questi colli di bottiglia: ha usato un LLM (un modello linguistico AI) per analizzare il codice di build del kernel e identificare i punti critici che rallentavano la compilazione.

Il risultato? L'AI ha trovato i problemi, ma il codice che ha generato per risolverli era, parole sue, "di molto brutto" — "hideous" in inglese. Stoakes ha dovuto revisionare e riscrivere manualmente buona parte di ciò che l'AI produceva, ma il processo ha comunque accelerato significativamente il lavoro di ricerca delle ottimizzazioni.

È una storia che conoscono bene molti sviluppatori che usano l'AI come assistente: l'AI è ottima per fare la ricognizione e trovare il punto esatto dove intervenire, ma raramente genera codice direttamente adatto alla produzione senza una revisione umana attenta.

## Cosa viene ottimizzato esattamente

Le patch toccano diversi sottosistemi del processo di build:

- **kbuild**: il sistema di build principale del kernel
- **kallsyms**: la tabella dei simboli del kernel
- **modpost**: lo strumento che gestisce i moduli
- **objtool**: per l'analisi degli oggetti binari
- **mksysmap**: per la mappa di sistema
- **Rust build system**: sì, il kernel ora ha anche ottimizzazioni nel suo supporto Rust

Il problema principale che le patch risolvono è la presenza di **colli di bottiglia single-threaded**: alcune fasi del processo di build dovevano per forza girare in sequenza, anche su macchine con decine di core disponibili. Eliminare questi colli di bottiglia permette di sfruttare meglio il parallelismo.

## Cosa significa per te

Se sei un normale utente Linux che non compila mai il kernel, queste patch non cambieranno la tua giornata. Ma se sei uno sviluppatore, un manutentore di distribuzioni, o un hobbista che ama compilare kernel custom, il beneficio è reale.

```bash
# Per vedere i tempi attuali di build sul tuo sistema
time make -j$(nproc) defconfig all
```

Esegui questo prima e dopo l'aggiornamento quando queste patch arriveranno in upstream (probabilmente con Linux 7.4) per misurare il miglioramento sul tuo hardware specifico.

## La storia più grande: AI nel kernel Linux

Questa non è la prima volta che l'AI fa capolino nello sviluppo del kernel. Linus Torvalds ha già dichiarato che la code review assistita dall'AI sta diventando la nuova normalità. Circa uno su cinque commit recenti porta un tag `Assisted-by:` che documenta l'uso di strumenti AI nella revisione.

La tendenza è chiara: l'AI non sostituisce i kernel developer (ci vuole ancora qualcuno che riveda quel "codice orrendo"), ma sta diventando uno strumento standard nella cassetta degli attrezzi. Esattamente come `git`, `sparse` o `coccinelle`.

Le patch v4 sono attualmente in revisione sulla mailing list e ci sono buone speranze che vengano accettate per Linux 7.4. Il kernel 7.3 è appena uscito come release candidate, quindi la finestra di merge per 7.4 si aprirà tra qualche settimane.
