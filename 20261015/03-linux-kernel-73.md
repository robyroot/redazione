---
title: "Linux 7.3-rc7 si avvicina al rilascio: AMD Zen6, Intel Nova Lake, Steam Controller 2026 e le AI nel workflow dei patch"
rilevanza: "MEDIA"
fonte: "https://linuxiac.com/arch-linux-october-2026-iso-is-out-with-linux-kernel-7-2-7-systemd-262/"
data_notizia: "2026-10-12"
tags: ["linux", "kernel", "AMD", "Intel", "gaming", "open-source"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato per RobyRoot: scrivi questo come un articolo entusiastico per chi segue lo sviluppo del kernel. Evidenzia le novità pratiche (nuovo hardware supportato, gaming con Steam Controller) e anche la parte controversa sull'AI nei workflow di sviluppo — è un tema caldo nella comunità Linux che si presta bene al dibattito.
---

# Linux 7.3 si avvicina: Zen6, Intel Nova Lake, il nuovo Steam Controller e l'AI che scrive i "Fixes:" tag

Il kernel Linux 7.3 è ormai in dirittura d'arrivo: siamo a **rc7** (release candidate 7), il che di solito significa che mancano pochi giorni alla release finale. Nel frattempo, la **7.2.10** è già disponibile come aggiornamento stabile, e tutti gli utenti del branch 7.2 dovrebbero installarla prima possibile.

Vediamo cosa porta di nuovo Linux 7.3.

## Hardware: AMD Zen6 e Intel Xe3P Nova Lake

Questa release consolida il supporto per due architetture hardware di nuova generazione:

**AMD Zen6** — la nuova generazione di processori Ryzen riceve enablement completo nel kernel 7.3. Per chi usa Ryzen AI Halo, c'è anche un driver dedicato per i LED RGB. Se stai aspettando di passare alla nuova generazione di hardware AMD, aspetta che 7.3 stabile sia disponibile prima di installarlo.

**Intel Xe3P "Nova Lake"** — le CPU Intel di nuova generazione, con grafica integrata Xe3P, ricevono supporto stabile. Il codice era presente come sperimentale nelle versioni precedenti; ora diventa parte integrante del kernel.

```bash
# Per verificare la versione del kernel dopo l'aggiornamento
uname -r

# Per controllare i driver grafici attivi
lspci -k | grep -A2 VGA

# Su Arch Linux, il kernel 7.3 sarà probabilmente nel repo extra entro fine ottobre
# Su Ubuntu 26.10, sarà incluso nel kernel di base
sudo apt update && apt list --upgradable | grep linux-image
```

## Novità gaming: driver per il nuovo Steam Controller 2026

Una delle aggiunte più interessanti per i gamer Linux è il **driver iniziale per il nuovo Steam Controller del 2026**. Valve ha aggiornato il suo controller e il supporto kernel nativo arriva già con 7.3. Chi usa Linux per il gaming su Steam (e con il diffondersi di Steam Deck e SteamOS 4, sono sempre di più) troverà il nuovo hardware riconosciuto out-of-the-box.

## La proposta che fa discutere: AI che aggiunge "Fixes:" ai patch

Al **Maintainers Summit 2026**, tenutosi l'8 ottobre a Praga, i principali maintainer del kernel hanno discusso dell'impatto dei Large Language Model sullo sviluppo. Una proposta concreta è emersa: aggiungere una **skill AI che aiuta gli sviluppatori ad aggiungere automaticamente i tag `Fixes:` ai patch**.

Il tag `Fixes:` è fondamentale nel workflow del kernel: identifica esattamente quale commit precedente introduce il bug corretto da un determinato patch. Dimenticarlo è un errore comune, soprattutto per i contributori meno esperti.

```bash
# Esempio di commit con Fixes: tag corretto
# git log --oneline
# a1b2c3d Fix NULL pointer dereference in xyz_driver
#
# Il corpo del commit dovrebbe contenere:
# Fixes: f4e5d6c ("drivers: xyz: add initial support")

# Per cercare commit senza Fixes: tag in una serie di patch
git log --oneline v7.2..HEAD | head -20
```

L'idea è controversa: da un lato semplifica il lavoro dei contributori, dall'altro solleva domande sull'affidabilità dell'AI nel tracciare correttamente le genealogie dei bug nel codice.

## Altre novità notevoli

- **Fedora 45** sta sostituendo il frame buffer console (FBcon) con **KMSCON** per la console testuale: addio al vecchio testo a 80 colonne, benvenuto rendering modulare del terminale
- **Supporto Hibernation in lockdown mode**: nuove patch propongono di allentare le restrizioni sull'ibernazione quando il sistema è in modalità lockdown (usata da sistemi con Secure Boot)
- **Driver QPaCE di Qualcomm**: accelerazione hardware per la compressione/decompressione di pagine in ZRAM (utile per sistemi con poca RAM che usano ZRAM come swap)
- **Proposta rimozione x32 ABI**: tornano le discussioni sull'eliminare l'ABI x32 (un ibrido tra x86 e x86-64 mai decollato), con buone possibilità che sparisca definitivamente

## Quando arriverà Linux 7.3 stabile?

Con rc7 già disponibile, la release finale di Linux 7.3 è attesa **entro fine ottobre 2026**. Ubuntu 26.10 lo includerà come kernel di base anche se la release finale del distro arriverà prima — un ciclo di sviluppo sovrapposto non insolito per questa finestra autunnale.

Se vuoi testarlo subito:

```bash
# Su Arch Linux (in rolling release, sarà disponibile presto)
sudo pacman -Syu linux

# Su Fedora 45 (già incluso nel ciclo di sviluppo)
sudo dnf update kernel

# Per compilare dal sorgente (per chi vuole rischiare)
wget https://cdn.kernel.org/pub/linux/kernel/v7.x/linux-7.3-rc7.tar.xz
tar -xf linux-7.3-rc7.tar.xz
cd linux-7.3-rc7
make menuconfig
make -j$(nproc)
sudo make modules_install install
```

L'ecosistema Linux continua a crescere a ritmo sostenuto: 7.3 porta supporto hardware moderno, miglioramenti pratici per i gamer e stimola conversazioni interessanti sul futuro del processo di sviluppo nell'era dell'AI.
