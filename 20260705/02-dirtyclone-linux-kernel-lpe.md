---
title: "DirtyClone: il kernel Linux ti porta a root e non lascia tracce"
rilevanza: "ALTA"
fonte: "https://research.jfrog.com/post/dissecting-and-exploiting-linux-lpe-variant-dirtyclone-cve-2026-43503/"
data_notizia: "2026-06-25"
tags: ["linux", "kernel", "sicurezza", "privilege-escalation", "CVE", "patch"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: il pubblico di RobyRoot usa Linux sul desktop e sui server. DirtyClone è nella tradizione delle grandi vulnerabilità del kernel (DirtyCOW, Dirty Pipe) e ha un exploit pubblico funzionante. Un articolo che spiega il meccanismo in modo accessibile e dà le istruzioni per aggiornare è esattamente ciò che serve.
---

# DirtyClone: il kernel Linux ti porta a root e non lascia tracce

Conosci DirtyCOW? E Dirty Pipe? Bene, fai spazio nella lista delle grandi vulnerabilità del kernel Linux: arriva **DirtyClone**, alias **CVE-2026-43503**. Un bug nel sottosistema di rete che permette a qualsiasi utente locale senza privilegi di diventare root, senza lasciare una singola riga nei log del kernel. I ricercatori di JFrog hanno pubblicato l'exploit il 25 giugno, e da quel momento il conto alla rovescia per aggiornare è scattato per tutti.

## La famiglia DirtyFrag e come funziona DirtyClone

DirtyClone fa parte di una famiglia di vulnerabilità del kernel chiamata **DirtyFrag**, che colpisce il modo in cui il kernel gestisce i buffer di rete (socket buffer, o *skb*) quando questi fanno riferimento a pagine di memoria condivise con la cache del filesystem.

Il trucco è sempre lo stesso: convincere il kernel a trattare memoria in sola lettura (file-backed page cache) come se fosse scrivibile, sfruttando le operazioni di clonazione dei pacchetti di rete. In DirtyClone il vettore specifico passa attraverso il meccanismo **copy-on-write (COW)** applicato ai pacchetti di rete clonati nel sottosistema XFRM/IPsec.

```
Utente non privilegiato
        |
        v
Crea socket e manipola pacchetti clonati
        |
        v
Kernel tratta memoria read-only come scrivibile (bug COW)
        |
        v
Scrittura arbitraria in pagine privilegiate del kernel
        |
        v
Escalation a root — nessun log prodotto
```

La parte più preoccupante? L'exploit **non lascia tracce su disco** e **bypassa i comuni strumenti di monitoraggio dell'integrità**. Sistemi come auditd e i log standard del kernel restano silenziosi durante l'attacco.

## Chi è vulnerabile?

Sono affette le versioni del kernel Linux dalla **6.1 alla 6.12** (incluse). Le serie LTS 5.15 e 5.10 sono ancora sotto indagine. Il requisito minimo per sfruttare la vulnerabilità è la capability `CAP_NET_ADMIN`, che in molte configurazioni è ottenibile da un utente non privilegiato tramite i **user namespace non privilegiati** — funzionalità abilitata di default su Ubuntu, Debian e molte altre distro.

```bash
# Controlla se i user namespace non privilegiati sono abilitati
cat /proc/sys/kernel/unprivileged_userns_clone
# Output 1 = abilitati (vulnerabile al vettore più semplice)

# Controlla la versione del kernel in uso
uname -r
```

## Come verificare se sei esposto

```bash
# Controlla la versione del kernel
uname -r

# Se la versione è tra 6.1 e 6.12 e i user namespace sono abilitati,
# sei potenzialmente vulnerabile.

# Verifica se il sistema ha già la patch (Debian/Ubuntu)
apt-get changelog linux-image-$(uname -r) 2>/dev/null | grep -i "43503"
```

## Come aggiornare

Il fix è stato integrato a partire da **Linux 7.1-rc5** ed è stato backportato dalle principali distribuzioni.

**Ubuntu/Debian:**
```bash
sudo apt update && sudo apt upgrade linux-image-generic
sudo reboot
```

**Fedora/RHEL/CentOS Stream:**
```bash
sudo dnf update kernel
sudo reboot
```

**Arch Linux:**
```bash
sudo pacman -Syu
# Il kernel 7.0.14 incluso nell'ISO di luglio 2026 contiene già la fix
sudo reboot
```

Dopo il riavvio, verifica la versione aggiornata:
```bash
uname -r
# Deve essere >= 7.1-rc5 oppure una versione patchata dalla tua distro
```

## Mitigazione temporanea (se non puoi riavviare subito)

Se hai sistemi critici su cui non puoi permetterti un riavvio immediato, puoi disabilitare i user namespace non privilegiati come mitigazione parziale:

```bash
# Disabilita i user namespace non privilegiati (mitigazione temporanea)
sudo sysctl -w kernel.unprivileged_userns_clone=0

# Per renderlo persistente fino al prossimo riavvio
echo "kernel.unprivileged_userns_clone=0" | sudo tee /etc/sysctl.d/99-dirtyclone-mitigation.conf
sudo sysctl -p /etc/sysctl.d/99-dirtyclone-mitigation.conf
```

Attenzione: questa mitigazione **non risolve il bug** e potrebbe rompere alcune applicazioni che usano i container (come Podman rootless). È solo un palliativo in attesa della patch definitiva.

## Il contesto: quarta falla Linux in sei settimane

DirtyClone è la **quarta vulnerabilità della famiglia DirtyFrag** scoperta nell'arco di sei settimane, dopo DirtyFrag originale, Fragnesia e pedit COW. Questo suggerisce che i ricercatori stanno scandagliando sistematicamente il sottosistema di rete del kernel alla ricerca di pattern simili. È probabile che ne arrivino altre.

Il messaggio è chiaro: tenere il kernel aggiornato non è un'attività opzionale. Con exploit pubblici disponibili e vulnerabilità che lasciano zero tracce, il rischio di compromissione silenziosa è concreto.

Aggiorna. Riavvia. Controlla.
