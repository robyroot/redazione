---
title: "Linux Kernel 7.3 è qui: USB4 per Mac Apple, Zen6 e il driver Steam"
rilevanza: "ALTA"
fonte: "https://ostechnix.com/linux-kernel-7-3-rc7-released/"
data_notizia: "2026-10-18"
tags: ["linux", "kernel", "open-source", "hardware", "ubuntu"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato per RobyRoot: enfatizzare il supporto USB4/Thunderbolt per Apple Silicon come segnale del crescente interesse di Linux verso l'ecosistema Mac, e le novità gaming con il driver Steam 2026. Ottimo contenuto per utenti desktop e dual-booter.
---

# Linux Kernel 7.3 è qui: USB4 per Mac Apple, Zen6 e il driver Steam

Dopo settimane di release candidate (ben sei, più una possibile settima), il kernel Linux 7.3 è finalmente arrivato. Linus Torvalds ha dato il via libera attorno al 18 ottobre 2026, e come sempre la lista delle novità è lunga. Stavolta però ci sono alcune cose davvero interessanti, soprattutto se hai un Mac con chip Apple Silicon o sei un gamer Linux.

## USB4 e Thunderbolt finalmente su Apple M1, M2 e M3

Questa è forse la notizia più grossa del ciclo 7.3. Linux porta finalmente il supporto iniziale per USB4 e Thunderbolt sui chip Apple M1, M2 e M3. Significa che chi usa Linux su hardware Apple — tramite Asahi Linux o distribuzioni derivate — inizia a vedere riconosciuti correttamente i dispositivi connessi via Thunderbolt.

Insieme al supporto USB4, è arrivato anche un nuovo driver PMGR (Power Management) specifico per Apple, che migliora la gestione energetica su questi sistemi. Non è ancora perfetto, ma è un passo enorme rispetto a dove eravamo un anno fa.

## AMD Zen6 e il driver RGB per Ryzen AI Halo

Se hai o stai valutando un processore AMD di ultima generazione, il kernel 7.3 porta l'abilitazione di AMD Zen6. Oltre a questo, c'è anche un nuovo driver per il controller LED RGB presente nei chip Ryzen AI Halo — sì, quelle lucine sul tuo laptop gaming AMD ora funzionano nativamente su Linux.

Per i fan Intel, arriva invece il supporto stabile per le GPU Intel Xe3P Nova Lake (grafica integrata), che fino ad ora richiedeva patch o kernel personalizzati.

## Il controller Steam 2026 è supportato

Steam Deck e gaming su Linux continuano a crescere, e il kernel 7.3 porta il supporto iniziale per il nuovo Steam Controller del 2026. Valve collabora attivamente con la community del kernel per garantire che il loro hardware funzioni out-of-the-box, e si vede.

Se usi Proton o Steam su Linux, questo aggiornamento arriva in buon momento prima delle grandi uscite autunnali.

## Come ottenere il kernel 7.3

Se vuoi provare subito il nuovo kernel, hai diverse strade:

```bash
# Su Ubuntu/Debian, verifica il kernel disponibile
uname -r
apt-cache search linux-image | grep 7.3

# Su Arch Linux (probabilmente già disponibile)
pacman -Syu linux

# Su Fedora (aggiornamento automatico con dnf)
dnf update kernel
```

In alternativa, puoi compilarlo manualmente scaricandolo da kernel.org:

```bash
# Scarica e verifica il sorgente
wget https://cdn.kernel.org/pub/linux/kernel/v7.x/linux-7.3.tar.xz
wget https://cdn.kernel.org/pub/linux/kernel/v7.x/linux-7.3.tar.sign
```

## Ubuntu 26.10 lo porta di default

Se non vuoi compilare nulla, aspetta Ubuntu 26.10 "Stonking Stingray", in uscita fine ottobre 2026. Questa versione includerà il kernel 7.3 di default, insieme a GNOME 51 e alle utility di sistema riscritte in Rust. Un aggiornamento completo davvero interessante.

Anche Fedora 45, attesa per il 27 ottobre, adotterà il kernel 7.3 e porterà KMSCON al posto del framebuffer per la console testuale — più performance e meno problemi grafici all'avvio.

## Il 2026 Maintainers Summit a Praga

A margine del rilascio, vale la pena menzionare che agli inizi di ottobre si è tenuto il Maintainers Summit a Praga: circa 30 sviluppatori chiave del kernel riuniti per discutere le priorità del progetto. Un appuntamento chiuso ai media ma importante per capire dove va Linux nei prossimi anni.

In sintesi: se usi hardware recente AMD o Intel, se sei curioso di Linux su Mac, o se giochi con Steam su Linux, il kernel 7.3 ha qualcosa per te. Aggiorna pure.
