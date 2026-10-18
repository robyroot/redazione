---
title: "Linux 7.3 è finalmente uscito: tutte le novità del nuovo kernel"
rilevanza: "ALTA"
fonte: "https://ostechnix.com/linux-kernel-7-3-rc7-released/"
data_notizia: "2026-10-18"
tags: ["linux", "kernel", "hardware", "gaming", "amd", "intel"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: rilascio del giorno, perfetto per un articolo tempestivo.
  Sottolineare le novità gaming (Steam controller, VRAM) e hardware (AMD Zen6, Intel Xe3P).
  Pubblico di riferimento: utenti Linux desktop e gamer su Linux.
---

# Linux 7.3 è finalmente uscito: tutte le novità del nuovo kernel

È arrivato. Oggi, 18 ottobre 2026, Linus Torvalds ha rilasciato ufficialmente **Linux 7.3**, il nuovo kernel stabile che arriva dopo sette release candidate e una fase di sviluppo durata circa due mesi. Si tratta di uno dei rilasci più attesi dell'anno, soprattutto per chi usa Linux su hardware recente o vuole giocare senza compromessi.

## AMD Zen6 e Intel Xe3P Nova Lake: il kernel incontra il nuovo hardware

Una delle novità più importanti di Linux 7.3 riguarda il supporto hardware. Il kernel porta finalmente il **supporto iniziale per i processori AMD Zen6**, la nuova architettura di AMD che promette salti significativi in efficienza energetica e prestazioni per core. Per chi segue da vicino l'ecosistema AMD, questa è una notizia che aspettava da un po'.

Sul fronte Intel, 7.3 porta il **supporto stabile per la grafica integrata Intel Xe3P Nova Lake**. Nelle versioni precedenti del kernel questo driver era ancora segnato come sperimentale; ora diventa ufficialmente stabile, il che significa migliore affidabilità e meno rogne per chi usa laptop con questo chip.

C'è anche una chicca per gli appassionati di hardware Ryzen AI: entra nel mainline il **driver per i LED RGB Ryzen AI Halo**, quei chip che AMD ha presentato come la prossima frontiera nell'AI on-device. Non cambia la vita di molti, ma è un segnale di quanto velocemente il supporto Linux stia tenendo il passo con l'hardware.

## Gaming su Linux: meno problemi con la VRAM

Buone notizie anche per i gamer. Linux 7.3 introduce **ottimizzazioni per sistemi con VRAM limitata**, un problema che ha tormentato più di un giocatore Linux negli ultimi anni. Con certi titoli pesanti, il driver Vulkan o DXVK poteva saturare la VRAM e causare cali drastici di prestazioni o crash. Le modifiche introdotte in questo ciclo di sviluppo migliorano la gestione della memoria video in questi scenari, con risultati tangibili su GPU con 8 GB o meno.

Anche più curiosa è l'inclusione del **supporto iniziale per il controller Steam 2026**, il nuovo gamepad che Valve ha presentato quest'anno. Non aspettarti che funzioni alla perfezione da subito, ma il fatto che sia già nel kernel ufficiale è un ottimo segnale: di solito queste cose richiedono molto più tempo.

## Come aggiornare o verificare il kernel

Se usi una distro rolling come **Arch Linux** o **openSUSE Tumbleweed**, Linux 7.3 arriverà nei repository normali nelle prossime ore o giorni. Arch ha già pubblicato una ISO di ottobre con kernel 7.2.7, quindi l'aggiornamento a 7.3 è questione di poco.

Per verificare quale kernel stai usando:

```bash
uname -r
```

Se hai bisogno di compilare il kernel manualmente (cosa rara ma a volte necessaria su hardware molto nuovo), puoi scaricarlo da kernel.org:

```bash
wget https://cdn.kernel.org/pub/linux/kernel/v7.x/linux-7.3.tar.xz
tar -xf linux-7.3.tar.xz
cd linux-7.3
make menuconfig
```

Le distro LTS come **Ubuntu 26.04 LTS** continueranno a usare kernel 7.2 per ragioni di stabilità. **Ubuntu 26.10**, invece, è già costruita sulla serie 7.3 e riceverà questo aggiornamento prontamente.

## Il dibattito sull'AI nel kernel

In parallelo al rilascio di 7.3, nella comunità kernel è in corso un dibattito interessante: i maintainer stanno valutando se **eliminare l'obbligo del tag "Assisted-by" per le patch scritte con l'aiuto di tool AI**. Linus Torvalds si è già espresso contro il ban degli strumenti AI, ma il tema della trasparenza nell'uso dell'AI nei contributi open source è tutt'altro che chiuso.

È un segnale dei tempi: sempre più sviluppatori usano assistenti AI per scrivere codice, e il kernel Linux — il progetto open source per eccellenza — si trova a fare i conti con questa realtà.

## In sintesi

Linux 7.3 è un rilascio solido che porta con sé:

- Supporto AMD Zen6 e Intel Xe3P Nova Lake stabile
- Driver Ryzen AI Halo LED RGB
- Supporto iniziale Steam controller 2026
- Migliore gestione della VRAM nei giochi
- Kernel point release 7.2.11 disponibile per chi non vuole aggiornare ancora

Se hai hardware recente, è il momento giusto per aggiornare.
