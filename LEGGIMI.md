# FemiaStyle — gestionale per il salone

Web app installabile su tablet, PC e telefono. I dati stanno in un Foglio Google del salone; l'app è ospitata gratis su GitHub Pages. Costo mensile: zero.

## Cosa c'è nella cartella

| File | A cosa serve |
|---|---|
| `index.html` | L'app |
| `manifest.json`, `sw.js`, `icon-*.png` | Installazione come app e funzionamento senza internet |
| `Code.gs` | Il "ponte" tra l'app e il Foglio Google (va incollato in Apps Script, **non** serve su GitHub) |

## 1. Il Foglio Google (10 minuti)

Meglio farlo con l'account Google **del salone**, così i dati sono loro.

1. Crea un Foglio Google vuoto, chiamalo per esempio "FemiaStyle – dati salone".
2. Menu **Estensioni → Apps Script**. Cancella il codice che c'è e incolla tutto `Code.gs`. Salva.
3. In alto scegli la funzione **setup** e premi **Esegui**. Google chiede le autorizzazioni: accetta (il messaggio "app non verificata" è normale, perché lo script è vostro: *Avanzate → Vai a…*). Nel Foglio compaiono le schede Clienti, Vendite, Righe, Prodotti, Movimenti, Servizi, Operatori, Formule, Appuntamenti.
4. Cambia il PIN: in cima a `Code.gs` scrivi il PIN scelto in `NUOVO_PIN`, salva, esegui **cambiaPin**. Il PIN iniziale è 1234.
5. **Esegui il deployment → Nuovo deployment → App web**.
   - Esegui come: **Me**
   - Chi ha accesso: **Chiunque**
   Copia l'indirizzo che finisce con `/exec`. Se lo apri nel browser deve dire "Il collegamento funziona".

"Chiunque" vuol dire che l'indirizzo risponde a chi lo conosce, ma senza il PIN non legge né scrive nulla. Dopo 10 PIN sbagliati si blocca per 10 minuti.

## 2. Pubblicare l'app su GitHub Pages

1. Nuovo repository su GitHub (per esempio `femiastyle`), carica `index.html`, `manifest.json`, `sw.js` e le tre icone.
2. **Settings → Pages → Branch: main / root → Save**. Dopo un minuto l'app è su `https://<utente>.github.io/femiastyle/`.

Il repository contiene solo il codice: i dati dei clienti non passano mai da GitHub.

## 3. Installarla su ogni dispositivo

- **Tablet o telefono Android (Chrome):** apri l'indirizzo → menu ⋮ → *Installa app*.
- **iPad o iPhone (Safari):** tasto Condividi → *Aggiungi alla schermata Home*.
- **PC Windows o Mac (Chrome o Edge):** apri l'indirizzo → icona di installazione nella barra degli indirizzi (o menu → *Installa FemiaStyle*). Si apre in una finestra sua, come un programma.

Poi in **Impostazioni** dell'app: incolla l'indirizzo `/exec`, scrivi il PIN, premi **Collega**. Va fatto una volta per dispositivo.

## Come si usa in negozio

Al primo avvio parte un **tutorial** con delle finestrelle che mostrano ogni parte dell'app. Si può spuntare "Non mostrare più il tutorial all'avvio" e rifarlo quando si vuole da *Impostazioni → Tutorial*. Vale per ogni dispositivo.

- **Agenda:** si apre sulla settimana, con una colonna per Enzo, Sandra e Valeria in ogni giorno: lo spazio bianco è libero. Le frecce grandi cambiano settimana, il tasto *Giorno* (o un tocco sulla data) apre il giorno nel dettaglio. *Cerca posto* trova i primi orari liberi per i servizi scelti. Per prenotare tocchi uno spazio libero, scegli la cliente (o scrivi il nome di una nuova) e i servizi: durata e prezzo arrivano dal listino.
- **Durante il giorno:** dall'appuntamento tocchi *È arrivata*, poi *Incassa*: si apre lo scontrino già compilato.
- **Chiusura giornata (dalle 19:30):** compare il tasto *Inizia*. Passa solo le clienti prenotate per il giorno e non ancora incassate, una alla volta. Se era segnata *Arrivata* chiede quanto ha pagato; se no, chiede prima se è venuta e poi il prezzo. Puoi anche segnare la tinta usata, rimandare (*Decido dopo*) o aprire la cassa completa. Alla fine mostra l'incasso del giorno da confrontare con la chiusura del registratore. Quelle non confermate restano e te le richiede dopo.
- **Promemoria:** sotto l'agenda c'è la lista delle clienti del prossimo giorno di apertura, con il tasto WhatsApp e il messaggio già scritto con giorno e ora.
- **Nuova vendita:** scegli la cliente, tocca i servizi e i prodotti, aggiungi la tinta usata (in ml), scrivi la formula di oggi. Premi *Registra*: l'app mostra l'importo da battere sul registratore telematico. Lo scontrino fiscale resta quello di sempre.
- **Conti aperti:** in cassa (e nella chiusura giornata) si sceglie *Pagato tutto*, *Una parte* o *Paga dopo*. Quello che resta si segna nella scheda della cliente ("Deve ancora pagare") e in Oggi sotto *Da incassare*. Quando paga: scheda cliente → *Registra pagamento*; l'app dice quanto battere sul registratore.
- **Magazzino:** tinte e ossidanti scalano da soli a ogni vendita. *Carico* quando arriva la merce, *Conta* per correggere dopo un inventario. Funziona con il lettore di codici a barre (fa da tastiera).
- **Clienti:** storico, spesa totale, ogni quanto vengono, formule colore, allergie, prova di tolleranza. Il tasto WhatsApp apre il messaggio già scritto.
- **Oggi:** incasso, prodotti da riordinare, clienti da richiamare, compleanni.

