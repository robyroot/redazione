---
title: "KDE Plasma 6.8: dopo 30 anni, X11 va in pensione e Wayland diventa l'unico standard"
rilevanza: "ALTA"
fonte: "https://linuxiac.com/kde-plasma-6-8-released-drops-x11-sessions-after-30-years-of-kde/"
data_notizia: "2026-10-14"
tags: ["KDE", "Wayland", "X11", "Linux desktop", "Plasma"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: il momento storico del passaggio — 30 anni di X11 sul desktop Linux che finiscono proprio nel giorno del compleanno di KDE. Ottimo per un pezzo nostalgico-tecnico che spiega perché Wayland è il futuro e cosa cambia praticamente per gli utenti.
---

# KDE Plasma 6.8: dopo 30 anni, X11 va in pensione e Wayland diventa l'unico standard

Il 14 ottobre 2026 è una data doppiamente storica per il mondo del desktop Linux: KDE compie 30 anni **e** rilascia Plasma 6.8, la versione che segna la fine definitiva del supporto a X11. Non è un cambiamento da poco — stiamo parlando della fine di un'era che ha accompagnato generazioni di utenti Linux fin dai tempi di KDE 1.

## Cosa cambia con Plasma 6.8

La notizia più grossa è semplice da spiegare: da questa versione in poi, KDE Plasma funziona **solo su Wayland**. Le sessioni X11 non sono più un'opzione supportata. Se al login cercate la vecchia voce "KDE Plasma (X11)", non la troverete più.

Questo non significa che X11 sparisce dalla faccia della terra — il protocollo esiste ancora, e le applicazioni X11 continuano a girare grazie a XWayland, il layer di compatibilità che traduce le chiamate X11 in Wayland. Quello che finisce è la possibilità di far girare l'**intero compositor Plasma** su X11.

## Perché Wayland e perché adesso

La transizione verso Wayland era annunciata da anni. Il protocollo nasce per risolvere i problemi strutturali di X11: sicurezza migliorata (ogni applicazione vede solo la propria finestra, non quelle degli altri), gestione nativa dei display ad alta densità, isolamento migliore dei processi.

X11 è un protocollo degli anni '80 rattoppato per decenni. Wayland è stato progettato da zero per i desktop moderni, con GPU, touchscreen, e monitor multipli a risoluzioni diverse. Il team KDE ha aspettato che l'ecosistema Wayland maturasse abbastanza da coprire tutti i casi d'uso — e ora, finalmente, ha ritenuto che il momento fosse arrivato.

La scelta di farlo proprio nel 30° anniversario di KDE (nato il 14 ottobre 1996 grazie a Matthias Ettrich) non è certamente casuale: è un modo per celebrare tre decenni di lavoro e guardare al futuro allo stesso tempo.

## Cosa fare se usate ancora X11

Se avete motivi concreti per restare su X11 — driver proprietari problematici, applicazioni legacy che non funzionano bene con XWayland, configurazioni multi-monitor particolari — avete alcune opzioni:

```bash
# Verificare la sessione corrente (Wayland o X11)
echo $XDG_SESSION_TYPE

# Verificare se XWayland è attivo (per le app X11 legacy)
xlsclients 2>/dev/null && echo "XWayland attivo" || echo "XWayland non disponibile"
```

In alternativa, potete usare altri ambienti desktop che mantengono ancora il supporto X11, come XFCE o MATE. Ma se siete utenti KDE, la direzione è tracciata.

## Le altre novità di Plasma 6.8

Il drop di X11 non è l'unica novità, anche se è la più rumorosa. Plasma 6.8 porta con sé:

- **Fix last-minute per NVIDIA**: un bug che causava problemi con alcune configurazioni su driver NVIDIA è stato corretto prima del rilascio
- **Aggiornamento di Discover**: il gestore software aggiorna ora correttamente le app Flatpak in automatico, risolvendo un bug fastidioso
- **Miglioramenti all'accessibilità** e alla gestione delle sessioni Wayland

## Il futuro del desktop Linux è Wayland

La mossa di KDE segue una tendenza che GNOME aveva già intrapreso qualche versione fa, quando aveva eliminato la sessione X11 per impostazione predefinita (anche se la manteneva come opzione). Ora anche KDE fa il passo definitivo.

Per la maggior parte degli utenti moderni, la transizione sarà del tutto trasparente — probabilmente state già usando Wayland senza saperlo. Ma per chi è rimasto ancorato a X11 per motivi di compatibilità, è arrivato il momento di fare i conti con il cambiamento.

Trent'anni dopo la nascita di KDE, il desktop Linux guarda avanti. E lo fa su Wayland.
