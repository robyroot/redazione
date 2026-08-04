---
title: "TeamCity On-Premises: vulnerabilità critica permette accesso remoto senza password (CVE-2026-63077)"
rilevanza: "ALTA"
fonte: "https://blog.jetbrains.com/teamcity/2026/07/cve-2026-63077/"
data_notizia: "2026-07-28"
tags: ["sicurezza", "vulnerabilità", "ci-cd", "devops", "rce", "jetbrains"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: urgenza aggiornamento per chi usa TeamCity on-premises
  nei propri homelab o ambienti aziendali. CVSS 9.8 è quasi il massimo possibile — questo
  è il tipo di CVE che va trattato come un incendio. Ottimo per sensibilizzare il pubblico
  italiano sulle pipeline CI/CD e la supply chain del software.
---

# TeamCity On-Premises: vulnerabilità critica permette accesso remoto senza password (CVE-2026-63077)

Se usi TeamCity On-Premises per le tue pipeline CI/CD, smetti di leggere e vai subito ad aggiornare. Sul serio. Questo è uno di quei casi in cui la patch non può aspettare.

JetBrains ha rilasciato un avviso di sicurezza urgente per una vulnerabilità critica che colpisce tutte le versioni di TeamCity On-Premises precedenti alla 2026.1.3 e alla 2025.11.7. Il codice di tracciamento è **CVE-2026-63077**, con un punteggio CVSS di **9.8 su 10**.

## Cos'è successo esattamente

Il problema sta nel protocollo di comunicazione usato tra il server TeamCity e i suoi agenti di build. Un attaccante con accesso HTTP o HTTPS al server può inviare una richiesta artigianale che bypassa completamente il sistema di autenticazione ed esegue comandi arbitrari con i privilegi del processo TeamCity.

Tradotto: **nessuna password, nessun token, nessun account necessario**. Basta avere accesso di rete al server.

La vulnerabilità è stata scoperta dal ricercatore Antoni Tremblay, che l'ha segnalata privatamente a JetBrains il 10 luglio 2026, permettendo all'azienda di sviluppare e distribuire una patch prima della divulgazione pubblica.

## Cosa rischi se non aggiorni

TeamCity è una piattaforma CI/CD usata da migliaia di team di sviluppo. Chiunque la usi on-premises (cioè installata sui propri server, non la versione cloud) è potenzialmente esposto. Un attaccante che sfrutta questa falla ottiene accesso al server con pieni privilegi, il che significa:

- Accesso a **credenziali e segreti** memorizzati nelle pipeline
- Possibilità di **modificare il codice** che viene compilato e distribuito
- Accesso a **artefatti di build** e configurazioni dei progetti
- In scenari peggiori, compromissione della **supply chain del software**

Questo ultimo punto è particolarmente preoccupante: un CI/CD compromesso può introdurre malware nel software che poi distribuisci ai tuoi utenti.

## Come verificare la versione che stai usando

Prima di tutto, controlla la versione di TeamCity installata. Puoi farlo dalla dashboard amministrativa oppure via riga di comando sul server:

```bash
# Se usi Docker
docker inspect teamcity-server | grep -i version

# Oppure controlla il file di build
cat /opt/TeamCity/BUILD_NUMBER
```

## Come risolvere

**Opzione 1 — Aggiorna TeamCity (consigliata)**

Le versioni sicure sono:
- `2026.1.3` (branch corrente)
- `2025.11.7` (branch LTS)

Scarica la nuova versione dal sito ufficiale JetBrains e segui la procedura standard di aggiornamento.

**Opzione 2 — Plugin di patch (se non puoi aggiornare subito)**

JetBrains ha rilasciato un plugin di sicurezza dedicato compatibile con TeamCity 2017.1 e versioni successive. Permette di applicare il fix senza aggiornare l'intera istanza — utile se hai dipendenze che rendono complicato un aggiornamento immediato.

```bash
# Verifica la versione dopo l'aggiornamento
curl -s http://localhost:8111/app/rest/server --user admin:password | grep version
```

**Opzione 3 — Misure temporanee**

Se proprio non puoi fare nessuna delle due cose, considera di isolare il server TeamCity dalla rete pubblica tramite firewall o VPN, limitando l'accesso solo agli IP autorizzati:

```bash
# Esempio con ufw
sudo ufw deny from any to any port 8111
sudo ufw allow from 10.0.0.0/24 to any port 8111
```

Questa non è una soluzione, ma un tampone emergenziale.

## Cosa dice JetBrains

JetBrains ha confermato che **TeamCity Cloud non è affetto** dalla vulnerabilità — il fix era già stato applicato preventivamente. Al momento della divulgazione pubblica, l'azienda non aveva evidenza di sfruttamento attivo, ma è solo questione di tempo: una volta che una vulnerabilità di questo tipo diventa pubblica, i tentativi di sfruttamento arrivano in poche ore.

## La lezione più grande

Le pipeline CI/CD sono diventate un bersaglio prioritario per gli attaccanti proprio perché controllano il codice che finisce in produzione. Non è la prima volta che TeamCity finisce nel mirino: nel 2024 ci furono diversi incidenti simili. Tenere aggiornato il proprio server CI/CD non è un optional, è parte integrante della sicurezza del software che produci.

Aggiorna. Adesso.
