---
title: "Secure Boot Microsoft scade il 27 giugno: cosa devi fare se usi Linux"
rilevanza: "ALTA"
fonte: "https://linuxiac.com/microsoft-secure-boot-key-expiration-affects-linux-ecosystem/"
data_notizia: "2026-06-10"
tags: ["secure-boot", "linux", "uefi", "microsoft", "kernel", "sicurezza"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: spiegare in modo chiaro cosa sta per succedere (e soprattutto cosa NON succederà) il 27 giugno, per evitare panico inutile e guidare chi deve davvero agire. Tono rassicurante ma concreto, con checklist pratica.
---

# Secure Boot Microsoft scade il 27 giugno: cosa devi fare se usi Linux

Il **27 giugno 2026** scade il certificato Secure Boot che Microsoft usa per firmare i bootloader Linux dal lontano 2011. Sembra una notizia allarmante, ma la realtà è più sfumata — e capire la differenza può farti risparmiare un bel po' di panico inutile.

## Prima di tutto: calma

La domanda che si stanno facendo tutti è: *il mio Linux smetterà di avviarsi il 28 giugno?*

Risposta breve: **no**, se il tuo sistema funziona oggi e non stai pianificando reinstallazioni nelle prossime settimane. Il vecchio certificato non viene rimosso dal firmware del tuo computer alla sua scadenza. I bootloader già firmati con il vecchio certificato continueranno a essere considerati validi dai firmware UEFI esistenti.

Il vero impatto è su un'operazione specifica: dopo il 27 giugno, Microsoft non accetterà più **nuove richieste di firma** per bootloader e shim con il vecchio certificato. Chi deve agire sono principalmente i maintainer delle distribuzioni — e la maggior parte lo ha già fatto.

## Come funziona Secure Boot su Linux (spiegato semplicemente)

Quando accendi il PC, il firmware UEFI verifica che il bootloader sia firmato da una chiave fidata. Su Linux, questa catena funziona così:

```
UEFI Firmware → shim (firmato da Microsoft) → GRUB/systemd-boot → Kernel
```

Il protagonista qui è **shim**: un piccolo bootloader intermedio firmato direttamente da Microsoft, che a sua volta verifica la firma di GRUB. La chiave Microsoft 2011 che scade è quella usata per firmare shim. Le distro major (Fedora, Ubuntu, Debian, openSUSE, RHEL, Arch) hanno già preparato e rilasciato nuove versioni di shim firmate con il certificato **2023**.

## Chi deve agire e come

**Utenti desktop con distro aggiornata:** probabilmente non devi fare nulla. Se hai fatto aggiornamenti di sistema nelle ultime settimane, la tua distro ha quasi certamente già installato la nuova versione di shim.

Verifica la versione di shim installata:

```bash
# Su Fedora/RHEL/CentOS Stream
rpm -q shim-x64

# Su Debian/Ubuntu
dpkg -l shim-signed | grep shim

# Su openSUSE Tumbleweed/Leap
rpm -q shim
```

Versioni minime sicure (aggiornate con il certificato 2023):
- **Fedora**: shim 15.8 o superiore
- **Ubuntu**: shim-signed 1.58 o superiore
- **Debian**: shim-signed 1.41 o superiore

Se hai versioni precedenti, aggiorna subito:

```bash
# Fedora/RHEL
sudo dnf update shim-x64 shim-ia32

# Ubuntu/Debian
sudo apt update && sudo apt install --only-upgrade shim-signed

# openSUSE
sudo zypper update shim
```

**Amministratori di server:** qui la situazione è leggermente più critica. I server esistenti che avviano correttamente oggi continueranno a farlo. Il problema sorge nelle **reinstallazioni**: se dopo il 27 giugno usi vecchie ISO di installazione con Secure Boot abilitato, potresti avere problemi.

Azione preventiva: aggiorna le tue ISO di recovery adesso, prima della scadenza.

```bash
# Verifica quale ISO stai usando
sha256sum /path/to/distro.iso

# Confronta con i checksum ufficiali della versione più recente
# scaricabile dal sito della tua distribuzione
```

## Se hai Secure Boot disabilitato

Se hai disabilitato Secure Boot nel BIOS/UEFI (pratica molto comune su sistemi Linux desktop, soprattutto per il dual boot o per usare moduli del kernel non firmati), questa notizia **non ti riguarda**. Puoi ignorarla tranquillamente.

Per verificare lo stato di Secure Boot:

```bash
mokutil --sb-state
# Output: "SecureBoot enabled" oppure "SecureBoot disabled"
```

## Il rischio reale: scenari di disaster recovery

Il punto critico è durante il **ripristino di emergenza**. Se un server dovesse crashare e tu dovessi avviare da una chiavetta ISO vecchia con Secure Boot abilitato, l'installazione potrebbe non funzionare. Oppure se provi a fare un'installazione su hardware nuovo usando immagini ISO che non hai aggiornato da mesi.

Preparati in anticipo scaricando le ISO più recenti delle distribuzioni che usi e conservandole in un posto sicuro. Le ISO rilasciate da giugno 2026 in poi includeranno già lo shim firmato con il certificato 2023.

## Checklist rapida

- [ ] Secure Boot abilitato sul mio sistema? (se no, ignora tutto)
- [ ] Aggiornamento sistema eseguito negli ultimi 30 giorni? (se sì, probabilmente a posto)
- [ ] Versione shim verificata e aggiornata
- [ ] ISO di recovery aggiornate alle versioni più recenti
- [ ] Server con reinstallazioni pianificate? Usa ISO del 2026

## Takeaway

La scadenza del 27 giugno è principalmente un evento tecnico per i maintainer delle distribuzioni, non un'emergenza per gli utenti finali. Se usi una distro aggiornata, sei quasi certamente già al sicuro. Le azioni concrete da fare adesso sono tre: aggiorna il sistema, scarica ISO di recovery recenti, e — se gestisci server — verifica la versione di shim prima di fine mese.

---

*Fonte: [Linuxiac](https://linuxiac.com/microsoft-secure-boot-key-expiration-affects-linux-ecosystem/), [Red Hat Developer](https://developers.redhat.com/articles/2026/02/04/secure-boot-certificate-changes-2026-guidance-rhel-environments), [LinuxLap](https://linuxlap.com/news/secure-boot-linux-2026/)*
