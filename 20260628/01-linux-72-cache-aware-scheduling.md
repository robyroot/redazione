---
title: "Linux 7.2 e il Cache-Aware Scheduling: lo scheduler che finalmente capisce la tua CPU"
rilevanza: "ALTA"
fonte: "https://www.phoronix.com/news/Linux-7.2-Scheduler"
data_notizia: "2026-06-28"
tags: ["linux", "kernel", "performance", "scheduling", "AMD", "Intel"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato: spiegare in modo accessibile perché lo scheduler di Linux
  non era "consapevole" della geometria della cache sui chip moderni, e cosa
  cambia con il CAS. Ottimo per lettori con hardware AMD EPYC/Ryzen o Intel Xeon/Core Ultra.
---

Se segui da un po' il mondo Linux, sai che Linus Torvalds è famoso per sfornare
aggiornamenti del kernel con una frequenza quasi religiosa. Linux 7.2 è ancora
in sviluppo — siamo nella fase post-merge window — ma una delle feature più
chiacchierate degli ultimi mesi è già atterrata nel mainline: il
**Cache-Aware Scheduling**, abbreviato CAS.

Non è una roba glamour come il supporto a nuove GPU o nuovi filesystem, ma per
chi ha a che fare con hardware serio, questa novità conta davvero.

## Il problema con lo scheduler attuale

Partiamo dal problema. Nei processori moderni, soprattutto quelli da server e
workstation, la memoria cache non è un blocco unico. Un chip come AMD EPYC o
Intel Xeon 6 è costruito come un insieme di cluster (o chiplet), ognuno con la
propria **Last Level Cache (LLC)**. I core dello stesso cluster condividono la
loro LLC, ma per parlare con i core di un cluster diverso devono passare
attraverso un'interconnessione più lenta.

Lo scheduler del kernel Linux, fino a oggi, non era "consapevole" di questa
geometria. Poteva tranquillamente assegnare due thread che lavorano sugli stessi
dati a cluster diversi, costringendoli a "parlare" attraverso il bus di
interconnessione invece di sfruttare la cache condivisa. Risultato: più latenza,
più cache miss, prestazioni al di sotto del potenziale dell'hardware.

## Cosa cambia con il CAS

Il Cache-Aware Scheduling affronta esattamente questo problema. L'idea è
semplice: se due task condividono dati, lo scheduler li tiene preferibilmente
sullo stesso dominio LLC. Così i dati restano "vicini" e i trasferimenti
superflui tra cluster vengono ridotti al minimo.

La feature è frutto di oltre un anno di lavoro da parte di ingegneri Intel, con
numerosi cicli di revisione. Toccare lo scheduler del kernel non è banale — un
bug lì può rovinare le prestazioni di qualsiasi workload — quindi il processo è
stato lungo e attento. La versione finale è stata accettata nella merge window
di Linux 7.2, aperta a metà giugno 2026.

## Come si attiva?

Il CAS non è abilitato di default. Viene esposto tramite una nuova opzione di
configurazione kernel: `CONFIG_SCHED_CACHE`. Questo approccio **opt-in** è
deliberato: permette a distribuzioni e utenti avanzati di testarlo sui propri
workload specifici prima che diventi il comportamento standard.

C'è anche un toggle runtime via DebugFS, comodissimo per fare benchmark
comparativi senza ricompilare il kernel ogni volta. Basta un echo in
`/sys/kernel/debug/sched/cache_aware` per abilitarlo o disabilitarlo al volo.

## Chi ci guadagna di più?

I benefici più evidenti si vedranno su:

- **Server con CPU NUMA multi-cluster**: AMD EPYC e Intel Xeon 6 sono i
  candidati principali, specialmente in workload database, HPC e rendering
  parallelo
- **Ambienti di virtualizzazione**: più VM che condividono lo stesso socket
  fisico beneficiano della migliore localizzazione dei dati
- **Workstation di fascia alta**: CPU consumer di nuova generazione come Intel
  Core Ultra (con cluster P-core e E-core separati) e AMD Ryzen X3D potrebbero
  già trarne vantaggio con certi carichi di lavoro

Per un desktop medio con una CPU mainstream a die singolo e LLC unificata, il
beneficio sarà più limitato. Ma con l'evoluzione delle architetture consumer
verso design sempre più eterogenei, il CAS diventerà rilevante su un numero
crescente di macchine nel corso dei prossimi anni.

## Quando arriverà sulla tua distro?

Linux 7.2 è atteso per la release finale verso settembre-ottobre 2026.

- **Arch Linux, openSUSE Tumbleweed**: probabilmente autunno 2026
- **Fedora 41/42**: integrato nel ciclo di release normale
- **Ubuntu, Debian**: inizio 2027 nella migliore delle ipotesi

Se vuoi provarlo subito, puoi compilare il kernel dai sorgenti aggiungendo
`CONFIG_SCHED_CACHE=y` alla tua configurazione, oppure scaricare i kernel
mainline da `kernel.ubuntu.com` non appena Linux 7.2-rc1 sarà disponibile.

## Perché tenerla d'occhio

Il CAS è uno di quegli upgrade "silenziosi" che non fanno rumore al momento del
rilascio, ma si fanno sentire nei benchmark e nella vita reale. Non è una
feature che vedi nel changelog di una distro, ma dietro le quinte può fare la
differenza tra un sistema che spreca cicli CPU e uno che sfrutta davvero quello
che l'hardware ha da offrire.

Con CPU sempre più complesse e cache sempre più frammentate tra cluster diversi,
avere uno scheduler consapevole di questa geometria non è un lusso — è una
necessità. Linux 7.2 fa finalmente questo passo.
