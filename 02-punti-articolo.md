# Punti dell'articolo — stato rivisto con i nuovi dati

> Ogni punto porta il suo **stato**: confermato / aperto / rischio-non-fatto /
> da-verificare. Dove serve, è indicata la **controparte** (difesa di Anthropic)
> da tenere dentro il testo.

> **BARICENTRO = B** (vedi `04`): il tecnico è **biglietto magro**, non il centro.
> Il peso vero sta su **P4 (legale)** e **P6 (sintesi)** — la parte fresca. Soglia
> sdoppiata: **P2 ~250** (biglietto, parte già spesa come apertura) · **P3 ~350**
> (contenuto fresco, primo caso di fragilità). Metro: ogni frase tecnica deve
> agganciarsi a un pilastro di P4 o P6, altrimenti è spiegone e si taglia.

---

## Piano 0 — Smontare il video (aggancio possibile)
Le affermazioni virali e le correzioni, ora dalla fonte primaria (post Anthropic
14 ago):
- "caratteri invisibili" → **falso**: niente è aggiunto, nessun carattere
  nascosto; è statistico.
- "correggi un tuo testo e diventa tutto suo" → **falso**: sul proofreading
  quasi tutte le parole restano dell'autore, il marchio ha poco/niente a cui
  attaccarsi.
- "da ora, tutto" → **falso**: solo modelli post-2 ago 2026; i precedenti in
  transizione.
- *Editoriale:* l'aggancio è una scelta. Alternativa all'apertura-debunk: aprire
  dal punto di attrito tecnico (vedi schema). Piano movibile/tagliabile.

## Piano 1 — Cos'è (impalcatura, non centro)
SynthID-Text a tournament sampling, **confermato da Anthropic + primaria Nature**;
**non tocca i logit**: i candidati si campionano ancora dalla distribuzione del
modello (sampling reale), poi chiave+contesto **selezionano il vincitore** — un
**bias fisso sovrapposto** al sampling, NON "al posto del generatore". Niente
caratteri nascosti. Solo quanto basta a montare il Piano 2.
**Stato: confermato (primaria Nature, Algoritmi 1-2/Methods).**

## Piano 2 — Claim tecnico *(biglietto magro ~250 — sblocca P6, NON gonfiare)*
> Ruolo: il claim più forte per solidità, ma nel pezzo è **biglietto**, non
> sezione. Serve solo il fatto che sblocca P6 (sampling reale + selezione a chiave
> fissa = output meno vario, segnale piantabile); il resto sotto resta materiale
> di riserva/nota, e parte è già l'**apertura**. Vedi baricentro in `04`.

Sotto **chiave fissa** l'entropia/diversità effettiva dell'output **cala** —
direzione certa, **entità non pubblicata**.
- **Meccanismo (primaria Nature, Alg. 1-2):** i candidati si campionano da p_LM;
  chiave+contesto (finestra H=4) fissano un g-value binario (Bernoulli 0.5) per
  token — ~metà vocabolario "verde" — e il torneo tira il vincitore verso i verdi.
  Chiave fissa → stesso bias a ogni run → la diversità inter-risposta cala. NON
  "sorgente sostituita": è un **dado truccato sempre nello stesso verso**.
- Frase corretta: NON "l'entropia della distribuzione cala". Dire *"la diversità
  inter-risposta / l'entropia effettiva dell'output sotto l'unica chiave fissa
  cala"* — misurata come riduzione di diversità inter-risposta (Self-BLEU) nel
  paper Nature.
- "Non-distorsivo" = garanzia **in aspettazione sulle chiavi**, NON sulla tua
  singola istanza sotto l'unica chiave.
