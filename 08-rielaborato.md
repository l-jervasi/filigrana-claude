# Trasparenza per chi? La filigrana di Claude e l'AI Act

Se sei un programmatore, un appassionato di tecnologia o semplicemente un fruitore di servizi di intelligenza artificiale, molto probabilmente avrai sentito parlare dell'"AI Act".

Questa legge, emanata dall'Unione Europea, punta, tra le altre cose, a facilitare il riconoscimento di contenuti, siano essi immagini, testi o video, provenienti da un qualsiasi sistema non umano.

Con gli obblighi di trasparenza entrati in vigore, le aziende che sviluppano LLM devono adeguarsi – o rischiano sanzioni o limitazioni.

Tra queste una delle prime è stata Anthropic con il suo Claude, adottando un sistema che a mio avviso merita un articolo.

## Come funziona: il dado truccato

Se chiedi due volte la stessa cosa ad un modello linguistico otterrai due risposte diverse, lo sai e te lo aspetti. Il motivo? Ad ogni parola il modello non prende la più probabile, ne pesca una dal mazzo secondo le probabilità. È un dado. Ed è quel dado a rendere l'output vario, a volte in modo sorprendente.

Il sistema trovato per Claude – si chiama SynthID-Text – interviene proprio su questo dado, ma non lo toglie, lo trucca. 
SynthID-Text non è un prodotto Anthropic, non l'ha inventato: viene da Google DeepMind, è descritto in un paper su Nature ed è una filigrana invisibile che lavora tramite chiave fissa a livello di token.

Continuando a mantenere l'analogia, è come se ad ogni tiro fosse aggiunta una spinta invisibile, sempre nello stesso verso, ovvero verso un sottoinsieme scelto da una chiave segreta e dal contesto. È come se il dado continuasse ad esserci ma cadesse più spesso su una faccia voluta dalla chiave. Pur ripetendo il lancio mille volte avremmo sempre la stessa identica spinta. Il risultato? Le risposte si assomigliano di più.

E ogni singola risposta porta, sparsa tra le parole, la stessa preferenza, più termini "della chiave" di quanti il caso ne metterebbe. È quella firma, leggibile solo con la chiave, che un rilevatore riconosce: non gli serve confrontare niente, gli basta il testo che ha davanti.

Fin qui è una curiosità tecnica. Il punto scomodo arriva adesso, ed è dove la faccenda smette di essere astratta e diventa tua.

Quella spinta lascia un'impronta che non hai scelto e non puoi vedere. E l'impronta resta addosso a chi il testo lo ha scritto, fatto rifinire da Claude e lo ha pubblicato così com'è. Non resta addosso a chi trova il modo di rimodellarlo solo nella forma, né a chi non l'ha mai marchiato. Il segnale pensato per la trasparenza si attacca all'onesto e scivola via da chi vuole liberarsene.

Ma come funziona in sostanza questo "dado" e cosa comporta il "dado truccato"? 

Come ti avevo accennato nell'introduzione, la spinta della chiave non tocca il calcolo delle probabilità: quelle restano quelle del modello, e i candidati per ogni parola si pescano ancora a caso da lì. A cambiare è chi, tra quei candidati, sceglie la parola: non più il caso tramite un seed generato randomicamente ogni volta, ma la chiave. Il caso propone, la chiave dispone.
Da questo ne esce una notizia buona per chi effettivamente usa il modello ed Anthropic lo dice esplicitamente quando afferma che il metodo è "non distorsivo": in media su tutte le chiavi possibili la distribuzione dell'output resta quella di sempre.

Il problema è però più sottile: la qualità rimarrà mediamente la stessa, ma a calare sarà la varietà nella direzione decisa dalla chiave fissa. Di quanto, non lo sappiamo: la configurazione di Claude non è pubblica. La direzione è certa, l'entità no.
Negli A/B test che portano a prova del "nessun calo di qualità" – milioni di risposte, valutatori che non colgono differenze – si misura la qualità di una risposta, non la varietà tra risposte: due cose diverse. Quanto margine ci sia da spendere, però, dipende da quanta varietà c'era in partenza. In certi testi è pochissima. Il codice di un programma ne è un esempio.

## Il caso particolare del codice

