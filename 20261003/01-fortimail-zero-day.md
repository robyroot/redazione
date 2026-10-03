---
title: "FortiMail sotto attacco: zero-day CVSS 9.8 sfruttato in the wild — aggiorna subito"
rilevanza: "ALTA"
fonte: "https://thehackernews.com/2026/10/critical-fortimail-zero-day-flaw.html"
data_notizia: "2026-10-02"
tags: ["cybersecurity", "fortinet", "zero-day", "vulnerabilità", "sysadmin"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: focus pratico su chi è esposto, come verificare se si è stati compromessi e i comandi concreti di mitigazione. Tono allarmistico il giusto — è una vulny CVSS 9.8 sfruttata live — ma senza fare FUD.
---

# FortiMail sotto attacco: zero-day CVSS 9.8 sfruttato in the wild — aggiorna subito

Se nella tua infrastruttura c'è un appliance **FortiMail di Fortinet**, fermati qui. Una vulnerabilità critica con punteggio CVSS **9.8 su 10** è attivamente sfruttata in campagne reali. CISA l'ha inserita nel catalogo delle vulnerabilità note sfruttate (KEV) e ha dato alle agenzie federali USA **tre giorni** per mettere in sicurezza i sistemi.

## Cos'è successo

Il 2 ottobre 2026 Fortinet ha pubblicato un bollettino urgente su **CVE-2026-104286**, una falla di tipo *path traversal* combinata con un'errata gestione del carattere NULL nelle versioni di FortiMail. L'impatto è devastante: un attaccante non autenticato può inviare una richiesta HTTP/HTTPS appositamente costruita e **scrivere file arbitrari** sul filesystem sottostante. Scrivere nel posto giusto equivale a esecuzione remota di codice — senza password, senza token, senza nient'altro.

Non è una PoC teorica: Fortinet stesso ha confermato lo sfruttamento attivo in the wild. The Hacker News e SecurityWeek riportano che i team di incident response stanno già gestendo compromissioni attive.

## Versioni colpite

| Branch | Versioni vulnerabili |
|--------|----------------------|
| 8.0.x  | 8.0.0 – 8.0.1 |
| 7.6.x  | 7.6.0 – 7.6.6 |
| 7.4.x  | 7.4.0 – 7.4.8 |
| 7.2.x  | 7.2.0 – 7.2.9 |

Se la tua versione non è in questa lista, stai (probabilmente) bene. Se ci sei, devi agire **adesso**.

## Come verificare se sei già compromesso

Fortinet ha rilasciato indicatori di compromissione (IoC): hash di file sospetti, indirizzi IP degli attaccanti e tracce nei log da cercare. Controlla i log di accesso HTTP/HTTPS su FortiMail:

```bash
# Accedi alla CLI di FortiMail
diagnose log filter enable
diagnose log filter field msg "NULL"
diagnose log display
```

Cerca richieste anomale con path che contengono sequenze `../` o caratteri `%00`. Se le trovi, considera il sistema compromesso e isola l'appliance dalla rete immediatamente.

## Workaround immediato (se non puoi patchare subito)

La patch definitiva è in arrivo, ma Fortinet ha già distribuito un **workaround** tramite la console di amministrazione:

```bash
# Via CLI FortiMail — disabilita l'accesso HTTP non autenticato alle API sensibili
config system global
    set admin-https-redirect enable
    set admin-http disable
end
```

In alternativa, blocca l'accesso alle porte 80/443 del pannello di gestione FortiMail da qualsiasi IP non autorizzato con un firewall a monte. Non esporre mai la console admin di un mail gateway direttamente su Internet — se lo stai facendo, è il momento di smettere.

## Applica la patch appena disponibile

Fortinet aggiorna FortiMail tramite il portale support.fortinet.com. Controlla la disponibilità dell'hotfix per la tua versione:

```bash
# Dalla CLI di FortiMail
execute update-now
# oppure dalla GUI: System > Firmware > Check for updates
```

Dopo l'aggiornamento, verifica la versione installata:

```bash
get system status | grep "Version"
```

## Il contesto più ampio

Questa non è la prima volta che Fortinet si trova nel mirino di attori di minaccia sofisticati. Nel corso degli ultimi anni, vulnerabilità su FortiGate, FortiNAC e FortiOS sono state sfruttate da gruppi APT e attori ransomware per ottenere un punto d'appoggio iniziale nelle reti aziendali. FortiMail — spesso esposto su Internet per ricevere posta — è un bersaglio particolarmente appetibile: è il primo punto di contatto con l'esterno e, se compromesso, può essere usato anche per intercettare o manipolare le email in transito.

## Cosa fare adesso

1. **Verifica subito la versione** di FortiMail in produzione
2. **Applica il workaround** se sei nella finestra di versioni vulnerabili
3. **Controlla i log** con gli IoC pubblicati da Fortinet
4. **Isola l'admin interface** da Internet (non dovrebbe mai essere pubblica)
5. **Tieni d'occhio** il portale Fortinet per la patch definitiva

Per chi gestisce mail gateway aziendali, questo è il tipo di vulnerabilità che non si può rimandare al prossimo ciclo di patching. Tre giorni è il limite dato alle agenzie federali — per chi è esposto su Internet, anche meno.

---

*Fonti: [The Hacker News](https://thehackernews.com/2026/10/critical-fortimail-zero-day-flaw.html), [SecurityWeek](https://www.securityweek.com/exploited-fortinet-fortimail-zero-day-calls-for-urgent-action/), [Help Net Security](https://www.helpnetsecurity.com/2026/10/02/fortinet-fortimail-vulnerability-cve-2026-104286/)*
