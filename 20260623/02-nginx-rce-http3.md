---
title: "CVE-2026-42530: vulnerabilità critica in NGINX HTTP/3 permette RCE remoto senza autenticazione"
rilevanza: "ALTA"
fonte: "https://thehackernews.com/2026/06/f5-patches-two-critical-nginx-open.html"
data_notizia: "2026-06-19"
tags: ["security", "nginx", "cve", "rce", "webserver", "http3"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: Articolo pratico rivolto a chi gestisce server Linux. Spiega la vulnerabilità in modo comprensibile, fornisce i comandi per verificare la versione NGINX e aggiornare, e include la workaround per chi non può aggiornare subito (disabilitare HTTP/3). Tono urgente ma calmo.
---

# CVE-2026-42530: vulnerabilità critica in NGINX HTTP/3 permette RCE senza autenticazione

Se gestisci un server web con NGINX e hai abilitato il supporto HTTP/3, questo è il momento di smettere di leggere e andare ad aggiornare. Poi torna qui per capire cosa è successo.

F5 ha rilasciato il 19 giugno 2026 patch d'emergenza fuori ciclo (*out-of-band*) per due vulnerabilità critiche in NGINX Open Source: **CVE-2026-42530** (CVSS v4: 9.2) e **CVE-2026-42055**. La prima, in particolare, riguarda il modulo HTTP/3 e può portare all'esecuzione di codice arbitrario da remoto senza che l'attaccante debba autenticarsi.

## Il dettaglio tecnico (semplificato)

CVE-2026-42530 è una vulnerabilità di tipo **use-after-free** nel modulo `ngx_http_v3_module`. In parole semplici: NGINX gestisce male la memoria quando una sessione HTTP/3 riapre lo stream dell'encoder QPACK in un momento critico. Questo causa una corruzione della memoria che può:

1. Mandare in crash il worker process di NGINX (Denial of Service)
2. In ambienti dove l'ASLR è disabilitato o aggirabile, aprire la strada all'esecuzione di codice arbitrario (RCE)

La vulnerabilità è **triggerabile da remoto, senza autenticazione**: basta inviare una sessione HTTP/3 appositamente costruita. Non è necessario avere un account o accesso speciale al server.

La seconda vulnerabilità, CVE-2026-42055, riguarda invece il modulo HTTP/2 e ha caratteristiche simili, anche se leggermente meno critiche (CVSS v4: 8.7).

## Versioni affette

Le versioni vulnerabili di NGINX Open Source sono:
- **1.31.0**
- **1.31.1**

L'esposizione dipende dal fatto che il supporto HTTP/3 sia abilitato nella configurazione. NGINX 1.31.2 o superiore non è vulnerabile.

## Verificare e aggiornare

Prima di tutto, controlla la versione di NGINX che stai usando:

```bash
nginx -v
# Oppure se NGINX gira come servizio:
sudo nginx -v 2>&1
systemctl status nginx | grep -i version
```

Se sei su 1.31.0 o 1.31.1, aggiorna immediatamente:

```bash
# Su Debian/Ubuntu
sudo apt update && sudo apt upgrade nginx

# Su RHEL/AlmaLinux/Rocky Linux
sudo dnf update nginx

# Su Arch Linux
sudo pacman -Syu nginx

# Su Alpine (molto comune in container Docker)
apk upgrade nginx
```

Se usi NGINX tramite container Docker, aggiorna l'immagine base:

```bash
docker pull nginx:stable
# Poi ricostruisci e ridistribuisci i tuoi container
```

## Workaround temporaneo: disabilitare HTTP/3

Se per qualsiasi motivo non puoi aggiornare immediatamente, la mitigazione è semplice: disabilita HTTP/3 nel file di configurazione.

Apri il tuo `nginx.conf` o il vhost interessato e rimuovi (o commenta) le direttive HTTP/3:

```nginx
server {
    listen 443 ssl;
    # Commenta o rimuovi questa riga:
    # listen 443 quic reuseport;
    
    # Rimuovi anche questi header se presenti:
    # add_header Alt-Svc 'h3=":443"; ma=86400';
    
    # ... resto della configurazione
}
```

Poi ricarica NGINX:

```bash
sudo nginx -t && sudo systemctl reload nginx
```

## Quanto è grave davvero?

Al momento della scrittura di questo articolo non sono stati segnalati exploit in-the-wild confermati per CVE-2026-42530. Tuttavia, il fatto che la vulnerabilità sia stata discussa pubblicamente e che esistano già *proof-of-concept* nella ricerca della sicurezza significa che la finestra di rischio si sta riducendo rapidamente.

NGINX è uno dei web server più diffusi al mondo — gira su milioni di server Linux. Se la vulnerabilità venisse weaponizzata, l'impatto potrebbe essere enorme. HTTP/3 è ancora una funzionalità relativamente nuova e molti server potrebbero averla abilitata senza rendersene conto, magari seguendo tutorial recenti.

## Checklist rapida

- [ ] Verificare la versione NGINX su tutti i server (`nginx -v`)
- [ ] Aggiornare a 1.31.2 o superiore
- [ ] Se non si può aggiornare subito, disabilitare HTTP/3 nella configurazione
- [ ] Controllare i log per sessioni HTTP/3 anomale nel periodo 15-19 giugno
- [ ] Aggiornare le immagini Docker basate su NGINX
- [ ] Verificare eventuali reverse proxy (Cloudflare, CDN) che potrebbero mascherare la versione

Non è il momento di rimandare. Aggiorna adesso.
