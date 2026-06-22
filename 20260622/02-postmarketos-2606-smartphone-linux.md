---
title: "postmarketOS 26.06 'Alpen Avocado': Linux vero sul tuo vecchio smartphone"
rilevanza: "MEDIA"
fonte: "https://postmarketos.org/blog/2026/06/21/v26.06-release/"
data_notizia: "2026-06-21"
tags: ["Linux", "mobile", "smartphone", "open-source", "sostenibilità", "PinePhone", "privacy"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: dare una seconda vita agli smartphone abbandonati è perfetto per il pubblico Linux + privacy. Sottolineare il lato green (meno rifiuti elettronici), la libertà da Google/Apple, e i dispositivi supportati italiani come Fairphone 4. Includere comandi pratici di installazione.
---

# postmarketOS 26.06 "Alpen Avocado": Linux vero sul tuo vecchio smartphone

Il 21 giugno 2026, il team di postmarketOS ha rilasciato la versione **26.06**, nome in codice *"Alpen Avocado"*. Se non conosci questo progetto, eccolo in una frase: è un'installazione di Linux completo — vero Linux, con kernel mainline — pensata per far girare sistema operativo libero sugli smartphone, compresi quelli che i produttori hanno abbandonato da anni.

Sì, quel Pixel 3A dimenticato in un cassetto può tornare utile.

## Perché postmarketOS è diverso

La maggior parte delle ROM Android alternative (LineageOS, GrapheneOS) si basa comunque su Android. postmarketOS è un'altra cosa: è basato su **Alpine Linux**, usa kernel Linux mainline (lo stesso che gira sul tuo PC), e puoi scegliere tra diversi ambienti desktop come se stessi configurando una distribuzione desktop normale.

I vantaggi:
- **Aggiornamenti di sicurezza a lungo termine** — Alpine Linux aggiorna il kernel mainline regolarmente, quindi non sei bloccato a un kernel Android del 2018
- **Zero Google** — nessun servizio Google Play, nessun tracciamento, nessun framework proprietario
- **Durata del dispositivo** — se il tuo telefono ha ancora l'hardware funzionante, merita software funzionante

## Cosa c'è di nuovo nella 26.06

Questa release porta diversi aggiornamenti sostanziali:

**Ambienti desktop aggiornati**
- **GNOME 50** per i tablet (la versione mobile rimane su GNOME 48 per ora, più ottimizzata per schermi piccoli)
- **KDE Plasma Mobile 6.6.5** — un salto significativo dalla 6.5.6 della release precedente
- **Phosh 0.55.0**, l'ambiente pensato specificamente per i telefoni, ora usa `greetd` e `phrog` come display manager, abbandonando il vecchio `tinydm`

**Cambiamenti di sistema**
- **systemd 261** come init predefinito
- Sostituito `pbsplash` con **Plymouth** per la schermata di avvio: ora hai un'animazione del logo invece di uno schermo statico
- **sudo-rs** al posto di `doas` come strumento predefinito per l'escalation dei privilegi
- Supporto cell broadcast nel gestore del modem (utile per i sistemi di allerta emergenza)

**Nuovi dispositivi supportati**
Tra i dispositivi aggiunti o promossi a categorie migliori: Google Asurada/Cherry/Corsola Chromebook, Radxa Dragon Q6A, PINE64 PineNote.

## Dispositivi supportati che potresti avere in casa

La lista completa è lunga, ma ecco i dispositivi probabilmente presenti nei cassetti degli italiani:

| Dispositivo | Categoria |
|---|---|
| **Fairphone 4** | Community |
| **Google Pixel 3A / 3A XL** | Community |
| **OnePlus 6 / 6T** | Community |
| **PinePhone / PinePhone Pro** | Community |
| **Samsung Galaxy S9** | Community |
| **Xiaomi Poco F1** | Community |
| **Purism Librem 5** | Community |
| **Nokia N900** | Community (sì, anche lui) |

La "categoria community" significa che funziona ma non è perfettamente testata come le versioni ufficiali. Per i dettagli su cosa funziona e cosa no su ogni dispositivo, il wiki di postmarketOS è il punto di riferimento.

## Come provarlo (senza distruggere il telefono)

Il modo più sicuro per iniziare è usare **pmbootstrap**, lo strumento ufficiale di installazione:

```bash
# Installa pmbootstrap (richiede Python 3.10+)
pip install pmbootstrap

# Inizializza la configurazione
pmbootstrap init

# Seleziona il tuo dispositivo dall'elenco interattivo
# Scegli il filesystem e l'ambiente desktop (es. phosh per mobile)

# Avvia il flash sul dispositivo (con sblocco bootloader richiesto)
pmbootstrap flasher flash_rootfs
pmbootstrap flasher flash_kernel
```

Ovviamente, **sbloccare il bootloader cancella i dati del telefono**: fai backup prima. E verifica sul wiki ufficiale (`wiki.postmarketos.org`) quale sia la procedura specifica per il tuo modello.

## La questione della maturità

postmarketOS non è ancora per tutti. Alcune funzionalità base degli smartphone moderni — chiamate VoLTE, stabilità della GPU su certi chip Qualcomm, standby efficiente — hanno ancora limitazioni su molti dispositivi. Il progetto è brutalmente onesto al riguardo: ogni device ha una pagina wiki che lista cosa funziona e cosa no.

Ma se hai un vecchio telefono con hardware ancora funzionante, un po' di pazienza, e l'appetito per un sistema veramente libero, postmarketOS 26.06 è il punto di partenza migliore di sempre. E la soddisfazione di guardare GNOME 50 girare su un Pixel 3A abbandonato da Google non ha prezzo.

Il pianeta ringrazia anche lui: ogni telefono riutilizzato è uno in meno nella discarica RAEE.
