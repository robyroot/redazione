---
title: "Branch Target Reuse: il nuovo attacco Spectre-v2 che ruba la password di root da Linux"
rilevanza: "ALTA"
fonte: "https://thehackernews.com/2026/09/new-spectre-v2-btr-attack-leaks-linux.html"
data_notizia: "2026-09-29"
tags: ["linux", "kernel", "sicurezza", "spectre", "cpu", "hardware", "vulnerabilità"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: ottimo mix tra Linux, sicurezza hardware e praticità. Il pubblico di RobyRoot capirà immediatamente la gravità perché Spectre è già conosciuto. Da spiegare bene la parte del JIT compiler che è il punto nuovo e interessante.
---

# Branch Target Reuse: il nuovo attacco Spectre-v2 che ruba la password di root da Linux

Spectre è di nuovo tra noi. Questa volta si chiama **Branch Target Reuse (BTR)** ed è una variante dell'attacco Spectre-v2 che i ricercatori della Vrije Universiteit Amsterdam e della Scuola Superiore Sant'Anna hanno scoperto e documentato nelle ultime settimane.

Il risultato pratico: un exploit funzionante in grado di estrarre l'hash della password di root direttamente dalla memoria del kernel Linux su CPU Intel, AMD e ARM.

## Come funziona (senza impazzire)

Per capire BTR bisogna tornare un attimo alle basi di Spectre. Le CPU moderne sono incredibilmente brave a "prevedere" quale codice eseguiranno subito dopo: è la **branch prediction**, e fa guadagnare moltissimo in performance.

Il problema? Quando la CPU si sbaglia nella previsione, ha già iniziato ad eseguire codice speculativamente — e questo codice, anche se poi viene "annullato", può lasciare tracce nella cache del processore che un attaccante può leggere.

BTR aggiunge una novità rispetto ai classici attacchi Spectre-v2: si concentra su ambienti che generano codice **dinamicamente**, come i compilatori JIT. Quando la JVM di Java, il motore V8 di Chrome, o il BPF JIT del kernel Linux riutilizzano un blocco di memoria per nuovo codice, le voci di branch prediction precedenti **non vengono invalidate automaticamente** dalla CPU.

Un attaccante può quindi manipolare queste voci stantie per far eseguire al processore codice speculativo che legge dati sensibili dalla memoria del kernel — inclusi gli hash delle password di root.

## Quali CPU sono vulnerabili

Praticamente tutte quelle moderne. I ricercatori hanno verificato il comportamento necessario per BTR su:

- **Intel**: dalla generazione Kaby Lake in poi
- **AMD**: Zen 2, Zen 3, Zen 4
- **ARM**: Cortex-A e Neoverse

In pratica, se hai un computer degli ultimi 8-10 anni, il tuo processore probabilmente ha il comportamento sfruttato da BTR.

## Il Linux kernel ha già le patch

La buona notizia è che il Linux kernel team ha risposto rapidamente. Le mitigazioni, tracciate come **CVE-2026-64507** e **CVE-2026-64508**, aggiungono:

1. **Flush dello stato di branch prediction** quando la memoria BPF JIT viene riutilizzata
2. **Hardening contro il JIT spraying**, una tecnica che rende più difficile piazzare codice malevolo in posizioni prevedibili

E proprio questa settimana il kernel ha rilasciato sette aggiornamenti stabili in un solo giorno (dalla 7.2.9 alla 5.10.271) che includono, tra le altre cose, queste fix.

Per verificare se il tuo sistema ha le patch:

```bash
# Controlla la versione del kernel
uname -r

# Verifica le mitigazioni Spectre attive
cat /sys/devices/system/cpu/vulnerabilities/spectre_v2

# Aggiorna su distribuzioni basate su apt
sudo apt update && sudo apt upgrade linux-image-generic

# Su Fedora/RHEL
sudo dnf upgrade kernel
```

## L'impatto pratico: devo preoccuparmi?

Per i desktop personali, il rischio è basso: l'attacco richiede di eseguire codice sul sistema bersaglio. Se sei l'unico utente del tuo laptop e non esegui codice non fidato, non hai molto di cui preoccuparti.

Per i **server multi-tenant, ambienti cloud, e sistemi con utenti multipli** è un'altra storia. Un attaccante che riesce a eseguire codice (anche unprivileged) su un server condiviso potrebbe potenzialmente estrarre dati da altri utenti o dal kernel stesso.

La raccomandazione è la solita, ma non per questo meno valida: **aggiorna il kernel**. Il fatto che sette versioni stabili siano uscite in un solo giorno mostra quanto il kernel team prenda sul serio la questione.

## Il ciclo che non finisce

BTR ci ricorda che le vulnerabilità hardware come Spectre non si risolvono davvero — si mitigano. Ogni nuova generazione di compilatori JIT o di funzionalità kernel è potenzialmente un nuovo vettore di attacco se interagisce male con i meccanismi di predizione delle CPU.

La battaglia tra ottimizzazione delle performance e sicurezza nel silicio è destinata a continuare. Per ora, però, il kernel Linux ha già i cerotti al posto giusto: basta applicarli.