Probabilmente questo sembra un controsenso: il codice permette tantissime possibilità, migliaia di algoritmi di risoluzione o di modi per rappresentare uno stesso calcolo. Ma non è qui che interviene la filigrana, non lavora sull'intero programma, sulle scelte implementative o su quali algoritmi e variabili utilizzare, lavora un token alla volta e lì la libertà è più rada.

Il nome che scegli una volta va poi ripetuto identico a ogni uso; dopo `for (int i = 0;` la parentesi è obbligata; `2 + 2` fa `4` e basta. Alcune scelte restano – nei nomi, nella struttura – ma isolate, in mezzo a lunghi tratti obbligati.
Meno possibilità per token rispetto alla prosa implicano meno appigli per il marchio, non zero ma in numero significativamente ridotto.

Nello studio "An Entropy-based Text Watermarking Detection Method" (Lu, Liu et al.), presentato ad ACL 2024, si dimostra che su un watermark standard la rilevazione, che sulla prosa riconosce il testo marchiato quasi sempre (il 99% dei casi), sul codice cala al 68%, a parità di falsi positivi.
A bassa entropia un token "verde" – quello che sarebbe scelto dalla chiave – è raro, e restano poche posizioni in cui il marchio può incidere. Non a caso esiste un intero filone di ricerca dedicato a marcare gli output a bassa entropia: esiste perché gli schemi standard, sul codice, non ce la fanno. L'esistenza del problema è di per sé una prova.

Secondo ciò che ha scritto Anthropic, sul codice l'effetto della marcatura è trascurabile, il marchio semmai si annida nei commenti, ed è vero, e per assurdo questa diventa più una confessione che una rassicurazione. Per quanto lo chiamino "non distorsivo" – e lo è di fatto ad alta entropia – marcare vuol dire una cosa sola: spingere la scelta verso una parola gradita al marchio, invece di quella che il modello preferirebbe. Dove le alternative plausibili sono tante quella spinta è un'inezia, si perde nel mucchio; ma sul codice le alternative sono due o tre, e lì si vede – una scelta che il modello lascerebbe a testa o croce diventa, sotto il marchio, tre volte su quattro quella marcata. È il marchio, ed è insieme uno scarto da ciò che il modello avrebbe prodotto da sé, ovvero, in sostanza, una "distorsione" del normale output.

Così il codice prende il peggio da entrambe le parti: marcato poco, perché i punti su cui agire sono rari, e dove è marcato piegato più che altrove. Piegato, non rotto – la scelta resta valida, un nome vale l'altro – solo, non è quella che il modello avrebbe scelto.

Solo dove la parola è davvero obbligata – la sintassi, `2+2` che fa `4` – non c'è nessun verde tra cui spingere, e allora niente. O il codice porta abbastanza scelte da marcare, e allora quelle scelte gliele stai piegando; o non le porta, e il marchio non c'è. "Effetto trascurabile sul codice" e "il codice è a malapena marchiato" sono la stessa frase: se davvero non ti tocca il codice, è perché non lo sta marcando, se lo fa lo sta distorcendo.

E quel poco che il codice si lascia marcare sta proprio nei punti più fragili per la filigrana stessa: i nomi, i commenti. Punti che si toccano senza toccare la logica – un commento si cancella, una variabile si rinomina, e il segnale se ne va. Quanto ne resti nel codice di Claude non lo sappiamo: il rilevatore non è ancora pubblico, nessuno l'ha misurato. Ma la direzione è chiara – in buona parte del codice il marchio non c'è per proprietà intrinseche al codice stesso; e dove c'è, si stacca con facilità.

## Il dubbio sulla proprietà intellettuale

