---
title: "KDE Plasma 6.8: addio a X11, da ottobre solo Wayland"
rilevanza: "ALTA"
fonte: "https://9to5linux.com/kde-plasma-6-8-desktop-environment-to-drop-the-x11-session-and-go-wayland-only"
data_notizia: "2026-09-27"
tags: ["kde", "wayland", "linux-desktop", "plasma", "x11"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato per RobyRoot: guida pratica per gli utenti che usano ancora X11 su KDE — cosa cambia, cosa fare, come verificare di essere già su Wayland o come migrarsi. Ottima opportunità per spiegare perché Wayland è meglio per la privacy (niente keylogging tra app, isolamento delle finestre).
---

# KDE Plasma 6.8: addio a X11, da ottobre solo Wayland

Il 14 ottobre 2026, con il rilascio di **KDE Plasma 6.8**, succederà qualcosa che gli utenti Linux aspettano (o temono) da anni: la sessione X11 sparirà dal login manager. Dopo trent'anni di onorata carriera, X11 va in pensione su KDE. Wayland diventa l'unica scelta.

## Cosa significa concretamente

Se usi KDE Plasma e al login hai sempre scelto "Plasma (X11)" invece di "Plasma (Wayland)", da ottobre quella voce non ci sarà più. Il login manager mostrerà solo la sessione Wayland.

Questo **non significa** che i tuoi programmi X11 smettono di funzionare. XWayland continua a girare in background e fa da ponte per tutte le app che non sono ancora migrate nativamente a Wayland. La differenza non la noterai quasi per nulla nell'uso quotidiano.

Quello che cambia è che non puoi più scegliere di avviare un'intera sessione desktop basata su X11. Il compositor, il gestore finestre, tutto il layer grafico sarà Wayland.

## Perché è una buona notizia

X11 è un protocollo degli anni '80, progettato in un'epoca in cui la sicurezza non era una priorità. Uno dei problemi più famosi è che **qualsiasi app può leggere l'input di un'altra app** — incluse le pressioni di tasto. È la ragione per cui i keylogger funzionano così bene su X11.

Wayland risolve tutto questo con un modello di isolamento molto più solido: ogni app vede solo la propria finestra, non può intercettare l'input di altre applicazioni. Per chi usa Linux anche per motivi di privacy, questa è una differenza sostanziale.

Oltre alla sicurezza, Wayland porta miglioramenti concreti:

- **HDR** (High Dynamic Range) nativo, già funzionante su Plasma
- **Variable Refresh Rate** (VRR/FreeSync/G-Sync) senza configurazioni manuali
- **Scaling frazionario** per i monitor HiDPI, molto più stabile che su X11
- **Condivisione schermo** funziona correttamente con PipeWire

## I numeri che hanno convinto KDE

KDE non ha fatto questo salto nel vuoto. I dati telemetrici degli utenti di Plasma 6.6 mostrano che il **95% ha già migrato spontaneamente a Wayland**. Solo il 5% rimane su X11, e in buona parte si tratta di situazioni edge case: driver proprietari vecchi, configurazioni multi-monitor complesse, software professionale con dipendenze specifiche.

Con queste cifre, mantenere la sessione X11 significherebbe investire tempo di sviluppo per un'opzione che quasi nessuno usa.

## Cosa fare se usi ancora X11

Prima di tutto, verifica su quale sessione stai girando. Apri un terminale e digita:

```bash
echo $XDG_SESSION_TYPE
```

Se risponde `wayland`, sei già a posto. Se risponde `x11`, hai ancora qualche settimana per testare la migrazione prima che diventi obbligatoria.

Per passare a Wayland manualmente:
1. Fai logout dal desktop
2. Nel login manager (SDDM), clicca sul tuo utente
3. In basso a sinistra cerca il menu della sessione
4. Seleziona **"Plasma (Wayland)"**
5. Fai login e testa

Se qualcosa non funziona, puoi ancora tornare su X11 scegliendo la sessione al prossimo login — finché esiste, ovviamente.

## Le eccezioni: quando X11 potrebbe mancarti

Ci sono scenari reali dove X11 ha ancora qualcosa da offrire:

- **GPU NVIDIA con driver proprietary vecchi**: il supporto Wayland di NVIDIA è migliorato moltissimo negli ultimi anni, ma driver molto datati potrebbero avere problemi
- **Software di registrazione screen legacy**: alcune app non supportano ancora correttamente il protocollo di screen capture di Wayland
- **Configurazioni multi-GPU complesse**: setup ibridi GPU Intel+NVIDIA possono ancora dare grattacapi

In questi casi, XWayland copre la maggior parte dei problemi. Ma se hai un caso limite, vale la pena testare prima del 14 ottobre.

## Il contesto più ampio: anche GNOME si è già mossa

KDE non è sola in questa direzione. GNOME ha già rimosso il supporto X11 nelle versioni più recenti, e la maggior parte delle distribuzioni principali ha Wayland come default da tempo. Fedora ce l'ha di default dal 2021, Ubuntu dal 2022.

Il 2026 si conferma l'anno in cui X11 va definitivamente in archivio. Era ora.
