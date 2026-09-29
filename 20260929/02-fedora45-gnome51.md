---
title: "Fedora 45 Beta è qui: GNOME 51, kernel 7.2 e una console Linux finalmente moderna"
rilevanza: "ALTA"
fonte: "https://9to5linux.com/fedora-linux-45-beta-released-with-linux-7-2-gnome-51-and-kde-plasma-6-7"
data_notizia: "2026-09-15"
tags: ["fedora", "linux", "gnome", "kde", "distro", "desktop"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato per RobyRoot: Ottimo pezzo per utenti desktop Linux. Evidenzia le novità pratiche (kmscon, GNOME 51, riproducibilità dei pacchetti) con un tono entusiasta e accessibile. Utile per chi valuta se aggiornare o switchare a Fedora.
---

# Fedora 45 Beta è qui: GNOME 51, kernel 7.2 e una console Linux finalmente moderna

Il 15 settembre 2026, il team Fedora ha rilasciato la beta di **Fedora 45**, e c'è roba interessante da vedere. Tra kernel 7.2, GNOME 51, KDE Plasma 6.7 e — finalmente — una console testuale degna del 2026, questa release promette bene. La versione finale è attesa per il **20 ottobre**.

## La console Linux entra nel 21° secolo: kmscon

Questa è probabilmente la novità più interessante per chi usa Linux su macchine fisiche. Fedora 45 adotta **kmscon** come console virtuale predefinita, in sostituzione del vecchio framebuffer console che risale agli anni '90.

kmscon è un'implementazione della console in user-space che sfrutta il kernel mode-setting (KMS) e offre:
- **Font scalabili** e rendering anti-aliased anche fuori dall'ambiente grafico
- Supporto Unicode completo
- Scrollback buffer decente
- Aspetto visivamente molto più pulito rispetto alla VT classica

Per chi si trovava a lavorare in console perché il desktop crashava, o semplicemente perché preferisce un approccio minimale, questo è un upgrade notevole.

## GNOME 51: le novità che contano

Fedora 45 Workstation è la prima grande distro a portare **GNOME 51** agli utenti. Le novità più interessanti:

- **Salvataggio e ripristino della luminosità del monitor** — finalmente gestita correttamente anche dopo il riavvio
- **Supporto elogind** come provider alternativo a libsystemd — buona notizia per le distro non-systemd
- **Nuova API per generare QR code** nativamente nelle applicazioni GNOME
- **Supporto all'input capture portal** per integrazione clipboard migliorata
- **Screencasting ottimizzato** — meno overhead CPU grazie alla riduzione dei paint e delle copie buffer

Per chi usa Fedora KDE Spin, la release porta invece **KDE Plasma 6.7** con il suo set di miglioramenti al compositor Wayland.

## Verificabilità dei pacchetti: una novità silenziosa ma importante

Fedora 45 introduce **build di pacchetti completamente riproducibili**. In pratica, dati gli stessi sorgenti e lo stesso ambiente di build, il risultato binario è identico ogni volta. Questo permette verifiche indipendenti dell'integrità dei pacchetti e rende molto più difficile inserire backdoor nella supply chain.

Allo stesso modo, la verifica delle firme RPM è ora attiva di default (`signature checking by default for RPM`). Piccola cosa, grande impatto sulla sicurezza.

## Altre novità degne di nota

- **WebUI installer** su tutte le immagini ISO Fedora Atomic
- **Immagini disk** per Fedora Atomic Desktop costruite con image-builder
- **oo7** come nuovo sistema di gestione dei segreti (secret management)
- **GCC 16.2** come compilatore di sistema

## Come provarlo ora

Se vuoi mettere le mani su Fedora 45 Beta, puoi scaricarla dal sito ufficiale e installarla su una VM o su hardware dedicato:

```bash
# Se usi Fedora 44 e vuoi fare upgrade alla beta
sudo dnf install dnf-plugin-system-upgrade
sudo dnf system-upgrade download --releasever=45
sudo dnf system-upgrade reboot
```

Tieni a mente che è una **beta**: per uso quotidiano in produzione aspetta la release finale del 20 ottobre. Per testare in una VM o su hardware secondario, invece, è il momento giusto — il feedback alla community è sempre benvenuto.

## Il quadro generale

Fedora 45 si conferma la distro che spinge più avanti l'adozione di tecnologie moderne nel mondo Linux desktop. kmscon, la riproducibilità dei build, e il passaggio a GNOME 51 prima di tutti gli altri la rendono un punto di riferimento per chi vuole il Linux desktop più aggiornato senza aspettare Ubuntu o Debian.

Ottobre è vicino: tienila d'occhio.
