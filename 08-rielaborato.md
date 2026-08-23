Se sei un programmatore, un appassionato di tecnologia o semplicemente un fruitore di servizi di intelligenza artificiale, molto probabilmente avrai sentito parlare dell'"AI Act".

Questa legge, emanata dall'Unione Europea, punta, tra le altre cose, a facilitare il riconoscimento di contenuti, siano essi immagini, testi o video, provenienti da un qualsiasi sistema non umano.

Con l'entrata in applicazione degli obblighi sulla trasparenza, il provvedimento ha avuto ripercussioni sulle aziende specializzate in LLM, le quali dovranno inevitabilmente adeguarsi agli standard imposti per non trovarsi ad affrontare eventuali sanzioni o limitazioni.

Tra queste una delle prime è stata Anthropic con il suo Claude, adottando un sistema che a mio avviso merita un articolo.

Se chiedi due volte la stessa cosa ad un modello linguistico otterrai due risposte diverse, lo sai e te lo aspetti. Il motivo? Ad ogni parola il modello non prende la più probabile, ne pesca una dal mazzo secondo le probabilità. È un dado. Ed è quel dado a rendere l'output vario, a volte in modo sorprendente.

Il sistema trovato per Claude – si chiama SynthID-Text – interviene proprio su questo dado, ma non lo toglie, lo trucca. 
SynthID-Text non è un prodotto Anthropic, non l'ha inventato: viene da Google DeepMind, è descritto in un paper su Nature ed è una filigrana invisibile che lavora tramite chiave fissa a livello di token.

Continuando a mantenere l'analogia, è come se ad ogni tiro fosse aggiunta una spinta invisibile, sempre nello stesso verso, ovvero verso un sottoinsieme scelto da una chiave segreta e dal contesto. È come se il dado continuasse ad esserci ma cadesse più spesso su una faccia voluta dalla chiave. Pur ripetendo il lancio mille volte avremmo sempre la stessa identica spinta, il risultato? Le risposte si assomigliano di più.

E ogni singola risposta porta, sparsa tra le parole, la stessa preferenza, più termini "della chiave" di quanti il caso ne metterebbe. È quella firma, leggibile solo con la chiave, che un rilevatore riconosce: non gli serve confrontare niente, gli basta il testo che ha davanti.

Fin qui è una curiosità tecnica. Il punto scomodo arriva adesso, ed è dove la faccenda smette di essere astratta e diventa tua.

Quella spinta lascia un'impronta che non hai scelto e non puoi vedere. E l'impronta resta addosso a chi il testo lo ha scritto, fatto rifinire da Claude e lo ha pubblicato così com'è. Non resta addosso a chi trova il modo di rimodellarlo solo nella forma, né a chi non l'ha mai marchiato. Il segnale pensato per la trasparenza si attacca all'onesto e scivola via da chi vuole liberarsene.

Ma come funziona in sostanza questo "dado" e cosa comporta il "dado truccato"? 

Come ti avevo accennato nell'introduzione, la spinta della chiave non tocca il calcolo delle probabilità: quelle restano quelle del modello, e i candidati per ogni parola si pescano ancora a caso da lì. A cambiare è chi, tra quei candidati, sceglie la parola: non più il caso tramite un seed generato randomicamente ogni volta, ma la chiave. Il caso propone, la chiave dispone.
Da questo ne esce una notizia buona per chi effettivamente usa il modello ed Anthropic lo dice esplicitamente quando afferma che il metodo è "non distorsivo": in media su tutte le chiavi possibili la distribuzione dell'output resta quella di sempre.

Il problema è però più sottile: la qualità rimarrà mediamente la stessa, ma a calare sarà la varietà nella direzione decisa dalla chiave fissa. Di quanto, non lo sappiamo: la configurazione di Claude non è pubblica. La direzione è certa, l'entità no.
Negli A/B test che portano a prova del "nessun calo di qualità" – milioni di risposte, valutatori che non colgono differenze – si misura la qualità di una risposta, non la varietà tra risposte: due cose diverse. Quanto margine ci sia da spendere, però, dipende da quanta varietà c'era in partenza. In certi testi è pochissima. Il codice di un programma ne è un esempio.

Probabilmente questo sembra un controsenso, il codice permette tantissime possibilità, migliaia di algoritmi di risoluzione o di modi per rappresentare uno stesso calcolo. Ma non è qui che interviene la filigrana, non lavora sull'intero programma, sulle scelte implementative o su quali algoritmi e variabili utilizzare, lavora un token alla volta e lì la libertà è più rada.

Il nome che scegli una volta va poi ripetuto identico a ogni uso; dopo `for (int i = 0;` la parentesi è obbligata; `2 + 2` fa `4` e basta. Alcune scelte restano – nei nomi, nella struttura – ma isolate, in mezzo a lunghi tratti obbligati.
Meno possibilità per token rispetto alla prosa implicano meno appigli per il marchio, non zero ma in numero significativamente ridotto.

Nello studio "An Entropy-based Text Watermarking Detection Method" (Lu, Liu et al.), presentato ad ACL 2024, si dimostra che su un watermark standard la rilevazione che sulla prosa riconosce il testo marchiato quasi sempre – il 99% dei casi – sul codice cala al 68%, a parità di falsi positivi.
A bassa entropia un token "verde" – quello che sarebbe scelto dalla chiave – è raro, e restano poche posizioni in cui il marchio può incidere. Non a caso esiste un intero filone di ricerca dedicato a marcare gli output a bassa entropia: esiste perché gli schemi standard, sul codice, non ce la fanno. L'esistenza del problema è di per sé una prova.

Secondo ciò che ha scritto Anthropic, sul codice l'effetto della marcatura è trascurabile, il marchio semmai si annida nei commenti, ed è vero, e per assurdo questa diventa più una confessione che una rassicurazione. Per quanto lo chiamino "non distorsivo" – e lo è di fatto ad alta entropia – marcare vuol dire una cosa sola: spingere la scelta verso una parola gradita al marchio, invece di quella che il modello preferirebbe. Dove le alternative plausibili sono tante quella spinta è un'inezia, si perde nel mucchio; ma sul codice le alternative sono due o tre, e lì si vede – una scelta che il modello lascerebbe a testa o croce diventa, sotto il marchio, tre volte su quattro quella marcata. È il marchio, ed è insieme uno scarto da ciò che il modello avrebbe prodotto da sé, ovvero, in sostanza, una "distorsione" del normale output.

Così il codice prende il peggio da entrambe le parti: marcato poco, perché i punti su cui agire sono rari, e dove è marcato piegato più che altrove. Piegato, non rotto – la scelta resta valida, un nome vale l'altro – solo, non è quella che il modello avrebbe scelto.

Solo dove la parola è davvero obbligata – la sintassi, `2+2` che fa `4` – non c'è nessun verde tra cui spingere, e allora niente. O il codice porta abbastanza scelte da marcare, e allora quelle scelte gliele stai piegando; o non le porta, e il marchio non c'è. "Effetto trascurabile sul codice" e "il codice è a malapena marchiato" sono la stessa frase: se davvero non ti tocca il codice, è perché non lo sta marcando, se lo tocca lo sta distorcendo.

E quel poco che il codice si lascia marcare sta proprio nei punti più fragili: i nomi, i commenti. Punti che si toccano senza toccare la logica – un commento si cancella, una variabile si rinomina, e il segnale se ne va. Quanto ne resti nel codice di Claude non lo sappiamo: il rilevatore non è ancora pubblico, nessuno l'ha misurato. Ma la direzione è chiara – dove conta la precisione il marchio quasi non c'è; e dov'è, si stacca con facilità.