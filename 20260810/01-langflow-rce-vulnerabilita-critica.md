---
title: "Langflow sotto attacco: falla critica permette di prendere il controllo completo dei server AI"
rilevanza: "ALTA"
fonte: "https://thehackernews.com/2026/08/cisa-flags-langflow-rce-tomcat-and-n.html"
data_notizia: "2026-08-10"
tags: ["cybersecurity", "AI", "vulnerabilita", "langflow", "open-source"]
livello: "intermediate"
nota_editoriale: |
  Ottimo angolo per RobyRoot: è la dimostrazione pratica di quanto siano fragili
  i tool AI "low-code" che negli ultimi mesi stanno spuntando ovunque nei
  laboratori casalinghi e nelle piccole aziende. Consiglio di collegarla a un
  taglio "self-hosting responsabile": chi installa Langflow o strumenti simili
  in homelab deve trattarli come infrastruttura critica, non come un giocattolo.
  Buona occasione anche per ricordare la regola d'oro "mai esporre pannelli di
  amministrazione direttamente su internet senza autenticazione forte".
---

Se negli ultimi mesi avete giocato con Langflow, il tool open source per costruire flussi di lavoro AI trascinando blocchetti invece di scrivere codice, questa è una notizia da leggere con attenzione. È stata scoperta e sfruttata attivamente una falla critica che permette a chiunque, senza nemmeno un account, di prendere il controllo totale del server su cui gira.

Langflow è uno strumento molto amato da chi sperimenta con agenti AI e applicazioni RAG (quelle che combinano un modello linguistico con una base di conoscenza personalizzata): interfaccia grafica, drag-and-drop, zero righe di codice per mettere insieme pipeline anche complesse. Dal 2025 è di proprietà di IBM, che lo ha acquisito insieme a DataStax per rafforzare la sua piattaforma watsonx. Insomma, non parliamo di un progettino di nicchia, ma di uno strumento usato da sviluppatori, aziende e appassionati in tutto il mondo.

**Cosa è successo, in pratica**

La vulnerabilità, catalogata come CVE-2026-9198, ha un punteggio di gravità 9,8 su 10: praticamente il massimo. Il problema nasce dalla combinazione di due difetti che, presi singolarmente, sarebbero già gravi, ma insieme diventano devastanti.

Il primo riguarda l'endpoint `/api/v1/auto_login`, pensato originariamente per semplificare l'accesso in scenari di test: nella pratica, permette a qualunque client sulla rete di ottenere un token da "superutente" senza fornire alcuna credenziale. Il secondo è l'endpoint `/api/v1/validate/code`, che serve a Langflow per validare pezzi di codice Python inseriti nei blocchi del flusso — peccato che lo faccia eseguendo quel codice con la funzione `exec()`, senza alcun sandboxing.

Mettendo insieme i due pezzi, un attaccante ottiene prima un token da amministratore gratis, poi lo usa per far eseguire al server qualsiasi comando Python voglia. Il risultato è un'esecuzione di codice da remoto completa, ottenuta da un utente anonimo su qualunque installazione esposta in rete con le impostazioni di default.

**Non è teoria: è già sotto attacco**

IBM ha reso pubblica la falla il 17 luglio 2026, rilasciando la patch lo stesso giorno — un tempo di risposta lodevole. Il problema è che moltissime installazioni non sono state aggiornate in tempo, e infatti CISA (l'agenzia americana per la cybersicurezza) ha aggiunto la CVE-2026-9198 al catalogo delle vulnerabilità sfruttate attivamente (Known Exploited Vulnerabilities) il 4 agosto 2026, segno che gli attacchi in corso non sono un'ipotesi ma un fatto documentato.

Diversi ricercatori hanno già pubblicato proof-of-concept funzionanti, il che significa che sfruttare la falla non richiede competenze particolarmente avanzate: bastano pochi minuti e uno scanner che individui i server Langflow esposti pubblicamente, cosa banale con strumenti come Shodan.

**Cosa fare se usate Langflow**

Se avete un'istanza Langflow, in homelab o in produzione, la prima cosa da controllare è la versione: tutte quelle comprese tra 1.0.0 e 1.10.0 sono vulnerabili. Aggiornate immediatamente a una versione successiva alla 1.10.0, disponibile tramite pip o Docker a seconda di come l'avete installata.

Ma la patch da sola non basta a insegnarci la lezione più importante di questa vicenda: **Langflow, come moltissimi tool AI nati per la sperimentazione rapida, non è stato progettato pensando a un'esposizione diretta su internet**. Se lo state usando in un homelab, tenetelo dietro una VPN (Tailscale o WireGuard vanno benissimo) o quantomeno dietro un reverse proxy con autenticazione a più fattori. Non fidatevi mai delle impostazioni predefinite di uno strumento pensato per "iniziare in fretta": spesso quella fretta si traduce in scorciatoie di sicurezza che qualcuno, prima o poi, trova e sfrutta.

Vale la pena ricordare che Langflow non è un caso isolato: nello stesso bollettino CISA di agosto compaiono anche falle attivamente sfruttate in Apache Tomcat e nella piattaforma di monitoraggio N-able N-central. Il filo conduttore è sempre lo stesso: strumenti potenti, spesso installati in fretta, esposti più del necessario. Con la proliferazione di tool AI self-hosted, questo tipo di errore diventerà sempre più comune — meglio abituarsi fin da subito a trattarli come si tratterebbe qualsiasi altro servizio critico esposto in rete.
