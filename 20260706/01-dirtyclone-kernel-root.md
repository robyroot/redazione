---
title: "DirtyClone e Bad Epoll: due falle nel kernel Linux ti regalano i permessi di root"
rilevanza: "ALTA"
fonte: "https://securityaffairs.com/194338/uncategorized/dirtyclone-fourth-linux-kernel-flaw-in-six-weeks-escalates-to-root.html"
data_notizia: "2026-07-04"
tags: ["linux", "kernel", "sicurezza", "privilege-escalation", "CVE", "patch"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: articolo urgente di sicurezza con guida pratica al patching. Enfatizzare che colpisce desktop, server E Android. Mostrare la mitigazione temporanea e il comando per aggiornare su ogni distro principale. Il fatto che sia il quarto exploit simile in sei settimane è la notizia nella notizia.
---

# DirtyClone e Bad Epoll: due falle nel kernel Linux ti regalano i permessi di root

Brutta settimana per il kernel Linux. In pochi giorni sono emerse due vulnerabilità distinte — **DirtyClone** (CVE-2026-43503) e **Bad Epoll** (CVE-2026-46242) — che permettono a un utente normale, senza privilegi speciali, di diventare root sulla propria macchina. Colpiscono desktop, server e dispositivi Android con kernel 6.4 in poi. Se non hai aggiornato il kernel di recente, è il momento di farlo adesso.

## Cosa sono e come funzionano

**DirtyClone** (CVE-2026-43503, CVSS 8.8) è l'ultima variante di una famiglia di exploit che abusano dello stack di rete del kernel. Il trucco sta nel modo in cui il kernel gestisce i buffer dei pacchetti di rete (`skb`) quando vengono "clonati" durante operazioni come XFRM/IPsec o RxRPC. L'attaccante inganna il kernel a trattare memoria in sola lettura del page cache come memoria di rete scrivibile, corrompendola. Il risultato: escalation di privilegi completa, e soprattutto **senza lasciare tracce su disco**.

È il quarto exploit della serie DirtyFrag in sei settimane — gli altri si chiamano DirtyFrag, Fragnesia e pedit COW. Una brutta catena.

**Bad Epoll** (CVE-2026-46242) è invece un bug di tipo use-after-free nell'interfaccia `epoll` del kernel — quella che usano quotidianamente browser, server web, e praticamente qualsiasi applicazione moderna per tenere d'occhio molti file descriptor contemporaneamente. Il problema: in `ep_remove()`, il puntatore `file->f_ep` viene azzerato sotto lock, ma il puntatore `@file` continua a essere usato. Una chiamata concorrente `__fput()` può liberare la struttura `eventpoll` nel frattempo, causando corruzione della memoria e — con il giusto timing — root.

## Quali sistemi sono a rischio

Entrambe le falle colpiscono Linux dalla versione 6.4 in su. In pratica:

- Ubuntu (tutte le versioni LTS recenti)
- Debian, Fedora, Arch Linux
- Android (kernel 6.6+, inclusi i Pixel attuali)
- Qualsiasi server Linux con kernel non aggiornato

Per DirtyClone, le distro più a rischio sono quelle che abilitano i **user namespace non privilegiati** di default: Ubuntu, Debian e Fedora.

## Come proteggersi subito

La patch definitiva è nel kernel 7.1.3 (e upstream commit `a6dc643c6931` per Bad Epoll). Ma puoi anche mitigare temporaneamente DirtyClone disabilitando i user namespace non privilegiati:

```bash
# Mitigazione temporanea per DirtyClone su Debian/Ubuntu
sudo sysctl -w kernel.unprivileged_userns_clone=0

# Per renderla permanente
echo "kernel.unprivileged_userns_clone=0" | sudo tee -a /etc/sysctl.d/99-security.conf
sudo sysctl -p /etc/sysctl.d/99-security.conf
```

Nota: questa mitigazione rompe alcune funzionalità come i container rootless con Podman o Flatpak in certi scenari. La soluzione corretta è aggiornare il kernel.

## Aggiorna il kernel adesso

```bash
# Ubuntu / Debian
sudo apt update && sudo apt full-upgrade -y
sudo reboot

# Fedora
sudo dnf upgrade --refresh -y
sudo reboot

# Arch Linux
sudo pacman -Syu linux linux-headers
sudo reboot

# Verifica la versione dopo il riavvio
uname -r
```

Per Ubuntu, Canonical ha già rilasciato gli aggiornamenti di sicurezza. Puoi verificare la disponibilità con:

```bash
apt-cache policy linux-image-$(uname -r | cut -d- -f1-2)-generic
```

## Il pattern che preoccupa

Quello che inquieta non è solo la singola vulnerabilità: è la cadenza. DirtyFrag, Fragnesia, pedit COW, DirtyClone, Bad Epoll — cinque exploit simili in poco più di un mese. I ricercatori stanno chiaramente scavando in modo sistematico nelle stesse aree del kernel, e probabilmente non hanno ancora finito.

La buona notizia è che tutti questi exploit richiedono **accesso locale** alla macchina. Non sono remotamente sfruttabili da soli — l'attaccante deve già avere un account sul sistema o aver già compromesso un processo unprivileged. Ma combinati con una qualsiasi altra vulnerabilità di accesso iniziale, diventano il secondo passo perfetto.

Tieni il kernel aggiornato. Sempre.
