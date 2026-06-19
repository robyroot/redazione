---
title: "WordPress sotto attacco: RCE critico in Everest Forms Pro, aggiorna subito"
rilevanza: "ALTA"
fonte: "https://thehackernews.com/2026/06/hackers-exploit-critical-everest-forms.html"
data_notizia: "2026-06-12"
tags: ["wordpress", "sicurezza", "vulnerabilità", "rce", "php"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: guida pratica per chi gestisce siti WordPress — come verificare se sei vulnerabile, aggiornare il plugin, e cosa fare se sei già stato compromesso. Urgenza alta: exploit attivi in-the-wild con 29.300 tentativi bloccati.
---

# WordPress sotto attacco: RCE critico in Everest Forms Pro, aggiorna subito

Se gestisci un sito WordPress con il plugin **Everest Forms Pro**, hai una priorità assoluta questa settimana: aggiornarlo immediatamente. Una vulnerabilità critica (CVE-2026-3300, CVSS 9.8) è già sfruttata attivamente da hacker in tutto il mondo per prendere il controllo completo dei siti colpiti.

## Cos'è successo

Il problema è in un'addon del plugin chiamata **Complex Calculation**. Questa funzione prende i valori inseriti dagli utenti nei form, li concatena in una stringa PHP e li passa direttamente alla funzione `eval()` — uno degli errori di programmazione più pericolosi che esistano.

Un aggressore completamente non autenticato (chiunque sul web, senza bisogno di account) può inviare un valore costruito ad arte con una singola virgoletta seguita da codice PHP arbitrario. Il risultato: esecuzione di codice remoto con i privilegi del server web. In pratica, chiunque può eseguire qualsiasi comando sul tuo server senza nemmeno fare login.

## Quanto è grave davvero

Numeri alla mano: dall'inizio degli exploit, i firewall hanno già bloccato oltre **29.300 tentativi di attacco**. Non si tratta di proof-of-concept teorici — ci sono gruppi organizzati che scandagliano il web alla ricerca di siti vulnerabili in questo momento.

Le conseguenze di un'infezione riuscita includono:
- Creazione di account amministratore nascosti
- Installazione di web shell persistenti (backdoor che sopravvivono all'aggiornamento del plugin)
- Defacement del sito o iniezione di spam e malware
- Furto di dati degli utenti registrati
- Utilizzo del server come pivot per altri attacchi

## Quali versioni sono vulnerabili

Tutte le versioni di **Everest Forms Pro fino alla 1.9.12** sono vulnerabili. La versione sicura è la **1.9.13**, rilasciata nelle scorse settimane.

Puoi verificare rapidamente la versione installata da terminale, se hai accesso SSH:

```bash
# Cerca il file principale del plugin
find /var/www -name "everest-forms-pro.php" 2>/dev/null | xargs grep -i "Version:" 2>/dev/null
```

Oppure, più semplicemente, dalla dashboard WordPress vai su **Plugin → Plugin installati** e cerca Everest Forms Pro.

## Come risolvere (in 5 minuti)

**Aggiornamento dalla dashboard WordPress:**
1. Accedi al pannello admin
2. Vai su **Plugin → Plugin installati**
3. Cerca "Everest Forms Pro"
4. Clicca su **"Aggiorna ora"**

Se non vedi l'aggiornamento disponibile, potrebbe essere un problema di license key scaduta. In quel caso, accedi al sito di wpeverest.io con il tuo account, scarica manualmente la versione 1.9.13 e sostituisci i file tramite FTP o File Manager del tuo hosting.

## E se il sito è già stato compromesso?

Se il sito ha ricevuto traffico sospetto nelle ultime settimane, controlla i log del server cercando richieste POST verso i form:

```bash
# Su Nginx
grep -i "everest" /var/log/nginx/access.log | grep "POST" | tail -100

# Su Apache
grep -i "everest" /var/log/apache2/access.log | grep "POST" | tail -100
```

Controlla anche la presenza di file PHP anomali nelle cartelle degli upload:

```bash
find /var/www/html/wp-content/uploads -name "*.php" 2>/dev/null
find /var/www/html/wp-content/uploads -name "*.phtml" 2>/dev/null
```

Se trovi qualcosa di sospetto, cambia immediatamente tutte le password (admin WordPress, database, FTP/SFTP) e considera un ripristino da backup precedente alla finestra di attacco.

## Mitigazione aggiuntiva con WAF

Se stai usando Wordfence o Sucuri, entrambi hanno già aggiunto firme per bloccare i tentativi di exploit noti. Ma il WAF è una rete di sicurezza, non una soluzione: **aggiorna il plugin** come primo passo.

Per verificare se Wordfence sta attivamente proteggendo:

```bash
# Via WP-CLI (se disponibile sul server)
wp wordfence scan --type=malware --path=/var/www/html
```

## Takeaway

Le vulnerabilità PHP eval injection esistono da decenni, eppure continuano ad apparire nei plugin WordPress più popolari. La lezione è sempre la stessa: tieni aggiornati i plugin, rimuovi quelli che non usi, e considera un WAF per i siti di produzione. Questa settimana hai però un'azione concreta e urgente da fare adesso: aggiorna Everest Forms Pro alla versione 1.9.13.

---

*Fonte: [The Hacker News](https://thehackernews.com/2026/06/hackers-exploit-critical-everest-forms.html), [Bleeping Computer](https://www.bleepingcomputer.com/news/security/critical-everest-forms-pro-flaw-exploited-to-take-over-wordpress-sites/)*