Adesso mettiamo che tu stia lavorando su un testo in prosa, dove l'entropia è alta e la filigrana tiene. Cosa cambia davvero per te?
Meno di quello che si può temere da una parte, qualcosa di più insidioso dall'altra.
Anche su questo si esprime Anthropic e di nuovo in maniera sincera: il marchio non cambia né chi è l'autore né sposta la responsabilità legale. Dal punto di vista legale è sostanzialmente inerte. Il copyright nasce, come sarebbe per un testo tradizionale, in automatico nel momento in cui scrivi senza deposito né registrazione – è così da Berna in poi, e lo ribadisce il codice
americano quando dice che la registrazione "non è condizione della protezione". 
Il copyright è presunto, chi mette il proprio nome sull'opera è considerato l'autore salvo prova contraria, così come sancito dalla Convenzione di Berna e dalla direttiva europea sull'enforcement. In un eventuale caso legale sarà l'accusatore a dover dimostrare il contrario, non tu a dover provare che sei il vero autore.
Inoltre il copyright, per esistere, ha bisogno di un autore umano. Un'IA non può detenerlo – e Claude nemmeno, per quanto sia lui a mettere le parole in fila. Vale su entrambe le sponde: negli USA i tribunali e l'ufficio copyright l'hanno detto senza appello; in Europa la legge chiede una "creazione intellettuale propria dell'autore", cioè di un umano.

Quindi il marchio per quanto riguarda il copyright non ti tocca?
In realtà lo fa eccome: un output puramente generato da una macchina non è proteggibile comunque, e i prompt da soli non ti rendono autore – la legge non cambia –, ciò che conta non è se hai usato l'IA, ma quanto di umano c'è dentro e se è abbastanza da meritare protezione, ed è qui che il marchio potrebbe fare la differenza.
Il marchio, infatti, incrina la presunzione di paternità, nessuno di norma ti chiede di dimostrare che un testo a tua firma è tuo: la domanda non esiste. Il marchio la fa esistere creando un segnale interrogabile che, se presente, porta ad una domanda: "quanto, di questo, ce l'hai messo tu?".
Il diritto d'autore non si gioca tra te e Claude, ma su un altro dato: "c'è abbastanza lavoro umano da meritare protezione?". Prima della filigrana la soglia era presunta a tuo favore, da quando esiste è qualcosa che si può chiedere di difendere.

E di nuovo, anche su questo frangente, colpisce più l'utente onesto. Colui che usava l'IA per scrivere tutto, un copyright non lo avrebbe avuto comunque. Chi invece ha scritto il 90% del testo e ha scelto che Claude rifinisse il resto viene colpito in pieno, è l'autore legittimo ma adesso porta addosso un marchio che ha in sé la possibilità di mettere in discussione ciò che è chiaramente suo.

Detto con onestà, ad oggi non ci sono casi in cui il tribunale ha chiesto di provare l'apporto umano sulla base di una filigrana – anche perché non esistono ancora gli strumenti per farlo – ma introduce un rischio strutturale creato dallo strumento. 
Che il marchio crei le condizioni perché la domanda venga posta è dimostrabile ora; che qualcuno te la porrà è una previsione, e
come tale va presa. 

Nel caso in cui questa previsione si avveri, il modo giusto ed onesto di lavorare non sarà nascondere l'uso dell'IA ma documentare se stessi ed il proprio apporto al lavoro – bozze, cronologia, prompt – e tracciare il proprio processo. Aggiunge complessità al lavoro ma garantisce il diritto sul pezzo, sia che a creare ambiguità sia la filigrana o meno.

Per quanto riguarda il tipo di marchio, era davvero necessaria una filigrana così invasiva? Risposta breve: no.
La legge europea sulla trasparenza – quella appena entrata in vigore – impone che l'output sia "rilevabile come generato dall'IA", ma non dice esplicitamente quale metodo usare per farlo. Il considerando presente nello stesso documento mette esplicitamente tra le tecniche ammesse, alla pari, i metadati e i metodi crittografici di provenienza. Un'etichetta staccabile, una firma allegata, un checksum: sarebbero bastati a essere in regola.
E in effetti la stessa Anthropic lo utilizza sui file immagine che genera, con lo standard C2PA.
A questo si aggiunge che per chi pubblica un testo, in realtà, l'obbligo è solo di dichiararlo e cade del tutto se c'è una revisione umana con responsabilità editoriale. 
Le vie leggere c'erano tutte. Sul testo, invece, hanno scelto un marchio incorporato nelle parole, che sopravvive al copia-incolla e non si stacca a volontà.
Ma quindi perché Anthropic ha scelto proprio questa via? La risposta non è certa o completamente documentata, una lettura "generosa" può essere che l'abbiano fatto per robustezza – la stessa legge la incoraggia "per quanto tecnicamente possibile". Ma è il tipo di robustezza il nodo: è ciò che fa sì che il marchio non si stacchi più da chi lo porta. E un marchio che non puoi togliere smette di essere un semplice adempimento di trasparenza – diventa qualcosa che ti resta addosso, voluto o no.

