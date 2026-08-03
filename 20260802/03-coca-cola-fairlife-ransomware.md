---
title: "Ransomware ferma la produzione di latte Coca-Cola: rubato un terabyte di dati da Fairlife"
rilevanza: "MEDIA"
fonte: "https://www.bleepingcomputer.com/news/security/coca-cola-confirms-data-theft-in-fairlife-ransomware-attack/"
data_notizia: "2026-08-02"
tags: ["ransomware", "cybersecurity", "privacy", "infrastrutture critiche"]
livello: "beginner"
nota_editoriale: |
  Angolo per RobyRoot: usare l'episodio per parlare dell'impatto "fisico" del ransomware quando
  colpisce OT/produzione (non solo furto dati, ma fermo di stabilimenti reali), tema spesso
  sottovalutato dal pubblico generalista. Buon collegamento con la sezione privacy per parlare di
  cosa succede ai dati di dipendenti/fornitori quando un'azienda subisce un attacco del genere.
---

Quando pensiamo a un attacco ransomware, spesso immaginiamo schermate bloccate e richieste di riscatto in Bitcoin. Quello che è successo a Fairlife, la controllata di Coca-Cola specializzata in latte ultrafiltrato e bevande proteiche, ci ricorda che dietro un attacco informatico ci sono spesso conseguenze molto concrete: in questo caso, la produzione di latte fermata negli Stati Uniti.

Coca-Cola ha confermato, in una comunicazione depositata presso la SEC (l'autorità di vigilanza sui mercati finanziari statunitense), che un attacco ransomware ha colpito i sistemi di Fairlife, causando il furto di dati aziendali e costringendo l'azienda a **sospendere la produzione in alcuni impianti statunitensi**. A rivendicare l'attacco è il gruppo **Anubis**, una gang ransomware relativamente nuova sulla scena ma già piuttosto attiva, che sostiene di aver sottratto circa **un terabyte di dati aziendali** e ha aggiunto Fairlife alla lista delle vittime sul proprio sito di data leak nel dark web, minacciando la pubblicazione del materiale se non verrà pagato un riscatto.

Fairlife non è un nome piccolo: produce latte ultrafiltrato, frullati proteici e bevande nutrizionali con oltre un miliardo di dollari di fatturato al dettaglio annuo, distribuiti tramite quattro stabilimenti produttivi negli USA. Gli attaccanti sarebbero riusciti ad accedere a una parte dei sistemi dell'azienda, inclusi quelli legati direttamente alla produzione — il che spiega perché l'impatto non si sia limitato al furto di dati, ma abbia toccato le linee produttive vere e proprie. Coca-Cola ha dichiarato che, non appena scoperta l'intrusione, ha segnalato l'accaduto alle autorità competenti e ha scelto di **non seguire le istruzioni degli attaccanti per negoziare** il riscatto — una linea sempre più comune tra le grandi aziende, anche se non priva di conseguenze operative, come dimostra proprio il fermo produzione. Al momento la maggior parte della produzione negli stabilimenti USA è stata ripristinata.

**Perché la vicenda merita attenzione anche fuori dagli USA.** Il caso Fairlife si inserisce in un trend che gli analisti di sicurezza monitorano da tempo: gli attacchi ransomware contro il settore alimentare e delle bevande sono in aumento, e non è un caso. Le aziende di questo comparto spesso convivono con sistemi OT (Operational Technology, cioè i sistemi che controllano fisicamente le linee di produzione) meno aggiornati rispetto all'IT tradizionale, e un fermo produzione ha un impatto economico immediato e visibile — condizioni che rendono queste vittime particolarmente "motivate" a pagare in fretta, agli occhi di chi organizza questi attacchi. Il settore alimentare, insomma, sta diventando un bersaglio sempre più appetibile proprio per la combinazione di superficie d'attacco ampia (fornitori, impianti, sistemi legacy) e pressione a ripristinare rapidamente l'operatività.

C'è anche il lato privacy da non sottovalutare: un terabyte di dati aziendali rubati può includere, oltre a segreti industriali e informazioni finanziarie, anche dati personali di dipendenti, fornitori e partner commerciali. Finché il gruppo Anubis non pubblica (o Coca-Cola non conferma) il contenuto esatto del materiale sottratto, non sappiamo con precisione quali categorie di dati siano coinvolte — ma la storia recente di casi simili suggerisce che raramente si tratta di "solo" documenti tecnici.

Per chi si occupa di sicurezza industriale o gestisce infrastrutture con componenti OT, il caso Fairlife è l'ennesima conferma che la segmentazione tra rete IT e rete di produzione, i backup offline e i piani di risposta agli incidenti testati regolarmente non sono un lusso da grande multinazionale: sono la differenza tra un incidente contenuto e uno stabilimento fermo per giorni.
