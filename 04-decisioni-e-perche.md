# Decisioni e perché — il razionale dietro le correzioni

> Gli altri file portano le **conclusioni**. Questo porta il **perché**: la strada
> per cui ci siamo arrivati, così una sessione nuova non smonta per ignoranza un
> punto già chiuso. Ogni voce: *cosa* si è deciso e *perché quella e non l'altra*.

---

## Principio-madre: "vero e dimostrabile", NON "inattaccabile"
**Perché.** A un certo punto, per rendere una tesi "inattaccabile", Claude l'ha
spostata su un terreno più debole ("cala la diversità, non l'entropia") — cioè ha
comprato l'invulnerabilità svuotando l'affermazione. L'autore l'ha bocciato: non
vuole il bunker, vuole il punto. Regola che ne esce: si scrive ciò che è vero e
dimostrabile anche se attaccabile; l'attaccabilità apre il dibattito, e il
dibattito è giusto. Le difese di Anthropic vanno DENTRO il testo e si mostra
perché non rispondono, non si tengono fuori. **Corollario:** se una frase regge
troppo comoda, è il segnale di controllarla — vale anche contro Claude in bozza.

## Piano 2 — perché "entropia sotto chiave fissa", non "entropia della distribuzione"
**Percorso.** L'autore ha detto "l'entropia cala". Claude ha prima corretto in
"cala la *diversità*, non l'entropia" — ma era una distinzione senza differenza.
L'autore ha ribattuto: con chiave fissa al posto del seed casuale, l'entropia
dell'output **cala**, ed è un fatto. Ha ragione. **Perché la frase è quella:**
"non-distorsivo" è una garanzia *in aspettazione sulle chiavi*; Anthropic ne usa
UNA, fissa. Sotto chiave fissa la garanzia non si applica: la riduzione di
diversità inter-risposta (misurata, Nature) **è** una riduzione di entropia
dell'output, stesso fenomeno in bit invece che in Self-BLEU. **Limite tenuto:**
"cala" è certo; "di quanto" no (config non pubblicata) → scrivere direzione come
fatto, entità come ignota. Non "collassa" (quello è il Gumbel-max ingenuo; il
tournament riduce ma non azzera).
**Precisazione sul meccanismo (verificata alla primaria Nature, Algoritmi 1-2 —
aggiunta dopo la lettura del PDF):** "chiave fissa *al posto* del seed casuale" è
una scorciatoia imprecisa. La chiave **non sostituisce** il sampling: i candidati
si campionano ancora da p_LM (caso reale), e chiave+contesto (finestra H=4)
fissano un g-value binario per token (Bernoulli 0.5) → il torneo tira il vincitore
verso i token "verdi". Con chiave fissa il bias è lo stesso a ogni run → la
diversità cala. Il g binario + pareggi rotti a caso è *perché* riduce ma non
azzera. Framing corretto: **"dado truccato sempre nello stesso verso"**, non
"sorgente sostituita". La conclusione (entropia effettiva cala sotto chiave fissa)
resta intatta; cambia solo la metafora del meccanismo. *(NB: "Self-BLEU" come nome
della metrica di diversità è ancora da confermare nella Supplementary Information —
nel corpo Nature c'è "inter-response diversity" + Extended Data Fig. 4.)*

## Piano 3 — perché due assi e non "il codice è meno marchiato"
**Percorso.** Claude aveva taggato "confermato (Anthropic)". L'autore: non ho
prove che il codice sia meno soggetto; se applichi lo stesso sistema il risultato
è lo stesso. Verifica → la letteratura *indipendente* misura che il codice a
bassa entropia porta un segnale più debole (z-score piccolo), ed esiste un filone
apposta perché gli schemi standard falliscono sul codice. Quindi:
- **Perché due assi:** l'autore ha aggiunto il secondo. Asse *visibilità* (poco
  marchio) e asse *entropia/distorsione* (il tradeoff è peggiore dove l'entropia
  è scarsa) sono cose diverse; sul secondo il codice sta **peggio**, non meglio.
