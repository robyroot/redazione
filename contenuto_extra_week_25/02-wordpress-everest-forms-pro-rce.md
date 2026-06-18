---
title: "Hacker prendono il controllo di siti WordPress via Everest Forms Pro: controlla adesso"
rilevanza: "ALTA"
fonte: "https://thehackernews.com/2026/06/hackers-exploit-critical-everest-forms.html"
data_notizia: "2026-06-10"
tags: ["wordpress", "vulnerabilità", "RCE", "plugin", "sicurezza", "CVE-2026-3300", "PHP"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: articolo pratico per webmaster italiani con WordPress.
  Il plugin ha milioni di install e l'exploit permette di prendere il controllo completo del sito
  senza autenticazione. Includere: come controllare se il plugin è installato, come aggiornare,
  e soprattutto come controllare i log per capire se qualcuno ha già attaccato (indicatore
  specifico: account "diksimarina"). Utile anche la sezione su come verificare da CLI con WP-CLI.
---

Da aprile 2026 gli hacker stanno sfruttando attivamente una vulnerabilità critica in **Everest Forms Pro**, un plugin premium per WordPress usato per creare form avanzati. La falla (CVE-2026-3300) ha un CVSS di **9.8 su 10** — praticamente il massimo — e permette a chiunque, senza alcun login, di eseguire codice PHP arbitrario sul server e prendere il controllo completo del sito.

Il patch esiste da marzo 2026, ma migliaia di siti non si sono ancora aggiornati. Se usi questo plugin, agisci adesso.

## Il problema tecnico (spiegato semplice)

La funzionalità "Complex Calculation" di Everest Forms Pro permette di eseguire calcoli personalizzati basati sui dati inseriti dall'utente nel form. Per farlo, il plugin prende quell'input, lo inserisce in una stringa PHP e lo esegue con la funzione `eval()`.

Il problema: la sanitizzazione usata — `sanitize_text_field()` — non blocca i caratteri PHP pericolosi come le virgolette singole. Un attaccante può quindi iniettare codice PHP arbitrario attraverso un campo del form e il server lo eseguirà fedelmente.

Zero autenticazione richiesta. Basta trovare un sito con il plugin attivo e mandare una richiesta POST appositamente costruita.

## Quanti siti sono a rischio?

Everest Forms Pro è popolare nei siti aziendali, e-commerce e di agenzie. La patch è disponibile dalla versione **1.9.13** (rilasciata il 18 marzo 2026), ma lo sfruttamento attivo è partito il 13 aprile — segno che in tanti non si erano aggiornati.

Wordfence ha già bloccato oltre **29.300 tentativi di exploit** solo nei sistemi monitorati dalla sua rete firewall. Il numero reale di attacchi è certamente molto più alto.

## Come capire se sei già stato compromesso

C'è un indicatore molto specifico. Il payload più comune usato dagli attaccanti tenta di creare un **account amministratore WordPress** con queste credenziali precise:

- **Username:** `diksimarina`
- **Email:** `diksimarina@gmail.com`

Controlla subito se questo account esiste nel tuo WordPress:

```bash
# Con WP-CLI (il modo più rapido)
wp user list --allow-root | grep diksimarina

# Oppure direttamente nel database MySQL
mysql -u DB_USER -p DB_NAME -e "SELECT user_login, user_email, user_registered FROM wp_users WHERE user_login='diksimarina';"
```

Controlla anche i log del server web per richieste sospette:

```bash
# Apache
grep -i "diksimarina" /var/log/apache2/access.log
grep "everest" /var/log/apache2/access.log | grep "POST"

# Nginx
grep -i "diksimarina" /var/log/nginx/access.log
grep "everest" /var/log/nginx/access.log | grep "POST"
```

Se trovi l'account, il tuo sito è stato compromesso: rimuovi subito l'account, cambia tutte le password admin, verifica i file PHP modificati di recente e considera un ripristino da backup pre-compromissione.

```bash
# Trova file PHP modificati negli ultimi 30 giorni (sintomo di backdoor)
find /var/www/html -name "*.php" -newer /var/www/html/wp-config.php -mtime -30
```

## Come aggiornare il plugin

**Via pannello WordPress:**

1. Vai su `Plugin > Plugin installati`
2. Cerca "Everest Forms"
3. Clicca "Aggiorna ora" se disponibile
4. Verifica che la versione mostrata sia **1.9.13 o superiore**

**Via WP-CLI da terminale:**

```bash
# Aggiorna il plugin
wp plugin update everest-forms --allow-root

# Verifica la versione installata
wp plugin get everest-forms --fields=name,version,status --allow-root
```

## Misura temporanea se non puoi aggiornare subito

Se per qualsiasi motivo l'aggiornamento immediato non è possibile, disabilita il plugin fino a quando non puoi farlo:

```bash
wp plugin deactivate everest-forms --allow-root
```

In alternativa, se usi Wordfence (anche la versione gratuita), le regole di blocco per questo exploit sono già incluse negli aggiornamenti automatici delle firme firewall.

## La lezione da portare a casa

CVE-2026-3300 è l'ennesimo esempio di un problema sistemico: WordPress ha oltre 60.000 plugin nel repository ufficiale, più un mercato premium enorme. La superficie di attacco è immensa.

La difesa più semplice ed efficace è anche la più sottovalutata: **aggiornare regolarmente**. Se gestisci più siti WordPress, considera strumenti di gestione centralizzata come MainWP o ManageWP, e imposta gli aggiornamenti automatici almeno per i plugin di sicurezza.

L'attacco più pericoloso è sempre quello che potevi prevenire con un click.
