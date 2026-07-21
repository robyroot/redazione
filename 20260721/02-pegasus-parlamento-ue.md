---
title: "Pegasus spiava l'eurodeputato che indagava su Pegasus: il paradosso che spinge l'UE ad agire"
rilevanza: "ALTA"
fonte: "https://edri.org/our-work/edri-gram-16-july-2026/"
data_notizia: "2026-07-03"
tags: ["privacy", "spyware", "sorveglianza", "UE", "Pegasus", "cybersecurity"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato per RobyRoot: la storia è perfetta per un mix tra sicurezza informatica e diritti digitali. Sottolineare l'ironia della situazione (l'investigatore spiato mentre investigava) e le implicazioni pratiche per i cittadini italiani, già scottati dallo spyware Paragon. Ottimo per sensibilizzare sul tema.
---

# Pegasus spiava l'eurodeputato che indagava su Pegasus: il paradosso che spinge l'UE ad agire

Ci sono storie che sembrano uscite da un film di spionaggio, ma purtroppo sono reali. Il 3 luglio 2026, il **Citizen Lab** dell'Università di Toronto ha pubblicato un'analisi forense che ha del paradossale: **Stelios Kouloglou**, ex europarlamentare greco e giornalista investigativo, è stato infettato con lo spyware **Pegasus** dell'azienda israeliana NSO Group — mentre serviva nella **commissione parlamentare europea che indagava proprio su Pegasus**.

Non è uno scherzo. L'investigatore era sotto sorveglianza mentre investigava sulla sorveglianza.

## Cosa è successo esattamente

Secondo la ricostruzione del Citizen Lab, il telefono di Kouloglou è stato compromesso almeno due volte:

- **21 ottobre 2022**: prima infezione documentata
- **6 e 7 marzo 2023**: seconda infezione

In quel periodo, Kouloglou era membro sostituto della **commissione PEGA** (Committee of Inquiry to investigate the use of Pegasus and equivalent surveillance spyware). Una commissione istituita proprio per fare luce sull'uso degli spyware da parte dei governi UE.

L'accesso al suo telefono significava potenzialmente accesso a documenti riservati, comunicazioni con altri membri della commissione, testimoni e fonti protette.

## Chi c'è dietro? Il Citizen Lab non lo dice (ancora)

La parte frustrante — ma metodologicamente corretta — dell'analisi è che il Citizen Lab **non attribuisce l'attacco a un governo specifico**. Quello che dicono è che l'autore probabilmente NON è il governo greco (nonostante la Grecia sia già coinvolta in altri scandali spyware con Predator), e che il pattern ricorda un cliente già investigato in passato da Citizen Lab e Access Now.

In sostanza: qualcuno con accesso a Pegasus NSO, non greco, ha deciso che un europarlamentare che indagava sugli spyware era un bersaglio interessante. Il che è, a dir poco, inquietante.

## La risposta della società civile

La rivelazione ha scatenato una reazione immediata. Un gruppo di **organizzazioni per i diritti civili** — tra cui EDRi, Amnesty International Security Lab e il Center for Democracy and Technology — ha pubblicato una dichiarazione congiunta chiedendo all'UE di agire.

Le richieste principali:

1. **Rafforzare l'enforcement** del Regolamento UE sul dual-use, che dovrebbe già limitare l'export di tecnologie di sorveglianza
2. **Audit completo** su come i fondi europei vengano usati da aziende coinvolte nello sviluppo di spyware
3. **Valutazione dell'impatto sui diritti fondamentali** nell'aggiornamento del regolamento
4. **Partecipazione della società civile** nei processi decisionali

La frustrazione è evidente: la commissione PEGA aveva già formulato raccomandazioni anni fa, e la Commissione europea è stata lenta nell'implementarle.

## Il collegamento con l'Italia

La storia tocca da vicino anche noi italiani. L'Italia è già stata al centro di uno scandalo simile: il Citizen Lab aveva documentato l'uso dello spyware **Graphite di Paragon** contro giornalisti e attivisti italiani. Paragon è un'azienda israeliana con forti legami commerciali in Europa — inclusa l'Italia.

Insomma, l'ecosistema degli spyware non è un problema astratto: è una minaccia concreta per giornalisti, attivisti, avvocati e chiunque si occupi di tematiche sensibili.

## Cosa puoi fare (concretamente)

Se ti occupi di giornalismo, attivismo o semplicemente tieni alla tua privacy:

```bash
# Mobile Verification Toolkit (MVT) - per controllare se il tuo telefono è compromesso
pip3 install mvt

# Analisi di un backup iOS
mvt-ios check-backup /path/to/backup --iocs ~/iocs/pegasus.stix2

# Analisi di un dump Android
mvt-android check-adb --iocs ~/iocs/pegasus.stix2
```

Puoi scaricare gli indicatori di compromissione (IOCs) aggiornati dal repository di Amnesty International Security Lab su GitHub.

Per una protezione più generale, considera:
- **GrapheneOS** se hai un Pixel (la scelta più robusta per Android)
- **Signal** per le comunicazioni sensibili
- Aggiornamenti regolari: molti spyware sfruttano vulnerabilità già patchate

## Il quadro più ampio

La storia di Kouloglou non è un caso isolato. Secondo le ultime stime, decine di giornalisti, avvocati e funzionari pubblici in Europa sono stati bersagliati da spyware commerciali negli ultimi anni. Il problema è sistemico.

L'UE ha gli strumenti normativi per affrontarlo, ma manca la volontà politica — o meglio, c'è una tensione tra gli stati membri che vogliono usare questi strumenti per scopi di "sicurezza nazionale" e i principi fondamentali di uno stato di diritto.

Il paradosso di Kouloglou — l'investigatore spiato mentre investigava — è il simbolo perfetto di questa contraddizione.
