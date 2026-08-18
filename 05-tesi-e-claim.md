# 05 — Tesi e claim (output fase 2)

> Fissato il **19 ago 2026**. Output della fase 2 del workflow (vedi `01`): la
> **tesi controllante** + l'**inventario dei claim** mappati a Piano / fonte / stato,
> + l'**arco di lettura**. Il dettaglio di ogni Piano sta in `02`; il *perché* in
> `04`; le fonti in `03`.
>
> ⚠️ **L'inventario è ordinato PER PESO, NON è la sequenza di lettura.** L'ordine
> dell'articolo è l'**arco** in fondo, che chiude sulla **tesi (T)** — non sul codice.

---

## Tesi controllante

**La filigrana di Claude è un meccanismo di trasparenza i cui costi cadono
inversamente alla colpa.** Non ti espropria e non ti incolpa — rende *interrogabile
quanto ci sei tu*. Questa interrogabilità colpisce l'autore **onesto** (marchiato,
esposto sulla soglia "quanto è tuo?"), mentre chi vuole **aggirarla** lo fa gratis
(modello open, riscrittura vera). Il rovescio esatto dell'**allarme popolare**: non
un *furto* del tuo testo, ma un *onere* spostato su chi non lo merita — e per giunta
una **scelta**, non un obbligo di legge, che vie più leggere (una nota, un checksum)
avrebbero evitato.

**Spina falsificabile — l'asimmetria appare su tre assi indipendenti, stesso verso:**
- **marcatura** (P4): interroga l'apporto dell'onesto;
- **evasione** (P6): gratis per chi aggira;
- **verifica** (P5): il detector adjudica il conforme, non l'evasore.

**Limite onesto tenuto dentro (non-bunker):** la parte legale è **rischio
strutturale**, non fatto — nessun tribunale ha ancora chiesto di provare l'apporto
umano *sulla base di una filigrana*. Si afferma al livello *"crea le condizioni
perché la domanda venga posta"*, NON *"ti verrà chiesto"*.

---

## Inventario claim (ordinato PER PESO — non è l'ordine di lettura)

| # | Claim | Piano | Fonte | Stato |
|---|-------|-------|-------|-------|
| **T** | **Tesi:** costi **inversi alla colpa** — marca l'onesto, sfiora l'evasore; rovescio dell'allarme popolare | P6 | sintesi 1–7 | ✅ deriva |
| **1** | Copyright: NON "lo perdi" ma **inversione dell'onere** (automatico + presunzione + onere sull'accusatore; il marchio fabbrica materiale interrogabile sulla soglia paternità-umana) | P4 | Berne 5(2)/15(1); 17 USC 408(a)/410(c); Feist; Dir. 2004/48 ✅ + Thaler/USCO ✅~ | ✅ meccanismo · **rischio, non fatto** |
| **2** | La marcatura intrinseca è **scelta, non obbligo** (Art. 50 neutro; Recital 133 ammette metadata/checksum; testo = *disclosure* + esenzione human-review) | P4/P6 | Art. 50 + Recital 133/134 ✅ | ✅ |
| **3** | **Evasione gratis** (open = mai marchiato; riscrittura vera = dissolto) | P5/P6 | Post Anthropic ✅ + logica | ✅ |
| **4** | **Trilemma** verifica=evasione: nessuna config del detector dà trasparenza *pubblica*; è il prezzo dell'intrinseco; Recital 135 aspira al corno irraggiungibile | P5 | logico + Art. 50/Recital 135 ✅ | ✅ · (Daubert ⚠️ opz.) |
| **5** | *(ex C1+C2)* Sotto **chiave fissa** la diversità/entropia effettiva **cala** — meccanismo: **bias fisso a chiave sovrapposto al sampling** (dado truccato), NON sostituzione; direzione certa, entità non pubblicata | P2 | Nature Alg. 1-2 / p.820 ✅ | ✅ direzione · **aperta entità** |
| **6** | Sul codice il marchio è **debole** (bassa entropia → segnale debole) | P3 | Lett. indipendente ✅~ + ammissione Nature p.820 ✅ | ✅ direzione |
| **7** | **Accoppiamento**: al pavimento di entropia *"trascurabile"* ≡ *"a malapena marchiato"* (cita-e-ribalta: difesa→confessione) | P3 | logico + Nature p.820 ✅ | ✅ |

**Precisione anti-regressione (dentro il claim 5, non in testa):** i candidati si
campionano ancora da p_LM, i logit sono intatti, non-distorsione = in aspettazione
sul seed. Vedi CORREZIONI CRITICHE in `CLAUDE.md` e P2 in `02`. *(Il vecchio C1 —
"non sostituisce / non tocca i logit" — NON va come primo claim: da solo è gergo, e
apre in negativo = suona minimizzante, si disarma la tesi. Vive come fondamento
direzionale del claim 5.)*

### Nota di solidità
La tesi (T) poggia **solo su claim ✅ confermati alla primaria**. Gli unici asterischi
sono *entità* (claim 5, aperta per config non pubblicata → si scrive **ignota**) e
*rischio-non-fatto* (claim 1, per design). **Nessuna gamba dipende da una fonte ⚠️:**
Daubert (claim 4) è opzionale; i "quattro-centesimi" non entrano come dato. La tesi è
già interamente sostenibile con ciò che abbiamo.

---

## Arco di lettura (QUESTO è l'ordine dell'articolo — chiude su T)

1. **Apertura + attrito** — il dado truccato: la casualità resta ma la chiave la
   spinge sempre nello stesso verso → *"che fine fa la varietà?"* *(gancio = già
   claim 5)*
2. **Tecnico** (biglietto magro, *risposta* all'attrito): claim **5 → 6 → 7**
   *(P1/P2/P3)*
3. **Salita legale**: claim **1 → 2** *(P4)*
4. **Verifica**: claim **3 → 4** *(P5)*
5. **Chiusura**: **T** — sintesi, *costi inversi alla colpa / rovescio dell'allarme
   popolare* *(P6)*

→ Nell'articolo il **codice (6,7) sta nel mezzo** (dentro il biglietto tecnico); la
**chiusura è la tesi**, non il codice. Portanti: 5(=P2), 1(=P4), T(=P6).

---

## Peso parole — RIPESATO (fase 2b, 19 ago)

Banda **~2.500** (2.200–2.800). Budget per-Piano ripesato contro i claim fissati:

| Sezione | Parole | Claim |
|---|---|---|
| Apertura + attrito | ~280 | gancio (= claim 5) |
| P2 oltre il gancio | ~150 | claim 5 *(thin — disciplina baricentro B)* |
| P3 codice | ~380 | claim 6 + 7 |
| **P4 legale** | **~600** | claim 1 + 2 *(sezione più grande, unica)* |
| P5 verifica | ~420 | claim 3 + 4 |
| P6 sintesi | ~350 | tesi T + travaso metà-P6 di claim 2 |
| meta (P7) | ~100 | opzionale |
| **Totale** | **~2.280** | dentro banda, margine fino a 2.800 |

**Esiti:** (1) **ci sta senza tagliare claim** (~2.280 su tetto 2.800); (2) **P4 unica
~600** = conferma baricentro B (P4 il peso, P2 il più magro); (3) **travaso**: la
*conseguenza* di claim 2 ("marcato oltre il pavimento = marchiatura non trasparenza")
va alla chiusura **P6**. → pronto per la **fase 3 (schema)**.
