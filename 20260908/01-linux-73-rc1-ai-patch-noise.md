---
title: "Linux 7.3 RC1 è qui: Linus apre il ciclo, ma le patch AI fanno impazzire i maintainer"
rilevanza: "ALTA"
fonte: "https://linuxiac.com/arch-linux-september-2026-iso-is-out-with-linux-kernel-7-2/"
data_notizia: "2026-09-01"
tags: ["linux", "kernel", "AI", "open-source", "arch-linux"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: doppio focus — il rilascio tecnico del kernel 7.3 RC1 per i lettori
  entusiasti del kernel, ma soprattutto l'angolo "AI e open source": il lamento di Greg Kroah-Hartman
  sulle patch generate da LLM è perfetto per il pubblico che segue sia Linux che l'AI. Ottimo per
  generare discussione nei commenti.
---

# Linux 7.3 RC1 è qui: Linus apre il ciclo, ma le patch AI fanno impazzire i maintainer

Settembre porta come sempre novità dal mondo del kernel Linux: Linus Torvalds ha annunciato la prima
Release Candidate di **Linux 7.3**, aprendo ufficialmente il nuovo ciclo di sviluppo. Ma accanto alle
novità tecniche, c'è una polemica che sta facendo discutere: i maintainer del kernel sono stufi delle
patch generate dall'AI.

## Cosa c'è di nuovo in Linux 7.3 RC1

Come di consueto, la RC1 è il punto di partenza: non è pensata per la produzione, ma raccoglie le prime
merge window delle patch accettate per il ciclo 7.3. Il kernel è in sviluppo attivo e i test sono
fondamentali per scovare regressioni prima del rilascio stabile.

Parallelamente, **Arch Linux ha già aggiornato la sua ISO di settembre 2026** portando a bordo il kernel
**7.2.2** stabile, insieme ad aggiornamenti importanti:

- **GCC 16.2.1** — il compilatore C/C++ di riferimento su Linux
- **glibc 2.44** — la libreria C fondamentale per praticamente ogni programma
- **Python 3.14.7** — una delle release minori della serie 3.14
- **mkinitcpio 41.1** — il tool per generare l'initramfs su Arch

Se usi Arch o una derivata, un bel `pacman -Syu` risolve tutto.

## Il vero problema: le patch AI che intasano il kernel

Qui viene la parte più interessante. **Greg Kroah-Hartman**, maintainer del kernel stable branch e uno
dei nomi più importanti dell'ecosistema Linux, ha lanciato un avvertimento: il ciclo 7.3 sarà
probabilmente "rumoroso" a causa dell'aumento di **bug report e patch generati da LLM**.

In pratica, alcuni sviluppatori (o aspiranti tali) stanno usando ChatGPT, Copilot o altri modelli per
generare patch da inviare alla mailing list del kernel — spesso senza capirle davvero. Il risultato?
I maintainer devono perdere tempo a smistare contributi di bassa qualità, rispondere a bug report
confusi, e rifiutare codice che "sembra corretto" ma non lo è.

```bash
# Esempio di workflow corretto per contribuire al kernel
# (non delegare a un LLM senza capire il codice)
git clone https://kernel.googlesource.com/pub/scm/linux/kernel/git/torvalds/linux
cd linux
# Studia il codice, leggi la documentazione
cat Documentation/process/submitting-patches.rst
```

## Perché è importante per la community open source

Questo non è solo un problema tecnico: è una **questione culturale**. Il kernel Linux è uno dei
progetti open source più complessi al mondo, con regole di contribuzione rigorose costruite in
decenni di sviluppo. Quando tool AI abbassano la barriera d'ingresso senza abbassare quella della
*comprensione*, il risultato è rumore che rallenta chi lavora davvero.

Non è un discorso anti-AI in senso assoluto. Kroah-Hartman e altri maintainer non sono
contro l'uso di AI come supporto allo sviluppo. Il problema è chi usa un LLM come scorciatoia
per contribuire senza avere le competenze necessarie.

## E Arch Linux intanto naviga tranquilla

Tornando alla parte pratica: Arch Linux 2026.09.01 con kernel 7.2.2 è stabile e pronta per
l'installazione. L'ISO da 1,5 GB è disponibile sul sito ufficiale e sui mirror italiani.

```bash
# Verifica il kernel attuale sul tuo sistema Arch
uname -r

# Aggiorna tutto con un singolo comando
sudo pacman -Syu
```

Se stai pianificando una nuova installazione o vuoi testare un ambiente Arch aggiornato in VM,
questo è un buon momento per farlo.

## Conclusione

Linux 7.3 RC1 è partito, Arch è aggiornata e il kernel continua a evolversi. Ma la storia più
interessante resta quella delle patch AI: un segnale che l'ondata di entusiasmo per i modelli
linguistici sta iniziando a creare attrito anche nelle community più strutturate dell'open source.
La qualità resta la priorità — e nessun LLM può sostituire la comprensione profonda del codice.
