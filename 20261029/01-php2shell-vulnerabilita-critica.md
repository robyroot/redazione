---
title: "PHP2Shell: vulnerabilità critica CVSS 10.0 colpisce PHP da decenni — aggiorna subito"
rilevanza: "ALTA"
fonte: "https://cybersecuritynews.com/emergency-java-update/"
data_notizia: "2026-10-21"
tags: ["sicurezza", "php", "vulnerabilità", "rce", "aggiornamento"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: urgenza immediata per chi gestisce server web con PHP.
  Molti lettori hanno siti WordPress, Nextcloud o app PHP custom. L'articolo deve spiegare
  come verificare la versione installata e aggiornare, con comandi pratici.
---

# PHP2Shell: vulnerabilità critica CVSS 10.0 colpisce PHP da decenni — aggiorna subito

C'è una notizia che non puoi ignorare se gestisci un server web con PHP: la PHP Foundation ha rilasciato patch di emergenza per due vulnerabilità critiche che si annidano in PHP da oltre vent'anni. Le CVE coinvolte sono **CVE-2026-109618** e **CVE-2026-109619**, soprannominate collettivamente "PHP2Shell", e almeno una delle due raggiunge un punteggio CVSS di 10.0 — il massimo assoluto.

## Cosa sono queste vulnerabilità

PHP2Shell permette a un attaccante remoto di eseguire codice arbitrario sul server senza autenticazione. In pratica, chiunque sappia come sfruttarla può prendere il controllo completo di un sistema che esegue una versione vulnerabile di PHP.

La gravità è doppia:
- **CVE-2026-109618** — CVSS 9.2: riguarda il parser delle richieste HTTP multipart, presente nel motore PHP sin dal 2004
- **CVE-2026-109619** — CVSS 10.0: sfrutta la gestione della serializzazione degli oggetti per ottenere RCE (Remote Code Execution)

Il fatto che queste falle esistano nel codice base da così tanti anni le rende potenzialmente già note ad attori malevoli da tempo. Non aspettare.

## Quali versioni sono vulnerabili

Tutte le versioni di PHP precedenti a:
- **PHP 8.5.12**
- **PHP 8.4.27**
- **PHP 8.3.36**
- **PHP 8.2.35**

Le versioni 8.1 e precedenti hanno già raggiunto la fine del supporto (EOL) e **non riceveranno patch**. Se stai ancora usando PHP 7.x o 8.1, sei vulnerabile senza via d'uscita ufficiale — migrare è l'unica opzione sicura.

## Come verificare la tua versione

Prima di tutto, controlla cosa hai installato:

```bash
php --version
```

Se gestisci più versioni con un sistema come `update-alternatives`:

```bash
update-alternatives --list php
```

Su sistemi con web server, puoi verificare la versione esposta anche via phpinfo():

```bash
curl -s http://localhost/phpinfo.php | grep "PHP Version"
```

(Ricordati di rimuovere il file phpinfo dopo il controllo!)

## Come aggiornare su Linux

**Debian/Ubuntu:**
```bash
sudo apt update
sudo apt upgrade php8.4 php8.4-cli php8.4-fpm
# oppure la tua versione specifica
php --version
```

**Fedora/RHEL/AlmaLinux:**
```bash
sudo dnf update php
```

**Arch Linux:**
```bash
sudo pacman -Syu php
```

**Con Plesk o cPanel**, usa il pannello di controllo dedicato per aggiornare PHP, oppure il tool da riga di comando del pannello.

Dopo l'aggiornamento, riavvia il web server:

```bash
# Apache
sudo systemctl restart apache2

# Nginx + PHP-FPM
sudo systemctl restart php8.4-fpm
sudo systemctl restart nginx
```

## Se non puoi aggiornare subito

Se per qualsiasi motivo non riesci ad aggiornare immediatamente, considera queste mitigazioni temporanee:

```bash
# Blocca le richieste multipart sospette via WAF o blocca l'input
# Monitora i log per tentativi di exploitation
sudo tail -f /var/log/apache2/error.log | grep -i "php\|multipart"
```

Un Web Application Firewall (ModSecurity con OWASP Core Rule Set) può bloccare i tentativi di exploit noti mentre pianifichi l'aggiornamento.

## Perché è così grave

PHP alimenta quasi **il 75% del web**. WordPress, Drupal, Joomla, Nextcloud, Roundcube, Matomo — praticamente tutto il self-hosting comune gira su PHP. Una vulnerabilità CVSS 10.0 su questa base è l'equivalente digitale di un incendio in una struttura senza sprinkler: si propaga in fretta.

La buona notizia è che le patch esistono e sono disponibili ora. Non aspettare il prossimo ciclo di manutenzione: questa è una priorità di oggi.

**Aggiorna adesso.**
