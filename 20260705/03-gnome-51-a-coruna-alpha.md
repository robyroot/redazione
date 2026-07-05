---
title: "GNOME 51 'A Coruña': arriva l'alpha e si vola verso settembre"
rilevanza: "MEDIA"
fonte: "https://www.phoronix.com/news/GNOME-51-Alpha"
data_notizia: "2026-07-04"
tags: ["linux", "GNOME", "desktop", "Wayland", "Flatpak", "open-source"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato per RobyRoot: i lettori che usano GNOME sul desktop (Ubuntu, Fedora, openSUSE) apprezzano sapere cosa aspettarsi nel prossimo rilascio. L'alpha di GNOME 51 è appena uscita e porta miglioramenti concreti su Wayland, Nautilus e GNOME Calendar. Un articolo leggero e ottimista, perfetto come contropunto alle notizie di sicurezza.
---

# GNOME 51 "A Coruña": arriva l'alpha e si vola verso settembre

Se usi GNOME come desktop principale, hai qualcosa di carino da aspettarti per l'autunno. È appena stata rilasciata la versione **alpha di GNOME 51**, nome in codice **"A Coruña"** — dalla città spagnola che ospiterà il GUADEC 2026 (la conferenza europea degli sviluppatori GNOME) dal 16 al 21 luglio. Il rilascio stabile è previsto per il **16 settembre 2026**.

## Costruire su basi solide

GNOME 51 parte da dove si era fermato GNOME 50 "Tokyo": un ambiente **completamente Wayland** (addio X11), con un'architettura modernizzata e una base di dipendenze più pulita. Il lavoro di questa alpha si concentra su tre fronti principali: miglioramento del **fractional scaling**, compatibilità migliorata con i **driver NVIDIA** (finalmente!), e la migrazione di ulteriori moduli da Autotools a **Meson** come sistema di build.

Non è roba che si vede subito nell'interfaccia, ma è il tipo di pulizia che rende l'ambiente più stabile e performante nel lungo periodo.

## Le novità più interessanti

**Nautilus più reattivo**

Il file manager di GNOME riceve miglioramenti alle prestazioni e all'accessibilità. Se hai una cartella con migliaia di file, dovresti notare la differenza.

**GNOME Calendar rifatto da zero**

Il calendario è stato completamente riscritto internamente: il modello dati ora usa `GListModel`, con ottimizzazioni al rendering e vari miglioramenti al codice. Non cambierà l'aspetto esteriore, ma la risposta dell'interfaccia sarà molto più fluida.

**GDM e compatibilità con KMSCON**

Il display manager GDM ora funziona correttamente con il terminale virtuale KMSCON, e c'è una nuova impostazione per cambiare la sessione di fallback. Utile per chi lavora su hardware particolare o ambienti headless.

**Epiphany più comodo**

Il browser di GNOME aggiunge una scorciatoia da tastiera per copiare l'URL della pagina corrente — una di quelle piccole cose che usavi già con altri browser e la cui mancanza era fastidiosa.

**Hardenizzazione della sicurezza**

I moduli `evolution-data-server` e `glib-networking` ricevono miglioramenti alla sicurezza interni. Non particolarmente visibili, ma importanti per chi usa GNOME in ambienti aziendali o gestisce email sensibili.

## Flatpak e l'app store condiviso

Una notizia collaterale interessante: Shelly (l'app GNOME per Flathub) nella versione 2.4.1.1 permette ora di installare applicazioni Flatpak direttamente dal sito web di Flathub cliccando sul pulsante "Install". Piccola comodità, ma elimina un passaggio per chi preferisce navigare da browser.

Nel frattempo, l'annoso progetto di un **app store condiviso tra GNOME e KDE** basato su Flatpak/Flathub continua a fare progressi lenti ma costanti. Se mai arriverà a compimento, sarà un bel momento per il desktop Linux.

## Come provare l'alpha (se sei curioso)

L'alpha è pensata per sviluppatori e testatori, non per uso quotidiano. Se vuoi comunque dare un'occhiata:

```bash
# Su Fedora Rawhide hai già accesso alle ultime build di GNOME
sudo dnf install fedora-release-rawhide
sudo dnf --releasever=rawhide distro-sync

# Oppure usa GNOME OS Nightly, l'immagine ufficiale per i test
# Disponibile su https://os.gnome.org (immagine Flatpak-based)
```

Per chi usa distro stabili, meglio aspettare: GNOME 51 arriverà su **Ubuntu 26.10** (ottobre 2026) e su **Fedora 45** (probabilmente ottobre 2026). Gli utenti Ubuntu 26.04 LTS dovranno aspettare il backport o accontentarsi di GNOME 50.

## Il calendario del rilascio

| Milestone | Data prevista |
|-----------|---------------|
| Alpha | Luglio 2026 |
| Beta | Agosto 2026 |
| RC | Settembre 2026 |
| Stabile | 16 settembre 2026 |

## Conclusione

GNOME 51 non è una rivoluzione visiva — e va bene così. Il progetto ha imboccato una strada di maturità e pulizia interna che sta dando i suoi frutti: meno bug, più performance, migliore compatibilità hardware. Con il GUADEC a luglio in Spagna e il rilascio stabile a settembre, i prossimi mesi saranno vivaci per l'ecosistema GNOME. Se sei un utente desktop Linux, hai buoni motivi per essere ottimista.