Senza internet l'app continua a funzionare: le modifiche partono appena torna la connessione. Più dispositivi si aggiornano tra loro ogni 2 minuti e ogni volta che riapri l'app.

## Google Calendar (facoltativo)

Gli appuntamenti si copiano da soli in un calendario Google **"FemiaStyle"**, nell'account del salone. Il collegamento va in una sola direzione: si prenota e si sposta sempre dall'app, il calendario serve per vedere gli appuntamenti sul telefono e ricevere le notifiche.

1. Al PC del negozio apri il Foglio → **Estensioni → Apps Script**, sostituisci tutto il codice con il nuovo `Code.gs` e salva.
2. In alto scegli la funzione **attivaCalendario** e premi **Esegui**. Google chiede il permesso di usare Calendar: accetta (*Avanzate → Vai a…*). Il calendario viene creato e ci finiscono gli appuntamenti già prenotati.
3. **Esegui il deployment → Gestisci deployment → matita → Versione: Nuova versione → Esegui il deployment.** L'indirizzo resta lo stesso, non serve ricollegare i dispositivi.
4. Per vederlo sui telefoni di Enzo, Sandra e Valeria: in Google Calendar (dal PC) → impostazioni del calendario "FemiaStyle" → **Condividi con persone specifiche** → aggiungi la loro email con "Visualizzare tutti i dettagli degli eventi". Non renderlo mai pubblico.

Ogni evento ha nome e iniziale del cognome della cliente, i servizi e chi li fa, con un colore per persona. Gli appuntamenti annullati spariscono dal calendario, quelli non venuti restano con "(non venuta)". Se cambi nomi nel listino, puoi aggiornare tutto eseguendo **sincronizzaCalendario**. Per spegnere il collegamento: **disattivaCalendario**.

## Cose da sapere

- **Privacy:** nome, telefono e storico servizi servono a fare il lavoro: basta il cartello con l'informativa alla cassa, senza firme. Chi vuole offerte, auguri e messaggi "ti aspettiamo" firma il mini-modulo e nella scheda si spunta "consenso ai messaggi promozionali": solo queste clienti compaiono tra i compleanni e le clienti da richiamare, e solo a loro l'app propone quei messaggi. I promemoria degli appuntamenti si mandano a tutte. Le allergie di base non si annotano (sono dati sulla salute): si attivano in *Impostazioni* solo con il modulo completo firmato. Il Foglio non va condiviso con nessuno fuori dal salone.
- **Backup:** Fogli Google tiene la cronologia delle versioni (*File → Cronologia versioni*). Ogni tanto conviene anche *File → Scarica → Excel*.
- **Analisi:** i dati sono normali tabelle nel Foglio, puoi farci tabelle pivot e grafici.
- **Uomo e donna:** nel listino ogni servizio è *Donna*, *Uomo* o *Tutto lo staff* (per esempio il taglio corto donna, che fa anche Enzo). Anche ogni persona dello staff ha il suo reparto: quando scegli Enzo vedi per primi i servizi da uomo, con Sandra e Valeria quelli da donna. *Cerca posto* con "Chiunque" propone per i servizi da uomo solo chi fa uomo, e viceversa.
- **Listino:** al primo `setup` il Foglio si riempie con il listino del salone (19 servizi, dal cartello). Dove il prezzo varia (es. shampoo e piega 18–25 €) l'app propone il minimo e si corregge al momento. Le durate sono stime: correggetele da *Listino e staff*.
- **Orari:** di base martedì–sabato dalle 8:30, nessuna pausa segnata (gli orari sono flessibili), agenda aperta fino alle 21 per gli appuntamenti della sera. Apertura, ultimo orario, pausa, ora della chiusura giornata e giorni di apertura si cambiano in *Impostazioni*. Ogni appuntamento occupa chi lo fa per tutta la sua durata. Se un giorno volete prendere un'altra cliente durante la posa del colore, si attiva in *Impostazioni* (poi nel listino si indicano i minuti di posa).
- **Aggiornare l'app:** carica il nuovo `index.html` su GitHub; i dispositivi lo prendono alla riapertura. Se cambi `Code.gs`: *Gestisci deployment → modifica → Versione: nuova*, così l'indirizzo resta lo stesso.
- **Non rinominare** le schede del Foglio né le intestazioni delle colonne. Spostare le colonne o aggiungerne di tue invece va bene.
