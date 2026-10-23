---
title: "PHP2Shell: due falle critiche mettono a rischio il 70% del web — aggiorna subito"
rilevanza: "ALTA"
fonte: "https://thehackernews.com/2026/10/php-issues-emergency-patches-for-two.html"
data_notizia: "2026-10-21"
tags: ["sicurezza", "php", "vulnerabilità", "web", "rce", "patch"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: guida pratica all'aggiornamento con comandi concreti per chi gestisce server PHP (WordPress, Drupal, VPS). Tono urgente ma non allarmistico: spiega cosa succede, chi è a rischio, come fixare.
---

# PHP2Shell: due falle critiche mettono a rischio il 70% del web — aggiorna subito

Se gestisci un sito web o un server con PHP, fermati e leggi questo articolo prima di fare qualsiasi altra cosa. La settimana scorsa il team PHP ha rilasciato patch d'emergenza per due vulnerabilità critiche di esecuzione di codice remoto (RCE) — nome in codice **PHP2Shell** — che riguardano praticamente qualsiasi installazione PHP su internet.

## Cosa sono CVE-2026-109618 e CVE-2026-109619

Entrambi i difetti derivano dallo stesso problema: quando una richiesta HTTP termina in modo anomalo, PHP può lasciare la propria memoria in uno stato corrotto. Un attaccante può sfruttare questa situazione per **eseguire comandi arbitrari sul server senza autenticazione** — cioè senza bisogno di un account o di una password.

Il punteggio CVSS v4.0 ufficiale è **9.2**, mentre il CISA americano li ha classificati addirittura **9.8**. Cloudflare ha già rilevato i primi tentativi di exploit in the wild, anche se per ora non ci sono breach confermati.

La buona notizia? Le patch d'emergenza sono arrivate il 21 ottobre. La cattiva? Con PHP che alimenta oltre il 70% dei siti web mondiali — tra cui WordPress, Drupal e Joomla — l'area esposta è enorme.

## Chi è vulnerabile

Ogni installazione PHP che serve richieste web è potenzialmente a rischio:

- **Apache con mod_php** (configurazione più a rischio)
- **PHP-FPM** (Nginx, Apache FastCGI)
- **php-cgi**
- **FrankenPHP**
- **LiteSpeed con LiteMage**

La falla è nel motore di PHP, non nelle applicazioni. Questo vuol dire che anche un WordPress perfettamente aggiornato è vulnerabile se gira su PHP non patchato.

Le versioni **PHP 8.1 e precedenti** non ricevono più aggiornamenti di sicurezza dal progetto PHP: se sei su una versione legacy, devi contattare il tuo hosting provider o migrare prima possibile.

## Come aggiornare PHP su Linux

Le versioni corrette sono:
- **PHP 8.5.12**
- **PHP 8.4.27**
- **PHP 8.3.36**
- **PHP 8.2.35**

### Su Ubuntu/Debian (con PPA di Ondřej Surý)

```bash
sudo add-apt-repository ppa:ondrej/php -y
sudo apt update
sudo apt upgrade php8.4 php8.4-fpm -y
php --version
```

### Su Fedora/RHEL/Rocky Linux

```bash
sudo dnf update php -y
php --version
```

### Su Arch Linux

```bash
sudo pacman -Syu php
```

### Verifica la versione installata

```bash
php --version
# Output atteso: PHP 8.4.27 o superiore
```

Dopo l'aggiornamento, riavvia il server web:

```bash
# Per Apache
sudo systemctl restart apache2

# Per PHP-FPM con Nginx
sudo systemctl restart php8.4-fpm
sudo systemctl restart nginx
```

## Se non puoi aggiornare subito

Le autorità olandesi per la cybersecurity (NCSC-NL) suggeriscono di **isolare le applicazioni PHP** dalle reti pubbliche come misura temporanea. Se gestisci una applicazione ad alto rischio e non puoi patchare immediatamente, valuta di metterla in manutenzione fino al completamento dell'aggiornamento.

Alcuni siti sono andati offline in via precauzionale in queste ore: un downtime volontario è meglio di una compromissione.

## Il dettaglio della fuga anticipata

Nota interessante sul lato operativo: secondo alcune fonti, le falle sono trapelate **prima della scadenza dell'embargo**, che sarebbe scaduto un giorno dopo il rilascio delle patch. Questo ha accelerato la pubblicazione, ma ha anche dato meno tempo ai gestori di sistemi per prepararsi. Un monito ulteriore a tenere sempre i sistemi aggiornati, senza aspettare l'urgenza.

## In sintesi

PHP2Shell non è hype mediatico: è una vulnerabilità reale, con punteggio critico, exploit già in circolazione e una superficie d'attacco che riguarda la maggior parte del web. Se gestisci un server PHP, **aggiornare oggi** è la cosa più importante che puoi fare per la sicurezza dei tuoi sistemi.

Controlla la versione di PHP, esegui l'update, riavvia i servizi. Fatto. Il tuo sito (e i tuoi utenti) ti ringrazieranno.
