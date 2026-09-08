---
title: "Cyber Resilience Act: dall'11 settembre scattano gli obblighi UE di segnalazione vulnerabilità"
rilevanza: "ALTA"
fonte: "https://www.insideprivacy.com/european-union-2/what-to-watch-in-2026-key-eu-privacy-cybersecurity-developments/"
data_notizia: "2026-09-07"
tags: ["privacy", "cybersecurity", "EU", "normativa", "cyber-resilience-act", "vulnerabilità"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato per RobyRoot: articolo "cosa cambia per noi" — spiegare il CRA in modo semplice
  al pubblico tech italiano. Rilevante sia per chi sviluppa software (anche open source!) sia per
  chi usa prodotti digitali in azienda. L'angolo open source è particolarmente interessante perché
  il CRA ha creato dibattito nella community Linux/FOSS riguardo agli obblighi per i maintainer.
---

# Cyber Resilience Act: dall'11 settembre scattano gli obblighi UE di segnalazione vulnerabilità

Dal **11 settembre 2026**, il **Cyber Resilience Act (CRA)** dell'Unione Europea inizia ad applicarsi
nella sua prima fase. Se sviluppate software, gestite prodotti digitali o vi interessa la sicurezza
informatica in ambito europeo, questo è il momento di capire cosa cambia — e cosa dovrete fare.

## Cos'è il Cyber Resilience Act

Il CRA è il primo regolamento europeo che impone **requisiti di sicurezza obbligatori per i prodotti
con elementi digitali** — in pratica, quasi tutto ciò che si connette a internet o a una rete. Router,
smartphone, software applicativo, dispositivi IoT, sistemi industriali: se ha un'interfaccia digitale
e viene venduto nell'UE, il CRA lo riguarda.

L'obiettivo è semplice: far sì che i produttori smettano di rilasciare prodotti insicuri "by default"
e assumano responsabilità concreta quando vengono scoperte vulnerabilità.

## Cosa scatta dall'11 settembre 2026

La prima fase del CRA riguarda gli **obblighi di segnalazione**:

- **Vulnerabilità attivamente sfruttate** devono essere notificate all'ENISA (Agenzia UE per la
  Cybersecurity) entro **24 ore** dalla scoperta
- **Incidenti di sicurezza gravi** che impattano la sicurezza del prodotto devono essere segnalati
  entro **72 ore**
- Notifica iniziale agli utenti colpiti deve avvenire **senza ritardi ingiustificati**

```
Timeline CRA:
- 11 settembre 2026: obblighi di segnalazione vulnerabilità e incidenti
- Dicembre 2027:     requisiti completi di sicurezza del prodotto
```

La fase completa — che include requisiti tecnici come security by design, aggiornamenti obbligatori,
documentazione di sicurezza e supporto per tutta la vita utile del prodotto — entrerà in vigore
nel **dicembre 2027**.

## Chi è obbligato: anche l'open source?

Questa è la domanda che ha animato mesi di discussioni nella community FOSS. La risposta breve:
**il CRA si applica principalmente ai produttori commerciali**, non ai maintainer di progetti
open source sviluppati su base volontaria e non per scopo commerciale.

Tuttavia, se un'azienda include software open source in un prodotto commerciale, quella azienda
diventa responsabile della conformità al CRA per l'intero prodotto — incluse le componenti
open source che utilizza. Questo ha spinto molte organizzazioni (come la Linux Foundation e la
OpenSSF) a sviluppare framework di sicurezza per aiutare i maintainer a documentare meglio la
sicurezza dei propri progetti.

```bash
# Esempio: strumenti per la sicurezza della supply chain open source
# OpenSSF Scorecard — verifica la sicurezza di un progetto GitHub
docker run -e GITHUB_AUTH_TOKEN=... gcr.io/openssf/scorecard:stable \
  --repo=github.com/torvalds/linux

# SBOM (Software Bill of Materials) con syft
syft packages dir:./mio-progetto -o spdx-json > sbom.json
```

## Cosa significa per gli sviluppatori italiani

Se sviluppate software che viene venduto (o distribuito a pagamento) nell'UE, dal settembre 2026:

1. **Dovete monitorare attivamente** le vulnerabilità nei componenti che usate
2. **Dovete segnalare** le vulnerabilità critiche entro 24 ore dalla scoperta
3. **Dovete comunicare** agli utenti le falle che li riguardano

Per ora, nella fase 2026, la priorità è la **segnalazione** — non ancora i requisiti tecnici completi.

## Il contesto più ampio: AI Act e CRA insieme

Il CRA non arriva da solo. Dal **2 agosto 2026**, si applicano anche gli obblighi di trasparenza
dell'**EU AI Act**, che impone requisiti di trasparenza per i sistemi AI a rischio limitato (come
i chatbot) e divieti per quelli ad alto rischio. Chi sviluppa prodotti che combinano AI e
connettività di rete si trova a dover gestire due regolamenti contemporaneamente.

Non è semplice, ma è la direzione che l'Europa ha scelto: più responsabilità per chi produce
tecnologia, più protezione per chi la usa.

## Come prepararsi (se non l'avete già fatto)

- **Inventariateli**: sapete quali componenti software usano i vostri prodotti? Un SBOM è il primo passo
- **Monitorate le CVE**: sistemi come MITRE CVE, OSV.dev o GitHub Security Advisories possono aiutare
- **Stabilite un processo di disclosure**: chi nel vostro team riceve le segnalazioni di vulnerabilità?
- **Informate gli utenti**: avete un canale dedicato per le notifiche di sicurezza?

```bash
# Monitora le vulnerabilità nelle dipendenze con strumenti open source
# Per progetti Python
pip-audit

# Per progetti Node.js
npm audit

# Per progetti Rust
cargo audit
```

## Conclusione

L'11 settembre 2026 non è una scadenza apocalittica, ma è un segnale concreto che le regole del
gioco stanno cambiando. L'Europa vuole prodotti digitali più sicuri, e lo sta imponendo per legge.
Per gli sviluppatori FOSS italiani il rischio diretto è limitato — ma conviene capire il quadro
normativo, soprattutto se il vostro codice finisce in prodotti commerciali. La community open source
ha già reagito con strumenti e pratiche che aiutano: usateli.
