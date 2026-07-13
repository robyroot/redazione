---
title: "DirtyClone: la falla Linux che ti dà root senza lasciare tracce"
rilevanza: "ALTA"
fonte: "https://thehackernews.com/2026/06/new-dirtyclone-linux-kernel-flaw-lets.html"
data_notizia: "2026-06-25"
tags: ["linux", "kernel", "sicurezza", "vulnerabilità", "privilege-escalation", "cve"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: spiegare in modo pratico come funziona la falla,
  perché è particolarmente insidiosa (nessuna traccia su disco) e come proteggersi
  subito con i comandi giusti. Pubblico target: sysadmin e utenti Linux avanzati.
---

# DirtyClone: la falla Linux che ti dà root senza lasciare tracce

Se usi Debian, Ubuntu o Fedora, hai quasi certamente sentito parlare di **DirtyClone** nelle ultime settimane. È la vulnerabilità del kernel Linux che ha fatto storcere il naso a tanti sysadmin: un bug che permette a qualsiasi utente locale di diventare root, senza scrivere nulla su disco e senza lasciare log leggibili dagli strumenti di integrità dei file. Una bella gatta da pelare.

## Cos'è DirtyClone e perché si chiama così

DirtyClone (CVE-2026-43503, CVSS 8.8) appartiene alla famiglia delle vulnerabilità "Dirty", che hanno tormentato il kernel Linux negli ultimi anni: DirtyPipe, DirtyFrag, DirtyFrag v2 (Fragnesia). Questa variante sfrutta un difetto nel modo in cui il kernel copia i pacchetti di rete internamente.

In pratica, quando due funzioni helper del kernel clonano un pacchetto di rete, rimuovono inavvertitamente un flag di sicurezza che dovrebbe segnalare che quella memoria è condivisa con un file su disco. Quel flag mancante è tutto ciò di cui un attaccante ha bisogno.

Il flusso d'attacco è così:
1. L'attaccante carica in memoria un binario privilegiato, tipo `/usr/bin/su`
2. Collega le pagine di memoria di quel binario a un pacchetto di rete
3. Forza il kernel a clonare quel pacchetto passando attraverso un tunnel IPsec controllato dall'attaccante
4. Durante la fase di decrittazione, il kernel sovrascrive i controlli di login del binario

Il risultato? Root. E la parte più inquietante è che l'operazione avviene tutta in memoria: nessun file su disco viene modificato, quindi strumenti come `aide`, `tripwire` o qualsiasi soluzione FIM (File Integrity Monitoring) non vedranno nulla di anomalo.

## Chi è vulnerabile

Le distribuzioni che abilitano gli **unprivileged user namespaces** sono le più esposte. Rientrano in questa categoria:

- **Ubuntu** (tutte le versioni moderne)
- **Debian** (dalla versione 12 in poi, con configurazione predefinita)
- **Fedora**
- Qualsiasi distro con il parametro `kernel.unprivileged_userns_clone=1`

Per verificare il tuo stato:

```bash
sysctl kernel.unprivileged_userns_clone
```

Se il risultato è `1`, sei potenzialmente vulnerabile se non hai ancora applicato la patch.

## Timeline: da bug a exploit pubblico

La storia di DirtyClone è curiosamente rapida:

- **19 maggio 2026**: JFrog Security Research segnala il bug al team di sicurezza del kernel Linux
- **21 maggio 2026**: la patch viene integrata nel mainline (commit `48f6a5356a33`)
- **23 maggio 2026**: assegnato il CVE-2026-43503
- **24 maggio 2026**: rilasciato Linux v7.1-rc5 con la correzione
- **25 giugno 2026**: JFrog pubblica un walkthrough completo dell'exploit, la prima dimostrazione pubblica funzionante

Praticamente 30 giorni tra la patch e la pubblicazione dell'exploit. I team di security hanno avuto un mese per aggiornarsi. Chi non l'ha fatto è adesso a rischio concreto.

## Come proteggersi subito

La soluzione definitiva è aggiornare il kernel. Su Ubuntu:

```bash
sudo apt update && sudo apt upgrade -y linux-generic
sudo reboot
```

Su Fedora:

```bash
sudo dnf update kernel -y
sudo reboot
```

Su Debian:

```bash
sudo apt update && sudo apt full-upgrade -y
sudo reboot
```

Se per qualsiasi motivo non puoi aggiornare subito (ambienti di produzione critici, kernel personalizzati), ci sono due mitigazioni temporanee:

**Mitigazione 1 — Disabilitare gli unprivileged user namespaces:**

```bash
sudo sysctl -w kernel.unprivileged_userns_clone=0
# Per renderlo persistente:
echo "kernel.unprivileged_userns_clone=0" | sudo tee /etc/sysctl.d/99-disable-userns.conf
sudo sysctl -p /etc/sysctl.d/99-disable-userns.conf
```

Attenzione: questa misura rompe alcune funzionalità (container non-root, sandbox di browser basate su Chromium, ecc.). Valuta l'impatto prima di applicarla in produzione.

**Mitigazione 2 — Blacklist dei moduli IPsec:**

```bash
echo "blacklist esp4" | sudo tee /etc/modprobe.d/dirtyclone-mitigation.conf
echo "blacklist esp6" >> /etc/modprobe.d/dirtyclone-mitigation.conf
echo "blacklist rxrpc" >> /etc/modprobe.d/dirtyclone-mitigation.conf
sudo update-initramfs -u
```

Questa opzione blocca l'exploit disabilitando i moduli necessari al tunnel IPsec, ma ovviamente interrompe le VPN basate su IPsec e AFS.

## Canonical ha già le patch

Canonical ha pubblicato le patch per tutte le versioni supportate di Ubuntu. Se usi Ubuntu e hai l'aggiornamento automatico attivo, probabilmente sei già protetto. Puoi verificare la versione del kernel corrente con:

```bash
uname -r
```

Controlla sul bulletin di sicurezza di Ubuntu (USN) quale versione corregge DirtyClone per la tua release.

## La lezione da portare a casa

DirtyClone ci ricorda due cose fondamentali. Prima: il monitoraggio dell'integrità dei file da solo non basta, perché un attaccante sofisticato può operare interamente in memoria. Seconda: aggiornare il kernel regolarmente non è opzionale, è la prima linea di difesa. Con trenta giorni tra la patch e l'exploit pubblico, il margine di sicurezza si è assottigliato parecchio.

Aggiornate. Adesso.
