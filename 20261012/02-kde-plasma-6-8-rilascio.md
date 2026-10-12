---
title: "KDE Plasma 6.8: il desktop Linux più amato sta per aggiornarsi"
rilevanza: "ALTA"
fonte: "https://linuxiac.com/kde-plasma-6-8-gets-final-fixes-ahead-of-october-14-release/"
data_notizia: "2026-10-12"
tags: ["kde", "plasma", "linux-desktop", "flatpak", "aggiornamento"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato per RobyRoot: Presentare Plasma 6.8 come un'evoluzione solida per chi usa KDE. Evidenziare il fix Flatpak che risolve un problema pratico quotidiano. Menzionare il documentario come fatto curioso e umano.
---

## KDE Plasma 6.8 arriva il 14 ottobre

Il 14 ottobre 2026 — tra pochissimi giorni — arriva KDE Plasma 6.8, il nuovo aggiornamento del desktop environment più configurabile e potente del mondo Linux. Il team di sviluppo ha appena terminato gli ultimi fix e la release è praticamente pronta.

Non è una release rivoluzionaria come lo fu Plasma 6.0, ma è esattamente quello che gli utenti chiedevano da tempo: stabilità, polish e correzione di quei piccoli fastidi che si accumulano nel tempo.

## Il fix che aspettavi: Flatpak e aggiornamenti automatici

Uno dei bug corretti in Plasma 6.8 riguarda **Discover**, il gestore di applicazioni di KDE. Se hai mai attivato gli aggiornamenti automatici per le app Flatpak e ti sei ritrovato con applicazioni non aggiornate senza capire perché, era colpa di un bug nell'integrazione tra Discover e il runtime di Flatpak.

Con 6.8 questo problema è risolto. Gli aggiornamenti automatici delle app Flatpak finalmente funzionano in modo affidabile.

Per verificare che tutto funzioni dopo l'aggiornamento:

```bash
# Controlla la versione di Plasma
plasmashell --version

# Aggiorna manualmente le app Flatpak (come test)
flatpak update

# Verifica le app Flatpak installate
flatpak list --app
```

## Come aggiornare a Plasma 6.8

Su **Arch Linux** (e derivate come Manjaro), l'aggiornamento arriverà automaticamente attraverso i repository rolling:

```bash
sudo pacman -Syu
```

Su **KDE neon** e **openSUSE Tumbleweed** sarà simile. Per le distro con release fissa come Kubuntu, puoi abilitare i backport KDE:

```bash
sudo add-apt-repository ppa:kubuntu-ppa/backports
sudo apt update
sudo apt upgrade
```

Dopo l'upgrade, un riavvio della sessione grafica (o un logout/login) è sufficiente per attivare Plasma 6.8.

## Bonus: il documentario KDE

Lo stesso giorno del rilascio di Plasma 6.8, KDE pubblicherà **"KDE: The Documentary"**, un film sulla storia del progetto. Se sei curioso di conoscere come è nata una delle più importanti community open source del mondo, è un ottimo momento per sedersi e guardare qualcosa di interessante.

La community KDE esiste dal 1996 — trent'anni di storia del desktop Linux libero meritano un documentario.

## GNOME 51 non sta a guardare

Vale la pena menzionare che GNOME 51 Alpha è già in fase di test pubblico, e **Ubuntu 26.10** (in uscita il 15 ottobre) arriverà con GNOME 51 e kernel Linux 7.3. Il desktop Linux non si è mai mosso così velocemente: tra Plasma 6.8 e GNOME 51, ottobre 2026 è un mese davvero intenso per chi vive sulla GUI.

Se sei indeciso tra KDE e GNOME, è un buon momento per provare entrambi in una macchina virtuale e capire quale si adatta meglio al tuo stile di lavoro.
