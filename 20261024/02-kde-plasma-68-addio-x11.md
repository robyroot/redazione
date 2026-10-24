---
title: "KDE Plasma 6.8: dopo 30 anni, addio alle sessioni X11"
rilevanza: "ALTA"
fonte: "https://linuxiac.com/linuxiac-weekly-wrap-up-week-42-2026-october-12-18/"
data_notizia: "2026-10-18"
tags: ["kde", "plasma", "x11", "wayland", "linux-desktop"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato per RobyRoot: momento storico per il desktop Linux — spiega in modo accessibile cosa significa la fine di X11 per gli utenti normali, cosa cambia nella pratica, e come capire se si è già pronti a passare a Wayland.
---

# KDE Plasma 6.8: dopo 30 anni, addio alle sessioni X11

È ufficiale: con il rilascio di **KDE Plasma 6.8**, le sessioni X11 non sono più disponibili di default. Per chi usa Linux da qualche anno, è un po' come guardare un vecchio amico salire su un treno e partire — lo sapevi che sarebbe successo, ma fa comunque un certo effetto.

Trent'anni di X11 sul desktop KDE. Non è poco.

## Cosa sta succedendo davvero

X11 (o X Window System) è il sistema grafico che ha fatto girare praticamente tutti i desktop Linux per tre decenni. È robusto, compatibile con tutto, e incredibilmente diffuso — ma è anche vecchio, complesso da mantenere, e intrinsecamente poco sicuro per gli standard moderni.

**Wayland** è il suo successore, sviluppato per essere più semplice, più sicuro, e più performante. Il lavoro è iniziato ufficialmente nel 2008, e da allora la transizione è stata... lenta. Molto lenta. Ma ormai il treno è partito definitivamente.

Con Plasma 6.8, il team di KDE ha deciso di togliere le sessioni X11 dall'elenco predefinito delle opzioni di login. Questo non significa che X11 smette di funzionare da un giorno all'altro — significa che non lo vedrai più come scelta nel menu del display manager a meno che tu non lo riabiliti esplicitamente.

## Perché adesso?

KDE ha lavorato intensamente sulla compatibilità Wayland negli ultimi anni. Con Plasma 6.0, rilasciato all'inizio del 2024, Wayland era già diventato l'opzione predefinita. Con Plasma 6.8, si fa un passo ulteriore: X11 non scompare, ma viene de-enfatizzato.

Il team ha spiegato che la maggior parte dei casi d'uso critici che ancora richiedevano X11 — come certi workflow di screen sharing, il supporto a tablet grafici, o alcune app legacy — sono ora gestibili anche su Wayland. Non perfettamente in ogni caso, ma abbastanza bene da giustificare questo passo.

C'è anche un fattore di risorse: mantenere due stack grafici completi in parallelo è costoso in termini di tempo degli sviluppatori. Prima si consolida su Wayland, meglio è per la qualità complessiva del desktop.

## Cosa cambia per te nella pratica

Se usi già KDE Plasma con Wayland (che è il default da un paio d'anni), **non cambia assolutamente nulla**. Continui come prima.

Se invece sei tra quelli che avevano tenuto X11 per qualche ragione specifica, ecco cosa devi sapere:

**Per verificare quale sessione stai usando:**
```bash
echo $XDG_SESSION_TYPE
# output: "wayland" o "x11"
```

**Per ri-abilitare X11 su Plasma (se proprio ne hai bisogno):**
```bash
# Su Debian/Ubuntu, installa il pacchetto KDE Wayland/X11 aggiuntivo
sudo apt install plasma-workspace-x11

# Su Fedora
sudo dnf install plasma-workspace-x11
```

Dopo aver installato il pacchetto, l'opzione "Plasma (X11)" tornerà disponibile nella schermata di login.

## Le app legacy: XWayland fa ancora il suo lavoro

Una delle preoccupazioni più comuni è quella delle app che non supportano Wayland natively — vecchi software, applicazioni commerciali, strumenti di niche. La risposta è **XWayland**, un livello di compatibilità che fa girare le app X11 all'interno di una sessione Wayland.

XWayland non viene rimosso. Continua a funzionare esattamente come prima per tutte le app che non si sono ancora adeguate.

```bash
# Per verificare se un'app sta usando XWayland
xlsclients  # lista le app X11 nella sessione corrente

# Oppure cerca nel nome del processo
ps aux | grep Xwayland
```

## I casi ancora problematici

Essere onesti è importante: ci sono ancora alcune situazioni in cui Wayland può dare problemi:

- **Applicazioni che usano screenshot/cattura schermo con API X11 native** — qualcuno potrebbe non funzionare bene
- **Certi setup multi-monitor con scale miste** — migliorato molto, ma non sempre perfetto
- **Alcune soluzioni VNC/RDP** — funzionano, ma possono richiedere configurazione aggiuntiva

Se sei in questi casi, hai ancora l'opzione di tornare a X11 come descritto sopra. Ma per la stragrande maggioranza degli utenti, Wayland è ormai pronto.

## Un momento storico per il desktop Linux

C'è qualcosa di simbolicamente importante in questa notizia. X11 è stato per decenni il "collante invisibile" che teneva insieme l'esperienza desktop Linux. Vederlo uscire di scena — anche gradualmente — segna una maturazione importante dell'ecosistema.

Wayland è più moderno, più sicuro, e consente funzionalità che X11 non avrebbe mai potuto supportare elegantemente (pensa al supporto HDR, al fractional scaling, all'isolamento delle app). Questa transizione era necessaria.

E se ci sono voluti 30 anni per arrivarci... be', il software libero ha i suoi tempi. Ma alla fine ci arriva sempre.