- Il tournament sampling evita il **determinismo pieno** del Gumbel-max ingenuo,
  ma riduce comunque la diversità (Nature: "some reduction to inter-response
  diversity").
- **Controparte da mettere dentro:** non-distorsivo in aspettazione; A/B su 20M
  risposte Gemini senza differenza significativa; valutatori umani senza
  differenza. → Riguardano la **qualità percepita per singola risposta**, NON la
  diversità inter-risposta: grandezze diverse.
- **Leva:** il paper Nature afferma non-distorsione E riduzione di diversità —
  convivono solo perché significano cose diverse (media-sulle-chiavi vs istanza a
  chiave fissa). L'analogia pi/Monopoly del post Anthropic descrive una
  sostituzione *deterministica* che, letta stretta, dà ragione alla riduzione di
  varietà mentre la prosa la nega. **Cautela (post-primaria):** quell'analogia
  **sovrastima il determinismo** rispetto al meccanismo vero (selezione biased su
  candidati stocastici, pareggi a caso) → usarla è a doppio taglio; meglio
  appoggiarsi al **meccanismo reale** ("dado truccato"), che già dà la conclusione
  ed è più difendibile.
**Stato: direzione confermata alla primaria (Nature: meccanismo Alg. 1-2 +
non-distorsione in aspettazione + riduzione diversità); entità aperta (config di
Claude non pubblicata). È il claim falsificabile → il più forte.**

## Piano 3 — Codice (angolo dev, a DUE assi) *(contenuto fresco ~350 — paga il suo spazio)*
> Ruolo: NON digressione tecnica ma **primo caso concreto di fragilità** → è già
> mezza dimostrazione di P6. Qui il tecnico È argomento, quindi merita le ~350.
> *(rivisto due volte)*
- **Asse visibilità:** il marchio è empiricamente **debole** sul codice a bassa
  entropia — *letteratura indipendente*, non parola di Anthropic: la quota di
  token marcati cala con l'entropia, z-score di rilevazione piccolo; ed esiste
  un intero filone ("Can we Watermark Low-Entropy Outputs?", HeavyWater/
  SimplexWater, schemi code-specifici) *proprio perché* gli schemi standard sono
  deboli sul codice. L'esistenza del problema è la prova.
- **Asse entropia/distorsione** *(aggiunta dell'autore):* il tradeoff
  rilevabilità↔distorsione è **peggiore** a bassa entropia — per estrarre un
  segnale devi consumare una frazione maggiore della poca entropia, quindi la
  distorsione *per bit* sale. Morde nella fascia **intermedia** (naming, scelte
  strutturali minori, wording dei commenti), non all'estremo quasi-deterministico
  (`2+2=4`, dove marchio e distorsione → 0).
- **L'accoppiamento (il grimaldello):** a bassa entropia non puoi avere insieme
  distorsione trascurabile E marcatura significativa — stessa risorsa. O lo
  schema **si astiene** (no marchio, no distorsione) o **forza** (marchio,
  distorsione sproporzionata). Quindi "effetto trascurabile sul codice" è
  *logicamente la stessa frase* di "il codice è a malapena marchiato": la
  rassicurazione su un asse è una confessione sull'altro.
- Il residuo si concentra in **commenti/naming**, rimovibili (comment-removal è
  una vulnerabilità nota).
- **Aperto:** quale comportamento (astensione vs forzatura) sceglie la config di
  Claude non è pubblicato; magnitudo esatta per Claude non misurata (detector
  non pubblico).
**Stato: direzione solida (letteratura indipendente); entità aperta; argomento
dell'accoppiamento logicamente stretto.**

## Piano 4 — Legale (asimmetria copyright↔responsabilità) *(portante, rivisto)*
- **Responsabilità:** cade sempre sull'umano che pubblica (l'IA non è soggetto
  giuridico). Il post Anthropic conferma: il marchio non cambia proprietà,
  authorship né responsabilità legale.
- **Copyright — NON "lo perdi".** Un testo sotto-soglia non era tuo comunque. Il
  danno reale *(correzione dell'autore)* è l'**inversione dell'onere della
  prova**: il copyright nasce automatico e per presunzione — nessuno ti chiede
  di provare che un testo a tua firma è tuo. La filigrana crea un segnale
  interrogabile che *invita la domanda* "quanto ci hai messo di tuo?" — domanda
  che senza marchio non esisterebbe. Colpisce **anche l'autore pienamente
  legittimo** (90% suo, Claude rifinisce), che può dover *provarlo* se contestato.
- **Base legale confermata (vedi `03`, verificata alla primaria):** copyright
  automatico (Berne 5(2); USA § 408(a)); presunzione di paternità *salvo prova
  contraria* (Berne 15(1); UE Dir. 2004/48 Art. 5; USA § 410(c), agganciata alla
  registrazione); onere sull'accusatore (Feist: ownership + copying). **Precisione
  che tiene il claim vero:** la presunzione è **rebuttable**; il marchio non
  attacca il nome, **fabbrica materiale interrogabile** offribile come *proof to
  the contrary* sulla soglia **paternità-umana/originalità**. Quindi la domanda
  "quanto è tuo?", di norma mai posta, diventa ponibile. NON "perdi il copyright",
  NON "prova che è tuo": *crea le condizioni perché la soglia venga interrogata*.
- Il marchio è **inerte** per proprietà/responsabilità (diritto sostanziale),
  **vivo** sul piano probatorio. Anthropic conferma il sostanziale; l'osservazione
  vive sul probatorio, intatto. Cita-e-ribalta in una riga.
- Tenere distinto: titolarità-dell'output vs battaglia training/fair-use (split a
  tre tra giudici distrettuali, irrisolto).
- **Limite onesto:** quanto morda dipende da una **prassi legale che ancora non
  esiste** — nessun tribunale ha chiesto di provare l'apporto umano *sulla base
  di una filigrana*. Scrivere come **rischio strutturale creato dallo strumento**,
  non come fatto. "Crea le condizioni perché la domanda venga posta" = dimostrabile;
  "ti verrà chiesto di provarlo" = previsione, da marcare come ipotesi.
- **Rimedio:** tracciabilità del processo (bozze, cronologia, prompt) —
  documentare sé stessi, non nascondere l'IA. Non è consulenza legale; materia
  in movimento, varia per giurisdizione.
**Stato: meccanismo solido; entità dipende da prassi non ancora formata (rischio,
non fatto).**

## Piano 5 — Paradosso della verifica
- **Detector non ancora pubblico** (Anthropic: "presto", dettagli in
  lavorazione — confermato 14 ago, primaria). Fatto controllabile.
- Quando esce, fa da **oracolo di evasione** (detector pubblico = banco di prova
  per la rimozione). I "quattro centesimi": è il costo di una passata di parafrasi
  per strippare, NON il prezzo del detector — ed è lo scenario meno interessante;
  l'evasione vera è **gratis** (modello open = mai marchiato; riscrittura vera =
  marchio dissolto). Non aprire dal prezzo: il punto è che aggirarlo è gratis.
