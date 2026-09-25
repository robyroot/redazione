---
title: "KDE Plasma 6.8 in beta e Fedora 45 con GNOME 51: il desktop Linux si rinnova"
rilevanza: "MEDIA"
fonte: "https://news.tuxmachines.org/n/2026/09/22/Akademy_KDE_and_GNOME.shtml"
data_notizia: "2026-09-22"
tags: ["KDE", "GNOME", "Fedora", "Linux", "desktop", "Plasma", "Flatpak"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato per RobyRoot: recensione pratica delle novità, con screenshot o descrizione delle feature più visibili per l'utente finale. Ottimo per i lettori che usano Linux desktop quotidianamente o stanno valutando il passaggio.
---

# KDE Plasma 6.8 in beta e Fedora 45 con GNOME 51: il desktop Linux si rinnova

Settimana movimentata sul fronte del desktop Linux: **KDE Plasma 6.8** è entrato in fase di beta pubblica, e quasi in contemporanea è arrivata la beta di **Fedora Linux 45** che porta con sé **GNOME 51**. Se stai valutando di aggiornare o semplicemente vuoi sapere cosa aspettarti nei prossimi mesi, ecco un riassunto delle novità più interessanti.

## KDE Plasma 6.8: cosa c'è di nuovo nella beta

KDE Plasma 6.8 è ora disponibile per i tester che vogliono provarlo prima del rilascio stabile. La serie 6.x ha già portato grandi cambiamenti rispetto a Plasma 5 (migrazione completa a Wayland come default, supporto HDR migliorato, ridisegno di componenti chiave), e la 6.8 continua su questa strada con raffinamenti e nuove funzionalità.

Tra le novità anticipate nella beta:
- Miglioramenti all'integrazione con Wayland per le applicazioni legacy X11
- Nuove opzioni di personalizzazione per la barra delle applicazioni
- Ottimizzazioni delle prestazioni, specialmente su hardware integrato Intel e AMD
- Integrazione AI opzionale (un tema che KDE sta esplorando attivamente, come vedremo)

Per installare la beta su Arch Linux o derivate:

```bash
# Su Arch con KDE testing enabled:
sudo pacman -Syu plasma-beta

# Su openSUSE Tumbleweed (che include già release recenti):
sudo zypper dup
```

## L'integrazione AI in KDE: un dibattito aperto

Vale la pena menzionare che questa settimana Tux Machines riporta un articolo intitolato "KDE and AI, and you, and me" — un titolo che lascia intendere che il progetto KDE stia riflettendo pubblicamente sul ruolo dell'intelligenza artificiale nel desktop.

La questione non è banale: dove ha senso integrare AI in un desktop, e dove invece diventa un gimmick o un rischio per la privacy? KDE sta cercando di rispondere a queste domande in modo trasparente con la community, il che è un approccio apprezzabile rispetto all'approccio "AI in tutto" di certi vendor commerciali.

## Fedora 45 Beta: GNOME 51 e kernel 7.2

La beta di Fedora 45 porta due novità principali: **GNOME 51** e il **kernel Linux 7.2**. Fedora è storicamente una delle prime distribuzioni ad integrare le versioni più recenti di GNOME, quindi è il posto migliore per vedere le nuove funzionalità in anticipo.

GNOME 51 porta miglioramenti all'app Impostazioni, ottimizzazioni dell'interfaccia Files (Nautilus), e ulteriori raffinamenti alle animazioni e ai gesti su touchpad e touchscreen. Non è un salto rivoluzionario rispetto a GNOME 48 o 49, ma è un'evoluzione costante e solida.

```bash
# Per provare Fedora 45 Beta in una VM con virt-manager:
# Scarica l'ISO dal sito ufficiale getfedora.org/it/workstation/
# e avvia l'installazione normalmente.

# Oppure con GNOME Boxes (il modo più semplice):
# Apri GNOME Boxes > Crea > Cerca "Fedora" > seleziona Fedora 45 Beta
```

## MX Linux 25.3 e SparkyLinux 2026.09: due release stabili

Se non vuoi software beta, questa settimana sono arrivate anche due release stabili degne di nota:

**MX Linux 25.3** è disponibile con base Debian 13.7 e kernel Linux 7.2 nelle build AHS. MX Linux è da anni una delle distribuzioni più apprezzate per la sua semplicità d'uso e la stabilità — perfetta per chi vuole un sistema che "funziona e basta" senza sorprese.

**SparkyLinux 2026.09** introduce il kernel 7.2 e una nuova edizione Labwc, che usa il compositor Wayland wlroots-based Labwc — interessante per chi vuole un desktop leggero e moderno senza il peso di KDE o GNOME completi.

## Flatpak 1.18.3: stabilità e bug fix

Sul fronte della distribuzione delle applicazioni, **Flatpak 1.18.3** è uscito con un focus su correzioni di bug e stabilità. Tra i fix principali: un crash nel system helper che si verificava durante l'iterazione delle cache directory, un bug nel portal che passava il file descriptor sbagliato in certi scenari, e un problema che causava il tracking del sender D-Bus errato.

Nulla di rivoluzionario, ma gli aggiornamenti di stabilità sono fondamentali per chi usa Flatpak come canale principale di distribuzione delle app.

```bash
# Aggiorna Flatpak e tutte le app installate:
flatpak update

# Verifica la versione installata:
flatpak --version
```

## Cosa tenere d'occhio

Nei prossimi mesi, le cose interessanti da seguire sono:
- Il rilascio stabile di KDE Plasma 6.8 (probabilmente a ottobre/novembre)
- Fedora 45 stabile (prevista per ottobre 2026)
- L'evoluzione del dibattito sull'AI integrata nei desktop, con le risposte concrete di KDE e GNOME

Il desktop Linux non ha mai smesso di evolversi rapidamente, e l'autunno 2026 si preannuncia ricco di novità per chi lo usa quotidianamente.
