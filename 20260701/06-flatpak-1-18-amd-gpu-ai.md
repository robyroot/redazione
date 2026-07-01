---
title: "Flatpak 1.18.0: 4,3 miliardi di download e supporto GPU AMD per l'AI locale"
rilevanza: "MEDIA"
fonte: "https://9to5linux.com/t2-linux-26-6-brings-linux-7-0-refined-kde-plasma-desktop-with-flatpak-support"
data_notizia: "2026-06-08"
tags: ["linux", "flatpak", "desktop", "AMD", "open-source", "AI", "flathub"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato per RobyRoot: collega il supporto AMD /dev/kfd all'interesse crescente per l'AI locale su Linux (Ollama, LM Studio, llama.cpp). Un utente che vuole fare inferenza AI con GPU AMD dentro una Flatpak ora può farlo nativamente. È un'apertura concreta verso l'AI desktop accessibile a tutti.
---

# Flatpak 1.18.0: 4,3 miliardi di download e supporto GPU AMD per l'AI locale

L'8 giugno 2026 è uscita **Flatpak 1.18.0**, definita come la release più significativa degli ultimi mesi per l'ecosistema del packaging Linux. Nel frattempo, Flathub ha superato i **4,3 miliardi di download totali** su 3.542 applicazioni — un numero che conferma come Flatpak sia diventato lo standard di fatto per la distribuzione di software su Linux desktop.

Ma la novità tecnica più interessante di questa release riguarda chi usa Linux con una GPU AMD e vuole fare **AI locale**: il supporto nativo per l'interfaccia compute AMD tramite `/dev/kfd`.

## Cos'è Flatpak (ripasso veloce)

Se sei nuovo a Linux o non hai seguito l'evoluzione del packaging negli ultimi anni, un breve ripasso. Flatpak è un formato universale di distribuzione applicazioni: invece di avere pacchetti diversi per ogni distro (`.deb` per Ubuntu, `.rpm` per Fedora, `.pkg.tar.zst` per Arch...), una singola Flatpak funziona su tutte le distribuzioni compatibili.

Le app Flatpak girano in una **sandbox** con accesso controllato alle risorse di sistema. Questo garantisce isolamento e sicurezza, ma significa anche che l'accesso all'hardware — come le GPU — deve essere esplicitamente concesso tramite un sistema di permessi.

## La novità chiave: GPU AMD per il compute

Fino a Flatpak 1.18.0, le app in sandbox potevano accedere alle GPU principalmente per il **rendering grafico** (OpenGL, Vulkan, giochi, interfacce grafiche). Ma `/dev/kfd` è un'altra storia.

`/dev/kfd` è l'interfaccia che le GPU AMD espongono per il **compute generalizzato** — ovvero l'esecuzione di codice parallelo per AI, machine learning, e calcolo scientifico tramite ROCm (il framework open-source AMD equivalente a CUDA). È la porta d'accesso alla potenza di calcolo della GPU per tutto ciò che non è rendering di immagini.

Con Flatpak 1.18.0, è possibile concedere alle app Flatpak l'accesso a `/dev/kfd` tramite il sistema DRI device permission. In pratica significa che strumenti come **Ollama**, **LM Studio** o **llama.cpp** — se distribuiti come Flatpak — potranno sfruttare direttamente la GPU AMD per l'inferenza AI locale, senza uscire dalla sandbox.

```bash
# Verifica la versione di Flatpak installata
flatpak --version

# Verifica i permessi attuali di un'app specifica
flatpak info --show-permissions <nome-app>

# Concedi accesso alla GPU a un'app specifica (DRI include /dev/kfd)
flatpak override --device=dri <nome-app>

# Aggiorna Flatpak su Debian/Ubuntu
sudo apt update && sudo apt upgrade flatpak

# Aggiorna tutte le app Flatpak installate
flatpak update
```

## Perché è importante per l'AI locale

L'AI locale su Linux sta crescendo rapidamente. Sempre più utenti vogliono eseguire modelli come Llama, Mistral o Phi direttamente sul proprio computer — senza cloud, senza abbonamenti, senza inviare dati a server terzi.

Le GPU AMD (specialmente le serie RX 7000) sono popolari tra gli utenti Linux proprio per il loro **supporto open-source tramite ROCm**. Finora, chi voleva usare la GPU AMD per l'inferenza AI su Linux aveva spesso a che fare con installazioni complesse fuori dalla sandbox Flatpak, con gestione manuale delle dipendenze ROCm.

Con questa release, il puzzle si completa meglio: il sistema di permessi Flatpak capisce e gestisce `/dev/kfd`, avvicinando l'esperienza AI locale a qualcosa di più accessibile anche per gli utenti meno tecnici. Non ancora completamente plug-and-play, ma un passo concreto nella direzione giusta.

## Come installare Flatpak e Flathub

Se non hai ancora Flatpak configurato con Flathub:

```bash
# Installa Flatpak
sudo apt install flatpak         # Debian/Ubuntu
sudo dnf install flatpak         # Fedora
sudo pacman -S flatpak           # Arch Linux

# Aggiungi il repository Flathub
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo

# Dopo aver aggiunto Flathub, cerca strumenti AI disponibili
flatpak search ollama
flatpak search lm-studio
```

## I numeri di Flathub nel 2026

4,3 miliardi di download su 3.542 app non sono un numero da poco. Flathub ospita ormai quasi tutto l'ecosistema applicativo desktop Linux: suite d'ufficio, browser, client di messaggistica, strumenti creativi come GIMP e Inkscape, ambienti di sviluppo, e sempre più strumenti AI.

Il messaggio è chiaro: Linux desktop non richiede più di compilare da sorgente per avere software aggiornato e funzionante. Flatpak sta portando la comodità dell'installazione one-click nell'ecosistema open-source, mantenendo la sicurezza dell'isolamento. E ora, con il supporto AMD compute, anche l'AI locale entra ufficialmente nel perimetro della sandbox.
