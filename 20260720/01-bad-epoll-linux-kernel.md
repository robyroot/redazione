---
title: "Bad Epoll: la falla nel kernel Linux che regala i privilegi di root al 99%"
rilevanza: "ALTA"
fonte: "https://thehackernews.com/2026/07/new-bad-epoll-linux-kernel-flaw-lets.html"
data_notizia: "2026-07-04"
tags: ["sicurezza", "linux", "kernel", "vulnerabilità", "CVE", "privilege-escalation"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: vulnerabilità critica che riguarda praticamente tutti i sistemi Linux (server, desktop, Android), con exploit pubblico al 99%. L'aspetto del PoC pubblico e la connessione con AI security research aggiungono interesse. Ideale per il pubblico che usa Linux su server o desktop.
---

# Bad Epoll: la falla nel kernel Linux che regala i privilegi di root al 99%

Se usi Linux su server, desktop o hai un dispositivo Android relativamente moderno, questa notizia ti riguarda direttamente. È stata resa pubblica la vulnerabilità **CVE-2026-46242**, ribattezzata **Bad Epoll**, una falla nel kernel Linux capace di trasformare qualsiasi utente locale senza privilegi in root — con un tasso di successo del 99%.

## Cos'è Bad Epoll e perché è pericolosa

Il nome viene dal componente colpito: **epoll**, il sottosistema del kernel Linux che gestisce la notifica asincrona di eventi I/O. Praticamente ogni applicazione server ad alte prestazioni lo usa: nginx, Apache, Node.js, Python asyncio, PostgreSQL e praticamente qualsiasi database. E lo usa anche Android, nel suo ciclo eventi principale.

Tecnicamente si tratta di una **use-after-free race condition**: nella fase di chiusura del file, epoll può liberare memoria ancora in uso da un altro thread. Sfruttando questa finestra temporale, un attaccante può riscrivere strutture interne del kernel e prendere il controllo completo del flusso di esecuzione — il che significa: root pieno, senza chiedere permessi.

Il PoC (Proof of Concept) è già su GitHub e funziona su kernel 6.12 con una affidabilità del 99% nei test. Non stiamo parlando di un exploit teorico.

## Chi è a rischio

I kernel Linux confermati vulnerabili vanno dalla versione **5.10 alla 6.11**. Questo copre:
- Quasi tutti i server Linux in produzione
- Distribuzioni desktop come Ubuntu, Fedora, Arch, Debian
- Dispositivi Android con kernel in quel range
- Container e ambienti cloud se il kernel dell'host è interessato

Non basta che la tua app giri in un container: se il kernel dell'host è vulnerabile, un attaccante con accesso al sistema può fare escalation di privilegi.

## Come aggiornarsi

La buona notizia è che la patch è disponibile upstream dal 24 aprile 2026, ben cinque settimane prima della divulgazione pubblica (avvenuta il 30 maggio). Le principali distribuzioni hanno già integrato il fix. Devi solo aggiornare il kernel.

Su sistemi basati su apt (Ubuntu, Debian e derivate):

```bash
sudo apt update && sudo apt upgrade -y
sudo reboot
```

Su Fedora/RHEL/CentOS:

```bash
sudo dnf update kernel -y
sudo reboot
```

Su Arch Linux:

```bash
sudo pacman -Syu
sudo reboot
```

Dopo il riavvio, verifica la versione con `uname -r` e controlla che sia una versione patched (7.1.4+, 6.18.39+, 6.12.96+ o versioni LTS aggiornate).

## Il dettaglio interessante: l'AI che trova il bug vicino ma non questo

C'è un retroscena che vale la pena raccontare. Il modello **Mythos di Anthropic** aveva già identificato nella stessa sezione di codice epoll un'altra vulnerabilità di privilege escalation: CVE-2026-43074. L'AI aveva scovato il primo bug, ma si è persa questo, molto simile, nascosto proprio accanto. È stato poi trovato da un ricercatore umano analizzando manualmente il codice circostante.

Il caso illustra bene lo stato attuale della sicurezza AI-assisted: i modelli sono utili come scanner di vulnerabilità, ma un occhio umano esperto rimane essenziale per esplorare le zone grigie attorno ai bug noti.

## Perché aggiornare adesso e non aspettare

Con un PoC pubblico al 99% di successo, il tempo che intercorre tra la divulgazione e un tentativo di exploit reale si misura in ore, non in settimane. Chiunque abbia accesso fisico o shell a un sistema Linux vulnerabile può diventare root con un singolo script.

Se gestisci server, controlla i kernel di tutti i nodi — fisici, VM e container. Se usi Linux sul desktop, un aggiornamento serale è sufficiente. Non c'è motivo per aspettare.
