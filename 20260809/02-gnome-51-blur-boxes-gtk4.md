---
title: "GNOME 51 in arrivo: sfocatura nativa su Wayland e Boxes riscritto da zero"
rilevanza: "MEDIA"
fonte: "https://ubuntuhandbook.org/index.php/2026/08/gnome-mutter-51-beta-added-native-background-blur/"
data_notizia: "2026-08-06"
tags: ["linux", "gnome", "wayland", "desktop"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato: puntare sul "finalmente" per la sfocatura nativa su Wayland (feature richiesta
  da anni, storicamente ottenuta solo con patch/tema di terze parti) e spiegare in modo semplice
  cos'è ext-background-effect-v1 per chi non mastica protocolli Wayland. Buon pezzo da abbinare a un
  richiamo a KDE Plasma 6.7 che di recente ha introdotto i desktop virtuali per schermo, per dare
  un quadro "la scena desktop Linux si muove su più fronti". Target: utenti desktop, non sviluppatori.
---

Chi usa GNOME su Wayland da qualche anno conosce bene questa scena: apri le impostazioni di sistema, cerchi un modo per avere quell'effetto di sfondo sfocato dietro pannelli e finestre — quello che su macOS o su certi temi Windows è normale amministrazione — e scopri che su GNOME nativo, senza estensioni di terze parti o temi non ufficiali, semplicemente non c'è. Con la beta di Mutter 51, il compositor che sta sotto il cofano di GNOME Shell, questa storia inizia finalmente a cambiare.

**Cosa cambia davvero**

La novità tecnica si chiama `ext-background-effect-v1`, un nuovo protocollo Wayland standardizzato. In parole povere: prima, se un'app voleva sfocare lo sfondo dietro una sua finestra (pensa a un pannello di controllo semi-trasparente, o a un lanciatore di app in stile "vetro smerigliato"), doveva arrangiarsi con soluzioni non ufficiali, spesso fragili e diverse da un ambiente desktop all'altro. Ora, grazie a questo protocollo, un'applicazione può chiedere direttamente al compositor di sfocare solo una zona specifica della propria finestra, mantenendo intatto l'aspetto generale di GNOME Shell. È lo stesso principio per cui, quando i vari pezzi del sistema (app, compositor, gestore finestre) parlano un protocollo comune invece di arrangiarsi ognuno per conto suo, tutto funziona in modo più prevedibile e con meno hack.

La cosa interessante è che, essendo un protocollo standard e non una funzione esclusiva di GNOME, in teoria altri ambienti desktop basati su Wayland potrebbero implementarlo a loro volta, portando più coerenza visiva nell'ecosistema Linux in generale — un problema storico per chi passa da un desktop environment all'altro e si ritrova ogni volta effetti grafici diversi o assenti.

**Non solo sfocatura**

Mutter 51 beta porta con sé anche una manciata di altre migliorie meno appariscenti ma altrettanto gradite da chi usa Linux ogni giorno sul portatile o su setup multi-monitor: un timeout configurabile per il "disable-while-typing" del touchpad (quella funzione che disattiva il touchpad mentre scrivi, per evitare click accidentali col palmo della mano), un supporto migliorato per i pulsanti aggiuntivi del mouse legati alla rotellina di scorrimento, correzioni per HDR e scaling su configurazioni multi-monitor, e la migrazione verso lo standard `xdg_session_management_v1` per salvare e ripristinare le sessioni di lavoro in modo più affidabile.

**GNOME Boxes, riscritto quasi da capo**

Parallelamente, un altro pezzo dell'ecosistema GNOME sta cambiando pelle: Boxes, l'applicazione per creare e gestire macchine virtuali in modo semplice (pensata per chi vuole provare una distro o un sistema operativo senza smanettare con QEMU o virt-manager a riga di comando), è stata portata su GTK4 e libadwaita. Si tratta di una riscrittura corposa, guidata dallo sviluppatore Felipe Borges, che punta a modernizzare sia l'interfaccia che le fondamenta tecniche dell'app dopo anni in cui Boxes era rimasta un po' ferma rispetto al resto dell'ecosistema GNOME già migrato ai toolkit più recenti.

**Quando arriva e su cosa lo trovi**

Siamo ancora in fase beta, quindi non è ancora il momento di aspettarsi tutto questo sul tuo sistema stabile: GNOME 51 stabile è atteso a stretto giro nelle prossime settimane, e arriverà di default su Ubuntu 26.10 e Fedora 45. Chi non vuole aspettare può già mettere le mani sulla beta tramite i repository Arch Linux Unstable, oppure provare una immagine nightly di GNOME OS pensata apposta per testare le novità in anteprima, magari in una macchina virtuale (perché no, anche con la nuova Boxes) prima che arrivi sul sistema che usi tutti i giorni.

Non è la rivoluzione dell'anno, ma è uno di quei aggiornamenti che, sommati nel tempo, fanno la differenza tra un desktop Linux che sembra "arrangiato" e uno che si sente rifinito. E per chi segue da tempo lo sviluppo di GNOME, vedere finalmente risolta una richiesta che girava da anni nelle segnalazioni della community è comunque una soddisfazione.
