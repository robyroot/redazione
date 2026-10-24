---
title: "PHP2Shell: due falle critiche RCE mettono a rischio il 70% dei siti web"
rilevanza: "ALTA"
fonte: "https://thehackernews.com/2026/10/php2shell-two-unpatched-critical-php.html"
data_notizia: "2026-10-21"
tags: ["sicurezza", "php", "vulnerabilità", "RCE", "aggiornamento"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: notizia urgente di sicurezza con impatto pratico enorme — molti lettori gestiscono server PHP o CMS (WordPress, Drupal). Spiega cos'è una RCE in modo accessibile, dai i comandi per aggiornare, e sottolinea chi è ancora esposto.
---

# PHP2Shell: due falle critiche RCE mettono a rischio il 70% dei siti web

Se gestisci un server web con PHP, fermati e leggi questo articolo prima di fare qualsiasi altra cosa. Il 21 ottobre 2026 è stata rilasciata una patch d'emergenza per due vulnerabilità critiche soprannominate collettivamente **PHP2Shell** — e il mondo della sicurezza informatica sta ancora cercando di capire la portata del danno potenziale.

## Cosa sono CVE-2026-109618 e CVE-2026-109619

Le due CVE interessano praticamente tutte le versioni di PHP attualmente in uso. Entrambe riguardano un difetto nella gestione della memoria (*out-of-memory handling*) che consente a un attaccante remoto di **eseguire codice arbitrario senza alcuna autenticazione**. In pratica, chiunque sa come sfruttare queste falle può prendere il controllo completo di un server web semplicemente inviando una richiesta HTTP appositamente costruita.

Il punteggio CVSS è tra i più alti possibili: **9.2 su CVSS v4.0** secondo The Hacker News, mentre CISA ha assegnato addirittura **9.8** nella propria lista KEV (Known Exploited Vulnerabilities). Non è una sfumatura di poco conto — significa che la vulnerabilità è già attivamente sfruttata in the wild.

Il team di ricerca Palo Alto Unit 42 ha confermato che i vettori di attacco non richiedono interazione da parte dell'utente, né privilegi particolari sul sistema target. Basta che il server esponga PHP su internet.

## Perché è così grave

PHP alimenta circa il 70% dei siti web mondiali. Tra questi ci sono milioni di installazioni di WordPress, Drupal, Joomla, Laravel, e praticamente ogni CMS immaginabile. La superficie di attacco è letteralmente enorme.

La reazione è stata immediata e, in alcuni casi, drastica: diversi governi europei e infrastrutture critiche come il Porto di Rotterdam hanno temporaneamente **portato offline i propri siti** per evitare il rischio di compromissione. Non è una scelta facile per un'infrastruttura pubblica, ma è indicativa di quanto la minaccia sia considerata seria.

Due giorni dopo il rilascio della patch, PHP ha anche segnalato una terza vulnerabilità correlata, **CVE-2026-115560**, che però è stata classificata come "difficilmente sfruttabile nella pratica" — ma vale comunque tenerla d'occhio.

## Come aggiornare subito

Se sei su un server Linux con PHP installato, ecco i comandi per aggiornare immediatamente:

**Su Debian/Ubuntu:**
```bash
sudo apt update && sudo apt upgrade php*
php --version  # verifica la versione installata
```

**Su RHEL/Fedora/CentOS:**
```bash
sudo dnf update php
php --version
```

**Su Arch Linux:**
```bash
sudo pacman -Syu php
```

**Con PHP-FPM**, dopo l'aggiornamento ricordati di riavviare il servizio:
```bash
sudo systemctl restart php-fpm
# oppure, per versioni specifiche:
sudo systemctl restart php8.3-fpm
```

Se usi un pannello come Plesk, cPanel o Virtualmin, verifica che anche lì l'aggiornamento sia applicato — spesso hanno meccanismi di aggiornamento separati.

## Controlla la tua versione esposta

Per vedere rapidamente quale versione PHP gira sui tuoi servizi:

```bash
# Versione CLI
php --version

# Versione usata da Apache (se usi mod_php)
apache2 -v && php -r "phpinfo();" 2>/dev/null | head -5

# Tutte le versioni PHP-FPM attive
systemctl list-units 'php*-fpm.service' --state=running
```

Le versioni con la patch sono: **8.4.14, 8.3.26, 8.2.31** e superiori. Se sei su una versione precedente, sei vulnerabile.

## Cosa fare se non puoi aggiornare subito

In alcuni contesti (hosting condiviso, ambienti di produzione critici con finestre di manutenzione pianificate) potrebbe non essere possibile aggiornare immediatamente. In questi casi:

1. **Limita l'esposizione** — blocca il traffico in entrata sospetto a livello di firewall o WAF
2. **Monitora i log** — cerca richieste anomale con payload insoliti nei log di Apache/Nginx
3. **Contatta l'hosting provider** — molti provider hanno già applicato la patch lato server

Ma la soluzione vera è una sola: **aggiornare PHP il prima possibile**. Non domani, adesso.

## Il quadro più ampio

Ottobre 2026 si sta rivelando un mese particolarmente difficile per la sicurezza web: oltre a PHP2Shell, sono arrivate patch critiche per GitLab (CVE-2026-110264, CVSS 10.0 RCE) e Java (CVE-2026-91403, CVSS 9.1). Il Patch Tuesday di Microsoft ha chiuso ben 1.413 vulnerabilità, di cui 75 critiche.

Se c'è una lezione da imparare, è che la gestione degli aggiornamenti di sicurezza non può essere procrastinata. Automatizza dove puoi, monitora i feed di sicurezza, e tieni sempre sotto controllo le versioni software esposte su internet.
