---
title: "Langflow e LangGraph sotto attacco: come proteggere le tue pipeline AI"
stato: "BOZZA"
fonte: "https://cybersecuritynews.com/microsoft-patch-tuesday-june-2026/"
tags: ["sicurezza", "ai", "langflow", "langgraph", "cybersecurity"]
livello: "intermediate"
---

Se costruisci applicazioni AI con **Langflow** o **LangGraph**, fermati un secondo. Questa settimana sono emerse vulnerabilità critiche in entrambi i framework — e una è già sfruttata attivamente.

Le piattaforme low-code per AI stanno diventando un bersaglio prioritario: velocità di adozione alta, attenzione alla sicurezza bassa. La combinazione perfetta per chi cerca falle.

## Cosa è successo

### Langflow: RCE attivamente sfruttata (10 giugno 2026)

Una vulnerabilità di Remote Code Execution in Langflow è stata divulgata e sfruttata attivamente nello stesso giorno. Il bug permette a un attaccante non autenticato di eseguire comandi arbitrari sul server.

Il vettore d'attacco: l'API di Langflow accetta payload JSON che, in certe configurazioni, passano attraverso un parser non sicuro. Se hai un'istanza esposta su internet senza autenticazione, sei a rischio adesso.

### LangGraph: catena di 3 CVE (12 giugno 2026)

Tre vulnerabilità in LangGraph pubblicate insieme. La catena permette di bypassare il sistema di autorizzazione, iniettare dati nello stato del grafo, e ottenere esecuzione di codice. Separatamente media severità, concatenate diventano critiche.

## Sei a rischio?

**Langflow:**
- Hai un'istanza accessibile da internet?
- Versione precedente a 1.4.2?
- Senza autenticazione davanti?

Se sì a tutte e tre: aggiorna immediatamente.

## Come proteggersi

### Aggiornamento

```bash
pip install langflow --upgrade
pip install langgraph --upgrade

# Verifica le versioni
pip show langflow | grep Version
pip show langgraph | grep Version
```

### Non esporre Langflow a internet senza protezione

Metti almeno autenticazione HTTP davanti all'interfaccia:

```nginx
location / {
    auth_basic "Restricted";
    auth_basic_user_file /etc/nginx/.htpasswd;
    proxy_pass http://localhost:7860;
}
```

Oppure usa una VPN e non esporre su internet direttamente.

### Principio del minimo privilegio

Il processo non dovrebbe girare come root:

```bash
useradd -r -s /bin/false langflow-svc
# Esegui il servizio come questo utente
```

## Il problema più grande

Langflow e LangGraph permettono di costruire pipeline AI in modo rapido. È il loro punto di forza — ed è anche il punto debole: molta potenza, poca visibilità su cosa gira sotto.

Se li usi in produzione:
- Tienili sempre aggiornati (segui le release su GitHub)
- Mai interfacce admin su internet senza autenticazione
- Isola il processo in un container con risorse limitate
- Monitora i log per richieste anomale

L'AI development è una superficie d'attacco nuova e in rapida espansione. Meglio iniziare a trattarla come tale.
