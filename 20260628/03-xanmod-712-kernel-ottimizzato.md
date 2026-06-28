---
title: "XanMod 7.1.2 è uscito ieri: il kernel ottimizzato che fa volare Linux"
rilevanza: "MEDIA"
fonte: "https://www.linuxcompatible.org/story/xanmod-linux-kernel-712-7014-and-61837-lts-released"
data_notizia: "2026-06-28"
tags: ["linux", "kernel", "xanmod", "performance", "gaming", "desktop", "ubuntu", "debian"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato: presentare XanMod a chi non lo conosce ancora, spiegare
  perché esiste un kernel custom rispetto al vanilla, e dare istruzioni pratiche
  per installarlo su Debian/Ubuntu. Il pubblico RobyRoot troverà utile la sezione
  su come scegliere il livello ABI corretto per il proprio hardware.
---

Chi segue da vicino il mondo Linux sa che accanto alla versione "vanilla" di
Linus Torvalds esistono una serie di kernel modificati ottimizzati per usi
specifici. Tra questi, **XanMod** è probabilmente il più popolare tra gli utenti
desktop e gaming su Debian e Ubuntu: proprio ieri, 27 giugno 2026, il progetto
ha rilasciato tre nuovi aggiornamenti simultanei.

**XanMod 7.1.2-xanmod1**, **7.0.14-xanmod1** e **6.18.37 LTS-xanmod1** sono
ora disponibili. Vediamo cosa portano e se vale la pena aggiornare.

## Cos'è XanMod, per chi non lo conosce

XanMod è un kernel Linux custom pensato per massimizzare le prestazioni su
desktop, workstation e sistemi gaming. Non è un progetto sperimentale o di
nicchia estrema: è attivo da anni, viene aggiornato regolarmente seguendo da
vicino il mainline, aggiungendo patch considerate stabili dalla comunità ma non
ancora accettate ufficialmente da Linus.

Le caratteristiche principali rispetto al kernel vanilla includono:

- **Compilazione con LLVM ThinLTO**: ottimizzazione inter-proceduale che può
  migliorare le prestazioni del 3-8% rispetto alla compilazione GCC standard
- **TCP BBRv3 come algoritmo di congestione predefinito**: migliore throughput
  di rete, specialmente su connessioni con perdita di pacchetti (utile per
  gaming online e streaming)
- **Patch TCP di Cloudflare**: ottimizzazioni per carichi di lavoro server e
  sessioni di rete ad alta frequenza
- **Ottimizzazioni AMD 3D V-Cache**: patch specifiche per i processori Ryzen
  X3D, usatissimi nel gaming, che sfruttano meglio la cache 3D stacked
- **Scheduler CFS orientato alla responsività**: configurazioni che privilegiano
  la latenza bassa rispetto al throughput massimo, rendendo il desktop più
  reattivo

## Cosa c'è di nuovo in questi rilasci

Le tre versioni incorporate ieri portano tutte le patch di sicurezza e
manutenzione upstream di Linux 7.1.2, 7.0.14 e 6.18.37. Sul fronte sicurezza:

- **Fix use-after-free in virtiofs**: rilevante per chi usa macchine virtuali
  con filesystem condiviso tra host e guest (QEMU/KVM, VirtualBox)
- **Pulizia dello stack networking Rose**: il protocollo AX.25 Rose riceve fix
  di stabilità
- **Correzioni memoria nel driver bnxt_re**: driver per schede di rete Broadcom
  ad alta velocità

Nulla di esplosivo a livello di feature, ma i fix di sicurezza upstream sono
importanti e questo aggiornamento li incorpora nel solito stack XanMod.

## Quale versione scegliere?

XanMod offre quattro livelli ABI x86_64 per adattarsi a hardware diverso:

| Livello | Requisiti CPU | Indicato per |
|---------|--------------|--------------|
| **v1** | Qualsiasi x86-64 | CPU molto vecchie, massima compatibilità |
| **v2** | SSE4.2 + POPCNT | CPU post-2008 circa (Core 2 Quad, Phenom II+) |
| **v3** | AVX, AVX2, BMI1/2 | Intel Haswell+ / AMD Zen in poi (consigliato per la maggior parte) |
| **v4** | AVX-512 | Intel Skylake-X+ / AMD Zen 4 in poi |

Per un desktop moderno con Ryzen o Intel Core di 12a generazione in poi,
**v3 o v4** daranno i risultati migliori. Puoi verificare il supporto AVX-512
del tuo processore con `grep avx512 /proc/cpuinfo`.

Il branch **6.18.37 LTS** è la scelta giusta se preferisci stabilità a lungo
termine rispetto alle ultime feature. Include anche una variante
**PREEMPT_RT** per workload a bassissima latenza: audio professionale con
JACK, sistemi real-time, strumentazione.

## Come installarlo su Ubuntu e Debian

Il modo più semplice è il repository APT ufficiale di XanMod. Questi i comandi
per aggiungere il repo e installare il kernel:

```bash
# Aggiungi la chiave GPG e il repository
curl -fsSL https://dl.xanmod.org/archive.key | sudo gpg --dearmor -o /usr/share/keyrings/xanmod-archive-keyring.gpg
echo 'deb [signed-by=/usr/share/keyrings/xanmod-archive-keyring.gpg] http://deb.xanmod.org releases main' | sudo tee /etc/apt/sources.list.d/xanmod-release.list

# Installa il kernel (scegli il livello ABI giusto per il tuo hardware)
sudo apt update && sudo apt install linux-xanmod-x64v3
```

Sostituisci `x64v3` con `x64v1`, `x64v2` o `x64v4` in base al tuo hardware.
Dopo il riavvio, verifica con `uname -r` che il sistema abbia caricato il nuovo
kernel.

## Vale la pena aggiornare?

Se già usi XanMod, sì — mantenersi aggiornati è sempre consigliabile per
ricevere i fix di sicurezza. Se non hai mai provato un kernel custom, XanMod è
un ottimo punto di partenza: è stabile, ben mantenuto e l'installazione su
Debian/Ubuntu è semplice quanto installare qualsiasi altro pacchetto APT.

I guadagni in termini di gaming e responsività del desktop si notano davvero,
specialmente su hardware AMD recente con 3D V-Cache. Vale la prova.
