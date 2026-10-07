---
title: "CVE-2026-90970: falla critica nel GitLab AI Gateway, RCE con CVSS 9.9 — aggiorna subito"
rilevanza: "ALTA"
fonte: "https://thehackernews.com/2026/10/gitlab-patches-critical-self-hosted-ai.html"
data_notizia: "2026-10-02"
tags: ["gitlab", "sicurezza", "CVE", "AI", "vulnerabilità", "RCE", "self-hosted"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: questa vulnerabilità è molto interessante perché colpisce l'AI Gateway, un componente relativamente nuovo che molte organizzazioni stanno adottando. L'angolo giusto è spiegare cos'è l'AI Gateway, perché la template injection è pericolosa, e chi è davvero a rischio (solo self-hosted). Utile aggiungere i comandi per verificare la versione e aggiornare.
---

# CVE-2026-90970: falla critica nel GitLab AI Gateway, RCE con CVSS 9.9 — aggiorna subito

Se nella tua organizzazione usate GitLab self-hosted con il componente **AI Gateway**, fermate tutto e leggete questo articolo. Il 2 ottobre 2026, GitLab ha pubblicato un advisory di sicurezza che descrive una vulnerabilità critica con un CVSS score di **9.9 su 10** — praticamente il massimo del pericolo.

## Cos'è l'AI Gateway di GitLab?

Prima di entrare nel dettaglio della falla, vale la pena spiegare cosa fa questo componente perché non tutti lo conoscono. L'**AI Gateway** è il servizio che fa da intermediario tra la tua istanza GitLab e i modelli AI — sia quelli di GitLab (Duo) sia, potenzialmente, modelli locali. Permette funzionalità come il completamento automatico del codice, la generazione di commit message, la revisione automatica delle merge request e, nelle versioni più recenti, l'esecuzione di agenti AI autonomi tramite la **Duo Agent Platform**.

È un componente abbastanza recente nell'ecosistema GitLab, introdotto per gestire la crescente integrazione con l'AI. E come spesso succede con i componenti nuovi, nasconde insidie non ancora ben collaudate.

## La vulnerabilità: template injection che diventa RCE

La CVE-2026-90970 è classificata come **CWE-1336**, ovvero un problema di **template injection**. In pratica, l'AI Gateway usa un sistema di template per configurare i "flow" degli agenti AI. Un utente autenticato con accesso alla Duo Agent Platform può creare una configurazione del flow appositamente manipolata per **uscire dalla sandbox del template engine** e far eseguire comandi arbitrari sul server che ospita il gateway.

Il risultato è **Remote Code Execution (RCE)**: l'attaccante ottiene la capacità di eseguire codice sul sistema con i privilegi del processo AI Gateway.

```
Tipo: Template Injection (CWE-1336)
CVSS: 9.9 (Critico)
Accesso richiesto: Autenticato (con accesso a Duo Agent Platform)
Impatto: RCE sul server AI Gateway
```

## Chi è davvero a rischio?

Qui c'è una distinzione importante che molti articoli inglesi non enfatizzano abbastanza. **Non tutti gli utenti GitLab sono a rischio**:

- **GitLab.com** (cloud): **non a rischio** — GitLab ha già patchato i propri gateway.
- **GitLab Dedicated**: **non a rischio** — gestito da GitLab, già aggiornato.
- **Self-managed con gateway ospitato da GitLab**: **non a rischio**.
- **Self-managed con AI Gateway self-hosted**: **A RISCHIO** — devi aggiornare.

Il secondo punto è cruciale: stai hostando tu stesso l'AI Gateway? Allora devi agire subito.

## Versioni affette e versioni sicure

Le versioni vulnerabili del gateway sono:
- Dalla 18.1.6 alla 19.2.3 (esclusa)
- 19.3 prima della 19.3.2
- 19.4 prima della 19.4.1

Le versioni che contengono la fix:
- **19.2.4** ✓
- **19.3.2** ✓
- **19.4.1** ✓

## Come verificare e aggiornare

Prima di tutto, verifica se stai usando l'AI Gateway self-hosted:

```bash
# Controlla se il servizio è attivo
systemctl status gitlab-ai-gateway 2>/dev/null || \
  docker ps | grep -i "ai-gateway" || \
  kubectl get pods -A | grep -i "ai-gateway"

# Se usi Docker Compose, verifica la versione dell'immagine
docker inspect gitlab-ai-gateway | grep -i '"Image"'
```

Per aggiornare con la procedura GitLab standard:

```bash
# Su installazioni Omnibus
sudo gitlab-ctl stop ai-gateway
sudo apt-get update && sudo apt-get install gitlab-ee
sudo gitlab-ctl reconfigure
sudo gitlab-ctl start

# Verifica la versione dopo l'aggiornamento
/opt/gitlab/embedded/bin/python3 -c "import ai_gateway; print(ai_gateway.__version__)"
```

## Perché questo bug merita attenzione oltre il patch

La CVE-2026-90970 è interessante da un punto di vista più ampio perché rappresenta un pattern che vedremo sempre più spesso: **la surface di attacco si espande con l'AI**. L'AI Gateway non esiste nella maggior parte delle istanze GitLab di tre anni fa. Oggi è un componente sempre più comune, e la sua architettura — template engine, esecuzione di "flow" semi-autonomi, connessioni a modelli esterni — crea nuovi vettori di attacco che i team di sicurezza devono imparare a gestire.

Se gestisci GitLab self-hosted e usi funzionalità AI, metti in agenda una review della superficie di attacco del tuo setup. Non basta applicare la patch: vale la pena capire esattamente quali componenti AI hai esposto e con quale livello di accesso.

Aggiorna, e poi siediti a fare quella review. Ne vale la pena.
