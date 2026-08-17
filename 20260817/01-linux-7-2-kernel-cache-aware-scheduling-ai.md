---
title: "Linux 7.2 è ufficiale: scheduling più intelligente e l'IA che ormai revisiona il kernel al posto nostro"
rilevanza: "ALTA"
fonte: "https://www.phoronix.com/news/Linux-7.2-Released"
data_notizia: "2026-08-17"
tags: ["linux", "kernel", "opensource", "ai"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato: spiegare il Cache-Aware Scheduling in termini semplici (perché conviene anche
  a chi ha un PC desktop, non solo ai server) e usare la dichiarazione di Torvalds sull'IA come spunto
  per un pezzo di riflessione più ampio su come l'intelligenza artificiale sta cambiando lo sviluppo
  del kernel. Possibile collegamento futuro con l'articolo sul voto Debian sui contributi IA (già
  coperto altrove in italiano, ma qui si può linkare come approfondimento correlato).
---

Il 16 agosto 2026 Linus Torvalds ha rilasciato ufficialmente **Linux 7.2**, l'ultima versione stabile del kernel che tiene in vita miliardi di dispositivi nel mondo: dai server nei data center al vostro laptop con Ubuntu, fino al telefono Android che avete in tasca. E come ogni rilascio del kernel, dietro il numero di versione si nasconde un bel po' di roba interessante.

## Cosa cambia davvero

La novità più chiacchierata di questa release è il **Cache-Aware Scheduling**, una funzione che ottimizza il modo in cui lo scheduler del kernel decide su quale core far girare i vari processi. In parole povere: quando due task condividono dati, il kernel ora cerca di tenerli sullo stesso dominio di cache di ultimo livello (LLC), riducendo i "cache miss" e quei fastidiosi rimbalzi di dati tra un core e l'altro che rallentano tutto. Non è fuffa da laboratorio: nei test su MongoDB si sono visti guadagni di throughput fino al 100%, e chi ha CPU AMD Zen 5 dovrebbe notare benefici concreti anche su carichi di lavoro più quotidiani.

Non è l'unica cosa nuova. Linux 7.2 porta anche:

- **Miglioramenti I/O** per ext4 e Btrfs, con guadagni di prestazioni misurabili su AMD EPYC Turin;
- Supporto al protocollo **USB4STREAM** sviluppato da Intel;
- Novità per le GPU AMD, incluso il supporto **HDMI 2.1 FRL** su AMDGPU;
- Miglioramenti ai driver per hardware Intel, con benefici anche per le nuove Intel Arc B390 Xe3;
- Un aggiornamento generale ai driver per laptop e periferiche, sempre gradito a chi usa Linux come sistema principale.

## Il dettaglio più curioso: l'IA che scrive bug report

La parte più interessante, però, non è tecnica ma "politica". Questa release porta con sé oltre 400 fix firmati da più di 230 contributor, un volume che Torvalds stesso ha attribuito in buona parte a strumenti di intelligenza artificiale che ormai scansionano continuamente il codice del kernel, segnalando bug che i revisori umani avevano trascurato o rimandato per anni.

Circa il 5% dei commit di questa release porta un tag "assisted-by" che segnala l'uso di strumenti IA nel processo. Attenzione però: la policy del kernel resta chiara, ogni contributo assistito da IA deve comunque passare sotto la revisione e la firma di una persona in carne e ossa. Non si tratta quindi di codice scritto e mergiato in automatico, ma di un aiuto nella fase di code review, dove l'IA fa da "primo filtro" per stanare problemi che altrimenti sarebbero rimasti nascosti per anni.

Nel suo annuncio sulla mailing list del kernel, Torvalds ha usato parole abbastanza schiette: non è "esattamente entusiasta" della mole di fix da gestire, ma ha ammesso che ormai è "la nuova normalità". Un cambiamento di prospettiva non da poco per uno che di solito è piuttosto scettico verso le mode tecnologiche.

## Quando arriva sul vostro sistema

Se usate una distro rolling release come Arch, CachyOS o openSUSE Tumbleweed, il kernel 7.2 arriverà nei repository nel giro di pochi giorni o settimane. Chi usa Ubuntu dovrà invece aspettare **Ubuntu 26.10**, la release prevista per l'autunno, che dovrebbe portarlo di serie. Fedora e le altre distro a rilascio semestrale seguiranno un percorso simile, mentre chi è su una LTS (Ubuntu 26.04, Debian stabile) probabilmente vedrà il 7.2 solo tramite backport opzionali o dovrà aspettare la prossima major release.

## Perché dovrebbe interessarvi

Se siete utenti Linux "normali", il Cache-Aware Scheduling è il tipo di miglioramento che non noterete mai esplicitamente, ma che renderà il sistema un filo più reattivo, specialmente su CPU multi-core moderne dove i processi si contendono continuamente le risorse di cache. Se invece gestite server o infrastrutture, vale la pena tenere d'occhio i benchmark sulle vostre applicazioni specifiche: guadagni "gratuiti" del genere, ottenuti solo aggiornando il kernel, capitano raramente.

E se lavorate nel mondo open source, la storia dell'IA che scandaglia il codice del kernel Linux è un segnale su dove sta andando tutto il settore: non sostituzione degli sviluppatori, ma un aiuto concreto per gestire una base di codice che ormai supera i 43 milioni di righe.
