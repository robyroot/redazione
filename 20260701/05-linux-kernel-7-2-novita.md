---
title: "Linux 7.2 in arrivo: scheduling cache-aware, driver Nova in Rust e firme post-quantum"
rilevanza: "ALTA"
fonte: "https://kernelnewbies.org/LinuxChanges"
data_notizia: "2026-06-28"
tags: ["linux", "kernel", "open-source", "GPU", "sicurezza", "Rust", "NVIDIA"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: il kernel 7.2 è rilevante sia per l'utente desktop (CPU scheduling più intelligente = sistema più reattivo) sia per chi segue NVIDIA su Linux (driver Nova in Rust). Enfatizza l'integrazione crescente di Rust nel kernel e il supporto post-quantum come segnali che Linux sta evolvendo in modo strutturale, non cosmetic.
---

# Linux 7.2 in arrivo: scheduling cache-aware, driver Nova in Rust e firme post-quantum

Mentre il kernel **Linux 7.1**, rilasciato il 14 giugno 2026, è ancora fresco di stampa, il ciclo di sviluppo del suo successore è già in pieno svolgimento. Linus Torvalds ha chiuso la merge window di **Linux 7.2** il **28 giugno**, con ben **13.412 commit** già integrati nel mainline. È uno dei merge window più densi degli ultimi anni, e le novità meritano un'occhiata ravvicinata.

## Cache Aware Scheduling: il tuo CPU sarà più intelligente

Una delle funzionalità più significative di Linux 7.2 è il **Cache Aware Scheduling** (CAS) — un'innovazione nel sottosistema di scheduling del kernel che cambia il modo in cui il processore assegna i thread ai core fisici.

In parole semplici: il kernel attuale spesso sposta un processo da un core a un altro senza considerare lo stato della cache CPU. Ogni volta che un thread cambia core, perde tutti i dati che aveva in cache e deve ricostruirli da zero — un'operazione che costa cicli di clock preziosi. Il CAS introduce la **consapevolezza della cache** nel schedulatore: cerca di mantenere i thread sullo stesso core (o sullo stesso cluster di core con cache condivisa) finché ha senso farlo.

Il risultato pratico? Meno cache miss, meno latenza, più reattività — soprattutto su sistemi con CPU ad alta densità di core come AMD Ryzen 9 o Intel Core Ultra. E la notizia è ancora migliore: sono già in sviluppo patch di estensione al CAS che mostrano ulteriori miglioramenti nelle prestazioni.

Per chi usa Linux come desktop quotidiano, questo si traduce in un sistema più fluido nelle operazioni multi-tasking intensive — editing video, compilazione, ambienti di sviluppo aperti.

## Driver Nova: NVIDIA open-source finalmente in Rust

Il **driver Nova** è il successore moderno di Nouveau — il driver open-source per GPU NVIDIA che ha accompagnato (con alti e bassi) gli utenti Linux per quasi vent'anni. La differenza fondamentale rispetto al predecessore? Nova è scritto in **Rust**, non in C.

In Linux 7.2, il driver continua a ricevere un ritmo sostenuto di sviluppo, con una porzione significativa del lavoro DRM (Direct Rendering Manager) del kernel dedicata proprio a Nova. Non è ancora pronto per uso quotidiano su tutte le GPU NVIDIA, ma il progresso è costante e la direzione è chiara: un driver GPU open-source moderno, memory-safe, e manutenibile a lungo termine.

```bash
# Verifica il driver GPU attualmente in uso (per schede NVIDIA)
lspci -k | grep -A 3 -i nvidia

# Su sistemi con driver nouveau attivo, puoi vedere i log Nova (dove disponibile)
dmesg | grep -i nova
```

Per chi segue la questione NVIDIA su Linux da anni, questo è un momento storico. Rust nel kernel non è più un esperimento: è parte integrante della roadmap del driver grafico più controverso dell'ecosistema Linux.

## IMA/EVM con firme post-quantum ML-DSA

Linux 7.2 porta anche il supporto per le **firme post-quantum ML-DSA** nel sottosistema di integrità **IMA/EVM** (Integrity Measurement Architecture / Extended Verification Module). Questi sono meccanismi del kernel che verificano l'integrità dei file di sistema — usati soprattutto in ambienti ad alta sicurezza come sistemi embedded, infrastrutture critiche e ambienti governativi.

**ML-DSA** (Module Lattice Digital Signature Algorithm) è uno degli algoritmi di firma digitale standardizzati dal NIST come resistenti agli attacchi dei computer quantistici. Integrarlo in IMA/EVM significa che Linux inizia a prepararsi concretamente per lo scenario post-quantum — non come ricerca teorica, ma come funzionalità operativa del kernel.

## Quando arriverà Linux 7.2 stabile?

Con la merge window chiusa il 28 giugno, le release candidate si susseguiranno nelle prossime settimane. Il ciclo tipico dura tra le 7 e le 9 settimane: la release stabile di Linux 7.2 è attesa indicativamente per **settembre 2026**.

Per seguire lo sviluppo o provare le RC:

```bash
# Verifica la versione kernel attualmente in uso
uname -r

# Su Arch Linux, il kernel mainline è disponibile tramite AUR
# (installa yay o paru prima se non disponibili)
yay -S linux-mainline linux-mainline-headers

# Su CachyOS, aggiorna all'ultima versione disponibile
sudo pacman -Syu

# Su Debian/Ubuntu, quando sarà disponibile
apt-cache policy linux-image-generic
```

**CachyOS** e **Arch Linux** sono tipicamente le prime distro ad includere le RC nei repository di testing per chi vuole sperimentare prima del rilascio stabile.

## Il quadro generale

Linux 7.2 non è un aggiornamento ordinario. Cache Aware Scheduling, Nova in Rust, e firme post-quantum sono tre segnali convergenti: il kernel Linux sta evolvendo in modo strutturale, non solo aggiungendo supporto per nuovo hardware. L'integrazione di Rust si allarga, la sicurezza crittografica guarda già al futuro post-quantum, e lo scheduler diventa finalmente consapevole della topologia della cache CPU moderna.

Per chi usa Linux desktop ogni giorno, i benefici di 7.2 saranno concreti e tangibili — anche senza mai aprire un terminale.
