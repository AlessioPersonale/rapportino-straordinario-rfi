# Rapportino Straordinario

Web app per compilare in pochi secondi il **Rapporto di Intervento Straordinario** (modello REP/DISP 07/2024) e ottenere il PDF compilato, scritto direttamente sopra il modulo originale.

Funziona interamente nel browser: nessun server, nessuna installazione, nessun dato inviato online. Funziona anche offline.

## Funzionalità

- **Giorno** in formato italiano (`gg/mm/aaaa`), con pulsante "Oggi"
- **Luogo** con menu a cascata Regione → Provincia → Comune (tutti i ~7.900 comuni italiani), con ricerca
- **Ticket / avviso**: scelta Sì/No e numero ticket
- **Chiamata C.E.I.** oppure **Prolungamento** (si escludono a vicenda):
  - *Chiamata C.E.I.*: numero di telefono, ora della chiamata e, per ogni agente, Rep/Disp, ora arrivo, ora termine, ora rientro e utilizzo auto privata
  - *Prolungamento*: per ogni agente solo l'ora di termine intervento
- **Agenti intervenuti**: fino a 5, come nel modulo
- **Descrizione intervento**: il testo scorre di riga in riga e va a capo solo a fine riga
- **Firma** in stampatello (nome e cognome in maiuscolo)
- Orari in formato 24 ore (`15:00`)
- **Output**: PDF scaricato come `NOME COGNOME gg-mm-aaaa.pdf`, con anteprima

## Uso

1. Scarica o clona il repository.
2. Apri `index.html` con un browser (Chrome, Edge, Firefox, Safari).
3. Compila i campi e premi **Genera PDF**.

## Struttura

```
index.html          interfaccia e logica di compilazione
modulo.pdf          modulo originale usato come sfondo
data/comuni.js      elenco regioni, province e comuni italiani
data/modulo.js      modulo PDF incorporato (base64) per l'uso da file locale
data/fonts.js       font Roboto incorporato (base64)
lib/pdf-lib.min.js  libreria per scrivere sul PDF
lib/fontkit.umd.min.js  supporto font personalizzati per pdf-lib
```

## Come funziona

Il modulo PDF non ha campi compilabili, quindi l'app disegna testo e croci sopra il PDF originale nelle coordinate esatte di ogni casella, usando [pdf-lib](https://pdf-lib.js.org/). Se il modulo cambia layout, vanno aggiornate le coordinate in `index.html` (costanti `COL`, `ROW_TOP`, `DESC_LINES` e le posizioni usate in `genera()`).

## Crediti

- [pdf-lib](https://github.com/Hopding/pdf-lib) e [@pdf-lib/fontkit](https://github.com/Hopding/fontkit) (MIT)
- Font [Roboto](https://fonts.google.com/specimen/Roboto) (Apache 2.0)
- Elenco comuni da [matteocontrini/comuni-json](https://github.com/matteocontrini/comuni-json) (dati ISTAT)

## Nota

Il modulo originale appartiene al suo titolare: verifica di poterlo includere nel repository prima di renderlo pubblico.