- **Daubert:** studio forense (lug 2026) — il watermarking di testo attuale non
  supera lo standard Daubert (non è prova utilizzabile in tribunale). ⚠️
  DA RI-VERIFICARE ALLA FONTE PRIMARIA (viene da riporti secondari).
- **Trilemma del detector:** chiuso → il pubblico non verifica (no trasparenza);
  aperto → banalmente aggirabile (no robustezza); semi-aperto (solo piattaforme
  fidate) → la verifica diventa un privilegio, non trasparenza pubblica — scuola/
  datore hanno il verdetto su di te, tu no. Il terzo è il più probabile e il più
  inquietante.
**Stato: detector-non-pubblico confermato (primaria); oracolo/Daubert da riporti
secondari → RI-VERIFICARE.**

## Piano 6 — Sintesi / tesi *(portante — chiusura)*
- Il marchio non ti espropria né ti incolpa da solo: rende **visibile quanto ci
  sei tu**. Poco tu → niente copyright (ma la responsabilità resta); tanto tu →
  titolo e voce tuoi, marchio che sbiadisce.
- L'obbligo grava **tutto sull'onesto**: modello open = zero marchio, riscrittura
  vera = zero marchio, solo l'utente passivo resta marchiato. Aggirarlo è gratis.
- Un sistema di trasparenza che punge l'onesto e sfiora chi lo vuole aggirare.
  L'esatto rovescio del panico del TikTok.

## Piano 7 — Mossa meta (opzionale, contingente)
L'articolo dichiara il proprio processo (outline dell'autore, bozza di Claude,
italiano dell'autore); la scomparsa del marchio via riscrittura genuina
*dimostra* la tesi invece di essere uno stunt. Contingente sulla decisione del
giro di ri-traduzione (differita).

---

## Ordine per il lettore (dallo schema di ritenzione)
1. **Apertura** da un fatto che ogni dev possiede: a temperatura, l'output cambia
   a ogni run = campionamento casuale.
2. **Attrito** come domanda naturale: il dado c'è ancora, ma la chiave (fissa) lo
   trucca sempre nello stesso verso → che fine fa la varietà dell'output?
3. **Tecnico** (1→2→3) come *risposta a una domanda già piantata*, non pedaggio.
4. **Salita** legale (4) + verifica (5).
5. **Chiusura** sintesi (6).

**Portanti: 2, 4, 6.** Cornice movibile/tagliabile: 0, 7. Se si taglia per
lunghezza, i portanti restano e il resto si comprime.
