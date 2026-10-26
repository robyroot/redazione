---
title: "KDE Plasma 6.8: dopo 30 anni, X11 va in pensione"
rilevanza: "ALTA"
fonte: "https://linuxiac.com/?p=221075"
data_notizia: "2026-10-14"
tags: ["KDE", "Wayland", "X11", "Linux", "desktop", "Plasma"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato per RobyRoot: spiegare cosa significa concretamente per l'utente medio passare a Wayland, sfatare la paura del cambiamento e dare indicazioni pratiche su cosa fare se si dipende ancora da X11.
---

# KDE Plasma 6.8: dopo 30 anni, X11 va in pensione

Il 14 ottobre 2026, nel giorno del suo **30° compleanno**, KDE ha lanciato un messaggio chiaro a tutta la comunità Linux: l'era di X11 come sessione desktop è ufficialmente finita. Con **KDE Plasma 6.8**, il protocollo grafico che ha dominato il desktop Linux per tre decenni lascia il posto a Wayland come unico sistema di visualizzazione supportato.

È un momento storico. E, come quasi tutti i momenti storici nel mondo open source, porta con sé un misto di entusiasmo e qualche legittima preoccupazione.

## Cosa cambia davvero per te

Per capire l'impatto pratico, è importante distinguere due cose:

**La sessione X11 di Plasma è andata.** Questo significa che quando avvii KDE Plasma 6.8, non trovi più l'opzione "Plasma (X11)" nella schermata di login. Wayland è l'unica scelta disponibile.

**Le app X11 continuano a funzionare.** Le applicazioni che usano ancora X11 — inclusi vecchi programmi e giochi — possono girare normalmente tramite **XWayland**, uno strato di compatibilità che traduce le chiamate X11 in Wayland. Per l'utente finale questo processo è completamente trasparente.

In breve: cambia come il desktop stesso funziona internamente, ma la maggior parte delle applicazioni che già usi non avrà problemi.

## Perché proprio adesso

La transizione era nell'aria da tempo. Secondo i dati di telemetria del progetto KDE, al momento del rilascio della 6.7 ben il **95% degli utenti di Plasma 6.6 stava già usando Wayland**. La sessione X11 era sopravvissuta per dare tempo agli utenti e agli sviluppatori di applicazioni di adattarsi; quel tempo è ormai scaduto.

Wayland offre vantaggi significativi rispetto a X11: migliore sicurezza (le app non possono "spiare" le altre finestre), supporto nativo per schermi ad alta risoluzione, migliore gestione del color management e prestazioni migliori su hardware moderno.

## Le novità di Plasma 6.8

Oltre alla storica rimozione di X11, Plasma 6.8 porta alcune novità interessanti:

- **Triple buffering per NVIDIA**: abilitato di default, riduce la latenza su GPU NVIDIA e migliora la fluidità visiva.
- **Integrazione Flatpak con Edge**: supporto per la versione Flatpak di Microsoft Edge in Plasma Browser Integration (sì, anche su Linux Edge ha i suoi utenti).
- **Miglioramenti generali a Wayland**: stabilità e compatibilità ancora migliorate per i casi limite.

## E se dipendo ancora da X11?

Se hai hardware o software che richiede assolutamente X11, le opzioni ci sono:

**1. Continua a usare Plasma 6.7**: il supporto per la sessione X11 in Plasma 6.7 proseguirà almeno fino a inizio 2027. Non è una soluzione permanente, ma dà tempo per trovare alternative.

**2. Distribuzioni LTS**: se usi una distribuzione con supporto a lungo termine che include una versione di Plasma precedente, sei a posto per anni. AlmaLinux 9, per esempio, include Plasma con sessione X11 ed è supportata fino al 2032.

**3. XWayland per le app problematiche**: per la maggior parte dei software "legacy", XWayland funziona benissimo. Vale la pena testare prima di preoccuparsi.

## Come verificare se sei pronto

Se già usi KDE Plasma, puoi controllare in che sessione stai girando:

```bash
echo $XDG_SESSION_TYPE
```

Se restituisce `wayland`, sei già sulla strada giusta. Se restituisce `x11`, il passaggio ti riguarda.

Per controllare la versione di Plasma installata:

```bash
plasmashell --version
```

## Un compleanno che segna un'epoca

Trent'anni fa, nel 1996, Matthias Ettrich annunciò il progetto KDE con l'obiettivo di creare un desktop usabile per Unix. Da allora KDE ha attraversato versioni, polemiche (chi ricorda il controverso passaggio a KDE 4?), fork, e rinnovamenti continui. Scegliere il proprio 30° anniversario per compiere questo passo simbolico non sembra casuale.

Wayland è il futuro del desktop Linux. Con Plasma 6.8, KDE ha ufficialmente smesso di guardare indietro.
