---
title: "Linux 7.3 è quasi pronto: AMD Zen 6, Intel Nova Lake e build 36% più veloci"
rilevanza: "ALTA"
fonte: "https://linuxiac.com/arch-linux-october-2026-iso-is-out-with-linux-kernel-7-2-7-systemd-262/"
data_notizia: "2026-10-10"
tags: ["linux", "kernel", "amd", "intel", "performance"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: articolo per gli appassionati di Linux desktop e sysadmin. Mescola le novità hardware di 7.3 con la notizia delle build più veloci prevista per 7.4. Tono entusiasta e tecnico ma accessibile.
---

# Linux 7.3 è quasi pronto: AMD Zen 6, Intel Nova Lake e build che vanno il 36% più veloci

Il ciclo di sviluppo di Linux 7.3 si sta avviando verso il traguardo: siamo alla release candidate 6 e il kernel finale è previsto per le prossime settimane. Intanto, dalle mailing list emerge anche un'altra notizia interessante: per Linux 7.4 potrebbero arrivare ottimizzazioni al sistema di build che renderebbero la compilazione del kernel fino al **36% più veloce** (e le build incrementali addirittura del **70%**).

## Cosa porta Linux 7.3

Questo ciclo di sviluppo è particolarmente interessante per chi usa hardware di nuova generazione:

### AMD Zen 6 e il nuovo ecosistema Ryzen AI
Linux 7.3 porta il supporto completo per i processori **AMD Zen 6**, la prossima generazione dell'architettura AMD. Ma c'è di più: arriva anche il **driver Ryzen AI Halo LED**, che gestisce i LEDs RGB integrati nei nuovi SoC Ryzen AI Halo. Piccola cosa, ma importante per chi vuole un'esperienza Linux completa su questi sistemi senza ricorrere a workaround.

### Intel Xe3P "Nova Lake"
Sul fronte Intel, Linux 7.3 aggiunge il supporto alla grafica integrata dei futuri processori **Nova Lake** basati sull'architettura **Intel Xe3P**. Un passo importante per garantire che questi chip funzionino bene su Linux fin dal day one, senza dover aspettare mesi per il supporto grafico.

### Rimozione del supporto x32 ABI
Una notizia che farà felici i puristi: stanno girando patch per rimuovere definitivamente la **x32 ABI** dal kernel. Si tratta di un'interfaccia ibrida a 32 bit per sistemi a 64 bit, introdotta nel 2012 e usata pochissimo. Eliminarla semplifica il codice e riduce la superficie di attacco.

### QPaCE: compressione ZRAM più veloce su Qualcomm
Qualcomm ha contribuito un nuovo driver **QPaCE** che accelera la compressione ZRAM sui SoC recenti della casa di San Diego. Per chi usa dispositivi ARM con ZRAM come swap (pensate a Raspberry Pi, tablet Linux o Snapdragon-powered laptop), potrebbe essere un bel miglioramento nelle prestazioni generali.

### Fedora 45 dice addio al framebuffer console
Non direttamente nel kernel, ma strettamente correlato: **Fedora 45** sta sostituendo la tradizionale framebuffer console con **KMSCON**, una console basata su KMS/DRM. Questo significa una transizione più fluida durante il boot e meno glitch visivi, soprattutto su sistemi con GPU moderne.

## La novità più interessante: build del kernel 36% più veloci

Una patch series in sviluppo per **Linux 7.4** promette di ridurre significativamente i tempi di compilazione del kernel:

- Build complete: **~36% più veloci**
- Build incrementali (dopo piccole modifiche): **~70% più veloci**

Se sei uno sviluppatore kernel o qualcuno che compila regolarmente il proprio kernel (cosa comune nella comunità Linux avanzata), questo è oro. Un ciclo di modifica-compila-testa che oggi richiede 20 minuti potrebbe scendere a meno di 15.

```bash
# Verificare la propria versione del kernel
uname -r

# Controllare il kernel disponibile nel proprio repo
apt info linux-image-generic  # Debian/Ubuntu
dnf info kernel                # Fedora/RHEL
pacman -Qi linux               # Arch Linux
```

## Quando arriva il kernel 7.3 stabile?

La rc6 è uscita a inizio ottobre. Tipicamente dopo la rc6 o rc7 arriva il finale. Aspettati la versione stabile di **Linux 7.3 entro la fine di ottobre 2026**.

Nel frattempo, se usi **Arch Linux**, l'ISO di ottobre 2026 include già il kernel **7.2.7** con **systemd 262**. Per chi vuole il bleeding edge senza compilare da soli, Arch è sempre una scelta solida.

## Vale la pena aggiornare subito?

Per uso desktop normale, meglio aspettare che 7.3 arrivi nei canali stabili della propria distro. Per chi usa hardware AMD Zen 6 o Intel Nova Lake, invece, potrebbe valere la pena guardare a distro come Arch o Fedora che adottano il kernel più rapidamente.

Il ciclo di sviluppo Linux continua a dimostrarsi vivace: supporto hardware aggiornato, ottimizzazioni delle performance, pulizia del codice legacy. Tutto quello che ci aspettiamo da Linus & co.
