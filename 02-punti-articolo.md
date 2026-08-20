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
  attaccarsi. **+ base legale (Art. 50(2), primaria — vedi `03`):** l'editing
  assistito / non-sostanziale è **esente per legge** dalla marcatura del provider.
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
- **Asse visibilità:** il marchio è empiricamente **più debole (NON assente)** sul
  codice. **Calibrazione (obiezione dell'autore 21 ago):** il codice NON è entropia
  quasi-zero — la libertà (nomi, forme, algoritmi) è reale ma è del **programma**, non
  del **token**: la filigrana agisce per-token, e lì i bivi sono radi (nome scelto 1 volta
  poi ripetuto forzato a ogni uso; struttura = 1 bivio poi sintassi obbligata). Per token
  **meno appigli che nella prosa, ma non zero.** Misurato (ACL 2024, `2403.13485`, su
  **KGW**): spike-entropy codice ~0,6 vs news ~0,8; rilevazione **~68% TPR@1%FPR sul
  codice vs ~99,6% prosa**. *Letteratura indipendente*, non parola di Anthropic; ed esiste
  un filone (HeavyWater/SimplexWater, schemi code-specifici) *proprio perché* gli schemi
  standard sono deboli sul codice. **Debole, non nullo** — un 68% non è zero.
- **Asse entropia/distorsione** *(aggiunta dell'autore):* il tradeoff
  rilevabilità↔distorsione è **peggiore** a bassa entropia — per estrarre un
  segnale devi consumare una frazione maggiore della poca entropia, quindi la
  distorsione *per bit* sale. Morde nella fascia **intermedia** (naming, scelte
  strutturali minori, wording dei commenti), non all'estremo quasi-deterministico
  (`2+2=4`, dove marchio e distorsione → 0).
- **L'accoppiamento (il grimaldello) — cita-e-ribalta della loro rassicurazione:**
  la premessa *"effetto trascurabile sul codice"* è **di Anthropic** (post 14 ago),
  non nostra; il "≡" è la mossa che la ribalta. Sotto **chiave fissa**, dove restano
  poche parole plausibili e una è "verde", il torneo **spinge la scelta verso quella**
  (50/50 → ~25/75 già col torneo minimo a 2; di più con 30 layer): quella spinta **È** il
  marchio ED **è uno scarto** da ciò che il modello avrebbe scelto. Dove la parola è
  obbligata (sintassi, `2+2=4`) non c'è verde e non succede niente. Quindi **mark ⟺
  scarto**: o il codice porta scelte da marcare, e allora quelle scelte gliele pieghi; o
  non le porta, e il marchio non c'è → *"effetto trascurabile" ≡ "a malapena marchiato"*.
  ⚠️ **Bounded** (corretto 21 ago, doppio giro): NON "collassa/azzera" (troppo forte) NÉ
  "non tocca mai" (troppo debole).
- **Deduzione, NON assunzione (Nature p. 820 + chiave fissa):** il tilt **non si assume
  dalla config** (distorsiva vs non — non pubblicata): si **deduce** — la "non distorsione"
  è media su tutte le chiavi, ma la chiave è **una, fissa**, e sotto quella l'output è
  tiltato. Nature p. 820 (*"can only choose tokens that score more highly under the g
  functions"*) conferma il **debole** (poco su cui lavorare), non il "forza".
- **Quindi, ancorato al pavimento di entropia** (il grosso del codice): *"effetto
  trascurabile"* ≡ *"a malapena marchiato"* — la rassicurazione su un asse **è**
  una confessione sull'altro. NB accuratezza: l'identità è stretta **al pavimento**;
  nella tasca a entropia localmente più alta (naming, scelte minori) è **tradeoff
  ripido, non identità** — ed è lì che il residuo di marchio si concentra. Nitidezza
  del binario ∝ quanto l'entropia è bassa.
- Il residuo si concentra in **commenti/naming**, rimovibili (comment-removal è
  una vulnerabilità nota).
- **Aperto:** quale comportamento (astensione vs forzatura) sceglie la config di
  Claude non è pubblicato; magnitudo esatta per Claude non misurata (detector
  non pubblico).
**Stato: direzione solida (letteratura indipendente + ammissione Nature p. 820);
entità aperta; accoppiamento logicamente stretto **al pavimento di entropia**
(cita-e-ribalta della "trascurabile" di Anthropic); fascia naming = tradeoff
ripido, non identità.**

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
- **Art. 50 (primaria, vedi `03`):** il provider NON è obbligato al watermark
  intrinseco (pavimento = machine-readable + detectable) — e il **Recital 133 elenca
  esplicitamente metadata e metodi crittografici di provenance tra le tecniche
  ammesse**: il "checksum sarebbe bastato" è **sancito dal legislatore**, non solo
  disponibile. L'intrinseco è **scelta** (un'opzione del menu), giustificata dal
  *"robust as far as feasible"*. **Disallineamento chiave:** chi rivede con
  responsabilità editoriale è **esente dalla disclosure** (50(4) + Recital 134), ma
  il marchio marca i token lo stesso. Chi la legge esenta dal dichiarare, il marchio
  marca.
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
- **La spina — per un watermark, verificare = evadere.** Il detector *è* la
  funzione che assegna i g-value con la chiave: esporlo perché il pubblico
  verifichi = esporre l'**oracolo** che permette di limare il marchio finché
  sparisce. Non è un bug: è il **prezzo della scelta intrinseca** (Art. 50 / P4).
  Tradeoff di fondo: **intrinseco** = sopravvive al testo nudo MA verifica=evasione;
  **staccato** (checksum/C2PA) = niente oracolo MA muore al copia-incolla. Anthropic
  ha scelto l'intrinseco per robustezza → **il trilemma è il conto**. Stesso
  accoppiamento di P3, sull'asse verifica.
- **Il trilemma** (asse: *chi esegue il detector* — esaustivo: nessuno/tutti/alcuni;
  ogni corno uccide un valore diverso):
  - **chiuso** (solo Anthropic) → salta la **trasparenza** (il pubblico non
    verifica, deve fidarsi dell'oracolo);
  - **aperto** (chiunque) → salta la **robustezza** (detector pubblico = oracolo di
    evasione);
  - **semi-aperto** (solo piattaforme "fidate") → salta l'**equità/pubblicità**
    (verifica come **privilegio**: scuola/datore hanno il verdetto su di te, tu no).
  → **Nessuna config consegna trasparenza *pubblica***: l'obiettivo dichiarato è
  **strutturalmente irraggiungibile** con questo meccanismo.
- **Evasione = gratis** (rinforza il corno aperto). I "quattro centesimi" = costo di
  una passata di parafrasi per strippare, NON il prezzo del detector — scenario meno
  interessante; l'evasione vera è **gratis** (modello open = mai marchiato;
  riscrittura vera = marchio dissolto). Non aprire dal prezzo: aggirarlo è gratis.
- **Controparte dentro (per verità, non armatura):** difesa vera = *"è un segnale di
  labeling su scala di piattaforma, non uno strumento per giudicare l'individuo"*
  (uso Google/SynthID = labeling di massa). Corretta — ma allora **non è la
  trasparenza-pubblica come venduta** per il singolo autore, e il danno è il **riuso
  prevedibile** per adjudicare l'individuo (scuole/datori già lo fanno con gli
  AI-detector): nel momento in cui la scuola segnala il tema, sei nel corno
  semi-aperto.
- **Aggancio Art. 50 (confermato, vedi `03`):** l'obbligo binding (50(2)) chiede
  *"detectable as artificially generated"* ma NON *"pubblicamente verificabile"*; rinvia
  a standard/codici (50(7)) → **compatibile con i corni non-pubblici**. **Recital 135
  (primaria):** la Commissione *"may encourage"* codes of practice per rendere *"the
  detection mechanisms accessible… to enable the public to effectively distinguish"* →
  la legge **aspira** al corno pubblico, ma solo via **soft-law**, e quell'aspirazione è
  **proprio ciò che il trilemma rende irraggiungibile** per un watermark (detector
  pubblico = oracolo). La legge chiede la cosa che il meccanismo non può dare in
  sicurezza.
- **Ponte a P6:** il trilemma è la versione **sull'asse-verifica** dell'asimmetria
  di P6 — anche il detector **adjudica il conforme, non l'evasore** (che non lascia
  nulla da rilevare). Costo della verifica di nuovo **inverso alla colpa**.
  Riga-cerniera: *"trasparenza che non è pubblica non è trasparenza — è adjudicazione
  istituzionale dell'onesto."*
