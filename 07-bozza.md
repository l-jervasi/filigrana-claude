# 07 — Bozza (fase 4)

> Iniziata il **19 ago 2026**. Prosa vera, italiano diretto (voce dell'autore).
> Cresce sezione per sezione seguendo l'arco di `06`. **Per ora: solo l'apertura**
> — campione per calibrare voce + consegne (decisione 4 dello schema).

---

## Apertura *(~280)*

Se chiedi due volte la stessa cosa a un modello linguistico, con la temperatura sopra
lo zero, ottieni due risposte diverse. Lo sai già: a ogni parola il modello non prende
la più probabile, ne pesca una dal mazzo secondo le probabilità. È un dado. Ed è quel
dado a rendere l'output vario — a volte sorprendente.

La filigrana di testo di Claude non toglie il dado. Lo trucca. A ogni tiro aggiunge una
spinta invisibile, sempre nello stesso verso, verso un sottoinsieme di parole scelto da
una chiave segreta e dal contesto. Il dado gira ancora, ma cade un po' più spesso dove
vuole la chiave. Ripeti la generazione mille volte e mille volte la spinta è identica:
le risposte si somigliano di più. Da quella somiglianza, statisticamente, un rilevatore
può capire che il testo è uscito da lì.

Fin qui è una curiosità tecnica. Il punto scomodo arriva adesso, ed è dove la faccenda
smette di essere astratta e diventa tua.

Quella spinta lascia un'impronta che non hai scelto e non puoi vedere. E l'impronta
resta addosso a chi il testo lo *tiene* — tu, che l'hai scritto, fatto rifinire, e lo
pubblichi così com'è. Non resta addosso a chi lo *riscrive* daccapo, né a chi non l'ha
mai marchiato. Il segnale pensato per la trasparenza si attacca all'onesto e scivola via
da chi vuole liberarsene.

È il contrario di quello che l'allarme popolare ha raccontato. Non ti stanno rubando il
testo. Ti stanno mettendo addosso un onere — e proprio a te.

## Tecnico *(P2, ~150 — biglietto magro)*

Torniamo al dado, perché la sua stranezza spiega il resto. La spinta della chiave non
*sostituisce* il caso: i candidati per ogni parola si pescano ancora dalla distribuzione
del modello — è la scelta tra loro a essere truccata. Per questo Anthropic può dire, con
ragione, che il metodo è "non distorsivo": *in media su tutte le chiavi possibili* la
distribuzione dell'output resta quella di sempre. Ma tu non usi tutte le chiavi. Ne usi
una, fissa — e sotto un'unica chiave fissa quella garanzia non ti riguarda: la varietà
tra una tua risposta e l'altra cala, nel verso deciso dalla chiave. Di quanto, non lo
sappiamo: la configurazione di Claude non è pubblica. La direzione è certa, l'entità no.
E gli A/B test che Anthropic cita misurano la qualità di *una* risposta, non la varietà
*tra* risposte — due cose diverse. Quanto margine ci sia da spendere, però, dipende da
quanta varietà c'era in partenza. In certi testi è pochissima. Nel codice, per esempio.

## Codice *(P3, ~380 — primo caso concreto di fragilità)*

Il codice è testo a bassa entropia. In gran parte non c'è scelta: dopo `for (int i = 0;`
la parentesi va chiusa, `2 + 2` fa `4`, il nome di una variabile appena dichiarata va
ripetuto identico. Dove non c'è varietà non c'è dado — e senza dado non c'è niente da
truccare.

Che il marchio sia debole sul codice, però, non conviene prenderlo dalla parola di
Anthropic: lo dice la letteratura indipendente. Misurato, il segnale sul codice è fiacco
— pochi token "verdi", z-score di rilevazione piccolo — e la quota marcata scende man
mano che scende l'entropia. Esiste perfino un filone di ricerca dedicato a marcare gli
output a bassa entropia: esiste *perché* gli schemi standard, sul codice, non ce la
fanno. L'esistenza del problema è la prova.

Anthropic la mette così: sul codice l'effetto è trascurabile, il marchio semmai si
annida nei commenti. Vero — e proprio per questo è una confessione, non una
rassicurazione. A bassa entropia marchio e distorsione sono la stessa risorsa: o lo
schema si astiene, e non marca; o forza, e spende la pochissima varietà disponibile
piegando una scelta che il modello avrebbe fatto diversa — cioè distorce. Non c'è una
terza via, "un po' di marchio a costo trascurabile": al pavimento dell'entropia,
*toccarlo lo altera, non toccarlo non lo segna*. Così "effetto trascurabile sul codice"
e "il codice è a malapena marchiato" dicono la stessa cosa con due facce diverse. E lo
ammette lo stesso paper originale di SynthID: quando la distribuzione è quasi certa, il
torneo può solo scegliere i token che il marchio favorisce — cioè contro la scelta
naturale del modello.

L'identità vale al pavimento. Appena l'entropia sale un po' — il nome di una variabile,
la formulazione di un commento — torna un margine, e lì il poco marchio che resta si
concentra. Ma è margine fragile: i commenti si tolgono, i nomi si cambiano, e il segnale
se ne va senza toccare una riga di logica. Quanto ne resti esattamente nel codice di
Claude non lo sappiamo — il rilevatore non è pubblico, nessuno l'ha misurato. La
direzione, però, è chiara, e punta sempre nello stesso verso: dove conta la precisione
il marchio quasi non c'è; e dov'è, si stacca.

## Legale *(P4, ~600 — la sezione più grande, il peso)*

Mettiamo che il marchio, invece, resti — su un testo in prosa, dove l'entropia è alta e
il segnale tiene. Cosa ti fa, davvero?

Meno di quel che si teme, e insieme qualcosa di più insidioso. Anthropic è esplicita, e
ha ragione: il marchio non cambia la proprietà del testo, non cambia chi ne è l'autore,
non sposta la responsabilità legale. Sul piano del diritto sostanziale è inerte. Il
copyright sul tuo testo nasce come prima: in automatico, nel momento in cui lo scrivi,
senza deposito né registrazione — è così da Berna in poi, e lo ribadisce il codice
americano quando dice che la registrazione "non è condizione della protezione". E nasce
*presunto*: chi mette il proprio nome su un'opera è considerato l'autore salvo prova
contraria — lo dicono con le stesse parole la Convenzione di Berna e la direttiva europea
sull'enforcement. In un'eventuale causa l'onere sta sull'accusatore: è chi ti contesta a
dover provare la copia, non tu a dover provare di aver scritto.

Qui sta il punto, e non è la perdita del copyright. È che il marchio incrina proprio
quella presunzione. Nessuno, di norma, ti chiede di dimostrare che un testo a tua firma è
tuo: la domanda non esiste. Il marchio la fa esistere. Crea un segnale interrogabile — un
dato che qualcuno può tirare fuori e mettere sul tavolo — che invita una domanda precisa:
*quanto, di questo, ce l'hai messo tu?* È la soglia dove il diritto d'autore si gioca
davvero: non "hai usato l'IA", ma "c'è abbastanza di umano da meritare protezione". Prima
del marchio quella soglia era presunta a tuo favore, senza sforzo. Dopo, è un terreno che
ti si può chiedere di difendere.

E colpisce l'onesto più di chiunque. Non l'utente che si fa scrivere tutto dall'IA —
quello un copyright non l'aveva comunque. Colpisce chi ha scritto il novanta per cento di
suo e ha lasciato che Claude rifinisse il resto: autore legittimo, che ora porta addosso
un segnale capace di rimettere in discussione ciò che è chiaramente suo.

Va detto con onestà dove finisce il dimostrabile. Nessun tribunale, a oggi, ha chiesto a
nessuno di provare l'apporto umano *sulla base di una filigrana*. Non è un fatto: è un
rischio strutturale creato dallo strumento. Che il marchio *crei le condizioni* perché la
domanda venga posta è dimostrabile ora; che qualcuno *te la porrà* è una previsione, e
come tale va presa. Il rimedio, se mai servisse, non è nascondere l'IA: è documentare sé
stessi — bozze, cronologia, prompt — la tracciabilità del proprio processo. (Questo
articolo, mentre lo scrivo, la sta producendo.)

E c'è un ultimo giro, che pesa. Non era nemmeno obbligatorio, marcare così. La legge
europea sulla trasparenza — l'articolo che entra in vigore adesso — chiede che l'output
sia "rilevabile come generato dall'IA", ma è neutra sul come: il considerando che
l'accompagna mette tra le tecniche ammesse, alla pari, i *metadati* e i *metodi
crittografici di provenienza*. Un'etichetta staccabile, una firma allegata, un checksum:
sarebbero bastati a essere in regola. E per chi *pubblica* un testo l'obbligo è solo di
*dichiararlo* — e cade del tutto se c'è una revisione umana con responsabilità
editoriale. Le vie leggere c'erano tutte. Hanno scelto un marchio incorporato nel testo,
che sopravvive al copia-incolla e non si stacca a volontà. La lettura generosa è che
l'abbiano fatto per robustezza — la legge la incoraggia, "per quanto tecnicamente
possibile". Ma la robustezza *è* esattamente ciò che rende il marchio imposto invece che
scelto: non è più conformità, è marcatura. La domanda ovvia, a questo punto, è un'altra:
e verificarlo, almeno, si può?

## Verifica *(P5, ~420)*

Il detector, per ora, non c'è: Anthropic dice "presto". Ma il ritardo non è un dettaglio
tecnico, è il sintomo di un problema senza soluzione pulita. Perché con una filigrana
*verificare* e *aggirare* sono la stessa mossa. Il rilevatore è la funzione che, con la
chiave, riconosce l'impronta; darlo al pubblico perché ciascuno controlli significa
consegnare a chiunque l'oracolo per limare il testo finché l'impronta sparisce. È il
prezzo dell'aver scelto un marchio *dentro* il testo: una firma staccata la verifichi
senza che questo aiuti a falsificarla, ma quella muore al primo copia-incolla; il marchio
intrinseco sopravvive, e proprio per questo non può mostrarsi.

Da lì un trilemma senza uscita. Detector **chiuso**, tenuto da Anthropic: il pubblico non
verifica nulla, deve fidarsi — e la trasparenza che era il fine si riduce a un atto di
fede. Detector **aperto**: chiunque verifica, e chiunque aggira — addio robustezza.
Detector **semi-aperto**, dato solo a piattaforme "fidate" — scuole, datori, editori: la
verifica diventa un privilegio. Loro hanno il verdetto su di te; tu no. Nessuna delle tre
dà ciò per cui il sistema esisteva: una trasparenza *pubblica*.

E la terza è la più probabile, e la più insidiosa, perché quel verdetto non regge dove
conta. In Italia una lite sulla paternità è civile, e lì il giudice pesa le prove
"secondo il suo prudente apprezzamento": un segnale non validato, dal tasso d'errore
ignoto, vale poco. In sede penale la Cassazione, con la sentenza Cozzini, ha fatto propri
i criteri di affidabilità del metodo scientifico — testabilità, tasso d'errore,
revisione, accettazione — con il giudice "custode del metodo": criteri che il marchio, a
oggi, non supererebbe. È il gemello italiano dello standard americano Daubert, e la
conclusione è la stessa: un segnale che un tribunale non prenderebbe per buono, usato da
chi tribunale non è, per giudicare le persone.

La difesa esiste, ed è onesta: il rilevatore nasce come etichetta su scala di
piattaforma, non come perizia sul singolo. Vero. Ma il danno non è l'uso previsto, è il
riuso — la scuola che segnala il tema, il datore che scarta la relazione — e con i
rilevatori di IA esistenti è già la norma. E la legge stessa lo insegue: il regolamento
europeo auspica che i meccanismi di rilevazione siano "accessibili", così che il pubblico
possa distinguere. Chiede, cioè, esattamente il corno che per una filigrana è
irraggiungibile.

Resta il fatto più semplice: chi vuole liberarsene lo fa gratis — un modello aperto non
l'ha mai marchiato, una riscrittura vera lo dissolve. Il detector, quando arriverà, saprà
dire "questo l'ha scritto Claude" a chi non ha fatto nulla per nasconderlo, e tacerà su
chi l'ha riscritto. Giudica chi si è adeguato, non chi ha aggirato.

## Chiusura *(P6, ~350 — salda il loop dell'apertura)*

Adesso i pezzi stanno insieme. Il marchio non ti espropria e non ti incolpa: quello
resta vero, l'abbiamo visto. Fa qualcosa di più sottile — rende visibile quanto, in ciò
che pubblichi, ci sei tu. E su quella visibilità si regge tutto il resto.

Guardala da vicino e vedrai che il costo cade sempre dalla stessa parte, la parte
sbagliata. Chi scrive di suo e si fa aiutare a rifinire porta il marchio, e con esso la
domanda su quanto sia davvero suo. Chi vuole sottrarsi non paga niente: un modello aperto
non lo marchia, una riscrittura vera lo cancella. E quando il detector arriverà, darà il
suo verdetto su chi non si è nascosto, non su chi si è nascosto bene. Marcatura,
evasione, verifica: tre assi diversi, un solo verso. Il peso grava sull'onesto e scivola
via da chi aggira. È un sistema di trasparenza i cui costi sono inversamente
proporzionali alla colpa.

Si obietterà che l'utente onesto è proprio il destinatario voluto: rendere leggibile
l'assistenza dell'IA è lo scopo dichiarato, non un effetto collaterale. È vero, ed è
esattamente qui che la trasparenza si rovescia in altro. Un conto è dichiarare — una
nota, che l'onesto avrebbe messo comunque e che la legge gli lasciava mettere. Altro è un
marchio che gli si attacca addosso a prescindere, che sopravvive alla sua volontà, e che
serve a farlo interrogare da chi tribunale non è. Non gli avevano nemmeno chiesto di
marcare così: hanno scelto lo strumento che grava di più, sul soggetto che si difende di
meno. Non è la trasparenza che diventa sorveglianza per malizia; è che la sua forma — un
marchio imposto, e non pubblicamente verificabile — la rende, di fatto, un giudizio
sull'onesto.

È il rovescio esatto dell'allarme che ha accompagnato tutto questo. Non ti stanno rubando
il testo. Ti stanno rendendo interrogabile — proprio te, che l'hai scritto — su quanto è
davvero tuo, mentre a chi ha barato non chiedono niente.
