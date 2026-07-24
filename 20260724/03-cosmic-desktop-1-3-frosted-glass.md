---
title: "COSMIC Desktop 1.3: arriva il vetro smerigliato e cresce l'alternativa Rust a GNOME e KDE"
rilevanza: "MEDIA"
fonte: "https://ubuntuhandbook.org/index.php/2026/07/cosmic-desktop-1-3-0-released-with-frosted-glass-ui-design/"
data_notizia: "2026-07-24"
tags: ["linux", "desktop-environment", "cosmic", "rust", "pop-os"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato: pezzo "leggero" da abbinare a screenshot/video del frosted glass per i social.
  Buona occasione per introdurre ai lettori meno esperti cosa sia COSMIC e perché un desktop scritto
  in Rust (invece che C/C++ come GNOME/KDE storicamente) sia interessante anche dal punto di vista
  della sicurezza e stabilità del sistema. Menzionare che al momento resta un ambiente per chi ama
  smanettare (PPA non ufficiali, pacchetti ancora indietro su Arch) più che una scelta plug-and-play.
---

Chi segue il mondo Linux da un po' avrà notato che, dopo anni in cui la scelta del desktop si riduceva praticamente a GNOME contro KDE Plasma (con qualche incursione di XFCE o Cinnamon per i nostalgici), negli ultimi tempi è spuntato un nuovo protagonista che sta facendo parecchio rumore: COSMIC, il desktop environment sviluppato da System76, l'azienda dietro Pop!_OS. E con la versione 1.3.0, appena rilasciata, COSMIC aggiunge un tocco estetico che farà felici gli amanti del design: l'effetto vetro smerigliato.

## Cos'è il "frosted glass" e come si attiva

La novità principale di questa release è la possibilità di applicare un effetto di trasparenza "sfocata" — quello che in inglese chiamano frosted glass — alla maggior parte degli elementi dell'interfaccia: pannelli, menu, finestre delle applicazioni, la vista d'insieme (l'equivalente dell'Activities di GNOME) e i controlli rapidi a schermo. Non è solo un interruttore on/off: da Impostazioni → Desktop → Aspetto puoi regolare sia lo spessore della trasparenza sia il livello di opacità del vetro, per trovare l'equilibrio giusto tra effetto estetico e leggibilità. Se ti ricordi l'Aero Glass di Windows Vista o certi temi Compiz di vent'anni fa, l'idea di fondo è quella — ma rifatta con un motore grafico moderno e accelerato via GPU.

## Le altre novità della 1.3

Al di là dell'effetto vetro, che sarà quello che finirà in tutti gli screenshot, la release porta con sé una serie di miglioramenti più pratici:

- **Supporto AVIF per gli sfondi**, grazie all'integrazione della libreria `libdav1d`: puoi finalmente usare direttamente immagini in questo formato moderno e più efficiente come wallpaper, senza doverle prima convertire in JPEG o PNG.
- **Opzione "nascondi sempre" per i pannelli**, utile per chi vuole il massimo dello spazio schermo disponibile e preferisce richiamare la barra solo quando serve.
- **Preservazione dello stile del pannello e del dock** quando massimizzi una finestra, un dettaglio piccolo ma che chi passa da un ambiente all'altro apprezzerà.
- **Monitor di sistema più completo**, con supporto alla sospensione della GPU NVIDIA e monitoraggio dei consumi energetici anche per le GPU AMD e Intel — utile per chi lavora su laptop e tiene d'occhio l'autonomia della batteria.

Sul fronte dei bug fix, sono stati risolti diversi problemi minori ma fastidiosi: lo scroll del mouse che non funzionava correttamente sulle icone della system tray, il Bluetooth che a volte non mostrava i dispositivi già accoppiati, corruzioni grafiche nei setup con più GPU, e alcuni gesti sul touchpad che non rispondevano come previsto.

## Perché COSMIC merita attenzione

Se non l'hai ancora provato, il motivo per cui vale la pena tenerlo d'occhio non è solo estetico. COSMIC è scritto (quasi) interamente in Rust, un linguaggio che per sua natura elimina intere categorie di bug legati alla gestione della memoria — quelli che storicamente affliggono progetti C/C++ più datati come parti di GNOME o KDE. Non significa che COSMIC sia "più sicuro" in senso assoluto, ma la scelta architetturale riflette una tendenza più ampia nell'ecosistema Linux, dove sempre più componenti di sistema vengono riscritti in linguaggi memory-safe.

Va detto con onestà: COSMIC non è ancora pronto per l'utente che vuole solo "installare e usare". La disponibilità nei repository varia parecchio a seconda della distro: su Fedora 45 arriva direttamente nei repository ufficiali, su Arch Linux (repository Extra) al momento si trova ancora alla versione 1.2.0, mentre su Ubuntu, la distro di casa di System76, bisogna appoggiarsi a un PPA non ufficiale per la versione 26.04. Chi vuole provarlo con il minimo sforzo probabilmente farà meglio a partire direttamente da Pop!_OS, dove COSMIC è l'ambiente predefinito e riceve gli aggiornamenti più rapidamente.

Per chi ama smanettare e vuole vedere con i propri occhi dove sta andando il desktop Linux nei prossimi anni, però, questa 1.3 con il suo vetro smerigliato è un ottimo motivo per fare un salto su una VM di prova.
