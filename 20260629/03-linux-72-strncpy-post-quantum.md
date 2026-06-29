---
title: "Linux 7.2 RC1: via strncpy dopo 6 anni e 362 patch, arrivano le firme post-quantistiche"
rilevanza: "MEDIA"
fonte: "https://www.phoronix.com/news/Linux-7.2-Drops-strncpy"
data_notizia: "2026-06-28"
tags: ["Linux", "kernel", "sicurezza", "post-quantum", "open-source"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato: due storie in una. La rimozione di strncpy è un racconto
  di come il kernel Linux si autoguarisca dal debito tecnico grazie a contributi
  distribuiti nel tempo. Le firme post-quantum IMA sono rilevanti per chi pensa
  alla sicurezza a lungo termine su sistemi embedded e server. Tono celebrativo
  ma accessibile, con contesto storico su strncpy per i non-sviluppatori.
---

Il 28 giugno 2026, Linus Torvalds ha rilasciato **Linux 7.2 RC1**, aprendo il consueto ciclo di release candidate che porterà al kernel stabile previsto tra agosto e settembre. Ma questa RC porta due notizie che meritano attenzione separata: l'eliminazione definitiva di `strncpy` dal codice sorgente del kernel, e l'aggiunta del supporto alle firme post-quantistiche nel sottosistema IMA.

Il source tree ha ufficialmente superato i **43 milioni di righe di codice**. Per confronto: il kernel Linux 1.0 del 1994 ne aveva circa 176.000.

## Addio strncpy: sei anni, 362 patch, zero rimpianti

Se non avete mai scritto codice C, `strncpy` vi dirà probabilmente poco. Ma se avete passato del tempo a fare sviluppo di sistema o sicurezza, avete quasi certamente un'opinione negativa su questa funzione — e probabilmente è giustificata.

`strncpy` è una funzione della libreria standard C nata negli anni '70 per copiare stringhe con un limite di lunghezza: sulla carta, una misura di sicurezza contro i buffer overflow. Il problema è che la sua semantica è particolarmente insidiosa. Se la stringa sorgente è più corta del buffer di destinazione, `strncpy` riempie il resto con null byte, sprecando cicli di CPU. Se è più lunga, **non aggiunge il terminatore null**, lasciando una stringa non terminata che può causare comportamenti indefiniti, corruzione di memoria e vulnerabilità di sicurezza.

Una funzione nata per essere sicura che è diventata nel tempo una fonte persistente di bug. Il kernel Linux ha iniziato a rimuoverla sistematicamente nel 2020. Ci sono voluti esattamente **sei anni e 362 patch** distribuite in decine di sottosistemi per eliminare ogni singolo call site. La merge window di 7.2 ha portato gli ultimi blocchi di rimozioni, e adesso `strncpy` non esiste più nel kernel. Il suo posto è stato preso da alternative più sicure come `strscpy` e `memcpy`, che hanno semantica prevedibile e non lasciano mai stringhe non terminate.

È uno di quegli episodi che racconta bene come funziona il kernel Linux: una decisione tecnica distribuita su anni di contributi da centinaia di sviluppatori diversi, portata avanti con pazienza e senza grandi fanfare. Nessuna azienda singola avrebbe potuto permetterselo — lo ha fatto la comunità.

## Cache Aware Scheduling: il kernel "vede" la gerarchia della cache

Tra le altre novità rilevanti della merge window, è finalmente arrivato nel mainline il **Cache Aware Scheduling**. Si tratta di un'ottimizzazione dello scheduler che permette al kernel di tenere conto della gerarchia della cache della CPU (L1, L2, L3) quando decide su quale core eseguire un processo.

L'idea di base è semplice: se un processo ha i suoi dati "caldi" nella cache di un core specifico, ha senso tenerlo lì invece di migrarlo su un core diverso dove dovrebbe ricaricare tutto dalla RAM molto più lenta. I benchmark mostrano guadagni concreti, con alcuni workload database che vedono throughput superiore del 30-100% in certi scenari. Utile soprattutto su macchine con molti core NUMA.

## Post-quantum IMA: il kernel guarda al futuro

La notizia forse meno visibile ma più interessante dal punto di vista della sicurezza a lungo termine riguarda il sottosistema **IMA** (Integrity Measurement Architecture). IMA è il meccanismo del kernel che verifica l'integrità dei file eseguibili prima di caricarli, usando firme crittografiche per garantire che i binari non siano stati manomessi.

Con Linux 7.2, IMA ed EVM guadagnano il supporto a **ML-DSA**, uno schema di firma post-quantistica standardizzato dal NIST come sostituto di RSA e ECDSA. I computer quantistici sufficientemente potenti potrebbero in futuro rompere le crittografie asimmetriche tradizionali — ML-DSA è progettato per resistere anche a questo scenario.

Non è ancora obbligatorio e la maggior parte dei sistemi continuerà a usare firme RSA/ECDSA per anni, ma la base infrastrutturale è ora nel kernel mainline, pronta per essere adottata. Per chi gestisce sistemi embedded, IoT industriale o dispositivi con ciclo di vita lungo — dove il software installato oggi dovrà essere sicuro anche tra 10-15 anni — iniziare a pianificare la migrazione post-quantum adesso ha molto senso.

## Quando arriva Linux 7.2 stabile?

Il rilascio stabile è atteso indicativamente tra il **16 e il 23 agosto 2026**, salvo la necessità di ulteriori cicli di correzione. Le distribuzioni principali come Ubuntu, Fedora e Arch inizieranno a integrarlo nel giro di qualche settimana dopo il rilascio ufficiale. Le distro rolling come Arch e openSUSE Tumbleweed saranno probabilmente le prime a portarvelo.
