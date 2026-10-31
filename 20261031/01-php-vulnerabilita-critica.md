---
title: "Allarme PHP: patch d'emergenza per due falle critiche, aggiorna subito"
rilevanza: "ALTA"
fonte: "https://thehackernews.com/2026/10/"
data_notizia: "2026-10-21"
tags: ["sicurezza", "php", "vulnerabilità", "patch", "cybersecurity"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: urgenza pratica — molti server Linux autoprodotti girano su PHP. Dare comandi precisi per aggiornare e verificare la versione. Sottolineare che anche la NSA ha emesso un advisory, cosa rara e significativa.
---

# Allarme PHP: patch d'emergenza per due falle critiche, aggiorna subito

Se hai un server che gira su PHP — e sono in tanti — questo è il momento di smettere di leggere e aggiornare. Il team di PHP ha rilasciato aggiornamenti d'emergenza il 21 ottobre per correggere due vulnerabilità critiche, tracciate come **CVE-2026-109618** e **CVE-2026-109619**, che possono portare all'esecuzione di codice remoto. Anche la **NSA** ha emesso un advisory raccomandando di aggiornare immediatamente o di portare offline i sistemi coinvolti.

## Cosa è successo

Le due falle riguardano il motore PHP stesso, non una libreria di terze parti. Questo le rende particolarmente pericolose: quasi tutto il codice PHP è potenzialmente esposto. I dettagli tecnici completi non sono ancora stati resi pubblici per evitare exploit di massa prima che la maggior parte dei server sia aggiornata, ma le informazioni disponibili parlano di un vettore di attacco via rete senza autenticazione.

Il fatto che sia intervenuta la NSA con un advisory pubblico — cosa che non capita spesso per falle applicative — è un indicatore chiaro dell'urgenza della situazione. Ottobre 2026 sta già venendo ribattezzato "Black October" dagli esperti di sicurezza per la concentrazione di incidenti, e questo si aggiunge alla lista.

## Quali versioni sono affette

Le correzioni sono disponibili nelle seguenti versioni:

- **PHP 8.5.12**
- **PHP 8.4.27**
- **PHP 8.3.36**
- **PHP 8.2.35**

Se stai usando una versione precedente a queste, sei vulnerabile. PHP 8.1 e versioni ancora più vecchie non ricevono più aggiornamenti di sicurezza e sono anch'esse esposte, ma non avranno patch — il percorso corretto è migrare a una versione supportata.

## Come verificare la tua versione

Prima di tutto, controlla cosa gira sui tuoi server:

```bash
php -v
```

Se stai usando PHP tramite un web server come Apache o Nginx, può essere utile anche:

```bash
php-fpm8.4 -v   # oppure la tua versione specifica
```

## Come aggiornare

**Su Debian/Ubuntu:**

```bash
sudo apt update
sudo apt upgrade php8.4 php8.4-fpm php8.4-cli
# adatta il numero di versione alla tua installazione
```

**Su RHEL/Fedora/AlmaLinux:**

```bash
sudo dnf update php
```

**Su Arch Linux:**

```bash
sudo pacman -Syu php
```

Dopo l'aggiornamento, ricordati di riavviare PHP-FPM o il tuo web server:

```bash
sudo systemctl restart php8.4-fpm
sudo systemctl restart nginx  # o apache2
```

**Se usi Remi repository:**

```bash
sudo dnf update php84-php
```

## E se non puoi aggiornare subito?

Se per qualche ragione non puoi applicare la patch immediatamente — sistemi legacy, testing, vincoli contrattuali — la raccomandazione della NSA è di **isolare il servizio dalla rete pubblica** finché non è possibile aggiornare. Un firewall che blocchi l'accesso esterno a porta 80/443 mentre mantieni l'accesso interno è meglio che lasciare il servizio esposto con versioni vulnerabili.

## Hosting condiviso e provider cloud

Se usi hosting condiviso (Aruba, Netsons, Siteground e simili) o un provider cloud con immagini gestite, controlla le comunicazioni del fornitore: molti hanno già applicato o stanno applicando le patch automaticamente. Verifica comunque nel pannello di controllo quale versione di PHP è attiva sul tuo account.

## Conclusione

Questa è una delle rare occasioni in cui "aggiorna subito" non è un consiglio burocratico ma una necessità reale. Due falle critiche nel motore PHP, un advisory NSA, e un periodo già denso di attacchi attivi: l'insieme è più che sufficiente per giustificare un intervento immediato. Pochi minuti per aggiornare possono evitare settimane di danni.
