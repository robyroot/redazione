---
title: "PHP2Shell: due falle critiche mettono a rischio milioni di siti web"
rilevanza: "ALTA"
fonte: "https://thehackernews.com/2026/10/php2shell-two-unpatched-critical-php.html"
data_notizia: "2026-10-20"
tags: ["php", "sicurezza", "vulnerabilità", "web", "wordpress"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: notizia urgente di sicurezza con impatto pratico su chiunque gestisca un sito o server web. Ottima opportunità per un mini-tutorial su come verificare la versione di PHP e aggiornare. Il collegamento con WordPress la rende ancora più rilevante per il pubblico italiano.
---

# PHP2Shell: due falle critiche mettono a rischio milioni di siti web

Ottobre 2026 si conferma un mese nero per la sicurezza informatica. Questa settimana sono venute alla luce due vulnerabilità critiche in PHP, battezzate collettivamente **PHP2Shell**, che mettono a rischio praticamente qualsiasi server web che esegue codice PHP — e stiamo parlando di una fetta enorme di internet.

## Cosa sono esattamente questi bug?

I due CVE in questione sono **CVE-2026-109618** e **CVE-2026-109619**, entrambi classificati con un punteggio CVSS v4.0 di **9.2 su 10** (addirittura 10/10 secondo alcune metriche CVSS v3.1). In pratica, siamo di fronte a falle di **esecuzione di codice remoto** (Remote Code Execution, RCE): un attaccante può potenzialmente eseguire comandi arbitrari sul server senza bisogno di credenziali.

La gravità reale l'ha dimostrata la cronaca: nelle ore successive alla divulgazione, siti governativi e portali di grandi aziende in diversi paesi hanno subito interruzioni temporanee mentre i team IT si affrettavano ad aggiornare. Non è una vulnerabilità teorica — è già sfruttata attivamente.

## Quali versioni sono vulnerabili?

Le versioni colpite includono praticamente tutte le branch attualmente in circolazione. I fix sono stati rilasciati in:

- **PHP 8.5.12**
- **PHP 8.4.27**
- **PHP 8.3.36**
- **PHP 8.2.35**

Le versioni precedenti alla 8.2 non ricevono più aggiornamenti di sicurezza, quindi se stai ancora girando su PHP 7.x o versioni ancora più vecchie, sei esposto e non arriverà nessuna patch: è il momento di migrare.

## Come verificare la tua versione di PHP

Prima di tutto, scopri quale versione stai usando:

```bash
# Da riga di comando
php --version

# Oppure con php-fpm
php-fpm --version

# Su sistemi con più versioni installate
update-alternatives --list php
```

Se gestisci un server con hosting condiviso o VPS, puoi anche creare un file di test temporaneo:

```php
<?php phpinfo(); ?>
```

Ma ricorda di eliminarlo subito dopo il controllo — lasciarlo in giro è un rischio di sicurezza in sé.

## Aggiornare PHP su sistemi Linux comuni

**Debian/Ubuntu:**
```bash
sudo apt update
sudo apt upgrade php8.3 php8.3-fpm
# o la versione che usi
sudo systemctl restart php8.3-fpm nginx
```

**CentOS/Rocky Linux/AlmaLinux:**
```bash
sudo dnf update php
sudo systemctl restart php-fpm httpd
```

**Arch Linux:**
```bash
sudo pacman -Syu php
```

## Il problema WordPress (e non solo)

Qui viene la nota dolente. WordPress ha già dichiarato che **non rilascerà un aggiornamento specifico** per queste vulnerabilità perché la responsabilità ricade sull'interprete PHP sottostante, non sul CMS. In pratica: se hai un sito WordPress, la tua hosting company o tu stesso dovete aggiornare PHP direttamente.

Questo vale anche per Laravel, Symfony, Drupal, Joomla e qualsiasi altra applicazione basata su PHP. Il fix non arriva dall'applicazione — arriva dall'interprete.

## Cosa fare se non puoi aggiornare subito?

In caso di impossibilità di aggiornamento immediato (ambienti legacy, test necessari, ecc.), alcune misure temporanee che possono ridurre l'esposizione:

- Abilita un **WAF** (Web Application Firewall) davanti al server
- Limita l'accesso al server PHP solo agli IP necessari
- Monitora attivamente i log per richieste anomale
- Valuta di mettere il servizio in manutenzione temporanea

## Conclusione

PHP2Shell è una di quelle vulnerabilità che non puoi permetterti di ignorare. Il consiglio è uno solo: **aggiorna ora**. Il processo richiede pochi minuti su qualsiasi sistema moderno e può salvarti da conseguenze molto più costose.

Se gestisci server per altri o sei responsabile IT in un'azienda, considera di mettere questo aggiornamento in cima alla lista delle priorità della settimana. La finestra di esposizione si restringe man mano che gli attaccanti perfezionano i loro exploit.
