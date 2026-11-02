---
title: "Linux 7.3 è la nuova versione stabile: il kernel 7.2 va in pensione"
rilevanza: "MEDIA"
fonte: "https://9to5linux.com/9to5linux-weekly-roundup-november-1st-2026"
data_notizia: "2026-10-18"
tags: ["linux", "kernel", "aggiornamento", "sicurezza", "distro"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato per RobyRoot: accessibile per tutti, includi comandi pratici per verificare la versione del kernel e aggiornare sulle distro più comuni. Enfatizza la fine del supporto per 7.2.
---

# Linux 7.3 è la nuova versione stabile: tempo di aggiornare e dire addio al kernel 7.2

Se segui il mondo Linux con una certa attenzione, probabilmente sai già che ogni qualche mese esce una nuova versione stabile del kernel. Questa volta è il turno di **Linux 7.3**, rilasciato ufficialmente il **18 ottobre 2026** da Linus Torvalds. E con lui arriva anche una notizia importante: il ramo **7.2 ha raggiunto la fine del supporto**.

## Cosa significa "fine del supporto" per il kernel 7.2

Greg Kroah-Hartman, il manutentore del kernel stable, ha rilasciato la versione **7.2.15** indicandola come l'ultima della serie. Nessuna patch di sicurezza arriverà più per il ramo 7.2: se la tua distribuzione usa ancora quel kernel, è il momento di pianificare un aggiornamento.

Non è una crisi, ma è un promemoria importante: i kernel non supportati non ricevono fix di sicurezza, e nel corso dei mesi le vulnerabilità possono accumularsi.

## Cosa c'è di nuovo in Linux 7.3

Il ciclo di sviluppo del 7.3 ha portato diverse migliorie interessanti:

- **Supporto hardware ampliato**: nuovi driver per GPU, aggiornamenti per piattaforme ARM e RISC-V
- **Miglioramenti alle prestazioni I/O**: ottimizzazioni nel sottosistema di storage, particolarmente utili per NVMe ad alta velocità
- **Sicurezza del kernel**: nuove mitigazioni per attacchi speculativi e raffinamenti nei meccanismi di sandboxing
- **Supporto WiFi 7**: avanzamento nel supporto per i nuovi standard wireless
- **Ottimizzazioni per CPU moderne**: miglioramenti per le architetture Intel Lunar Lake e AMD Zen 6

Nello stesso rilascio, Kroah-Hartman ha anche pubblicato gli aggiornamenti per i rami a lungo termine: **7.3.1**, **6.18.60**, **6.12.115**, **6.6.161**, **6.1.191**, **5.15.224** e **5.10.273**. I rami LTS continuano a ricevere patch di sicurezza indipendentemente dalle versioni principali.

## Quale versione del kernel stai usando?

Prima di tutto, verifica:

```bash
# Versione del kernel corrente
uname -r

# Informazioni più dettagliate
uname -a

# Con il flag -v per la data di build
uname -v
```

Se vedi `7.2.x` nell'output, sei nel ramo che ha appena perso il supporto.

## Come aggiornare il kernel

Il modo più sicuro è sempre quello di affidarsi al gestore pacchetti della tua distribuzione:

```bash
# Arch Linux (usa già kernel 7.3 con gli aggiornamenti recenti)
sudo pacman -Syu

# Fedora 45 (beta, con 7.3 incluso)
sudo dnf upgrade --refresh

# Ubuntu 26.04 LTS (potrebbe richiedere HWE kernel per 7.3)
sudo apt update && sudo apt upgrade

# openSUSE Tumbleweed
sudo zypper refresh && sudo zypper update
```

Su **Arch Linux**, il kernel 7.3 è già disponibile nei repository principali. L'ISO di novembre 2026 include però ancora il 7.2.11 — se hai installato recentemente con quella ISO, un semplice `pacman -Syu` completo penserà a tutto.

## Il ciclo di sviluppo continua: 7.4 è già in arrivo

Nel frattempo, il ciclo di sviluppo non si ferma mai. LWN riporta che **Linux 7.4-rc1** è già stato rilasciato, segnalando la chiusura della merge window per quel ciclo. L'rc1 è la prima release candidate, tipicamente instabile e destinata a sviluppatori e tester — non è per uso quotidiano.

Se vuoi seguire il kernel in tempo reale, il posto migliore è sempre [kernel.org](https://kernel.org) e il blog di Greg Kroah-Hartman su LWN.

## Vale la pena aggiornare subito?

Se usi una rolling release come Arch o openSUSE Tumbleweed, l'aggiornamento arriverà automaticamente nel normale ciclo. Per le distro a rilascio fisso come Ubuntu o Debian, dipende dalla politica di backporting del kernel — spesso il kernel LTS resta quello supportato per tutta la vita della release.

L'importante è sapere che stai usando, e che il tuo kernel riceve ancora patch di sicurezza. Un kernel obsoleto e non aggiornato è una finestra aperta per chi vuole entrare.
