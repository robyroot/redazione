---
title: "Cisco Firewall Management Center: una password fissa scritta nel codice apre le porte agli hacker"
rilevanza: "ALTA"
fonte: "https://securityaffairs.com/196289/security/u-s-cisa-adds-a-cisco-secure-firewall-management-center-fmc-flaw-to-its-known-exploited-vulnerabilities-catalog.html"
data_notizia: "2026-08-05"
tags: ["cybersecurity", "cisco", "firewall", "vulnerabilità", "reti-aziendali"]
livello: "intermediate"
nota_editoriale: |
  Storia perfetta per spiegare il concetto di "credenziali hardcoded" a un pubblico non solo tecnico: è un errore di progettazione tanto banale quanto pericoloso, e qui riguarda il cervello che gestisce i firewall aziendali. Buon gancio anche per parlare di "security impact rating" vs CVSS basso (5.3) che sottostima il rischio reale — utile per chi si chiede perché i punteggi CVSS a volte ingannano. Consigliato tono didattico più che allarmistico: il target di questo bug è l'IT aziendale, non l'utente domestico, ma vale la pena spiegare perché conta comunque per tutti (il firewall protegge anche i dati dei clienti).
---

C'è una categoria di vulnerabilità che fa sempre un po' più rabbia delle altre: quelle causate non da un bug complesso sfuggito a mesi di test, ma da una scelta di design decisamente ingenua. È il caso di CVE-2026-20316, la falla scoperta a fine luglio in Cisco Secure Firewall Management Center (FMC), il software che le aziende usano per configurare, monitorare e gestire in modo centralizzato i propri firewall Cisco. Il problema? Un account con password fissa, identica su ogni installazione, scritta direttamente nel software.

**Cos'è successo davvero**

FMC è il "cervello" da cui gli amministratori di rete controllano le regole di sicurezza di tutti i firewall aziendali: chi può parlare con chi, quali porte sono aperte, quali connessioni vengono bloccate. È il classico strumento che, se compromesso, non ti dice solo "qualcosa è andato storto", ma può dire agli attaccanti esattamente dove sono i punti deboli della tua rete.

Il bug in questione riguarda un account a basso privilegio con credenziali hardcoded, cioè scritte fisse nel codice e identiche su ogni installazione del software in tutto il mondo. Un attaccante che riesce a raggiungere l'interfaccia di gestione di un FMC esposto non deve rubare né indovinare nulla: gli basta usare quella password, sempre la stessa, per entrare. Da lì può leggere dati di configurazione sensibili, politiche di sicurezza e log degli eventi, informazioni che raccontano nel dettaglio come è strutturata la difesa della rete.

Cisco ha assegnato alla falla un punteggio CVSS di 5,3, tutto sommato moderato sulla carta, ma l'ha comunque classificata con un "Security Impact Rating" alto. Il motivo è semplice: da sola questa vulnerabilità dà solo un accesso limitato, ma può diventare il primo tassello di un attacco più ampio, combinata con altri bug per scalare i privilegi fino al controllo completo del sistema. Un po' come lasciare aperta una porta secondaria di casa: magari non è quella del salotto, ma è comunque una porta che non dovrebbe esistere.

**Già sfruttata attivamente**

Non si tratta di un rischio teorico: la CISA ha aggiunto CVE-2026-20316 al suo catalogo delle vulnerabilità note come sfruttate (KEV Catalog) il 29 luglio, confermando che gli attacchi sono già in corso nel mondo reale. Cisco ha pubblicato anche indicatori di compromissione per chi vuole verificare se il proprio sistema è già stato toccato: in modalità expert, un comando come `cat /var/log/messages | grep license` che restituisce riferimenti al file `/var/tmp/license.tmp` può essere un segnale che qualcuno è passato di lì.

**Cosa fare se gestisci un FMC**

L'unica soluzione reale è aggiornare: Cisco ha rilasciato le hotfix per le versioni interessate e non esistono workaround temporanei affidabili, quindi rimandare la patch significa restare esposti. Se sei un amministratore di rete o lavori per un'azienda che si appoggia a un partner Cisco per la gestione della sicurezza, questo è il momento di controllare la versione in uso e, se necessario, sollecitare l'aggiornamento immediato.

**Perché conta anche se non tocchi mai un firewall Cisco**

Anche chi non ha nulla a che fare con l'amministrazione di rete dovrebbe conoscere questa storia, perché è un esempio da manuale di due problemi che si ripetono in continuazione nel mondo della sicurezza informatica. Primo: le credenziali fisse, identiche su ogni installazione, sono un errore di progettazione che dovrebbe essere sparito decenni fa, eppure continua a comparire anche in prodotti enterprise di fascia alta usati da banche, ospedali e pubbliche amministrazioni. Secondo: un punteggio CVSS basso non significa automaticamente "rischio basso". Vale sempre la pena guardare anche la valutazione di impatto del vendor e il contesto in cui un bug può essere usato, non fermarsi al primo numero che si legge in un titolo.