- **Non prova da tribunale (localizzato — primarie confermate 19 ago):** il segnale
  del detector non è *court-grade*, e vale per il lettore **italiano/europeo**, non
  solo USA.
  - **Civile** (dove vive la lite su paternità/copyright) — **Art. 116 c.p.c.**:
    *"il giudice deve valutare le prove secondo il suo prudente apprezzamento"* →
    nessun gate lo esclude, ma valutazione libera e nessuna gerarchia → un giudice
    prudente dà **poco peso** a un segnale non validato, a tasso d'errore ignoto.
  - **Penale** — **Cass. pen. sez. IV n. 43786/2010 (*Cozzini*)**: criteri Daubert-like
    (verificabilità/falsificabilità · peer review · tasso d'errore · accettazione
    generale · indipendenza dell'esperto), giudice **"custode del metodo scientifico"**
    → il marchio inciampa su tutti.
  - **Daubert** (USA, 1993) resta come *analogo di contorno*.
  - **Onestà:** Cozzini è **penale**, la lite è **civile** → citare **entrambi i
    fori**, non spacciare l'uno per l'altro; "il marchio fallirebbe i criteri" è
    **inferenza strutturale** (applico i criteri alle proprietà note), NON una
    sentenza. *(Studio forense lug-2026: DROPPATO — si ragiona dai criteri confermati,
    non serve un dato di seconda mano.)*
**Stato: detector-non-pubblico confermato (primaria); trilemma logicamente stretto
+ agganciato ad Art. 50 (primaria); verifica=evasione = prezzo dell'intrinseco
(spina). Non-prova-da-tribunale su primarie IT (Art. 116 c.p.c. + Cozzini); Daubert
USA di contorno; studio lug-2026 droppato.**

## Piano 6 — Sintesi / tesi *(portante — chiusura)*
- Il marchio non ti espropria né ti incolpa da solo: rende **visibile quanto ci
  sei tu**. Poco tu → niente copyright (ma la responsabilità resta); tanto tu →
  titolo e voce tuoi, marchio che sbiadisce.
- L'obbligo grava **tutto sull'onesto**: modello open = zero marchio, riscrittura
  vera = zero marchio, solo l'utente passivo resta marchiato. Aggirarlo è gratis.
- Un sistema di trasparenza che punge l'onesto e sfiora chi lo vuole aggirare.
  L'esatto **rovescio dell'allarme popolare**: non un *furto* del tuo testo, ma un
  *onere* su chi non lo merita. *(Scelta (b), 19 ago: sganciato dal video TikTok
  — mai sourceato — e dal Piano 0, tagliabile. La chiusura regge da sola; il
  rovescio è di sostanza: natura (furto→onere) + incidenza (tutti→l'onesto).)*
- **Base legale (Art. 50, primaria — vedi `03`):** per il testo la legge chiede
  *disclosure* (una nota), non marcatura, ed **esenta** chi rivede con responsabilità
  editoriale; Anthropic marca comunque, **oltre il pavimento**. Chiusura sviluppata in
  sessione (18 ago): **marchiatura-non-disclosure** (modello-citazione: la firma
  allegata basta all'onesto, l'intrinseco è imposto) + **asimmetria della conseguenza**
  (il costo cade *inversamente* alla colpa: onesto marchiato+esposto, evasore a costo
  zero). È la svolta nuova della chiusura, NON un recap di P4+P5.

## Piano 7 — Mossa meta (opzionale, contingente)
L'articolo dichiara il proprio processo (outline dell'autore, bozza di Claude,
italiano dell'autore); la scomparsa del marchio via riscrittura genuina
*dimostra* la tesi invece di essere uno stunt. Contingente sulla decisione del
giro di ri-traduzione (differita).
- **Nota legale (Art. 50(4), primaria — vedi `03`):** l'articolo stesso — testo di
  interesse pubblico sotto controllo editoriale dell'autore — è **esente dall'obbligo
  di disclosure**. Dichiarare il processo è quindi una **scelta** retorica/etica, non
  un dovere di legge: rafforza il Piano 7 come mossa volontaria che *dimostra* la tesi.

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
