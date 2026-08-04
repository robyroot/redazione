---
title: "Linux 7.2-rc6: il release candidate più grande di sempre (e le LTS ricevono patch di sicurezza urgenti)"
rilevanza: "ALTA"
fonte: "https://www.linuxcompatible.org/story/linux-kernel-72-rc6-arrives-as-largest-rc6-in-kernel-history-ai-patches-and-networking-backlog"
data_notizia: "2026-08-03"
tags: ["linux", "kernel", "sicurezza", "LTS", "AI"]
livello: "intermediate"
nota_editoriale: |
  Due angoli possibili per RobyRoot: (1) una guida pratica "come e perché aggiornare subito il kernel LTS" per chi gestisce server Samba/ksmbd esposti in rete; (2) un pezzo di opinione sul fatto che Torvalds definisca le patch generate da AI "la nuova normalità" nello sviluppo del kernel, che si presta bene al taglio editoriale del blog su Linux + AI.
---

Chi segue lo sviluppo del kernel Linux sa che le release candidate (le famose "rc") servono a stabilizzare il codice prima del rilascio finale. Di solito, più si avvicina la rc6, più i cambiamenti si riducono: è il momento in cui si sistemano gli ultimi bug, non se ne aggiungono di nuovi. Ecco perché la 7.2-rc6, uscita il 2 agosto 2026, ha sorpreso tutti: è la rc6 più grande nella storia del kernel, con un numero di commit senza precedenti per essere così avanti nel ciclo di rilascio.

Linus Torvalds stesso ha commentato la cosa con una certa cautela: "Spero sia tutto qui, ma è un po' inquietante quanto siano grandi i cambiamenti a questo punto, anche se nulla qui dentro sembra particolarmente strano". Non è un allarme, ma nemmeno una scrollata di spalle.

## Perché è così grande

Due i motivi principali. Il primo è un accumulo di patch di networking rimaste in coda tra un ciclo di rilascio e l'altro, complice anche il periodo di conferenze di settore che rallenta sempre un po' i merge. Il secondo motivo è più interessante e guarda al futuro: secondo Torvalds, una fetta consistente del volume arriva da patch generate con l'aiuto di AI e LLM, un fenomeno che lui stesso descrive ormai come "la nuova normalità" nello sviluppo del kernel. Che piaccia o meno, il codice scritto (o assistito) da modelli linguistici sta diventando parte strutturale del flusso di lavoro dei kernel developer, non un esperimento isolato.

In termini di distribuzione, circa il 60% delle modifiche riguarda i driver, il 20% il networking, e il resto si divide tra architettura, strumenti e filesystem — una proporzione tutto sommato normale, solo su scala più ampia.

## Le correzioni più rilevanti

Tra i fix concreti di questa rc6 spicca una correzione critica per x86 che risolveva un problema di identificazione errata dei processori AMD Zen 5, scambiati per Zen 6 — un bug che avrebbe potuto causare comportamenti imprevedibili su hardware recente. Ci sono poi dei quirk ATA per i dischi Western Digital Red Plus difettosi, utili a chi ha NAS o storage domestico basato su questi drive, e un'ampia serie di pulizie nei driver DRM (la parte grafica del kernel).

La versione stabile 7.2 è attesa per metà agosto 2026, e nel frattempo le patch per la 7.3 stanno già confluendo nel mainline, con lavoro preliminare per il supporto a Zen 6, RDNA5 e Intel Starfire.

## Patch di sicurezza urgenti sulle LTS

Parallelamente, il 3 agosto 2026 sono uscite le nuove versioni delle tre kernel LTS attive: 6.18.42, 6.12.101 e 6.6.148. Qui il focus non è la novità ma la sicurezza, e ci sono un paio di fix che vale la pena conoscere se gestite server Linux.

Il primo riguarda **ksmbd**, il server SMB3 implementato in kernel space: Namjae Jeon, Wentao Guan e Haofeng Li hanno corretto diverse vulnerabilità nella validazione delle Access Control List (ACL), pensate per impedire che liste di controllo accessi malformate mandino in crash o in stato inconsistente il server. Se esponete condivisioni SMB via ksmbd su una rete non completamente fidata, questo è un aggiornamento da non rimandare.

Il secondo fix, firmato da Mikulas Patocka, chiude un buffer overflow nel meccanismo di Forward Error Correction di **dm-verity**, la componente che garantisce l'integrità dei filesystem in sola lettura (usata ad esempio in Android e in molte distro orientate alla sicurezza). Terzo, Jiayuan Chen ha risolto un problema di lettura fuori dai limiti e un leak di puntatori nel sottosistema **BPF sock_ops**, che poteva portare a divulgazione di informazioni sensibili.

Sul fronte hardware, gli utenti AMD troveranno anche una serie di correzioni al driver AMDGPU che convertono chiamate BUG_ON() (che possono bloccare il sistema) in WARN_ON() più sicure, riducendo il rischio di kernel panic su schede gfx8-gfx12.

## Cosa fare

Se usate una distro basata su kernel LTS (Debian, Ubuntu LTS, molte distro enterprise), verificate che l'aggiornamento del kernel sia arrivato tramite il gestore pacchetti e programmate un riavvio appena possibile, specialmente se avete ksmbd attivo. Non serve panico, ma nemmeno rimandare all'infinito: sono classici fix "silenziosi" che raramente fanno notizia fuori dai circoli più tecnici, ma che chiudono buchi reali.
