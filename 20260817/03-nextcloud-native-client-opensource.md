---
title: "Nextcloud Native: il client open source che prova a unire Drive, Calendar e Gmail in un'unica app"
rilevanza: "MEDIA"
fonte: "https://linuxiac.com/this-new-nextcloud-client-looks-surprisingly-good-already/"
data_notizia: "2026-08-17"
tags: ["opensource", "privacy", "linux", "selfhosting"]
livello: "beginner"
nota_editoriale: |
  Angolo consigliato: framing "alternativa privacy-friendly a Google Workspace" per chi vuole
  uscire dall'ecosistema Google/Microsoft tramite self-hosting. Buon pezzo introduttivo, magari
  con avvertenza chiara che è software alpha e quindi non ancora pronto per un uso "production"
  su dati importanti senza backup.
---

Se usate già Nextcloud per tenere file, foto e calendario lontani dai server di Google, questa settimana c'è una notizia che potrebbe interessarvi da vicino: il 16 agosto 2026 è spuntato **Nextcloud Native**, un nuovo client open source che prova a fare quello che finora nessuno era riuscito a fare bene: mettere Files, Foto, Talk, Calendario, Mail, Note e Deck dentro un'**unica app nativa**, invece che in una raccolta di applicazioni separate o, peggio, in un client web travestito da app desktop.

## Cos'è di preciso

Nextcloud, per chi non lo conoscesse, è la piattaforma open source più usata per farsi il proprio "cloud personale": un server (che potete ospitare voi stessi, su un NAS o un piccolo VPS) che offre sincronizzazione file, condivisione, calendario, rubrica, videochiamate e molto altro, tutto sotto il vostro controllo invece che sui server di Google o Microsoft. Il problema storico di Nextcloud, però, è sempre stato l'esperienza utente: un'app per i file, una per le foto, una per la posta, ognuna con la sua interfaccia e le sue stranezze.

Nextcloud Native nasce proprio per risolvere questo. È un progetto sviluppato in modo **indipendente** dal team **Obiente**, non affiliato né sponsorizzato da Nextcloud GmbH (l'azienda dietro il progetto ufficiale), disponibile pubblicamente su GitHub. L'app comunica con il server tramite le API ufficiali e verificate di Nextcloud, ma poi presenta tutti i dati con un'interfaccia nativa unica, con sezioni dedicate a file, foto, conversazioni, eventi e altri servizi, invece che con la solita accozzaglia di web-view incollate insieme.

## Su cosa gira

Al momento sono disponibili build funzionanti per **Linux, Android e Windows**, con Linux indicato esplicitamente come piattaforma primaria per lo sviluppo desktop interattivo. Il supporto per Mac e iOS è in programma ma non ancora disponibile. La versione Android non è semplicemente l'interfaccia desktop rimpicciolita: è stata ripensata con un layout pensato per il touch.

## Occhio: è ancora alpha

Va detto chiaramente: si tratta di software in fase **alpha**, quindi giovane, in sviluppo attivo e potenzialmente instabile. Non è il momento di affidargli i vostri unici backup senza rete di sicurezza, ma è già abbastanza rifinito da attirare l'attenzione della community: chi lo ha provato lo descrive come "sorprendentemente buono" già in questa fase iniziale, il che fa ben sperare per gli sviluppi futuri.

## Perché interessa a chi tiene alla privacy

Il punto centrale, per i lettori di RobyRoot, è quello che questo progetto rappresenta: un altro tassello che rende più facile e più piacevole abbandonare l'ecosistema Google (o Microsoft) senza rinunciare alla comodità di avere tutto in un unico posto. Uno dei motivi per cui tante persone, pur volendo maggiore privacy, restano ancorate a Gmail, Google Drive e Google Calendar è proprio la comodità di un'esperienza integrata. Progetti come Nextcloud Native attaccano esattamente questo punto debole, offrendo un'alternativa self-hosted che, almeno sulla carta, non ha nulla da invidiare in termini di usabilità.

Vale la pena ricordare che con Nextcloud (in qualunque client lo usiate) il controllo dei vostri dati resta interamente nelle vostre mani: decidete voi dove risiede il server, chi vi ha accesso, e nessuna azienda terza analizza le vostre email o le vostre foto per scopi pubblicitari.

## Come provarlo

Se volete dare un'occhiata, i build di Nextcloud Native sono scaricabili dal sito ufficiale del progetto o direttamente dal repository GitHub `Obiente/nc-native`. Ovviamente serve già avere un server Nextcloud attivo (vostro o di terzi) a cui collegarvi: il client da solo non basta, è "solo" l'interfaccia con cui parlare al vostro cloud personale.

Per chi segue da tempo il mondo self-hosting, è un progetto da tenere d'occhio nei prossimi mesi: se lo sviluppo mantiene il ritmo attuale, potrebbe diventare il modo più comodo per usare Nextcloud su Linux.