- **Perché "accoppiamento":** a bassa entropia marchio e distorsione sono la
  *stessa risorsa*: o lo schema si astiene (no marchio) o forza (distorsione
  sproporzionata). Quindi "effetto trascurabile sul codice" ≡ "codice a malapena
  marchiato" — la rassicurazione su un asse confessa l'altro.
- **Perché NON Anthropic come fonte:** ha interesse a rassicurare i dev; il
  sostegno regge solo se viene da terzi. Ed è più forte così, non più debole.

## Piano 4 — perché "inversione dell'onere", non "perdi il copyright"
**Percorso.** Claude diceva "rischi di non possedere il testo". L'autore ha
affilato: non è che perdi il diritto (un testo sotto-soglia non era tuo comunque),
è che nasce la **necessità di dimostrare** che il diritto è tuo — cosa che senza
filigrana nessuno ti chiederebbe. **Perché conta più della perdita:** il copyright
di norma vale per presunzione, nessuno ti fa provare che un testo a tua firma è
tuo; la filigrana crea un segnale che *invita la domanda* e colpisce **anche
l'autore pienamente legittimo** (90% suo), non solo quello marginale. **Limite
tenuto:** nessun tribunale l'ha ancora fatto sulla base di una filigrana →
scrivere come **rischio strutturale creato dallo strumento**, non come fatto.
"Crea le condizioni per la domanda" = dimostrabile; "ti chiederanno di provarlo"
= previsione (marcare come ipotesi). **Rimedio:** tracciabilità del processo
(bozze, git, prompt) = documentare sé stessi, non nascondere l'IA.

## Piano 5 — perché "aggirarlo è gratis", non "quattro centesimi"
**Perché.** I quattro centesimi sono il costo di una *passata di parafrasi* per
strippare — lo scenario più stupido (parti da testo di Claude e lo vuoi identico
ma pulito). L'evasione vera è **gratis**: modello open = mai marchiato;
riscrittura genuina = marchio dissolto. Citare il prezzo fa sembrare la barriera
più alta di quanto sia. Daubert e oracolo restano **da verificare alla primaria**.

## Compute — perché "marginale, lato Anthropic" (punto chiuso)
**Perché.** La marcatura agisce in fase di campionamento su una distribuzione già
calcolata (il forward pass lo paghi comunque): una funzione pseudo-casuale + una
selezione, niente forward pass extra, niente token fatturati. Sta sul lato
inferenza di Anthropic, non in bolletta all'utente. L'obiezione "pago io il
calcolo per marchiarmi" non regge; quella che regge è "modificano l'output e mi
fido sulla parola".

## Lunghezza — perché 2.500 (blog) e 200–300 (LinkedIn)
**Perché il numero.** Tetto = ritenzione del lettore tecnico (~10-11 min).
Pavimento = onestà: i tre portanti (2, 4, 6) hanno una sfumatura obbligatoria
(magnitudo + controparte + buco), ~400-500 parole l'uno; sotto le ~2.000 devi
tagliare un intero argomento, non limare. Quindi il budget è una **funzione di
selezione**: ~2.500 porta bene *tre* argomenti, non sei. Budget per piano
(rivisto col baricentro B, sotto): apertura+attrito ~300 *(il gancio È già P2)* ·
P2 oltre il gancio ~150 · P3/codice ~350 · legale P4 ~450 · verifica P5 ~350 ·
sintesi P6 ~300 · meta ~100 → totale ~2.000-2.200, dentro banda con margine. Il
tecnico scende rispetto alla versione A (~1.000); il peso passa a P4+P6. Se una
sezione sfonda, cede un'altra, non cresce il totale.

