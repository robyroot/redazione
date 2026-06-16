---
title: "NVIDIA Ising: i primi modelli AI open source per il quantum computing"
rilevanza: "ALTA — novità assoluta, incrocio AI + open source + quantum"
fonte: "https://nvidianews.nvidia.com/news/nvidia-launches-ising-the-worlds-first-open-ai-models-to-accelerate-the-path-to-useful-quantum-computers"
fonti_secondarie:
  - "https://www.tomshardware.com/tech-industry/artificial-intelligence/nvidia-releases-ising-open-ai-models"
  - "https://thequantuminsider.com/2026/04/14/nvidia-launches-ising-the-worlds-first-open-ai-models-to-accelerate-the-path-to-useful-quantum-computers/"
data_notizia: "14 aprile 2026"
tags: ["nvidia", "quantum-computing", "ai", "open-source", "ricerca"]
livello: "intermediate"
nota_editoriale: |
  Notizia uscita ad aprile ma ancora pochissimo trattata in italiano.
  Ottima per RobyRoot: unisce AI, open source e quantum in un unico pezzo.
  Tono consigliato: spiegazione accessibile di cosa è il quantum computing,
  poi focalizzarsi su perché è rilevante che sia open source.
---

Il quantum computing è uno di quei temi che sembrano sempre a dieci anni dal diventare utili davvero. E in parte è così. Ma questa settimana NVIDIA ha fatto qualcosa che potrebbe avvicinare quella data: ha rilasciato **Ising**, la prima famiglia di modelli AI open source pensati specificamente per far funzionare meglio i computer quantistici.

Non è un annuncio di marketing. È roba concreta, disponibile su GitHub e Hugging Face, e già adottata da Harvard, Fermi National Lab e Lawrence Berkeley National Laboratory.

## Il problema che Ising risolve

I computer quantistici sono straordinariamente potenti in teoria. In pratica, hanno due problemi enormi che li rendono ancora poco utilizzabili:

**1. Gli errori.** I qubit (l'equivalente quantistico dei bit classici) sono instabili. Anche la minima interferenza dall'ambiente li "corrompe". Per usare un computer quantistico in modo affidabile, devi rilevare e correggere questi errori in tempo reale — ed è computazionalmente pesantissimo.

**2. La calibrazione.** Prima di usare un processore quantistico, devi calibrarlo: misurare come si comporta ogni qubit, compensare le imperfezioni hardware. Questo processo richiedeva tipicamente **giorni** di lavoro.

Ising attacca entrambi i problemi con due componenti:

### Ising Calibration
Un modello visione-linguaggio che interpreta automaticamente le misurazioni dai processori quantistici. Risultato: la calibrazione che richiedeva giorni ora si fa in **poche ore**.

### Ising Decoding
Due varianti di reti neurali convoluzionali 3D per la correzione degli errori in tempo reale. I numeri: **2.5x più veloce** e **3x più accurato** rispetto a pyMatching, lo standard open source attuale.

## Perché open source cambia tutto

Fino ad ora, i sistemi di controllo per quantum computing erano o proprietari o molto accademici. Ising è disponibile gratuitamente su GitHub, Hugging Face e build.nvidia.com, integrato con CUDA-Q (la piattaforma quantum software di NVIDIA).

Questo significa che qualsiasi laboratorio, università o startup nel settore può:
- Prendere questi modelli e usarli subito
- Adattarli alla propria architettura hardware specifica
- Contribuire miglioramenti alla community

La lista di chi li ha già adottati è impressionante: Harvard, Fermi National Accelerator Laboratory, Lawrence Berkeley National Laboratory, IQM Quantum Computers, IonQ, Sandia National Laboratories, e una decina di altri.

## Cosa c'entra con noi

Il quantum computing è ancora lontano dall'uso quotidiano. Ma questo tipo di novità conta per due motivi:

**Per chi lavora in sicurezza informatica**: i computer quantistici, quando saranno abbastanza stabili, romperanno la maggior parte della crittografia attuale. La crittografia post-quantum (già in sviluppo) sarà il prossimo grande capitolo della cybersecurity. Capire l'evoluzione del quantum computing aiuta a prepararsi.

**Per chi crede nel software libero**: che una tecnologia così strategica venga rilasciata open source invece di restare chiusa in laboratori proprietari è una scelta politica oltre che tecnica. E vale la pena notarla.

Il mercato del quantum computing dovrebbe superare gli 11 miliardi di dollari entro il 2030. Ising è una delle prime volte che il mondo open source entra seriamente in questo spazio.

Tienilo d'occhio.

---

**Repository**: disponibile su [GitHub](https://github.com/NVIDIA/cuda-q-academic) e [Hugging Face](https://huggingface.co/nvidia)
**Documentazione**: [nvidia.com/ising](https://www.nvidia.com/en-us/solutions/quantum-computing/ising/)
