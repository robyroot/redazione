---
title: "PHP2Shell: due falle RCE critiche in PHP mettono a rischio milioni di server"
rilevanza: "ALTA"
fonte: "https://thehackernews.com/2026/10/php2shell-two-unpatched-critical-php.html"
data_notizia: "2026-10-20"
tags: ["sicurezza", "php", "rce", "vulnerabilità", "server"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: notizia urgente e pratica — chiunque gestisca un VPS o un sito PHP deve aggiornare subito. Ottima per enfatizzare l'importanza degli aggiornamenti tempestivi.
---

# PHP2Shell: due falle RCE critiche in PHP mettono a rischio milioni di server

Se gestisci un server con PHP — e statisticamente è molto probabile che lo fai — è il momento di aprire il terminale e aggiornare. Subito.

PHP ha rilasciato un aggiornamento di sicurezza fuori ciclo per tappare due vulnerabilità di esecuzione remota di codice (RCE) senza autenticazione, già soprannominate dai ricercatori **PHP2Shell**. Le falle hanno ricevuto un rating di gravità CVSS di 9.2 (scala 4.0), ma nelle prime comunicazioni riservate giravano valutazioni di 10.0 — il massimo assoluto.

## Cosa sono esattamente queste vulnerabilità?

Le due CVE permettono a un attaccante non autenticato — cioè chiunque, senza nessun account o credenziale — di eseguire codice arbitrario sul server. In pratica, se il tuo server gira PHP vulnerabile ed è esposto su internet, chiunque può prenderne il controllo.

Non è ipotetico: questo tipo di falla è il sogno di ogni botnet e gruppo ransomware. Con due righe di exploit, un attaccante può installare una web shell, estrarre database, cifrare file o trasformare il tuo server in un nodo di attacchi DDoS.

Il nome "PHP2Shell" richiama esattamente questo scenario: da PHP a Shell, in pochi secondi.

## Quali versioni sono colpite?

Al momento della pubblicazione, le falle riguardano **multiple versioni attive** di PHP. Il team di sviluppo ha rilasciato patch di emergenza — verificate immediatamente quale versione stai usando e controlla se è disponibile un aggiornamento.

```bash
# Controlla la versione di PHP installata
php --version

# Su Debian/Ubuntu, aggiorna PHP
sudo apt update && sudo apt upgrade php

# Su sistemi con php-fpm
sudo apt upgrade php-fpm

# Su RHEL/Fedora/AlmaLinux
sudo dnf update php

# Verifica la versione dopo l'aggiornamento
php --version
```

Se usi un hosting condiviso, controlla il pannello di controllo (cPanel, Plesk, DirectAdmin) — la maggior parte dei provider aggiorna automaticamente, ma non fa male verificare.

## Come capire se sei già stato compromesso?

Dopo aver aggiornato PHP, fai una verifica rapida dei log e degli accessi anomali:

```bash
# Controlla i log di accesso Apache per richieste sospette
sudo grep -i "eval\|base64_decode\|system\|exec\|passthru" /var/log/apache2/access.log

# Per Nginx
sudo grep -i "eval\|base64_decode\|system\|exec" /var/log/nginx/access.log

# Cerca file PHP creati di recente (ultimi 7 giorni)
find /var/www -name "*.php" -newer /var/www/index.php -mtime -7

# Controlla processi insoliti
ps aux | grep -E "python|perl|bash|sh" | grep -v root
```

Se trovi file `.php` sospetti con nomi casuali (es. `a3x9f.php`, `shell.php`, `cmd.php`), potrebbero essere web shell già installate.

## Ottobre 2026: il mese più pericoloso dell'anno per i sysadmin

Questa non è l'unica brutta notizia del mese. Nel solo ottobre 2026 abbiamo visto:

- Una vulnerabilità GitLab con CVSS 10.0 (CVE-2026-110264), fixata il 21 ottobre
- Attacchi attivi su PAN-OS GlobalProtect (CVE-2026-0257), già usati da gruppi ransomware
- Cisco Secure Email Gateway sotto attacco (CVE-2026-76519, CVSS 9.8)
- Oltre 1.400 vulnerabilità nel Patch Tuesday Microsoft di ottobre

Il pattern è chiaro: ottobre è il mese in cui si fanno i conti prima dell'inverno — anche per i criminali informatici.

## La regola aurea

Aggiornare PHP sembra banale, ma è statisticamente una delle cose che i sysadmin rimandano di più. "Funziona, perché toccarla?" è il pensiero che ha aperto le porte di migliaia di server.

La risposta è semplice: **perché qualcun altro potrebbe toccarla prima di te**.

Fissa un alert mensile per verificare gli aggiornamenti di sicurezza dei componenti chiave del tuo stack: PHP, nginx/Apache, il kernel, le librerie di sistema. Cinque minuti una volta al mese possono risparmiarti settimane di recupero da un incidente.