## Baricentro — perché B (tecnico = biglietto magro), con soglia sdoppiata
**Decisione.** Centro di gravità = **B**: il tecnico (P2/P3) fa il minimo per
reggere il resto; il peso vero sta su **P4 (legale)** e **P6 (sintesi/
inversione)**, la parte fresca. NON A (tecnico come contenuto, ~1.000 parole).
**Perché.** (1) Con A competi dove Anthropic/GPTZero hanno la primaria e tu no →
perdi in partenza. (2) Coerenza interna: la tesi è che il marchio NON è la
sostanza (P6); un pezzo che spende metà del bilancio-parole sulla meccanica del
marchio si contraddice da solo.
**La soglia è sdoppiata — P2 e P3 NON sono un blocco unico con un budget solo:**
- **P2 (~250, di cui parte è già l'apertura)** = biglietto magro puro. Serve solo
  il fatto che sblocca P6: la casualità è sostituita da una scelta a chiave →
  output meno vario, segnale piantabile. "Non-distorsivo in aspettazione vs
  istanza" resta UNA riga, non una sezione. Il gancio iniziale ("dove finisce la
  varietà se la sorgente è fissa?") È già P2, quindi non costa budget due volte.
- **P3 (~350)** = contenuto fresco che paga il suo spazio. Non digressione
  tecnica ma **primo caso concreto di fragilità** (codice a bassa entropia = poco
  marchio = mezza dimostrazione di P6). Qui il tecnico È argomento.
**Rischio da evitare (non quello che sembra):** non "troppo poco tecnico per
reggere il legale", ma **piantare un solo seme e credere basti**. P4 e P6 poggiano
su pilastri diversi: P4 ha bisogno che si capisca *marchio = processato, non
scritto, e scatta anche sul poco*; P6 ha bisogno che si capisca *marchio fragile/
aggirabile*. Il biglietto magro deve piantarli **entrambi**.
**Metro operativo:** ogni frase tecnica deve agganciarsi a un pilastro di P4 o P6.
Se spiega la meccanica senza servire legale o sintesi → è spiegone, si taglia.
Non "quanto tecnico", ma "quale tecnico regge quale conclusione".

## Funnel — perché LinkedIn è esca, non sintesi
**Perché.** In 200-300 parole non si *dimostra* ciò che al blog serve 2.500 per
dimostrare; provarci produce la versione svuotata o il clickbait. Il LinkedIn
porta **un solo** gancio (candidato P4), lo enuncia con precisione ma NON lo
dimostra, e rimanda al blog. **Coerenza del gancio:** l'esca va formulata al
livello di verità del blog ("crea le condizioni per la domanda", non "ti
chiederanno di provarlo"), o il lettore che clicca si sente ingannato. Si scrive
**per ultimo**, estratto dal blog finito.

## Registro — perché non aprire con "le due chiavi"
**Perché.** Pubblico tecnico ma **non specialista** (calibro: l'autore stesso, che
il meccanismo l'ha capito solo ora). Concetti che richiedono spiegazione non vanno
prima di averli spiegati. Si apre da un fatto che ogni dev già possiede (a
temperatura l'output cambia a ogni run), l'attrito arriva come domanda naturale
(sorgente del caso fissa → dov'è la varietà?), e "non-distorsivo in aspettazione"
si spiega DOPO che il lettore si è fatto la domanda. Il lettore scopre il
problema invece di subirlo. NB: non è "prima il facile", è "prima la sostanza" —
niente didattica su cos'è un LLM, che annoia anche il tecnico.

## Struttura — perché il gancio è una *conseguenza*, il tecnico è la *risposta*
**Perché.** Il lettore tecnico decide presto se restare, ma il tecnico crudo in
apertura respinge. Si separa gancio (conseguenza controintuitiva, capibile a
freddo) da spiegazione (il meccanismo). Il tecnico (1→2→3) va vicino all'inizio
ma *dopo* aver piantato la domanda a cui risponde. Portanti 2,4,6; cornice 0,7
movibile/tagliabile.

## Agenti/skill — perché dopo, non prima
**Perché.** La frequenza che giustifica il tooling non è provata (un articolo, non
ancora scritto); e costruire strumenti è il terreno comodo dell'autore
(programmazione), la scrittura è quello scomodo — rischio di rimandare la
scrittura costruendo l'infrastruttura. La skill si estrae come **residuo** del
primo articolo, codificando il processo che ha funzionato, mai i fatti (che
marciscono). Eventuale agente solo stretto e a monte del gate.
EOF
