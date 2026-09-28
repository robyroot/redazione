---
title: "Linux 7.3 RC3: patch scritte dall'AI, supporto Apple Thunderbolt e 41 milioni di righe"
rilevanza: "MEDIA"
fonte: "https://www.linuxcompatible.org/story/linux-kernel-73rc3-released-big-filesystem-footprint-and-aiassisted-patches"
data_notizia: "2026-09-14"
tags: ["linux", "kernel", "apple", "rust", "AI", "open-source"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: focus sul tema "AI che scrive patch per il kernel Linux" — è controverso e interessante. Linus stesso ha scherzato attribuendo all'AI la dimensione enorme dell'RC. Ottimo per un pubblico curioso di AI e open source insieme.
---

# Linux 7.3 RC3: patch scritte dall'AI, supporto Apple Thunderbolt e 41 milioni di righe

Il kernel Linux ha appena superato i **41 milioni di righe di codice**. La terza Release Candidate di Linux 7.3 è uscita a metà settembre, e stavolta Linus Torvalds non ha usato mezze misure nel descriverla: "potremmo anche dare la colpa all'AI per questo RC enorme".

Non era un complimento, ma neanche una critica. Era più una constatazione — il kernel sta cambiando, e l'AI ha iniziato a mettere le mani nel codice.

## L'elefante nella stanza: patch generate con l'AI

Linux 7.3-rc3 include per la prima volta una serie di patch che sono state assistite da strumenti di intelligenza artificiale. Non si tratta di codice generato al 100% da un LLM, ma di ottimizzazioni e refactoring dove i developer hanno usato tool AI per individuare pattern, suggerire migliorie e velocizzare il lavoro.

Il risultato è visibile nelle dimensioni: l'RC3 è stata definita da Torvalds stesso "another fairly large RC", con un footprint sui filesystem decisamente superiore alla norma. Parte di questa crescita viene dal dump massiccio di codice per le GPU AMD (circa un terzo dell'intero diff dell'RC1), ma le patch AI-assisted contribuiscono alla complessità generale.

La comunità del kernel è divisa. C'è chi vede l'AI come uno strumento di produttività legittimo, e chi teme che introduca bug sottili difficili da individuare durante il code review. Il dibattito è aperto, e Linux 7.3 sarà un banco di prova interessante.

## Finalmente il supporto Thunderbolt per i Mac con chip Apple

Una delle novità più attese è il **supporto USB4 e Thunderbolt per i chip Apple M1, M2 e M3**. Sì, hai letto bene: Linux sta lavorando per supportare nativamente le porte Thunderbolt dei Mac con processori Apple Silicon.

Questo non significa che installare Linux su un MacBook M3 diventi banale (ci sono ancora mille altri problemi), ma è un passo importante per il progetto Asahi Linux e per tutti quelli che vogliono usare hardware Apple con un kernel upstream.

Il supporto Thunderbolt è fondamentale perché abilita dock station, schermi esterni, storage ad alta velocità e altri periferici connessi via quella porta. Senza di esso, avere Linux su un Mac è un'esperienza molto limitata.

## La grande ristrutturazione di KVM

Linux 7.3 porta anche un **overhaul massiccio di KVM** (Kernel-based Virtual Machine), il modulo che gestisce la virtualizzazione nel kernel Linux. È arrivata una serie da 45 patch per la gestione della memoria degli host guest, che migliora le prestazioni e la sicurezza delle macchine virtuali.

Per chi usa QEMU/KVM per fare girare VM Linux o Windows, questi cambiamenti si traducono in:

- Migliore isolamento della memoria tra host e guest
- Riduzione della latenza nelle operazioni di memoria
- Gestione più efficiente delle grandi allocazioni

Per vedere le novità di KVM disponibili nel tuo sistema:

```bash
# Verifica la versione del kernel
uname -r

# Controlla se KVM è attivo
lsmod | grep kvm

# Informazioni sul modulo KVM
modinfo kvm
```

## Ottimizzazioni al build time: fino al -70% con AI

Separato dal kernel stesso, ma correlato al mondo del kernel development, c'è un'altra notizia interessante: un ricercatore ha identificato **colli di bottiglia nel sistema di build del kernel Linux** usando strumenti AI, e le ottimizzazioni proposte potrebbero ridurre i tempi di compilazione incrementale fino al **70%**.

Queste ottimizzazioni non sono ancora merged nel kernel, ma potrebbero arrivare con Linux 7.4. Per chi fa sviluppo kernel o compila custom kernel regolarmente, è una notizia da seguire.

Compilare il kernel Linux da zero richiede normalmente dai 20 ai 60 minuti a seconda dell'hardware. Una riduzione del 70% sui tempi incrementali (le ricompilazioni dopo una modifica) cambierebbe parecchio il workflow dei developer.

## Quando arriva Linux 7.3 stabile?

Con RC3 uscita a metà settembre e il ciclo RC che dura circa sei settimane dall'RC1 (lanciata il 30 agosto), la versione stabile di Linux 7.3 è attesa per **metà-fine ottobre 2026**.

Le distro rolling release come Arch Linux e Manjaro riceveranno il kernel molto rapidamente dopo il rilascio stabile. Le distro con cicli di release più lunghi (Ubuntu LTS, Debian) lo adotteranno nei mesi successivi.

Per chi vuole provare già adesso:

```bash
# Su Arch Linux, kernel mainline disponibile su AUR
yay -S linux-mainline

# Verifica la versione dopo l'installazione
uname -r
```

La progressione di Linux da 40 a 41 milioni di righe racconta da sola quante cose il kernel deve gestire nel 2026: dai Mac con chip ARM alle GPU di ultima generazione, dai container alle VM, dai device IoT ai supercalcolatori. È un progetto enorme, e continua a crescere.
