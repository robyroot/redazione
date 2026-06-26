---
title: "Linux 7.2: Cache Aware Scheduling porta il tuo PC a un livello superiore (MongoDB +100%)"
rilevanza: "ALTA"
fonte: "https://www.phoronix.com/news/Linux-7.2-MM"
data_notizia: "2026-06-20"
tags: ["linux", "kernel", "performance", "scheduler", "database"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: spiegare in modo accessibile cosa cambia concretamente per
  gli utenti Linux con CPU moderne (AMD Ryzen, Intel Core Ultra), mostrando i benchmark reali
  su MongoDB e MySQL come hook visivo. Ottimo per chi usa Linux come server o workstation.
---

# Linux 7.2: Cache Aware Scheduling porta il tuo PC a un livello superiore (MongoDB +100%)

Se hai un PC con una CPU moderna — un AMD Ryzen 7000 o un Intel Core Ultra — Linux 7.2 sta per cambiare le carte in tavola in modo significativo. Il kernel ha finalmente integrato il **Cache Aware Scheduling (CAS)**, una funzionalità attesa da anni che promette miglioramenti di performance anche oltre il 100% su certi carichi di lavoro. E no, non stiamo parlando di benchmark sintetici artificiali: i guadagni si vedono su MongoDB, MySQL e applicazioni reali.

## Cos'è il Cache Aware Scheduling e perché importa

Lo scheduler di Linux — il componente che decide quale processo gira su quale core della CPU — fino ad oggi era sostanzialmente cieco rispetto a un dettaglio fondamentale delle CPU moderne: la **cache L3 (LLC, Last Level Cache)**.

Le CPU di ultima generazione hanno topologie complesse. Un Ryzen 9 ha più chiplet, ognuno con la propria cache L3. Un Core Ultra ha cluster di P-core ed E-core con cache separate. Quando Linux spostava un thread da un core all'altro senza considerare questi confini, il thread si ritrovava a lavorare con una cache "fredda", dovendo ricaricare tutti i dati dalla RAM — operazione lentissima rispetto all'accesso alla L3.

Il Cache Aware Scheduling risolve esattamente questo: **insegna allo scheduler a tenere i thread il più possibile all'interno dello stesso dominio di cache**, evitando migrazioni costose tra cluster diversi. La feature è stata sviluppata principalmente da ingegneri Intel e ha impiegato oltre un anno per maturare abbastanza da essere accettata nel kernel mainline.

## I numeri che fanno impressione

I benchmark mostrati su Phoronix sono genuinamente sorprendenti:

- **MongoDB con NVMe storage**: fino al **+30% di throughput**
- **MongoDB con storage lento (HDD o I/O limitato)**: fino al **+100% di throughput**
- **MySQL**: in alcuni scenari si parla di guadagni fino al **+360%** con le estensioni CAS già in sviluppo

Come è possibile un +100% solo ottimizzando lo scheduler? Su workload a bassa intensità di I/O — come certi pattern di lettura di MongoDB — la CPU passa moltissimo tempo ad aspettare dati dalla cache. Se i dati sono già nella L3 giusta, si elimina una bottleneck enorme.

## Cosa merge con Linux 7.2 esattamente

In Linux 7.2 entrano due miglioramenti distinti ma complementari:

**1. Cache Aware Scheduling (CAS)**
Attivato con `CONFIG_SCHED_CACHE`. Lo scheduler ora è consapevole della topologia LLC e prende decisioni di bilanciamento del carico che rispettano i confini di cache.

**2. Miglioramenti MGLRU (Multi-Gen LRU)**
Si tratta di ottimizzazioni al gestore della memoria virtuale che riducono il trashing della cache su carichi misti. Sono questi miglioramenti MGLRU che producono il +100% su MongoDB nelle misurazioni attuali.

Sono due path separati, ma insieme ridisegnano il modo in cui Linux gestisce risorse condivise su hardware moderno.

## Quando arriva e come testarlo

Linux 7.1 è uscito il 14 giugno 2026. La finestra di merge per 7.2 è appena aperta, quindi il kernel stabile 7.2 arriverà indicativamente tra settembre e ottobre 2026.

Se vuoi testare subito senza aspettare, puoi usare il kernel `linux-next` o compilare dal branch `sched/core` del repository TIP:

```bash
# Clona il tree TIP (solo branch sched/core)
git clone --depth=1 --branch sched/core \
  https://git.kernel.org/pub/scm/linux/kernel/git/tip/tip.git
cd tip
make menuconfig   # assicurati di abilitare CONFIG_SCHED_CACHE
make -j$(nproc)
```

In alternativa, su Arch Linux puoi provare il pacchetto AUR `linux-cachyos` o `linux-zen` che tipicamente integrano patch sperimentali dello scheduler prima del mainline.

## Impatto reale per gli utenti normali

Non serve avere un server MongoDB in casa per beneficiarne. Il CAS migliora in generale la **reattività del desktop** su CPU multi-chiplet, la **compilazione di progetti grandi** (dove molti thread si contendono la cache), e **le sessioni di gaming** dove la latenza dei frame conta.

Per chi usa Linux come workstation o server, Linux 7.2 è probabilmente l'aggiornamento più interessante del 2026 lato performance — e non richiede nessuna modifica dalla tua parte: basta aggiornare il kernel quando arriverà nelle tue distro preferite.
