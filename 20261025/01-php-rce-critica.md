---
title: "PHP sotto attacco: due vulnerabilità critiche RCE mettono a rischio milioni di siti"
rilevanza: "ALTA"
fonte: "https://thehackernews.com/2026/10/php2shell-two-unpatched-critical-php.html"
data_notizia: "2026-10-21"
tags: ["php", "sicurezza", "vulnerabilità", "rce", "aggiornamento", "web"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: enfatizza l'impatto concreto su chi gestisce server web con PHP (la maggior parte dei VPS hobbisti e sysadmin italiani). Mostra i comandi per verificare la versione installata e aggiornare subito. Urgenza massima.
---

# PHP sotto attacco: due vulnerabilità critiche RCE mettono a rischio milioni di siti

Se gestisci un server web con PHP — e staticamente almeno il 70% del web gira ancora su PHP — è il momento di aggiornare **adesso**. Non domani, non nel weekend: adesso.

Il 21 ottobre 2026, il team di sicurezza di PHP ha rilasciato patch di emergenza per due vulnerabilità critiche di esecuzione di codice remoto (RCE), battezzate collettivamente **PHP2Shell** dalla comunità della sicurezza. Le CVE sono **CVE-2026-109618** e **CVE-2026-109619**, con un punteggio CVSS che va da 9.2 fino a 9.8 secondo le diverse fonti — in ogni caso, siamo nella fascia "critica assoluta".

## Cosa rischiate in concreto

Le due falle permettono a un attaccante remoto di eseguire comandi arbitrari sul server, senza necessità di autenticazione. In pratica: se il tuo server PHP è esposto su internet e non aggiorni, chiunque può prenderne il controllo.

The Hacker News riporta che alcune fonti hanno già osservato tentativi di sfruttamento attivo in the wild. Altre fonti (scritte prima che uscisse la patch) dicevano che non ci fossero ancora exploit documentati — ma questa finestra si chiude in fretta. Con CVE così gravi, i kit di exploit escono nel giro di ore dalla pubblicazione dei dettagli tecnici.

## Quali versioni sono vulnerabili

Praticamente tutte le versioni di PHP attive sono interessate. Le patch sono arrivate per:

- **PHP 8.5.12**
- **PHP 8.4.27**
- **PHP 8.3.36**
- **PHP 8.2.35**

Se usi versioni più vecchie (8.1, 7.x, 5.x) sei fuori supporto ufficiale e **non riceverai patch** — questo dovrebbe essere il momento definitivo per migrare.

## Come verificare la tua versione

Collegati al tuo server via SSH e:

```bash
php --version
```

Oppure, se usi PHP-FPM:

```bash
php-fpm8.3 --version
```

Per vedere le versioni disponibili nei repo della tua distro:

```bash
# Su Debian/Ubuntu
apt list --upgradable 2>/dev/null | grep php

# Su Fedora/RHEL/CentOS
dnf check-update php*

# Su Arch Linux
pacman -Qu php
```

## Come aggiornare

Su **Debian/Ubuntu**:

```bash
sudo apt update && sudo apt upgrade php8.3 php8.3-fpm php8.3-cli
sudo systemctl restart php8.3-fpm
```

Su **Fedora/RHEL**:

```bash
sudo dnf update php
sudo systemctl restart php-fpm
```

Su **Arch Linux**:

```bash
sudo pacman -Syu php
sudo systemctl restart php-fpm
```

Se usi **PHP compilato da sorgenti** o tramite repository non standard (come Ondřej Surý su Ubuntu), aggiorna dal tuo provider abituale e verifica che la versione installata corrisponda alle versioni patchate elencate sopra.

## Docker e ambienti containerizzati

Se usi immagini Docker ufficiali di PHP, aggiorna il tag nel tuo `Dockerfile`:

```dockerfile
FROM php:8.3.36-fpm-alpine
```

Poi rebuilda e rideploya:

```bash
docker pull php:8.3.36-fpm-alpine
docker compose up -d --build
```

## Nel frattempo, mitigazioni temporanee

Se per qualsiasi motivo non puoi aggiornare subito (ambiente legacy, dipendenze complesse), considera di:

1. **Limitare l'accesso al server PHP** via firewall o IP allowlist
2. **Attivare un WAF** (ModSecurity, Cloudflare, ecc.) come strato di protezione temporaneo
3. **Monitorare i log** per richieste anomale

Queste sono misure palliative, non soluzioni. L'unica vera fix è aggiornare.

## Il contesto più ampio: PHP e la sicurezza nel 2026

PHP continua a essere il bersaglio preferito per questo tipo di vulnerabilità proprio perché è ovunque. WordPress, Drupal, Joomla, Nextcloud, Magento — praticamente ogni CMS popolare gira su PHP. Questo lo rende un obiettivo ad alto valore per i criminali informatici.

La buona notizia è che il team PHP reagisce velocemente: dall'annuncio pubblico alla patch sono passate meno di 48 ore. Ora tocca a noi sysadmin fare la nostra parte.

Non aspettare. Aggiorna. Adesso.
