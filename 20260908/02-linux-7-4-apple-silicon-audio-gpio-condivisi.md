---
title: "Linux 7.4 e i Mac Apple Silicon: si sblocca l'audio e il risparmio energetico 'impossibile'"
rilevanza: "MEDIA"
fonte: "https://www.phoronix.com/news/Linux-Apple-Audio-Shared-GPIO"
data_notizia: "2026-09-08"
tags: ["linux", "kernel", "apple-silicon", "asahi-linux", "hardware", "open-source"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: raccontare il lavoro paziente di mainlining di
  Asahi Linux come esempio concreto di reverse engineering fatto bene e di perché
  "farlo entrare nel kernel ufficiale" conta più che avere una patch che funziona.
  Buona occasione per un box riepilogo sullo stato di Linux sui Mac M-series nel 2026.
  Pubblico: appassionati Linux e possessori di Mac ARM curiosi.
---

Chi segue Asahi Linux — il progetto che porta Linux sui Mac con chip Apple Silicon — lo sa bene: ogni versione del kernel è un altro mattoncino che si incastra al posto giusto. L'ultimo riguarda due problemi storici e collegati fra loro: l'audio e la gestione dell'alimentazione degli altoparlanti.

## Il problema del pin condiviso

Sui Mac con SoC della serie M, il pin di spegnimento software di ogni codec audio degli altoparlanti è collegato **alla stessa identica linea GPIO**. Detta in modo semplice: un solo "interruttore" fisico controlla componenti diversi. Per il software del kernel è un rompicapo, perché ogni driver vorrebbe gestire "il suo" pin in autonomia, ma qui il pin è uno solo e va coordinato fra tutti.

Gli sviluppatori di Asahi lo avevano ribattezzato il power management "impossibile": far dormire e risvegliare i codec senza pestarsi i piedi a vicenda richiedeva acrobazie nel codice, mantenute finora solo nell'albero "downstream" di Asahi, cioè fuori dal kernel ufficiale.

## La soluzione: GPIO condivisi

Le patch pubblicate il 4 settembre 2026 sfruttano una nuova infrastruttura entrata da poco nel kernel: i **GPIO condivisi**, che permettono a più driver e componenti di usare in modo ordinato la stessa linea GPIO, con un meccanismo pulito di coordinamento.

Il driver audio Apple Silicon verrà riscritto per appoggiarsi a questa infrastruttura. Il risultato atteso è doppio:

- **audio più affidabile** sui Mac M-series con Linux
- una **architettura molto più pulita** rispetto al codice downstream attuale, che a quel punto potrà essere semplificato o eliminato

Il tutto è previsto per la merge window di **Linux 7.4**, la prossima finestra di sviluppo dopo il ciclo del 7.3.

## Perché il "mainlining" conta

Qui c'è la parte che vale la pena spiegare a chi si avvicina al mondo del kernel. Avere una patch che funziona sul proprio PC è una cosa; farla accettare nel kernel ufficiale (il "mainline") è un'altra, molto più impegnativa.

Il codice mainline deve:

- rispettare le convenzioni e le API generali del kernel, non soluzioni ad hoc
- essere rivisto da manutentori terzi, spesso con richieste di riscrittura
- restare mantenibile per anni, anche quando gli autori originali non ci sono più

Il vantaggio, in cambio, è enorme: quel supporto arriva automaticamente a **tutte** le distribuzioni che usano un kernel recente, senza patch esterne, senza repository aggiuntivi, senza rischio che qualcosa si rompa al prossimo aggiornamento. È la differenza fra "funziona se usi la nostra immagine" e "funziona e basta".

Asahi Linux ha scelto da tempo questa strada faticosa, e versione dopo versione i pezzi entrano: il grande lavoro sull'audio nel 7.1, il monitoraggio della batteria in mainline, il supporto Apple Thunderbolt apparso nel 7.3-rc1, e ora questo tassello sul power management.

## Lo stato di Linux sui Mac ARM nel 2026

Riassumendo per chi si stesse chiedendo "ma quindi Linux gira bene sui MacBook M?":

- **MacBook Air/Pro con M1 e M2**: esperienza desktop molto solida, con accelerazione grafica, Wi-Fi, audio, sospensione e gestione energetica in buona parte funzionanti
- **M3 e successivi**: supporto in progressione, più acerbo
- l'installazione resta un'operazione da utente consapevole: si affianca a macOS, non lo sostituisce del tutto, e va fatta seguendo la documentazione ufficiale

La direzione è chiara: ogni ciclo del kernel il "downstream" di Asahi si assottiglia e il mainline cresce. Linux 7.4 sarà un altro passo in quella direzione, e stavolta tocca a uno dei problemi più ostici che il team abbia affrontato.