Detto questo, la domanda ovvia che può venire in mente è se esiste un sistema per verificare la presenza del marchio.

## La verifica: una promessa difficile

Anthropic dice "presto", ma da quando l'ha annunciato sono passati oltre dieci giorni e il rilevatore ancora non c'è. 
Il ritardo non è un dettaglio tecnico ma risponde ad un problema per il quale non esiste una soluzione pulita. Quando si parla di filigrana verificare e aggirare sono le due facce di una stessa medaglia. Il rilevatore è lo strumento che, con la chiave, riconosce il marchio; permettere che chiunque possa utilizzarlo significa dare la possibilità a chiunque di limare l'output ottenuto fino a che tale marchio sparisce. Ed è così che funziona una firma dentro al testo: la firma esterna la verifichi senza che questo aiuti a falsificarla, ma muore al copia-incolla; il marchio intrinseco sopravvive a quest'ultimo, ma proprio per poterlo fare non può permettere di essere verificato.

Da qui ne esce un trilemma irrisolvibile. Rilevatore totalmente chiuso in mano ad Anthropic, nessuna condivisione della chiave, tutto interno. La trasparenza da fine si tramuta in vero e proprio atto di fede sulla sola fonte disponibile ed imposta.
Rilevatore totalmente aperto: si verifica il problema discusso sopra, chiunque verifica implica che chiunque può aggirare, si perde totalmente la robustezza.
Rilevatore semi-aperto, dato solo a piattaforme "fidate" come datori, scuole, editori. Trasforma la verifica in un privilegio dove loro hanno il verdetto sul tuo lavoro, tu no. E con nessuna delle tre soluzioni si ha quello che invece si auspicava: una trasparenza pubblica.

Di queste tre opzioni, quella che più probabilmente verrà adottata è la terza, ma è anche la più insidiosa perché quel verdetto non regge dove conta. 
In Italia una lite sulla paternità di un testo è civile, e lì il giudice pesa le prove "secondo il suo prudente apprezzamento": un segnale non validato, dal tasso d'errore non noto vale poco; mentre in sede penale la Cassazione, tramite la sentenza Cozzini, ha valutato le prove con criteri di affidabilità del metodo scientifico – testabilità, tasso d'errore, revisione, accettazione – e sarà il giudice a fare da "custode del metodo": il marchio di Anthropic, ad oggi, non supererebbe tali criteri.

E fuori dall'Italia? La nostra sentenza Cozzini è la gemella dello standard americano Daubert, e anche lì la conclusione è la stessa: il segnale non sarebbe preso come buono da un tribunale ma potrà essere usato da chi tribunale non è, per giudicare le persone.

Ma quindi la filigrana è una mossa assurda di Anthropic? 
Difese per il metodo adottato ci sono e sono oneste: il marchio non nasce per validare il singolo scritto o come prova da usare contro una singola persona. Lo dice Anthropic stessa – segnala che un testo potrebbe essere passato da Claude, non lo dimostra – ed è inferenza statistica, ha senso sui grandi numeri, non per inchiodare un singolo passaggio.

Ma il danno non sta nell'uso per come è pensato, sta nell'uso collaterale; la scuola che segnala un tema, il datore di lavoro che scarta una relazione – un segnale grezzo che finisce per giudicare il singolo. E non è un'ipotesi, i rilevatori di IA già oggi vengono usati nelle scuole, falsi positivi compresi: è già così.

Ed è lo stesso traguardo che ricerca la legge: il regolamento europeo auspica che i meccanismi di rilevazione siano "accessibili", di modo da far sì che "il pubblico possa distinguere". Punta, dunque, verso il rilevatore aperto a tutti, ma questo è esattamente il tipo di rilevatore che una filigrana non può avere, il rilevatore che uccide la robustezza. In sostanza ricerca una trasparenza pubblica che questo tipo di marchio non può dare.

