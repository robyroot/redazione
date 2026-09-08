---
title: "Due zero-day nei SonicWall SMA 1000 già sotto attacco: uno ha punteggio 10.0"
rilevanza: "MEDIA"
fonte: "https://www.bleepingcomputer.com/news/security/sonicwall-warns-of-actively-exploited-sma1000-zero-day-flaws/"
data_notizia: "2026-09-08"
tags: ["cybersecurity", "vulnerabilita", "vpn", "zero-day", "sonicwall", "cisa-kev"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: usare il caso SonicWall come pretesto per parlare
  del problema più ampio dei dispositivi "di bordo" (VPN, firewall, gateway) come
  bersaglio preferito degli attaccanti, e di cosa può fare in concreto un piccolo
  reparto IT. In Italia esiste già un avviso ACN, quindi non è una notizia
  totalmente scoperta: meglio puntare sull'analisi e sui consigli pratici più che
  sul semplice annuncio.
---

Torniamo a parlare di appliance per l'accesso remoto, perché anche stavolta c'è poco da stare tranquilli. SonicWall ha rilasciato il 1º settembre 2026 degli hotfix d'emergenza per due vulnerabilità nei suoi dispositivi **Secure Mobile Access (SMA) serie 1000**, confermando che erano già sfruttate in attacchi reali.

## Le due falle

**CVE-2026-83548** è la più grave: un difetto di tipo SSRF (server-side request forgery) **pre-autenticazione** nell'interfaccia "Appliance Work Place". Punteggio CVSS: **10.0**, il massimo possibile. In pratica un attaccante remoto, senza credenziali, può indurre l'appliance a effettuare richieste per suo conto e raggiungere funzionalità sensibili che non dovrebbe poter toccare.

**CVE-2026-83549** è una command injection a livello di sistema operativo nella console di gestione (Appliance Management Console), sfruttabile **dopo** l'autenticazione da un utente con privilegi di amministratore, in condizioni specifiche. Da sola vale CVSS 7.8.

Il problema è che le due si combinano: concatenate, permettono l'**esecuzione di codice remoto senza autenticazione**. La prima apre la porta, la seconda esegue i comandi.

## Chi è colpito e cosa fare

I modelli interessati sono gli SMA **6210, 7210 e 8200v**. Le correzioni sono nelle versioni **12.4.3-03526** e successive, e **12.5.0-02952** e successive.

Entrambe le CVE sono state aggiunte al catalogo **CISA KEV** (Known Exploited Vulnerabilities), l'elenco statunitense delle falle di cui è documentato lo sfruttamento attivo: negli USA le agenzie federali hanno l'obbligo di correggerle entro scadenze precise, e per tutti gli altri è un segnale forte di priorità. Anche l'**Agenzia per la Cybersicurezza Nazionale** (ACN) italiana ha pubblicato un avviso sul caso.

Se gestite uno di questi dispositivi, l'ordine delle operazioni è questo:

1. **Applicate subito l'hotfix.** Non aspettate la prossima finestra di manutenzione: qui lo sfruttamento è già in corso.
2. **Controllate i log** dell'appliance alla ricerca di richieste anomale verso l'interfaccia Work Place o di comandi inattesi sulla console di gestione, risalendo indietro di qualche settimana.
3. **Ruotate le credenziali** degli account amministrativi e invalidate le sessioni VPN attive: se il dispositivo è stato compromesso, la patch non caccia fuori chi è già entrato.
4. **Verificate le regole di accesso** e gli account utente, cercando modifiche che non avete fatto voi.

## Il problema di fondo

Non è un caso isolato. Per gli SMA 1000 è la **terza catena di zero-day sfruttati da dicembre** (a gennaio 2026 era toccato a CVE-2025-23006), e negli ultimi due anni gli appliance di accesso remoto di praticamente tutti i grandi vendor — non solo SonicWall — sono finiti nel mirino.

Il motivo è logico, se ci si mette dalla parte dell'attaccante. Questi dispositivi:

- stanno **esposti su Internet** per definizione, perché servono a far entrare i dipendenti da fuori
- sono **il punto di ingresso** verso la rete interna e i servizi di identità aziendali
- spesso vengono **aggiornati con ritardo**, perché "se funziona non si tocca" e ogni update comporta una finestra di disservizio
- eseguono firmware complessi e chiusi, difficili da ispezionare per chi li usa

Il risultato è che un solo appliance bucato può significare sessioni VPN dirottate, configurazioni esfiltrate, policy di accesso modificate e credenziali in chiaro.

La lezione, per un piccolo reparto IT, non è "cambiate vendor": tutti hanno avuto il loro incidente. È piuttosto trattare l'appliance di bordo come il componente più critico che avete: aggiornamenti rapidi e prioritari, accesso alla console di gestione ristretto e mai esposto pubblicamente, monitoraggio dei log attivo e un piano già pronto per ruotare credenziali e sessioni quando (non se) arriverà il prossimo bollettino.
