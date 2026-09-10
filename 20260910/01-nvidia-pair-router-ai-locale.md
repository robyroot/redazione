---
title: "NVIDIA PAIR: un router open source per far girare l'AI su tutti i PC di casa"
rilevanza: "ALTA"
fonte: "https://blogs.nvidia.com/blog/local-ai-ifa-next-gen-agents-nv-pair-rtx-spark/"
data_notizia: "2026-09-10"
tags: ["intelligenza-artificiale", "open-source", "privacy", "self-hosting"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato: "local-first AI" e privacy. PAIR permette di sfruttare hardware
  che hai gia in casa senza mandare prompt e file nel cloud. Da collegare al filone
  Ollama/LM Studio gia trattato su RobyRoot. Essere onesti sui limiti: gira solo su
  GPU NVIDIA recenti e Apple Silicon M4+, e distribuisce interi job (non e tensor
  parallelism), quindi non fa girare un modello piu grande della singola macchina.
  Utile un box "come si prova in 10 minuti" con un mini-lab a due PC.
---

# NVIDIA PAIR: un router open source per l'AI locale

Il 3 settembre NVIDIA ha rilasciato in beta **Personal AI Router**, abbreviato in **PAIR**: un software libero, pubblicato su GitHub con licenza Apache 2.0, che trasforma i computer della tua rete domestica in un piccolo cluster per l'inferenza AI. L'idea e semplice e, per chi tiene alla privacy, parecchio interessante: invece di mandare le richieste a un servizio cloud, le smisti tra i PC che hai gia in casa, tenendo prompt, file e contesto degli agenti dentro la tua LAN.

## Cosa fa (e cosa non fa)

Nonostante il nome, PAIR non e un router hardware e nemmeno un nuovo motore di inferenza. I modelli continuano a girare dove giravano prima, cioe dentro **Ollama** o **LM Studio**. PAIR si mette in mezzo: scopre in automatico gli altri PC compatibili sulla rete (usa mDNS per il discovery e mTLS per cifrare il traffico tra i nodi), tiene traccia di quali macchine sono libere e a quale modello, e quando arriva una richiesta la manda a chi ha capacita in quel momento. Poi restituisce la risposta all'applicazione che l'aveva chiesta.

All'applicazione, PAIR espone due endpoint: uno compatibile con Ollama e uno compatibile con le API OpenAI. Questo significa che qualsiasi client o agente che gia parla con Ollama o con un endpoint OpenAI-like puo usare PAIR senza modifiche.

Il punto debole da capire subito e che la distribuzione avviene **a livello di job**: PAIR prende un'intera richiesta e la assegna a una macchina libera. E perfetto per carichi paralleli, tipo un'app multi-agente che spezza un compito in tanti sotto-task indipendenti, o piu utenti in casa che fanno domande contemporaneamente. Non e invece pensato per far girare un modello che non entra nella singola GPU: quello richiederebbe il tensor parallelism, che qui non c'e. Inoltre il modello deve essere gia presente sul nodo che lo deve eseguire.

## Hardware richiesto

Qui arriva la nota dolente per chi ha un parco macchine misto. PAIR supporta le GPU **NVIDIA GeForce RTX serie 20 e successive**, le RTX PRO da workstation, i sistemi **DGX Spark** e i **Mac con Apple Silicon M4 o piu recenti**. Niente Radeon, niente Intel Arc, niente schede piu vecchie. Il software gira comunque su Windows, macOS e Linux, con interfaccia grafica e da riga di comando.

## Perche ne parliamo su RobyRoot

Il tema dell'AI "che resta a casa tua" e sempre piu concreto. Chi usa gia Ollama sul PC fisso e magari ha un portatile o un secondo desktop che passa gran parte del tempo acceso e inutilizzato, con PAIR puo mettere a fattor comune quella potenza senza dover riscrivere nulla. E soprattutto senza che una singola parola dei tuoi prompt esca dalla rete locale: nessun account, nessun log lato provider, nessun dubbio su come vengono usati i tuoi dati per addestrare il prossimo modello.

C'e anche un aspetto piu strategico. Il fatto che sia proprio NVIDIA a rilasciare uno strumento del genere, per giunta con licenza permissiva, racconta bene dove sta andando il mercato: l'inferenza locale non e piu una nicchia da smanettoni, ma un caso d'uso che i produttori di hardware vogliono spingere. Per l'ecosistema open source e una buona notizia, con l'asterisco del lock-in: PAIR "apre" il codice ma spinge verso schede NVIDIA e Mac recenti.

## Come iniziare

Il progetto e su GitHub sotto `NVIDIA/Personal-AI-Router`, con installer firmati per Windows, macOS e Linux. Per una prova minima bastano due macchine sulla stessa rete: si installa PAIR su entrambe, si abilita Ollama o LM Studio, si scaricano gli stessi modelli sui nodi e si punta il proprio client all'endpoint di PAIR. Trattandosi di una beta, mettete in conto qualche spigolo: vale la pena testarlo in un lab prima di farci affidamento per il lavoro quotidiano.
