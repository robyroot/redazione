---
title: "Meta lancia Muse Spark Open: 816 miliardi di parametri e gira su due Mac Studio"
rilevanza: "ALTA"
fonte: "https://techcrunch.com/2026/10/15/meta-launches-an-open-weight-model-that-runs-on-macs/"
data_notizia: "2026-10-15"
tags: ["AI", "open-source", "LLM", "Meta", "Apple", "privacy"]
livello: "intermediate"
nota_editoriale: |
  Angolo consigliato per RobyRoot: focus sul fatto che è open-weight (non open-source puro) e che gira in locale — tema caldo per chi vuole AI senza mandare dati al cloud. Chiarire bene la differenza tra 816B parametri totali e 42B attivi (architettura MoE), spesso fraintesa nei media.
---

# Meta lancia Muse Spark Open: 816 miliardi di parametri e gira su due Mac Studio

Meta ha presentato Muse Spark Open il 15 ottobre 2026, e il clamore è giustificato: si tratta del modello AI open-weight più potente mai rilasciato da un'azienda americana. Con 816 miliardi di parametri totali e una finestra di contesto da un milione di token, compete direttamente con i migliori modelli cinesi come GLM-5.3 di Zhipu AI.

Ma la cosa più strana — e interessante — è che Meta lo ha ottimizzato per girare su due Mac Studio con chip M5 Ultra. Sì, hai letto bene.

## MoE: 816B totali, 42B attivi

Prima di tutto, un chiarimento tecnico che molti titoli si sono dimenticati di fare. Muse Spark Open usa un'architettura Mixture of Experts (MoE). Questo significa che il modello ha 816 miliardi di parametri in totale, ma durante ogni inferenza ne attiva solo circa 42 miliardi.

È un po' come avere un team di 816 esperti ma consultarne solo 42 alla volta — quelli più adatti alla domanda specifica. Risultato: prestazioni elevate con un consumo computazionale molto più basso rispetto a un modello "denso" della stessa dimensione.

## Due Mac Studio come supercomputer AI

Meta ha collaborato con Apple per ottimizzare il modello tramite il framework MLX, la libreria di Apple per il machine learning su Silicon. La configurazione di riferimento prevede due Mac Studio M5 Ultra collegati tra loro, con almeno 1 TB di memoria unificata totale.

Non è una cosa per tutti — due Mac Studio M5 Ultra costano parecchio — ma il punto concettuale è rivoluzionario: un modello di questa potenza che gira in locale, senza cloud, senza mandare dati a nessuno. Per chi è attento alla privacy, questo apre scenari prima impensabili.

```bash
# Esempio concettuale di run con MLX (richiede hardware adeguato)
pip install mlx mlx-lm

# Download dei pesi (richiede account Hugging Face con accesso approvato)
huggingface-cli download meta-llama/muse-spark-open --local-dir ./muse-spark-open

# Avvio del modello
python -m mlx_lm.generate \
  --model ./muse-spark-open \
  --prompt "Spiega la differenza tra MoE e transformer denso"
```

## Licenza: open-weight, non open-source

Qui arriva la nota dolente. La licenza si chiama "Muse Model License" e non è open-source nel senso tradizionale. I pesi sono disponibili gratuitamente, ma:

- Le aziende con ricavi sopra i 20 milioni di dollari che offrono accesso API devono stipulare un accordo separato con Meta
- L'uso commerciale è consentito ma con restrizioni specifiche
- Il codice sorgente dell'architettura rimane proprietario

È lo stesso schema usato da Meta per Llama 3. "Open-weight" non è "open-source": puoi usare il modello, ma non sei libero di modificarlo e redistribuirlo come vorresti.

## Prestazioni: il migliore americano, ma...

Nei benchmark indipendenti, Muse Spark Open si posiziona come il miglior modello open-weight di origine americana, con ottimi risultati su coding, ragionamento matematico e compiti agentici. Tuttavia, secondo alcune valutazioni rimane leggermente indietro rispetto ai concorrenti cinesi più recenti come GLM-5.3 e Kimi K3.

La finestra di contesto da 1 milione di token è invece un punto di forza notevole: puoi farci leggere interi codebase, documenti lunghi, o tenere conversazioni molto estese senza perdere il filo.

## E per chi non ha due Mac Studio?

Per la stragrande maggioranza degli utenti, il modo più pratico di usare Muse Spark Open sarà via API cloud — disponibile su Hugging Face Inference, AWS, Azure e altri provider. Le performance saranno le stesse, ma ovviamente i dati escono dal tuo controllo.

Alternativamente, tieni d'occhio le versioni quantizzate che la community pubblicherà nei prossimi giorni su Hugging Face: versioni Q4 o Q6 potrebbero girare su hardware molto più accessibile, anche se con qualità ridotta.

Insomma, Meta ha fatto un passo importante verso l'AI locale e open-weight. Non è perfetto, ma la direzione è quella giusta.
