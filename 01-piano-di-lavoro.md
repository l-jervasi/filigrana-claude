# Piano di lavoro — Articolo sulla filigrana di Claude

## Obiettivo
Articolo **analitico/di opinione** (non spiegone di cronaca) sul sistema di
filigrana del testo di Claude e sull'obbligo dell'AI Act (Art. 50), scritto
dalla prospettiva di uno sviluppatore.

- **Lingua:** italiano, direttamente (niente giro inglese→traduzione in fase di
  elaborazione).
- **Pubblico:** lettore tecnico / semi-tecnico, dato per competente ma **non
  necessariamente specialista di watermarking** (calibro: "il me di tre giorni
  fa" — capisce se glielo spieghi bene, ma non lo sa in partenza).
- **Perché ancora vale scriverlo:** lo spiegone di cronaca è saturo (Forbes,
  TechCrunch, Axios, ecc.) e superato dal FAQ ufficiale Anthropic del 14 ago.
  Restano freschi: l'asimmetria legale (Piano 4), la sintesi "onere sull'onesto"
  (Piano 6), e l'angolo codice a due assi (Piano 3). Finestra stretta: ogni
  giorno un altro angolo viene preso da altri.

## Principi guida (vincoli non negoziabili)
1. **Vero e dimostrabile, non inattaccabile.** La magnitudo si dichiara dove è
   ignota; le controparti (le difese di Anthropic) stanno *dentro* il testo, non
   escluse; i buchi si nominano. Preferire claim **falsificabili**.
2. **Fonti verificate alla fonte primaria**, non prese di seconda mano. I dati
   vivi (detector, studi recenti) si ri-verificano prima della pubblicazione.
3. **Claude è affidabile su struttura e prima stesura, NON come fonte di verità
   sui fatti live.** Tutto ciò che è fattuale passa dal gate dell'autore.
4. **Voce italiana = dell'autore** (per la titolarità). Il giro di
   ri-traduzione finale è staccato e da decidere in un secondo momento.
5. **Registro:** entrare da un fatto che ogni dev possiede già, introdurre
   l'attrito come domanda naturale, guadagnare il vocabolario tecnico riga per
   riga, zero didattica introduttiva. Per il lettore tecnico la ritenzione =
   precisione mostrata presto, non gancio vago.

## Flusso di lavoro (chi fa cosa, con i gate)
| # | Fase | Claude | Autore | Gate |
|---|------|--------|--------|------|
| 1 | Ricerca e verifica fonti | recupera i documenti primari, prepara le schede (frase esatta, fonte, data, stato di revisione) | valida cosa entra | ✅ autore |
| 2 | Tesi e claim | mappa ogni claim alla fonte con lo stato (confermato/aperto/entità ignota) | fissa tesi e lista claim | |
| 3 | Schema | propone la sequenza per il lettore | sega e riordina | |
| 4 | Bozza in italiano | stende (default) | revisione pesante di sostanza | |
| 5 | Revisione di sostanza | dove segnali un buco, ristruttura o riporta alla fonte | verifica: vero? coerente? controparti dentro? magnitudo dichiarata? | ✅ autore |
| 6 | Paragrafi e ritmo | segnala dove il lettore molla | decide i tagli | |
| 7 | Verifica finale + disclosure | affianca | ri-controlla i dati vivi + riga sull'uso di Claude | ✅ autore |

*(Opzionale, differito: giro di ri-traduzione per la voce d'autore — da decidere.)*

- **Gate 1, 5, 7:** il controllo passa all'autore e non si avanza senza ok —
  perché sono i punti dove Claude è debole (fatti live) e l'autore forte
  (dominio, spirito critico).
- **Retroazione:** se al Piano 5 salta un claim non supportato, si torna al
  Piano 1 per quella fonte. Flusso a strati con ritorno, come sul codice.

## Nota su agenti/skill
Costruire la skill riusabile **dopo** il primo articolo, come residuo di ciò che
ha funzionato — non prima, quando il processo lo si sta ancora indovinando.
Scrivi prima, astrai dopo. La skill deve codificare il *processo* (es. "per ogni
claim vivo, ri-verifica alla fonte"), mai i *fatti* (che marciscono in giorni).
Eventuale agente solo se stretto e a monte del gate (fetch + schede), mai uno
che scrive in autonomia saltando il controllo dell'autore.
