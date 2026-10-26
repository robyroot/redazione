---
title: "PHP2Shell: due falle critiche RCE in PHP, aggiorna subito!"
rilevanza: "ALTA"
fonte: "https://bleepingcomputer.com/news/security/php-ships-emergency-patches-for-critical-php2shell-flaws"
data_notizia: "2026-10-21"
tags: ["sicurezza", "PHP", "vulnerabilità", "RCE", "patch"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: focalizzarsi sull'impatto pratico per chi gestisce server con PHP (molto comune in Italia). Dare comandi immediati per verificare la versione e aggiornare. Spiegare perché questa vulnerabilità è particolarmente pericolosa.
---

# PHP2Shell: due falle critiche RCE in PHP, aggiorna subito!

Se gestisci un server web con PHP, lascia perdere tutto e leggi queste righe: il 21 ottobre 2026 il team di sicurezza di PHP ha rilasciato patch d'emergenza per due vulnerabilità critiche di esecuzione di codice remoto (RCE) soprannominate collettivamente **PHP2Shell**.

Le due falle — **CVE-2026-109618** e **CVE-2026-109619** — hanno ottenuto un punteggio CVSS v4.0 di **9.2 su 10**, il che le colloca tra le vulnerabilità più serie degli ultimi anni per l'ecosistema PHP. Una versione iniziale errata circolata online parlava addirittura di 10/10, il massimo assoluto: la correzione al 9.2 ufficiale non cambia di molto la sostanza.

## Cosa succede esattamente

Le due vulnerabilità condividono la stessa radice (classificata come CWE-824, accesso a puntatore non inizializzato): quando una richiesta HTTP termina in modo anomalo, PHP può lasciare la memoria in uno stato corrotto. Un attaccante remoto non autenticato può sfruttare questa condizione per **eseguire comandi arbitrari sul server** prima ancora che venga eseguita una sola riga del tuo codice applicativo.

L'ambiente più a rischio è **mod_php su Apache**, ma la falla colpisce anche:
- PHP-FPM
- php-cgi
- FrankenPHP
- LiteSpeed

In pratica: qualsiasi installazione PHP che risponda a richieste web è potenzialmente vulnerabile.

## Dettagli tecnici della patch

PHP ha rilasciato aggiornamenti per tutte le versioni ancora supportate:

| Versione | Patch |
|---|---|
| PHP 8.5 | 8.5.12 |
| PHP 8.4 | 8.4.27 |
| PHP 8.3 | 8.3.36 |
| PHP 8.2 | 8.2.35 |

Se stai usando PHP 8.1 o versioni precedenti, sei fuori dal supporto attivo: dovresti migrare a una versione supportata il prima possibile.

## Come verificare la tua versione

Prima di tutto, controlla quale versione di PHP hai installata:

```bash
php --version
```

Per verificare la versione usata da Apache o Nginx, puoi anche creare un file di test temporaneo:

```bash
echo "<?php phpinfo(); ?>" > /var/www/html/phpinfo.php
```

Poi aprilo dal browser e cerca la riga "PHP Version". **Ricordati di eliminare questo file subito dopo** — esporre phpinfo() in produzione è una pessima idea.

## Come aggiornare PHP

Su sistemi Debian/Ubuntu:

```bash
sudo apt update
sudo apt upgrade php8.4  # sostituisci con la tua versione
```

Su Fedora/RHEL/CentOS:

```bash
sudo dnf update php
```

Su Arch Linux:

```bash
sudo pacman -Syu php
```

Dopo l'aggiornamento, verifica di nuovo con `php --version` e riavvia il server web:

```bash
# Apache
sudo systemctl restart apache2

# Nginx + PHP-FPM
sudo systemctl restart php8.4-fpm
sudo systemctl reload nginx
```

## Nessuna mitigazione alternativa

La cosa che fa più paura di PHP2Shell è che **il team PHP stesso ha dichiarato esplicitamente che non esiste una mitigazione completa**: l'unica strada sicura è aggiornare. Non c'è WAF, non c'è configurazione, non c'è workaround che possa mettere al sicuro un'installazione con una versione vulnerabile.

A differenza di molte vulnerabilità dove si può guadagnare tempo con regole aggiuntive, qui non hai alternative: o aggiorni, o sei esposto.

## Come stanno andando le cose "in the wild"

Al momento del rilascio delle patch, PHP aveva dichiarato nessuno sfruttamento attivo noto, ma la situazione è cambiata rapidamente. CrowdStrike e altri vendor di sicurezza riportano **tentativi di exploit già in circolazione** nelle ore successive alla pubblicazione. La fuga di notizie avvenuta prima dell'embargo ha accelerato i tempi: gli attaccanti avevano potenzialmente le informazioni sulle falle prima che le patch fossero disponibili.

Il consiglio è chiaro: **non aspettare**. Aggiorna adesso, poi preoccupati del resto.
