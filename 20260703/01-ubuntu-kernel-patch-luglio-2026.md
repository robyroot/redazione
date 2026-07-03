---
title: "Ubuntu rilascia un mega-patch per il kernel: aggiorna subito tutte le LTS"
rilevanza: "ALTA"
fonte: "https://www.linuxcompatible.org/story/linux-kernel-updates-for-ubuntu-64a"
data_notizia: "2026-07-01"
tags: ["ubuntu", "sicurezza", "kernel", "patch", "dirty-frag", "fragnesia", "CVE"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato per RobyRoot: urgenza pratica — "aggiorna adesso" con comandi copia-incolla.
  Il pubblico italiano ha già letto di Dirty Frag a maggio, ma questa mega-patch chiude tutto
  in un colpo solo su ogni versione LTS. Perfetto per chi si era perso i singoli aggiornamenti.
---

# Ubuntu rilascia un mega-patch per il kernel: aggiorna subito tutte le LTS

Se stai ancora aspettando di aggiornare il kernel Ubuntu, smettila di aspettare: il 1° luglio 2026 Canonical ha spinto un aggiornamento di sicurezza massiccio che copre tutte le versioni LTS ancora supportate, dai mattoni delle 20.04 alle 26.04 appena uscite. Dentro ci sono le correzioni per Dirty Frag, Fragnesia e decine di altre vulnerabilità. È il tipo di patch che non si rimanda.

## Cosa c'è dentro questo aggiornamento

Il pacchetto tocca praticamente ogni versione attiva di Ubuntu:

- **Ubuntu 20.04 LTS** (Focal Fosse) — ancora in manutenzione
- **Ubuntu 22.04 LTS** (Jammy Jellyfish)
- **Ubuntu 24.04 LTS** (Noble Numbat)
- **Ubuntu 26.04 LTS** (Plucky Puffin) — uscita pochi mesi fa

Sono inclusi anche i kernel cloud-specific per AWS, Azure, GCP e Oracle — quindi se gestisci macchine virtuali su questi provider, la patch è altrettanto urgente.

## Le vulnerabilità principali: Dirty Frag e Fragnesia

Probabilmente ne hai già sentito parlare a maggio, ma facciamo un recap veloce.

**Dirty Frag** (CVE-2026-43284, CVE-2026-43500) è una coppia di bug di privilege escalation locale che colpisce i moduli IPsec (`esp4`, `esp6`) e il protocollo `rxrpc`. In parole povere: un utente senza privilegi di root potrebbe sfruttarli per diventare amministratore del sistema. Il punteggio CVSS arriva a 8.8 — alto.

**Fragnesia** (CVE-2026-46300) è forse ancora più insidiosa perché è stata *introdotta* dalla patch di Dirty Frag. Il ricercatore William Bowling del team V12 ha scoperto che correggere CVE-2026-43284 ha esposto una violazione di invariante latente nel sottosistema XFRM ESP-in-TCP, creando di fatto un nuovo vettore d'attacco. CVSS 7.8, con exploit pubblico già disponibile su GitHub dal 13 maggio.

Questo aggiornamento Ubuntu chiude entrambe le famiglie di vulnerabilità in un solo passaggio.

## Come aggiornare: tre comandi e hai finito

Apri un terminale e lancia:

```bash
sudo apt update
sudo apt upgrade -y
sudo reboot
```

Il reboot è obbligatorio perché il kernel nuovo entra in gioco solo dopo il riavvio. Se non vuoi riavviare subito (magari è un server di produzione), puoi verificare quale kernel è in uso con:

```bash
uname -r
```

E confrontarlo con i pacchetti installati:

```bash
dpkg -l | grep linux-image | grep "^ii"
```

Il kernel aggiornato compare nella lista ma diventa attivo solo dopo il riavvio.

## Kernel live patching: un'alternativa per i server

Se gestisci un server che non puoi permetterti di riavviare, Ubuntu offre **Livepatch** — un sistema che applica le patch al kernel in esecuzione senza interruzioni. È gratuito per uso personale fino a 5 macchine con un account Ubuntu One:

```bash
sudo snap install canonical-livepatch
sudo canonical-livepatch enable <TOKEN>
```

Puoi ottenere il token gratuito su [ubuntu.com/security/livepatch](https://ubuntu.com/security/livepatch).

## E se uso i kernel cloud su AWS o Azure?

Per le istanze cloud, l'aggiornamento è disponibile tramite i normali canali `apt`. Non devi fare nulla di speciale: il processo è identico. Quello che cambia è il nome del pacchetto kernel:

```bash
# Su istanze AWS
dpkg -l | grep linux-image-aws

# Su istanze Azure
dpkg -l | grep linux-image-azure
```

Dopo l'aggiornamento, su cloud la cosa più comoda è spesso fermare l'istanza, avviarla di nuovo e verificare il kernel con `uname -r`.

## Perché questa patch è diversa dalle solite

Normalmente un singolo aggiornamento di sicurezza copre una manciata di CVE. Questo copre *decine* di vulnerabilità in un colpo solo, tra cui due famiglie di bug che hanno fatto girare la testa alla comunità di sicurezza Linux negli ultimi due mesi. Il fatto che Canonical abbia sincronizzato il rilascio per tutte le LTS contemporaneamente suggerisce che abbiano considerato l'urgenza elevata.

Non aspettare il weekend per farlo. Tre comandi, un riavvio, e sei a posto.
