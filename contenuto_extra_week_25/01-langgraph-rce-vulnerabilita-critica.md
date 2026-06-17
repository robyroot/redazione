---
title: "LangGraph sotto attacco: la catena di bug critici che mette a rischio i tuoi server AI"
rilevanza: "ALTA"
fonte: "https://cybersecuritynews.com/vulnerability-chain-in-langgraph/"
data_notizia: "2026-06-10"
tags: ["cybersecurity", "LangGraph", "vulnerabilità", "RCE", "AI"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: molti sviluppatori italiani usano LangGraph per agenti AI in produzione. Focalizzarsi sul "come mettersi al sicuro subito" con comandi pratici di aggiornamento e verifica della versione installata.
---

## Cos'è LangGraph e perché dovresti preoccuparti

Se stai costruendo agenti AI, probabilmente hai sentito parlare di LangGraph. È il framework open source di LangChain per costruire applicazioni stateful e multi-agente — una di quelle librerie che si è diffusa così rapidamente che quasi nessuno si è fermato a chiedersi quanto fosse sicura. Beh, qualcuno l'ha fatto, e i risultati non sono belli.

Una ricerca di sicurezza pubblicata nelle ultime settimane ha scoperto una catena di vulnerabilità critiche in LangGraph che, se sfruttate in combinazione, permettono a un attaccante di prendere il controllo completo di un server che esegue questa libreria. Stiamo parlando di Remote Code Execution (RCE): il peggio del peggio in ambito sicurezza.

## La catena letale: tre CVE, un disastro

I ricercatori hanno identificato tre vulnerabilità che, prese singolarmente, sarebbero già gravi. Messe insieme, sono devastanti:

- **CVE-2025-67644**: Iniezione SQL nel componente checkpointer che usa SQLite. Un input non sanitizzato finisce direttamente nella query.
- **CVE-2026-28277**: Esecuzione di codice remoto tramite deserializzazione di msgpack. Quando LangGraph carica checkpoint salvati, si fida ciecamente dei dati ricevuti.
- **CVE-2026-27022**: Iniezione Redis nel backend alternativo del checkpointer.

Il flusso dell'attacco è classico: prima si inietta nel database tramite la prima CVE, poi si sfrutta la deserializzazione insicura per eseguire codice arbitrario sul server. Il risultato finale è il controllo completo della macchina.

## Chi è a rischio

La cosa preoccupante è la scala. LangGraph conta oltre **46,5 milioni di download mensili** e viene usato in migliaia di ambienti di produzione: sistemi di customer support automatizzati, pipeline di automazione aziendale, assistenti interni. Se il tuo deployment usa il checkpointer SQLite o Redis con input proveniente dagli utenti — e la maggior parte lo fa — sei potenzialmente vulnerabile.

La buona notizia: l'attacco richiede che il server accetti input utente non validato nei componenti checkpointer. Le installazioni cloud gestite (LangGraph Cloud) non sono direttamente esposte. Il problema riguarda i **deployment self-hosted**.

## Come verificare e proteggersi subito

Prima cosa: controlla la versione di LangGraph che stai usando.

```bash
pip show langgraph
```

Poi aggiorna immediatamente alle versioni che includono le patch:

```bash
pip install --upgrade langgraph langchain-core
```

Verifica anche le dipendenze transitive con pip-audit:

```bash
pip install pip-audit
pip-audit
```

Se non puoi aggiornare subito, come misura temporanea puoi limitare l'accesso ai componenti checkpointer validando rigorosamente tutti gli input prima che raggiungano LangGraph. Non è una soluzione definitiva, ma riduce la superficie d'attacco nell'immediato.

Vale anche la pena controllare i log per accessi anomali al checkpointer:

```bash
# Cerca pattern di SQL injection nei log della tua applicazione
grep -i "union select\|'; --\|drop table" /var/log/tua-app/app.log
```

## Il problema più grande: la sicurezza nell'era degli agenti AI

Questa storia è un campanello d'allarme per l'intero ecosistema degli agenti AI. Stiamo costruendo sistemi sempre più complessi che orchestrano decine di modelli, strumenti e API — spesso dando loro accesso a database, file system e servizi esterni. Ma la sicurezza di questi framework viene troppo spesso trattata come un afterthought.

LangGraph non è un caso isolato. Le vulnerabilità trovate (SQL injection, deserializzazione insicura) sono tra le più vecchie e conosciute in assoluto — eppure continuano a comparire in librerie moderne usate in produzione da aziende serie. Questo dovrebbe farci riflettere su come valutiamo e scegliamo i componenti per i nostri stack AI.

La regola è semplice: **qualsiasi framework AI che tocca dati utente deve essere trattato come codice che gira in un ambiente ostile**. Input validation, sandboxing, aggiornamenti regolari, audit periodici. Non è opzionale.

Aggiorna LangGraph oggi. Non aspettare il prossimo incidente di sicurezza per farlo.
