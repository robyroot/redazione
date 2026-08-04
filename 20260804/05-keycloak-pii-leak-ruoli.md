---
title: "Keycloak: un bug di controllo accessi espone i dati personali degli utenti tramite i ruoli (CVE-2026-17059)"
rilevanza: "ALTA"
fonte: "https://cyberpress.org/keycloak-user-pii-oidc-client-metadata/"
data_notizia: "2026-07-28"
tags: ["sicurezza", "keycloak", "privacy", "iam", "sso", "open-source", "vulnerabilità"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: doppio impatto — sicurezza E privacy. Keycloak è
  usatissimo nel mondo open source e negli homelab come soluzione SSO alternativa a
  soluzioni proprietarie. Il fatto che un admin "limitato" possa vedere dati di tutti
  gli utenti è esattamente il tipo di bug silenzioso e devastante che colpisce le
  organizzazioni più attente alla privacy. Ottimo per il pubblico che usa self-hosting.
---

# Keycloak: un bug di controllo accessi espone i dati personali degli utenti tramite i ruoli (CVE-2026-17059)

Keycloak è probabilmente la soluzione open source per la gestione delle identità più usata al mondo. Homelab, startup, università, PA — chiunque voglia un sistema SSO (Single Sign-On) senza dipendere da servizi cloud proprietari finisce quasi sempre qui. Ed è per questo che la vulnerabilità appena corretta merita tutta la tua attenzione.

Il 28 luglio 2026, il team di Keycloak ha rilasciato la versione **26.7.0** con una patch silenziosa per **CVE-2026-17059**: un bug di broken access control che permetteva a un amministratore con privilegi limitati di raccogliere i dati personali (PII) di **tutti gli utenti del realm**, compresi quelli a cui non avrebbe mai dovuto avere accesso.

## Come funziona il bug

Keycloak permette di creare account amministrativi con permessi granulari: puoi dare a qualcuno la possibilità di gestire solo certi realm, certi gruppi, o certi client, senza dargli accesso ai dati di tutti gli utenti.

Il problema è in come Keycloak gestisce la ricerca degli utenti tramite i ruoli. Invece di passare per la directory principale degli utenti (che rispetta i permessi), un admin limitato poteva interrogare l'endpoint di appartenenza a un ruolo e ottenere la lista completa degli utenti che lo possiedono — con nome, email, e tutti i dati del profilo.

In pratica: se configuri un ruolo `users` che tutti gli utenti hanno, un admin con permessi minimi può semplicemente fare una query su quel ruolo e ottenere i dati di tutto il tuo database utenti.

```bash
# Esempio di query che sfruttava la vulnerabilità (endpoint role-members)
GET /admin/realms/{realm}/roles/{role-name}/users

# Restituiva: lista completa di utenti con email, nome, attributi — 
# anche se l'admin non aveva permessi di lettura utenti generali
```

## Chi è affetto

La vulnerabilità riguarda Keycloak nelle versioni precedenti alla **26.7.0**. Se stai usando una versione self-hosted, controlla subito cosa hai installato:

```bash
# Docker: controlla l'immagine
docker inspect keycloak | grep -i image

# JAR: controlla la versione
ls /opt/keycloak/lib/quarkus/ | grep keycloak-quarkus-server
```

Se la versione è inferiore a 26.7.0, devi aggiornare.

## L'impatto reale sulla privacy

Questo bug è particolarmente insidioso per due motivi.

Primo, **è silenzioso**. Un admin malintenzionato o compromesso può raccogliere tutti i dati degli utenti senza trigger allarmi, perché sta usando endpoint legittimi — solo con un percorso di accesso che non dovrebbe essere consentito.

Secondo, **Keycloak è spesso il custode di dati sensibili**. Nelle organizzazioni che usano SSO, Keycloak contiene email, numeri di telefono, attributi personalizzati — potenzialmente anche informazioni mediche, aziendali, o finanziarie se l'attributo mapping è configurato per includerle.

Dal punto di vista del GDPR, un'organizzazione che subisce questa tipologia di accesso non autorizzato potrebbe trovarsi obbligata a notificare una violazione dei dati — anche se tecnicamente l'accesso è avvenuto tramite funzionalità legittime.

## Come aggiornare Keycloak

**Con Docker (il modo più comune in homelab):**

```bash
# Ferma il container corrente
docker stop keycloak

# Aggiorna l'immagine
docker pull quay.io/keycloak/keycloak:26.7.0

# Riavvia con la nuova immagine
docker run -d --name keycloak \
  -e KEYCLOAK_ADMIN=admin \
  -e KEYCLOAK_ADMIN_PASSWORD=yourpassword \
  -p 8080:8080 \
  quay.io/keycloak/keycloak:26.7.0 start-dev
```

**Con docker-compose:**

```yaml
# docker-compose.yml — aggiorna il tag immagine
services:
  keycloak:
    image: quay.io/keycloak/keycloak:26.7.0
    # resto della configurazione invariato
```

```bash
docker compose pull && docker compose up -d
```

## Cosa fare oltre all'aggiornamento

L'aggiornamento risolve il bug, ma è anche un buon momento per fare un audit degli account amministrativi nel tuo realm:

1. **Vai su Admin Console → Realm Settings → Users**
2. **Verifica chi ha ruoli `realm-management`** — questi sono gli admin con potenziale accesso più ampio
3. **Applica il principio del minimo privilegio**: assegna solo i ruoli `manage-*` specifici per le funzioni necessarie, non `realm-admin` a tutti

```bash
# Via CLI, elenca gli admin del realm
/opt/keycloak/bin/kcadm.sh get-roles --rolename realm-admin \
  --rname realm-management --cclientid realm-management -r yourrealm
```

## Perché vale la pena tenere Keycloak aggiornato

Keycloak rilascia aggiornamenti frequenti e non tutti portano patch di sicurezza così critiche, ma il progetto è attivo e il team risponde velocemente alle segnalazioni. La versione 26.7.0 include anche migliorie di performance per ambienti con molti utenti e fix per alcuni problemi con i provider LDAP.

Se gestisci un'istanza Keycloak, considera di iscriverti alle release notes via GitHub o al blog ufficiale per ricevere notifiche tempestive sui futuri aggiornamenti.