E si può andare persino oltre il rimuoverlo. Nello studio "Watermark Stealing in Large Language Models" – Jovanović, Staab e Vechev, ETH di Zurigo, ICML 2024 – si è arrivati a dimostrare che, interrogando un modello con filigrana – KGW2-SelfHash, una green-red-list distorsiva –, si riesce a ricostruire buona parte della sua regola tanto da non solo rimuovere il marchio, ma aggiungerlo ad un testo scritto da un umano. Non si parla né di Claude né di SynthID-Text, ma di uno schema della stessa famiglia; questo porta ad una conclusione importante: una firma a chiave si impara dagli output e un segnale che si può falsificare non prova più niente.

Si potrebbe obiettare che non si sta parlando di Claude, e sì, è assolutamente vero, la fattibilità sull'LLM di Anthropic è probabile ma non certa e, soprattutto, mentre per KGW2-SelfHash si parla di una spesa irrisoria – 50$ di chiamate API per generare testo marchiato – la spesa su Claude, non essendo stato testato, è ignota e potrebbe non essere altrettanto irrisoria. Quindi il sistema alla fine è valido? A mio avviso, no e per un motivo semplice: chi vuole liberarsene lo fa gratis – un modello aperto non
l'ha mai marchiato, e a un testo marcato bastano una traduzione o una riscrittura perché il segnale sparisca. Il rilevatore, quando arriverà, saprà dire "questo l'ha scritto Claude" a chi non ha fatto nulla per nasconderlo, e tacerà su chi l'ha tradotto o riscritto. Giudica chi si è adeguato, non chi ha aggirato.

## Uniamo i punti: chi ci rimette davvero?

La conclusione, a mio avviso, è pura inferenza logica: il marchio non ti espropria e non ti incolpa – questo è innegabile – dice solo "hey, qui c'è passato Claude!", e non sappiamo se dirà con quale entità o solo sì o no. E lo fa sempre sullo stesso tipo di utente, quello sbagliato. Chi scrive il pezzo e fa ricontrollare e rivedere il testo dall'IA porta il marchio e con esso il ragionevole dubbio su quanto sia davvero suo. E il rilevatore, in qualunque modo decideranno di implementarlo, non farà altro che acuire il problema, non migliorarlo. 
Marcatura, evasione, verifica: da qualunque lato la guardi, il verso è lo stesso. Il peso grava sull'onesto e scivola via da chi aggira. È un sistema di trasparenza i cui costi sono inversamente proporzionali alla colpa.

Sì, si dichiara che è proprio questo l'intento ed è proprio l'utente onesto il destinatario designato a rendere leggibile l'assistenza dell'IA. Questo è vero, ma tra dichiarare – con una nota che probabilmente l'onesto avrebbe messo in quanto obbligo di legge – e un marchio imposto che ti si appiccica addosso corre la stessa differenza che c'è tra essere persone oneste e renderne conto ed essere costantemente sorvegliati.
Non è speculazione o malizia, è un dato: la forma stessa dello strumento – marchio non pubblicamente verificabile (ad ora), scelto dove bastava meno – lo rende, di fatto, un giudizio sull'onesto.

Non ti stanno rubando la proprietà sul tuo lavoro, quella rimane esattamente dov'era. Ti stanno rendendo interrogabile su quanto è davvero tuo; dall'altro lato, ed è ironico, a chi ha barato non viene chiesto assolutamente niente.

## Una piccola curiosità su questo pezzo

E chiudo con due parole su questo stesso testo – quello che hai appena letto – dato che, dopo tutto quello che ho scritto, sono d'obbligo: questo articolo utilizza Claude e lo fa a più livelli.

L'idea di base nasce da una mia curiosità arricchita da una conversazione con Claude. Da un botta e risposta sono nati prima il piano e le varie tesi, e con essi ciò che ci volevo dentro – in sostanza tutto mio – poi la ricerca di fonti – lui trova, io valido, e lui controlla se aggiornate – la stesura di una prima bozza seguendo il piano – praticamente solo Claude – ed infine la rilettura e la correzione finale con la riscrittura in voce personale – mia e con molte parti corrette nella sostanza non solo nella forma – per terminare in un ultimo controllo formale di Claude. 
Il tutto tracciato e documentato via commit su git.
Un lavoro di Claude? In parte, ma credo molto più mio. La sentenza la lascio al lettore e a prova, in calce, di seguito il link alla repository pubblica.