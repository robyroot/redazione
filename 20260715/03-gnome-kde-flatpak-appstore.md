---
title: "GNOME e KDE fanno pace: nasce un app store unificato basato su Flatpak"
rilevanza: "MEDIA"
fonte: "https://blog.desdelinux.net/en/gnome-and-kde-team-up-to-create-a-flatpak-based-app-store/"
data_notizia: "2026-07-01"
tags: ["linux", "gnome", "kde", "flatpak", "desktop", "open-source"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato per RobyRoot: spiegare perché questa collaborazione è storica e cosa significa
  per gli utenti Linux desktop. Flatpak come formato universale, confronto con gli store attuali
  (GNOME Software, Discover), e cosa cambia concretamente per chi installa app su Linux.
---

# GNOME e KDE fanno pace: nasce un app store unificato basato su Flatpak

Nel mondo del desktop Linux ci sono due tribù storiche: quelli di GNOME e quelli di KDE. Anni di scelte diverse, filosofie opposte, toolkit in competizione (GTK vs Qt). Ma luglio 2026 porta una notizia che pochi avrebbero scommesso di vedere: **GNOME e KDE stanno costruendo insieme un app store basato su Flatpak**.

Se sei utente Linux desktop, questa è una delle notizie più concrete e positive degli ultimi anni.

## Il problema che questo risolve

Chiunque abbia usato Linux sul desktop conosce il problema: installare applicazioni è frammentato. Hai i pacchetti nativi della tua distribuzione (APT, DNF, Pacman), i Flatpak su Flathub, gli Snap, gli AppImage, e ogni desktop ha il suo gestore grafico con interfaccia diversa.

Su GNOME c'è **GNOME Software**. Su KDE c'è **Discover**. Entrambi funzionano, ma mostrano contenuti diversi, hanno interfacce diverse, e non parlano tra loro. Se cambi desktop environment, perdi familiarità con il tuo store di app.

Flatpak e Flathub hanno già risolto il problema a livello di formato — le app Flatpak girano su qualsiasi distribuzione. Ma mancava ancora uno **store grafico unico** che potessero condividere tutte le interfacce desktop.

## Cosa sta nascendo

L'iniziativa congiunta GNOME-KDE punta a creare un'esperienza d'uso unificata per l'installazione, l'aggiornamento e la rimozione di applicazioni Flatpak. Non si tratta di fondere i due progetti — GNOME Software e Discover continueranno ad esistere — ma di condividere:

- Un **backend comune** per la gestione delle app Flatpak
- Metadati coerenti e aggiornati da Flathub
- Standard condivisi per le notifiche di aggiornamento
- Un'interfaccia che "funziona" sia su Plasma che su GNOME senza sorprese

In pratica: installi un'app su GNOME, poi passi a KDE su un altro sistema, e trovi la stessa logica, gli stessi metadati, le stesse icone e le stesse informazioni di sicurezza.

## Perché è una buona notizia per gli utenti

Se usi Linux desktop, i benefici pratici sono concreti:

**1. Meno confusione per i nuovi arrivati.** Una delle critiche frequenti a Linux desktop è che non sai dove trovare le app. Un'esperienza unificata abbassa la barriera d'ingresso.

**2. Più app di qualità su Flathub.** Se gli sviluppatori sanno che la loro app su Flathub raggiunge tutti gli utenti desktop Linux tramite uno store unico e ben curato, hanno più incentivi a mantenerla.

**3. Sicurezza migliorata.** Flatpak usa sandbox per isolare le applicazioni. Uno store unificato può applicare politiche coerenti sui permessi e avvisare gli utenti in modo chiaro quando un'app richiede accessi particolari.

**4. Aggiornamenti più affidabili.** Backend condiviso significa meno bug legati all'interfaccia e più risorse concentrate sul funzionamento del core.

## Come si collega alle novità recenti di KDE

Questa collaborazione arriva in un momento di grande attività per KDE. **KDE neon 20260616** ha risolto i fastidiosi bug con le icone dei Flatpak nel system tray, aggiunto un tester per il microfono integrato e implementato i desktop virtuali per schermo — una funzione molto richiesta dagli utenti multi-monitor.

E **KDE Linux**, il progetto che punta a una distribuzione con base immutabile e Flatpak come formato primario per le app, è in sviluppo attivo. A giugno 2026 tutti i build hanno avuto successo e la documentazione si espande, incluso il supporto per metodi di input in cinese, giapponese, coreano e vietnamita.

## Cosa puoi fare adesso

Se vuoi iniziare a usare Flatpak e prepararti all'era dello store unificato:

```bash
# Installa Flatpak (Ubuntu/Debian)
sudo apt install flatpak

# Aggiungi Flathub come sorgente
flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo

# Riavvia il sistema, poi cerca app su Flathub
flatpak search firefox

# Installa un'app
flatpak install flathub org.mozilla.firefox

# Aggiorna tutte le app Flatpak
flatpak update
```

L'iniziativa GNOME-KDE è ancora in fase di sviluppo, senza una data di rilascio definitiva per l'app store unificato. Ma il fatto che i due principali progetti desktop Linux stiano collaborando invece di ignorarsi — o peggio, duplicare il lavoro — è già di per sé una vittoria per tutto l'ecosistema.
