---
title: "Flatpak 1.18: finalmente il supporto per AMD ROCm nelle app sandbox (e due CVE tappati)"
rilevanza: "MEDIA"
fonte: "https://9to5linux.com/flatpak-1-18-linux-app-sandboxing-and-distribution-framework-officially-released"
data_notizia: "2026-06-08"
tags: ["linux", "flatpak", "AMD", "ROCm", "GPU", "sicurezza", "desktop"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato per RobyRoot: notizia pratica con impatto immediato per chi usa GPU AMD su Linux. Il supporto ROCm in Flatpak è stato richiesto dalla community per anni — ora è realtà. Ottimo per chi vuole far girare app AI/ML in sandbox senza rinunciare all'accelerazione GPU.
---

# Flatpak 1.18: le app sandbox ora possono usare la GPU AMD per il calcolo (e non solo per la grafica)

Il 8 giugno 2026 è uscita Flatpak 1.18, la release più significativa del framework di distribuzione app Linux degli ultimi mesi. La novità di punta è il supporto nativo per **AMD ROCm** nelle applicazioni in sandbox — qualcosa che la community chiedeva da tempo — ma ci sono anche due correzioni di sicurezza importanti e una serie di miglioramenti pratici che rendono l'esperienza quotidiana più fluida.

## AMD ROCm finalmente in sandbox

Fino a oggi, le applicazioni Flatpak che volevano usare la GPU AMD per il calcolo (non solo la grafica) avevano due opzioni entrambe brutte: o richiedere accesso a *tutti* i device del sistema (di fatto bucando la sandbox), oppure non supportare ROCm del tutto.

Con Flatpak 1.18, le app possono richiedere esplicitamente l'accesso al device `/dev/kfd` — il kernel fusion driver di AMD — tramite il permesso `dri`. Questo permette a strumenti di machine learning, editor di video con accelerazione GPU, e applicazioni di calcolo scientifico di usare AMD ROCm in modo corretto e sicuro, senza rinunciare all'isolamento della sandbox.

In pratica: se hai una GPU AMD e usi Flatpak, ora puoi avere la tua app AI che macina dati sulla GPU **senza aprire buchi di sicurezza**.

Per verificare che un'app abbia questo permesso:

```bash
# Vedi i permessi di un'app specifica
flatpak info --show-permissions nome.app.id

# Oppure cerca il permesso dri
flatpak info --show-permissions nome.app.id | grep dri
```

## Due CVE corretti: sandbox escape e cancellazione file arbitraria

Questa release tappa anche due vulnerabilità di sicurezza:

**CVE-2026-34078** — Una falla che permetteva una completa sandbox escape, consentendo a un'app malevola di accedere ai file dell'host. Gravità alta.

**CVE-2026-34079** — Permetteva la cancellazione arbitraria di file sull'host da dentro la sandbox. Anche questa a gravità alta.

Se usi Flatpak, aggiornare alla 1.18 è assolutamente prioritario. Su quasi tutte le distro è sufficiente:

```bash
# Su distro che usano i repository ufficiali (Fedora, Arch, ecc.)
sudo pacman -Syu flatpak        # Arch
sudo dnf upgrade flatpak        # Fedora
sudo apt update && sudo apt upgrade flatpak  # Debian/Ubuntu

# Verifica la versione installata
flatpak --version
```

## Altre novità pratiche

**Installazione da URI flatpak+https://**

Ora puoi installare app direttamente da un link web senza passare per Flathub o impostare un repository manuale:

```bash
flatpak install --from https://esempio.com/app/miapp.flatpakref
```

**Supporto immagini OCI**

Flatpak 1.18 supporta l'installazione diretta da immagini OCI (il formato dei container Docker/Podman). Questo apre le porte a nuovi flussi di distribuzione e CI/CD.

**Fish shell più veloce**

Chi usa Fish come shell predefinita noterà che i completamenti Flatpak si caricano significativamente più velocemente. Piccola cosa, ma chi ci lavora tutto il giorno apprezza.

**Output migliorato**

I messaggi di `flatpak update` e gli errori di `flatpak-coredumpctl` sono stati riscritti per essere più leggibili e utili. Meno output criptico, più informazioni pratiche.

## Il momento giusto per aggiornare

Flatpak ha raggiunto **4,3 miliardi di download totali** nel 2026 su 3.542 applicazioni — è ormai il sistema di distribuzione app de facto per il desktop Linux. Con questa release il progetto risolve uno dei problemi aperti più longevi (ROCm in sandbox) e chiude due buchi di sicurezza seri.

Se non hai ancora aggiornato, è il momento giusto. E se hai una GPU AMD e usi applicazioni AI o ML, la 1.18 potrebbe finalmente sbloccare l'accelerazione hardware che aspettavi.

```bash
# Aggiorna tutte le app Flatpak installate
flatpak update

# Controlla se ci sono permessi da rivedere dopo l'update
flatpak permission-list
```

Per i maintainer che vogliono abilitare ROCm nelle proprie app: basta aggiungere `--device=dri` al manifest e dichiarare la dipendenza da `org.freedesktop.Platform.GL.default`. La documentazione ufficiale è già stata aggiornata su docs.flatpak.org.
