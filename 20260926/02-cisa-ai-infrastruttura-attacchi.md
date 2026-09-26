---
title: "Il tuo stack AI self-hosted è finito nella lista delle vulnerabilità sfruttate della CISA"
rilevanza: "ALTA"
fonte: "https://thehackernews.com/2026/09/cisa-adds-seven-exploited-flaws-as.html"
data_notizia: "2026-09-02"
tags: ["sicurezza", "AI", "self-hosted", "CISA", "vulnerabilità", "LiteLLM", "Artifactory"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: chi usa stack AI self-hosted (Ollama, LiteLLM, stack open source) deve saperlo. L'angolo "anche le infrastrutture AI diventano bersagli" è fresco e rilevante per il pubblico tech del blog. Tre delle sette vulnerabilità nel KEV di settembre riguardano componenti AI — una prima volta nella storia del catalogo.
---

# Il tuo stack AI self-hosted è finito nella lista delle vulnerabilità sfruttate della CISA

Il 2 settembre 2026 la CISA (la cybersecurity agency americana) ha aggiunto sette nuove vulnerabilità al suo catalogo **KEV** (Known Exploited Vulnerabilities). Di queste sette, tre riguardano componenti tipicamente usati in infrastrutture AI — la prima volta in assoluto che quasi metà di un batch KEV colpisce l'AI stack.

Se stai usando strumenti come **LiteLLM**, **Kestra**, **JFrog Artifactory** o **Cisco Switchvox** nei tuoi progetti, questo articolo ti riguarda direttamente.

## Le vulnerabilità AI nel mirino

Le tre CVE che colpiscono l'infrastruttura AI sono:

**CVE-2026-59822 – LiteLLM** (CVSS 8.8)
LiteLLM è uno degli strumenti più usati come gateway e proxy per i modelli AI, specialmente in chi vuole usare più provider con una sola API. Il bug permette a un attaccante non autenticato di stabilire una sessione **Model Context Protocol** tramite un Bearer token arbitrario. In pratica: accesso completo all'API AI senza credenziali valide, con possibilità di fare harvesting delle API key di tutti i provider configurati.

**CVE-2026-82329 – JFrog Artifactory** (CVSS 9.8 – Critica)
Artifactory è molto usato come repository di artefatti, anche per modelli ML e pacchetti Python. Una misconfiguration di default permette a un attaccante non autenticato in rete di **ottenere privilegi amministrativi**. In un contesto AI/ML, questo significa accesso a tutti i modelli, dataset e build pipeline.

**CVE-2026-9586 – Kestra** (CVSS alto)
Kestra è una piattaforma di workflow orchestration popolare nei pipeline AI/ML. La vulnerabilità permette l'esecuzione di comandi remoti non autenticata.

## Come vengono sfruttate in pratica

I gruppi di attacco collegati al ransomware **Qilin** (anche noto come Agenda) stanno concatenando queste vulnerabilità per:

1. Entrare attraverso LiteLLM o Artifactory senza autenticazione
2. Stabilire **reverse shell** per persistenza
3. **Rubare API key** di OpenAI, Anthropic, o altri provider configurati
4. Installare **crypto miner** sulle GPU disponibili
5. Enumerare utenti, gruppi e topologie di accesso federato

Il crypto mining sulle GPU è particolarmente redditizio: una singola macchina con più GPU A100 può generare migliaia di dollari al mese in criptovalute se sfruttata.

## Come proteggersi

Prima di tutto, verifica le versioni in uso:

```bash
# Controlla la versione di LiteLLM
pip show litellm | grep Version

# LiteLLM: aggiorna alla versione >= 1.84.0
pip install --upgrade litellm
```

Per JFrog Artifactory, il problema sta nella configurazione di default. Verifica:

```bash
# Controlla se il tuo Artifactory ha l'autenticazione anonima disabilitata
curl -s http://localhost:8081/artifactory/api/system/security/settings | python3 -m json.tool
```

Se vedi `"anonAccessEnabled": true` nella risposta, stai esponendo Artifactory senza autenticazione.

Per Kestra, aggiorna alla versione più recente e assicurati che la porta di management non sia esposta su Internet.

## Il quadro più grande: l'AI stack diventa superficie d'attacco

Fino a poco fa, i componenti AI self-hosted erano visti come "solo strumenti interni" — nessuno li esponeva intenzionalmente su Internet, e i bug di sicurezza erano considerati secondari rispetto alle funzionalità.

Quella fase è finita.

Man mano che l'AI si integra nei flussi di lavoro aziendali e i team DevOps espongono questi servizi per consentire l'accesso da remoto o in cloud ibrido, la superficie d'attacco cresce. E gli attaccanti lo sanno: un server con GPU, API key di provider AI e accesso ai modelli interni vale molto di più di un semplice web server.

La lezione è semplice: **tratta il tuo stack AI con la stessa attenzione alla sicurezza che daresti a un database di produzione**. Firewall, autenticazione, aggiornamenti regolari. Non è paranoia — è igiene di base.

## Riferimenti utili

- [Catalogo KEV della CISA](https://www.cisa.gov/known-exploited-vulnerabilities-catalog) — tienilo d'occhio
- Versioni corrette: LiteLLM ≥ 1.84.0, Kestra ultima stabile, Artifactory con patch di settembre 2026
