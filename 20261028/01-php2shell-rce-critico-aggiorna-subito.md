---
title: "PHP2Shell: due falle RCE critiche in PHP, aggiorna subito"
rilevanza: "ALTA"
fonte: "https://bleepingcomputer.com/news/security/php-ships-emergency-patches-for-critical-php2shell-flaws"
data_notizia: "2026-10-21"
tags: ["php", "sicurezza", "rce", "vulnerabilità", "cybersecurity"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: mostrare ai lettori come verificare la versione di PHP e aggiornarla su sistemi Linux comuni (Debian/Ubuntu, Arch, server). Pratico e urgente per chi gestisce un VPS o uno stack web.
---

# PHP2Shell: due falle RCE critiche in PHP, aggiorna subito

Se gestisci un sito web, un VPS o qualsiasi server che usa PHP, la notizia di questa settimana ti riguarda direttamente: il 21 ottobre 2026 il PHP Security Team ha rilasciato patch di emergenza per due vulnerabilità critiche, soprannominate **PHP2Shell**, che permettono a un attaccante non autenticato di eseguire codice arbitrario sul server.

I CVE sono **CVE-2026-109618** e **CVE-2026-109619**, entrambi valutati **CVSS 4.0 pari a 9.2** — una cifra che in gergo significa "aggiorna adesso, non domani". Palo Alto Networks stima oltre 22 milioni di istanze PHP esposte su internet, e le analisi più recenti confermano che entrambe le vulnerabilità sono **già sfruttate attivamente**, tanto da essere inserite nel catalogo CISA KEV (Known Exploited Vulnerabilities).

## Cosa va storto nel codice PHP

La prima vulnerabilità (CVE-2026-109618) nasce da una gestione errata della memoria durante condizioni di **out-of-memory**: quando PHP esaurisce la RAM disponibile in mezzo all'elaborazione di una richiesta, può lasciare strutture dati interne in uno stato inconsistente, aprendo la porta all'esecuzione di codice. La seconda (CVE-2026-109619) sfrutta uno **stato globale non resettato** dopo il rilascio della memoria di backup, un bug sottile che si trascina almeno dalla versione 5.4 del 2012.

Entrambe sono sfruttabili tramite richieste HTTP multipart/form-data, il meccanismo usato comunemente per caricare file sui siti web. Non serve autenticazione: basta inviare la richiesta giusta al server.

## Quali versioni sono vulnerabili e come aggiornare

Le versioni corrette sono:

| Branch | Versione sicura |
|--------|-----------------|
| PHP 8.5 | 8.5.12 |
| PHP 8.4 | 8.4.27 |
| PHP 8.3 | 8.3.36 |
| PHP 8.2 | 8.2.35 |

PHP 8.1 è già fuori dal supporto ufficiale e **non riceverà patch**. Se sei ancora su 8.1 o versioni precedenti, è il momento di migrare.

Per verificare la versione attuale:

```bash
php --version
```

### Aggiornamento su Debian/Ubuntu

```bash
sudo apt update && sudo apt upgrade php
# oppure se usi il PPA di Ondřej Surý
sudo add-apt-repository ppa:ondrej/php
sudo apt update && sudo apt upgrade
```

### Aggiornamento su Arch Linux / Manjaro

```bash
sudo pacman -Syu php
```

### Con Docker

Se usi immagini PHP ufficiali su Docker, aggiorna il tag e ricostruisci:

```bash
docker pull php:8.4-fpm
docker compose build --no-cache
docker compose up -d
```

## Mitigazioni temporanee (non sostituiscono la patch)

Se per qualche motivo non puoi aggiornare subito (dipendenze legacy, ambienti di produzione critici), alcune mitigazioni temporanee possono ridurre il rischio:

- **Disabilita `session.upload_progress`** nel `php.ini`: `session.upload_progress.enabled = 0`
- **Blocca le richieste multipart/form-data** a livello di WAF o reverse proxy (nginx, Apache mod_security) se non le utilizzi

Ma attenzione: il PHP Security Team ha chiarito che **nessuna configurazione mitiga completamente** le due falle. L'aggiornamento è l'unica soluzione definitiva.

## Verifica se sei già stato colpito

Se sospetti una compromissione, cerca nei log del web server richieste anomale verso script PHP, e in particolare upload non attesi:

```bash
# cerca richieste POST con multipart negli access log di nginx
grep -i "multipart" /var/log/nginx/access.log | grep " 200 " | tail -50
```

Controlla anche processi inattesi avviati dall'utente che esegue PHP (spesso `www-data` su Ubuntu):

```bash
ps aux | grep www-data
```

## Il quadro generale

PHP2Shell arriva in un ottobre particolarmente agitato per la sicurezza: nello stesso mese abbiamo visto il Patch Tuesday Microsoft con 1413 vulnerabilità, una falla critica in GitLab con CVSS 10.0, e un attacco alla supply chain che ha colpito LiteLLM su PyPI. L'autunno 2026 non è esattamente tranquillo per chi gestisce infrastrutture.

La morale è sempre la stessa: mantenere i software aggiornati non è un'opzione, è igiene digitale. Se usi PHP, aggiorna oggi.
