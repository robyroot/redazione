---
title: "Flatpak 1.18: finalmente le app AI e GPU AMD girano in sandbox su Linux"
rilevanza: "MEDIA"
fonte: "https://linuxiac.com/flatpak-1-18-released-with-amd-compute-interface-support/"
data_notizia: "2026-06-08"
tags: ["flatpak", "linux", "AMD", "AI", "open-source", "sandbox", "ROCm"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato per RobyRoot: notizia molto concreta per chi ha una GPU AMD e vuole
  usare tool AI locali (Ollama, Stable Diffusion, ecc.) tramite Flatpak. Prima di 1.18 era
  necessario rinunciare alla sandbox per accedere a /dev/kfd. Ora non più.
---

# Flatpak 1.18: finalmente le app AI e GPU AMD girano in sandbox su Linux

Se hai una scheda grafica AMD e ti piace tenere le app Linux dentro una sandbox Flatpak, finora hai dovuto scegliere: o sicurezza (sandbox) o performance AI (accesso GPU). Con **Flatpak 1.18**, uscito l'8 giugno 2026, questo compromesso non esiste più. Il supporto nativo per il compute interface AMD — il cuore di ROCm e OpenCL — è finalmente integrato.

## Il problema che 1.18 risolve

Flatpak isola le app in un ambiente sandbox per motivi di sicurezza. Questo è ottimo per la maggior parte delle app, ma ha sempre creato un grattacapo per chi vuole sfruttare la GPU AMD per calcolo parallelo (intelligenza artificiale, machine learning, rendering).

Il device AMD usato per il compute si chiama `/dev/kfd` — esposto dal modulo kernel `amdkfd`. Prima di Flatpak 1.18, per usarlo da un'app Flatpak bisognava concedere accesso a **tutti i dispositivi** con il permesso `--device=all`, che è l'equivalente di aprire un varco enorme nella sandbox. Non certo l'approccio ideale.

Flatpak 1.18 introduce il permesso specifico `devices=dri`, che ora include automaticamente `/dev/kfd` insieme ai dispositivi grafici standard. In pratica: la sandbox rimane chiusa, ma l'app può comunicare con la GPU AMD per il compute senza bisogno di permessi eccessivi.

## Cosa cambia in pratica per te

Se usi tool come **Ollama**, **Stable Diffusion WebUI**, o altri strumenti AI distribuiti come Flatpak, il comportamento cambia in modo netto:

**Prima di Flatpak 1.18:**
```bash
# Dovevi aggiungere questo per far funzionare la GPU AMD:
flatpak override --user --device=all com.esempio.AppAI
# Questo apriva TUTTI i device, non solo la GPU — pessimo per la sicurezza
```

**Con Flatpak 1.18:**
```bash
# Non serve nessun override manuale: il permesso dri include ora /dev/kfd
# Le app aggiornate che dichiarano devices=dri ottengono accesso a ROCm automaticamente

# Per verificare la versione di Flatpak installata:
flatpak --version

# Per aggiornare Flatpak (su Fedora/openSUSE/Arch):
sudo dnf upgrade flatpak         # Fedora
sudo zypper update flatpak       # openSUSE
sudo pacman -Syu flatpak         # Arch Linux
```

Verifica che la tua GPU AMD sia riconosciuta correttamente:
```bash
# Controlla che il modulo amdkfd sia caricato
lsmod | grep amdkfd

# Verifica che /dev/kfd esista e sia accessibile
ls -la /dev/kfd

# Con ROCm installato, testa il riconoscimento della GPU
rocminfo | grep 'Agent Type\|Name'
```

## Le altre novità di Flatpak 1.18

Il supporto AMD ROCm è la novità principale, ma 1.18 porta anche altri miglioramenti:

- **Tempi di avvio migliorati sotto Fish shell**: se usi Fish come shell, le app Flatpak si avviano più rapidamente grazie a ottimizzazioni nella gestione dell'ambiente
- **Output di `flatpak update` più chiaro**: i messaggi mostrano meglio cosa sta succedendo durante gli aggiornamenti
- **`flatpak-coredumpctl` migliorato**: gestione degli errori più robusta per il debug dei crash

Non è un aggiornamento rivoluzionario su tutti i fronti, ma il fix AMD è abbastanza significativo da giustificare l'aggiornamento per chi usa GPU rosse.

## Il quadro più grande: Flatpak e AI locale

Questa novità si inserisce in un trend chiaro: sempre più persone vogliono girare modelli AI **localmente**, sul proprio hardware, senza inviare dati a cloud di terze parti. Le GPU AMD con ROCm sono una valida alternativa alle NVIDIA con CUDA, spesso a costi inferiori.

Flatpak 1.18 abbassa un ostacolo concreto per distribuire tool AI open source in modo sicuro e semplice. Se sei uno sviluppatore che vuole pubblicare su Flathub un'app che sfrutta l'inferenza GPU, ora puoi farlo senza chiedere permessi eccessivi agli utenti.

L'aggiornamento dovrebbe arrivare nei prossimi giorni nelle repository delle principali distribuzioni. Su Flathub, le app che vogliono sfruttare il nuovo permesso dovranno aggiornare il loro manifest — quindi aspettati qualche settimana prima che le app AI su Flathub si aggiornino per usare nativamente `/dev/kfd`.
