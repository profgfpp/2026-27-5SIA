# Molteplicità, relazioni e modello E-R

Nella lezione precedente abbiamo iniziato a inserire **un rombo tra due entità**.

Fino a questo momento avevamo spesso rappresentato le entità semplicemente collegate da una linea:

```text
[ALUNNO] ---------------- [CLASSE]
```

Adesso vogliamo rendere esplicito **che cosa rappresenta quel collegamento**.

Nella notazione E-R che utilizzeremo, la relazione viene rappresentata con un **rombo**:

```text
[ALUNNO] -------- ◇ APPARTENENZA ◇ -------- [CLASSE]
```

Il motivo non è soltanto grafico. Il rombo ci costringe a riconoscere che fra le due entità esiste un concetto autonomo: la **relazione**.

Nel nostro esempio potremmo chiamarla `ISCRIZIONE` oppure `APPARTENENZA`.

Inizialmente potremmo essere tentati di scrivere direttamente una frase:

```text
ALUNNO ---- è iscritto a ---- CLASSE
```

Da questo momento preferiremo invece dare alla relazione un nome, possibilmente sostantivato:

```text
[ALUNNO] -------- ◇ APPARTENENZA ◇ -------- [CLASSE]
```

oppure:

```text
[ALUNNO] -------- ◇ ISCRIZIONE ◇ -------- [CLASSE]
```

Questo ci aiuta a pensare alla relazione come a un vero elemento del modello, e non semplicemente come al verbo di una frase.

> **Da qui in avanti useremo quindi rettangoli per le entità e rombi per le relazioni.**

Una volta introdotta la relazione, però, ci accorgiamo subito che manca ancora qualcosa.

Consideriamo:

```text
[CLASSE] -------- ◇ APPARTENENZA ◇ -------- [ALUNNO]
```

Sappiamo che classi e alunni sono collegati, ma non sappiamo ancora **quanti** elementi possano essere coinvolti.

Una classe è composta da quanti alunni?

Certamente non da uno solo:

```text
1A
 ├── Marco Verdi
 ├── Maria Bianchi
 ├── ...
 └── ...
```

Quindi a una classe possono appartenere **molti alunni**.

Viceversa, se prendiamo un singolo alunno e guardiamo la situazione che stiamo modellando:

> a quante classi appartiene?

Normalmente a **una sola classe**.

Possiamo riassumere così:

```text
un ALUNNO  → una CLASSE
una CLASSE → molti ALUNNI
```

Ed è qui che compare il concetto di **molteplicità**.

---

## Come si legge la molteplicità

Questo è uno dei passaggi più delicati, perché la convenzione utilizzata può sembrare inizialmente controintuitiva.

Consideriamo:

```text
[CLASSE] ─── 1 ─── ◇ APPARTENENZA ◇ ─── N ─── [ALUNNO]
```

Per stabilire la molteplicità sul ramo che porta a `CLASSE`, dobbiamo partire dall'entità opposta.

Ci chiediamo:

> Un ALUNNO a quante CLASSI appartiene?

La risposta è:

> a una sola.

Per questo sul ramo verso `CLASSE` troviamo:

```text
1
```

Per stabilire invece la molteplicità sul ramo verso `ALUNNO`, partiamo da una classe:

> A una CLASSE quanti ALUNNI possono appartenere?

La risposta è:

> molti.

Perciò sul ramo verso `ALUNNO` troviamo:

```text
N
```

Possiamo visualizzarlo così:

```text
                         parto da qui
                              ↓
[CLASSE] ─── 1 ─── ◇ APPARTENENZA ◇ ─── N ─── [ALUNNO]
    ↑
    └── un ALUNNO appartiene a UNA CLASSE
```

e nel verso opposto:

```text
[CLASSE] ─── 1 ─── ◇ APPARTENENZA ◇ ─── N ─── [ALUNNO]
    │                                                 ↑
    └──── una CLASSE contiene MOLTI ALUNNI ──────────┘
```

Una buona regola mentale è quindi:

> **Per scegliere la molteplicità da scrivere su un ramo, parto dall'entità opposta e mi domando quante istanze posso raggiungere dall'altra parte.**

È una convenzione. All'inizio può sembrare strana, ma utilizzandola più volte diventa naturale.

Possiamo capire meglio il concetto anche guardando delle vere **istanze**, o **occorrenze**.

Supponiamo di avere:

```text
ALUNNI
----------------
Mario Rossi
Marco Verdi
Maria Bianchi
```

e:

```text
CLASSI
----------------
1A
1E
```

Le associazioni potrebbero essere:

```text
Mario Rossi    -------- 1E
Marco Verdi    -------- 1A
Maria Bianchi  -------- 1A
```

oppure, graficamente:

```text
Mario Rossi    ───────┐
                      └──── 1E

Marco Verdi    ───────┐
                      ├──── 1A
Maria Bianchi  ───────┘
```

Ogni singolo alunno compare in una sola associazione:

```text
Mario Rossi → 1E
```

Non avremo, almeno nel modello che stiamo costruendo:

```text
Mario Rossi → 1E
Mario Rossi → 1A
```

La stessa classe, invece, può comparire in molte associazioni:

```text
Marco Verdi   → 1A
Maria Bianchi → 1A
...
```

Possiamo quindi pensare alla molteplicità anche in questo modo:

> **quante associazioni possono coinvolgere una singola istanza quando attraversiamo la relazione?**

---

## Minimo e massimo

Scrivere soltanto:

```text
1
N
```

ci fornisce soprattutto informazioni sul **massimo**.

Possiamo però essere più precisi introducendo due valori:

```text
(minimo, massimo)
```

Per esempio:

```text
(1,N)
```

significa:

> almeno una, ma potenzialmente molte.

Mentre:

```text
(0,N)
```

significa:

> nessuna, una oppure molte.

Analogamente:

```text
(0,1)
```

significa:

> zero oppure una.

E:

```text
(1,1)
```

significa:

> esattamente una.

In sintesi:

| Molteplicità | Significato |
|---|---|
| `(0,1)` | zero oppure una |
| `(1,1)` | esattamente una |
| `(0,N)` | da zero a molte |
| `(1,N)` | da una a molte |

Quando minimo e massimo coincidono entrambi con `1`, possiamo anche abbreviare semplicemente con:

```text
1
```

A questo punto possiamo porci una domanda meno banale:

> Nel nostro sistema può esistere una CLASSE senza alcun ALUNNO?

Nella realtà ordinaria della scuola potremmo dire che una classe, per essere tale, deve avere almeno un alunno.

Quindi, partendo da una classe:

```text
quanti ALUNNI?
```

la risposta potrebbe essere:

```text
da 1 a N
```

e avremmo:

```text
[CLASSE] ─── 1 ─── ◇ APPARTENENZA ◇ ─── (1,N) ─── [ALUNNO]
```

La lettura è:

- un alunno appartiene a una sola classe;
- una classe contiene almeno un alunno e può contenerne molti.

Ma questa non è necessariamente l'unica scelta possibile.

Pensiamo al **registro elettronico**. La segreteria potrebbe predisporre tutte le classi del nuovo anno scolastico prima di avere assegnato gli studenti.

Potrebbe quindi esistere temporaneamente:

```text
Classe 1A
Alunni assegnati: 0
```

In quel sistema la molteplicità verso `ALUNNO` diventerebbe:

```text
(0,N)
```

e quindi:

```text
[CLASSE] ─── 1 ─── ◇ APPARTENENZA ◇ ─── (0,N) ─── [ALUNNO]
```

Questo ci porta a un principio molto importante:

> **la molteplicità non dipende soltanto dalla realtà in astratto, ma dai requisiti del sistema che stiamo progettando.**

La domanda non è soltanto:

> «Nella vita reale può succedere?»

ma anche:

> «Nel sistema che dobbiamo realizzare vogliamo permettere che succeda?»

Possiamo fare lo stesso ragionamento dall'altra parte.

> Può esistere nel nostro sistema un ALUNNO che non appartiene ancora a nessuna CLASSE?

Se il sistema registra soltanto studenti già iscritti e assegnati:

```text
1
```

può bastare.

Se invece permettiamo di inserire un alunno prima dell'assegnazione definitiva alla classe, potremmo avere:

```text
(0,1)
```

Il **minimo** ci dice quindi se la partecipazione è obbligatoria o facoltativa:

```text
0 → partecipazione facoltativa
1 → partecipazione obbligatoria
```

Il **massimo** ci dice invece se una singola istanza può essere associata a una sola istanza oppure a molte.

---

## Un caso molti-a-molti: cittadino e nazione

Consideriamo due nuove entità:

```text
[CITTADINO]                    [NAZIONE]
```

Fra esse introduciamo la relazione:

```text
[CITTADINO] -------- ◇ CITTADINANZA ◇ -------- [NAZIONE]
```

Cominciamo da una nazione.

> Una nazione può avere quanti cittadini?

Molti.

Sul ramo verso `CITTADINO` avremo quindi un massimo `N`.

Ora percorriamo la relazione nel verso opposto.

> Un cittadino quante cittadinanze può avere?

La prima risposta intuitiva potrebbe essere:

> una.

Ma non è necessariamente vero. Esistono persone con **doppia cittadinanza** e, più in generale, persone che possiedono più cittadinanze.

Quindi anche dall'altra parte possiamo avere:

```text
N
```

Otteniamo così:

```text
[CITTADINO] ─── N ─── ◇ CITTADINANZA ◇ ─── N ─── [NAZIONE]
```

cioè una relazione:

```text
N : N
```

**molti-a-molti**.

Possiamo confrontarla con il caso precedente:

```text
[CLASSE] ─── 1 ─── ◇ APPARTENENZA ◇ ─── N ─── [ALUNNO]
```

che è invece una relazione:

```text
1 : N
```

Il punto importante è che una relazione possiede **due rami**, e ogni ramo deve essere ragionato separatamente:

```text
              ◇ CITTADINANZA ◇
               /             \
              /               \
     ramo verso             ramo verso
      CITTADINO              NAZIONE
```

La molteplicità non è quindi una singola etichetta applicata globalmente al rombo.

Ogni ramo ha la propria.

Ma anche nell'esempio della cittadinanza possiamo approfondire il discorso sul minimo.

> Un cittadino deve necessariamente avere almeno una cittadinanza?

Esistono persone **apolidi**, cioè prive di cittadinanza.

Situazioni di questo tipo possono emergere per ragioni storiche, politiche o territoriali, soprattutto quando cambiano confini, Stati o ordinamenti. Anche la storia europea ha conosciuto territori passati da uno Stato a un altro e persone che hanno dovuto ridefinire la propria cittadinanza.

Una regola che inizialmente sembrava ovvia:

```text
ogni persona possiede esattamente una cittadinanza
```

si rivela quindi troppo semplice.

Se vogliamo rappresentare anche gli apolidi:

```text
0 cittadinanze
1 cittadinanza
2 cittadinanze
...
```

la molteplicità può diventare:

```text
(0,N)
```

Possiamo poi porre la domanda opposta:

> Può esistere una nazione senza cittadini?

È una domanda volutamente estrema, ma ci costringe a riflettere sul livello di precisione del modello.

Possiamo pensare a Stati appena costituiti, territori contesi o esperimenti politici. Un caso curioso è quello dell'**Isola delle Rose**, una piattaforma costruita al largo della costa adriatica sulla quale venne proclamata una nuova entità indipendente.

Possiamo quindi almeno immaginare un'entità politica definita prima di possedere una vera popolazione.

Ma la domanda progettuale resta:

> **Il nostro sistema ha davvero bisogno di rappresentare anche questo caso?**

Se sì, dobbiamo tenerne conto.

Se no, possiamo adottare una regola più semplice.

Per esempio, decidendo di ammettere entrambe le situazioni limite, potremmo avere:

```text
[CITTADINO] ── (0,N) ── ◇ CITTADINANZA ◇ ── (0,N) ── [NAZIONE]
```

Non dobbiamo però trasformare ogni esercizio in un'enciclopedia del mondo.

---

## Modellare significa scegliere

La realtà è enormemente complessa.

Se tentassimo di inserire tutto ciò che esiste dentro un diagramma E-R, non finiremmo mai.

Fra la realtà e il modello esiste quindi un passaggio fondamentale:

```text
REALTÀ
   │
   ▼
REQUISITI
   │
   ▼
MODELLO
```

I **requisiti** funzionano come una lente.

La realtà contiene una quantità enorme di informazioni; i requisiti selezionano quelle rilevanti per il problema che dobbiamo risolvere.

> Non dobbiamo modellare tutto ciò che esiste.
>
> Dobbiamo modellare ciò che serve.

E non dobbiamo neppure pretendere che il primo modello sia perfetto.

Possiamo iniziare, per esempio, pensando:

```text
un cittadino → una nazione
```

e assegnare inizialmente:

```text
1
```

Poi discutiamo meglio il problema, scopriamo:

```text
doppia cittadinanza
apolidia
situazioni amministrative particolari
```

e raffiniamo:

```text
1
 ↓
(0,N)
```

Non significa necessariamente che il primo modello fosse sbagliato in modo grossolano. Significa che il modello sta diventando progressivamente **più aderente ai requisiti**.

Lo sviluppo software funziona spesso così:

```text
prima ipotesi
     ↓
prototipo
     ↓
uso e confronto
     ↓
nuovi requisiti
     ↓
raffinamento
```

È lo stesso concetto espresso dalla famosa vignetta dell'**altalena nello sviluppo software**: il cliente immagina una certa soluzione, l'analista la interpreta in un modo, il progettista in un altro e il risultato può ancora essere differente.

Il cliente stesso non possiede necessariamente fin dall'inizio una descrizione perfetta di ciò che desidera.

Spesso vede una prima versione e dice:

> «No, questa cosa in realtà la vorrei fatta diversamente.»

La progettazione è quindi un processo progressivo di comprensione.

Questo ci porta anche a evitare due estremi.

Da una parte possiamo semplificare troppo:

```text
ogni cittadino possiede una sola cittadinanza
```

e perdere casi importanti.

Dall'altra possiamo cercare di prevedere ogni eccezione teoricamente possibile e costruire un modello enorme, difficile da usare e forse inutile.

Serve quindi una certa misura.

I latini dicevano:

> *Est modus in rebus.*

C'è una misura nelle cose.

Anche nella progettazione informatica la soluzione migliore non è necessariamente quella più semplice né quella più complessa: è quella con **il livello di complessità adeguato al problema**.

Questo principio riguarda anche il modo in cui impariamo.

Non esiste una separazione netta tra una cultura “tecnica” e tutto il resto della cultura. La tradizione scolastica italiana è stata fortemente influenzata dalla cultura umanistica e classica, con figure come Giovanni Gentile e Benedetto Croce. Questo patrimonio è importante, ma può diventare problematico se porta a considerare le discipline scientifiche come qualcosa riservato soltanto a chi sarebbe naturalmente “portato”.

Si sente spesso dire:

> «Io non sono portato per la matematica.»

Ma comprendere matematica, informatica o ragionamento logico non è semplicemente una caratteristica che alcune persone possiedono e altre no.

Sono capacità che si costruiscono con esercizio, metodo ed esperienza.

Allo stesso tempo anche una formazione esclusivamente tecnica può diventare sterile se viene ridotta alla sola capacità di utilizzare strumenti e procedure.

Un informatico, un ingegnere o un tecnico non dovrebbe soltanto saper “far funzionare le cose”: deve essere capace di comprenderne il contesto, comunicarle e ragionare sulle conseguenze.

Anche per questo la molteplicità non va semplicemente memorizzata.

Possiamo imparare una definizione come:

> «La molteplicità indica quante istanze possono essere associate attraverso una relazione.»

e continuare comunque a sbagliare tutti i diagrammi.

Per comprenderla davvero bisogna usarla più volte:

```text
ALUNNO / CLASSE
CITTADINO / NAZIONE
...
```

ripetendo sempre lo stesso ragionamento:

```text
parto da una singola istanza
           ↓
attraverso la relazione
           ↓
quante istanze trovo dall'altra parte?
           ↓
stabilisco il massimo
           ↓
può essere zero?
           ↓
stabilisco il minimo
```

La molteplicità è quindi più un **modo di ragionare** che una definizione da imparare a memoria.

---

## Il ramo della relazione

Nella notazione che useremo, la molteplicità appartiene al **ramo della relazione**.

Per esempio:

```text
[CLASSE] ───── 1 ───── ◇ APPARTENENZA ◇ ───── (1,N) ───── [ALUNNO]
```

Graficamente possiamo scrivere il valore più vicino al rombo o all'entità. Ciò che conta è capire che esso riguarda il segmento che collega l'entità alla relazione:

```text
ENTITÀ ───────────── ◇ RELAZIONE ◇
       ↑
       ramo
```

Una relazione binaria possiede quindi due rami:

```text
                    ◇ RELAZIONE ◇
                    /           \
                   /             \
              ramo A             ramo B
                 /                 \
          [ENTITÀ A]            [ENTITÀ B]
```

e i due rami possono avere molteplicità diverse.

Questo diventerà particolarmente importante quando passeremo dal diagramma alle tabelle.

---

## Dove stiamo andando: dalle entità alle tabelle

Il modello E-R è un modello **concettuale**.

Non è ancora il database concreto.

Alla fine dovremo arrivare a delle **tabelle**.

Abbiamo già visto, almeno in prima approssimazione:

```text
ENTITÀ
  ↓
TABELLA
```

Per esempio, l'entità:

```text
ALUNNO
```

con attributi:

```text
nome
cognome
codice fiscale
```

potrà portarci a:

```text
ALUNNO
+----------------+----------------+------------------+
| nome           | cognome        | codice_fiscale   |
+----------------+----------------+------------------+
| ...            | ...            | ...              |
+----------------+----------------+------------------+
```

Ma allora compare una domanda importante:

> Che cosa succede ai rombi?

Cioè:

> come vengono tradotte le relazioni quando passiamo alle tabelle?

Per ora anticipiamo soltanto che non esiste una risposta unica.

In alcuni casi una relazione potrà essere rappresentata attraverso un riferimento contenuto in una tabella.

In altri, soprattutto nelle relazioni molti-a-molti, avremo bisogno di una **tabella dedicata alla relazione**.

Quindi:

```text
molteplicità
     ↓
tipo di relazione
     ↓
modo in cui verrà trasformata in tabelle
```

Le molteplicità non sono quindi una decorazione del diagramma. Avranno conseguenze concrete nella progettazione del database.

Possiamo costruire una specie di “geografia” generale del lavoro:

```text
                         REALTÀ
                            │
                            ▼
                        REQUISITI
                            │
                            ▼
                 PROGETTAZIONE CONCETTUALE
                            │
                            ▼
                       MODELLO E-R
                            │
                            ▼
                  PROGETTAZIONE LOGICA
                            │
                            ▼
                  SCHEMA DEL DATABASE
                            │
                      tabelle e colonne
                            │
                            ▼
                       POPOLAMENTO
                            │
                            ▼
                          DATI
                            │
                            ▼
                    INTERROGAZIONE (SQL)
```

La realtà è troppo complessa per essere riportata integralmente.

I requisiti selezionano ciò che ci interessa.

Il modello E-R rappresenta concettualmente quella porzione di realtà.

Successivamente la struttura viene trasformata in tabelle.

Le tabelle vengono poi riempite di dati e interrogate.

---

## Schema e dati

Qui è utile distinguere bene **struttura** e **contenuto**.

Supponiamo di avere:

```text
ALUNNO
```

con:

```text
nome
cognome
codice_fiscale
```

Lo **schema** descrive la struttura:

```text
ALUNNO(nome, cognome, codice_fiscale)
```

Non contiene necessariamente:

```text
Mario Rossi
Anna Verdi
Luca Bianchi
```

Quelli sono i **dati**.

In modo molto semplice:

```text
SCHEMA
─────────────────────────────────
nome | cognome | codice_fiscale
```

mentre:

```text
DATI
─────────────────────────────────
Mario | Rossi   | ...
Anna  | Verdi   | ...
Luca  | Bianchi | ...
```

Lo schema stabilisce quali colonne esistono.

Le righe rappresentano invece le singole istanze memorizzate.

Possiamo quindi dire che lo schema del database è costituito, almeno in prima approssimazione, dai nomi delle tabelle e dalla struttura delle loro colonne.

Quando abbiamo predisposto:

```text
ALUNNO(nome, cognome, codice_fiscale)
```

possiamo iniziare ad aggiungere:

```text
Mario Rossi ...
Maria Bianchi ...
Marco Verdi ...
```

Questa operazione si chiama **popolamento** del database:

```text
schema vuoto
     │
     │ aggiungiamo righe
     ▼
database popolato
```

Il popolamento riguarda principalmente i dati, cioè le righe.

In sistemi nei quali i dati arrivano continuamente si incontra anche il termine:

```text
data ingestion
```

cioè **ingestione dei dati**.

Pensiamo a una rete di stazioni meteorologiche:

```text
sensore temperatura
        │
        ├── dato
        ├── dato
        ├── dato
        ├── dato
        └── ...
```

I dati vengono continuamente acquisiti e inseriti nel sistema.

La struttura esiste già: stiamo alimentando il database.

Lo schema tende a essere più stabile dei dati, ma può comunque cambiare.

Supponiamo di accorgerci che alla tabella:

```text
ALUNNO
```

manca una colonna.

Potremmo passare da:

```text
PRIMA

ALUNNO
nome
cognome
```

a:

```text
DOPO

ALUNNO
nome
cognome
codice_fiscale
```

Quando modifichiamo la struttura di un database già esistente entriamo nel tema delle **migrazioni**.

Modificare lo schema di un database già pieno di dati è un'operazione più delicata del semplice aggiungere nuove righe, perché i dati già presenti devono continuare a essere compatibili con la nuova struttura.

Un altro concetto importante è quello di **scalabilità**.

Un sistema dovrebbe continuare a funzionare anche quando cresce la quantità di dati:

```text
10 record
100 record
1 000 record
10 000 record
1 000 000 record
```

Un progetto che funziona bene con dieci elementi ma crolla quando ne arrivano centomila presenta un problema di scalabilità.

Anche per questo la struttura dei dati deve essere progettata con attenzione.

---

## Estrarre informazioni

Dopo avere progettato lo schema, creato le tabelle e popolato il database, vogliamo finalmente utilizzare i dati.

Potremmo chiedere:

> mostrami tutte le persone il cui cognome è Rossi.

Oppure:

> per ogni cognome, dimmi quante persone lo possiedono.

Sono due interrogazioni differenti.

Possiamo immaginarle quasi in linguaggio naturale:

```text
Dammi tutte le persone
il cui cognome è Rossi
```

oppure:

```text
Per ogni cognome
conta quante persone lo possiedono
```

Il linguaggio che utilizzeremo per esprimere richieste di questo tipo è **SQL**.

SQL è prevalentemente un linguaggio **dichiarativo**:

> diciamo **che cosa** vogliamo ottenere, invece di specificare passo per passo l'algoritmo che deve cercarlo.

Possiamo quindi distinguere almeno tre operazioni:

```text
MIGRARE
POPOLARE
ESTRARRE
```

e collegarle così:

```text
SCHEMA
   │
   │ migrazione
   ▼
NUOVO SCHEMA


SCHEMA
   │
   │ popolamento / ingestion
   ▼
DATI


DATI
   │
   │ interrogazione SQL
   ▼
INFORMAZIONI ESTRATTE
```

Sono momenti differenti del lavoro sui database.

Nel corso cercheremo di non studiarli come mondi completamente separati.

Non avrebbe molto senso fare mesi di sola progettazione e soltanto dopo iniziare a vedere che cosa possiamo fare con i dati.

L'idea è procedere, almeno in parte, su **due binari paralleli**:

```text
        PROGETTAZIONE
             │
             │
             ▼

==============================>

             ▲
             │
        SQL / ESTRAZIONE
```

Da una parte lavoreremo su:

- requisiti;
- entità;
- relazioni;
- molteplicità;
- trasformazione in tabelle.

Dall'altra inizieremo a ragionare su:

- dati;
- interrogazioni;
- filtraggio;
- raggruppamento;
- SQL.

Le due parti finiranno naturalmente per incontrarsi, perché una query può essere costruita bene soltanto se comprendiamo **come sono organizzati i dati e come sono collegati fra loro**.

Una cattiva progettazione può infatti rendere difficili anche domande semplici.

```text
BUONA PROGETTAZIONE
        ↓
DATI BEN ORGANIZZATI
        ↓
QUERY PIÙ NATURALI
        ↓
RISULTATI PIÙ AFFIDABILI
```

Pensiamo, per esempio, al settore sanitario.

Un ospedale può utilizzare molti sistemi informativi:

```text
pazienti
ricoveri
esami
reparti
medici
prenotazioni
referti
...
```

Questi sistemi possono essere stati realizzati in periodi differenti, da fornitori differenti e secondo modelli differenti.

Se i dati sono organizzati male o i sistemi non sono stati progettati per comunicare fra loro, anche un'interrogazione apparentemente semplice può diventare complessa o lenta.

```text
CATTIVA PROGETTAZIONE
        ↓
DATI DIFFICILI DA COLLEGARE
        ↓
QUERY COMPLESSE O LENTE
```

Nel settore sanitario si aggiunge inoltre un'altra questione: i dati trattati possono essere estremamente delicati.

Non abbiamo soltanto:

```text
nome
cognome
indirizzo
```

ma anche informazioni relative a:

```text
malattie
diagnosi
esami
terapie
ricoveri
```

Una buona progettazione deve quindi tenere contemporaneamente conto almeno di:

```text
ORGANIZZAZIONE DEI DATI
          +
PROTEZIONE DEI DATI
```

Più il sistema cresce, più entrambe le questioni diventano importanti.

---

## Che cosa deve entrare nel modello?

A questo punto possiamo tornare a una domanda fatta durante la lezione.

Nel diagramma relativo alla scuola:

> Perché non inseriamo anche l'entità `SCUOLA`?

La scuola esiste davvero.

Potremmo disegnare:

```text
[SCUOLA]
    │
    │
    ▼
[CLASSE]
    │
    │
    ▼
[ALUNNO]
```

Perché allora non dobbiamo necessariamente inserirla?

Perché il fatto che qualcosa esista nella realtà non significa che debba automaticamente comparire nel nostro modello.

Pensiamo a un esempio volutamente assurdo.

L'insegnante indossa una camicia di un certo colore:

```text
colore_camicia_docente = ...
```

L'informazione appartiene alla realtà.

Ma serve al nostro sistema scolastico?

No.

Quindi:

> **un'informazione può essere vera e contemporaneamente irrilevante per il modello.**

La stessa cosa può accadere con `SCUOLA`.

Se progettiamo un sistema che deve funzionare **soltanto nella nostra scuola**, possiamo immaginare il nostro mondo così:

```text
+-----------------------------------------+
|            LA NOSTRA SCUOLA            |
|                                         |
|   CLASSI                                |
|   ALUNNI                                |
|   DOCENTI                               |
|   ...                                   |
|                                         |
+-----------------------------------------+
```

Tutto ciò che modelliamo appartiene implicitamente a quella stessa scuola.

In questo caso inserire:

```text
[SCUOLA]
```

potrebbe non aggiungere alcuna informazione.

È un po' come immaginare una mosca che viva sempre dentro una stanza.

Per quella mosca il proprio mondo è:

```text
+-----------------------+
|       LA STANZA       |
|                       |
|         mosca         |
|                       |
+-----------------------+
```

Ciò che si trova fuori non fa parte del mondo che stiamo descrivendo.

Allo stesso modo, se il nostro sistema vive interamente dentro una singola scuola, la scuola può rimanere **contesto implicito**.

Ma se allarghiamo il problema e vogliamo progettare un sistema utilizzato da:

```text
Scuola A
Scuola B
Scuola C
Scuola D
...
```

allora diventa indispensabile sapere:

> a quale scuola appartiene questa classe?

A quel punto avremo bisogno anche di:

```text
[SCUOLA] -------- ◇ APPARTENENZA ◇ -------- [CLASSE]
```

Quindi:

```text
SISTEMA PER UNA SOLA SCUOLA
→ SCUOLA può essere superflua

SISTEMA PER MOLTE SCUOLE
→ SCUOLA diventa necessaria
```

Non è cambiata la realtà.

È cambiato **il confine del sistema**.

Lo stesso ragionamento vale per il ristorante.

Se realizziamo un sistema soltanto per il ristorante del signor Cesare:

```text
+------------------------------------+
|       RISTORANTE DEL SIGNOR        |
|             CESARE                 |
|                                    |
| TAVOLI                             |
| SERVIZI                            |
| COMANDE                            |
| PIATTI                             |
| ...                                |
+------------------------------------+
```

l'informazione:

```text
questo tavolo appartiene al ristorante del signor Cesare
```

è sempre identica.

Potrebbe quindi essere inutile rappresentarla.

Se invece progettiamo il sistema per una catena di ristoranti:

```text
[RISTORANTE]
     │
     ├── sede 1
     ├── sede 2
     ├── sede 3
     └── ...
```

allora dobbiamo distinguere:

- a quale sede appartiene un tavolo;
- quale sede ha prodotto una certa vendita;
- quale sede ha un certo flusso di cassa;
- e così via.

In quel caso `RISTORANTE` diventa un'entità importante.

Questo ci porta a una cautela generale.

Durante un'intervista o l'analisi dei requisiti possiamo sottolineare molte parole importanti.

Ma:

> **parola importante ≠ automaticamente entità**

Se leggiamo:

```text
"Il ristorante ha dei tavoli..."
```

la parola:

```text
RISTORANTE
```

può essere fondamentale per capire il contesto, ma non deve necessariamente diventare:

```text
[RISTORANTE]
```

nel diagramma.

Dobbiamo domandarci:

> devo memorizzare più istanze di questa cosa?

> devo distinguere una di queste istanze dalle altre?

> mi serve per rispondere alle domande richieste dal sistema?

Sono i requisiti a stabilire ciò che deve entrare nel modello.

---

## Un percorso iterativo

Anche il modo in cui affronteremo questi argomenti sarà progressivo.

Non faremo necessariamente:

```text
prima TUTTI i requisiti
poi TUTTO il modello E-R
poi TUTTA la progettazione logica
poi FINALMENTE le tabelle
```

senza mai vedere dove stiamo andando.

Il percorso sarà più iterativo:

```text
REQUISITI
   ↓
primo modello
   ↓
prime tabelle
   ↓
vediamo cosa succede
   ↓
torniamo al modello
   ↓
lo raffiniamo
   ↓
nuove tabelle
   ↓
...
```

Abbiamo già intravisto il risultato finale, anche se non possediamo ancora tutti gli strumenti per costruirlo correttamente.

Poi torniamo indietro e approfondiamo ogni passaggio.

Questo è utile anche per capire perché le molteplicità sono così importanti.

Quando passeremo dal modello E-R alle tabelle, il tipo di relazione influenzerà direttamente il modo in cui costruiremo il database.

Per esempio:

```text
ALUNNO → una sola CLASSE
```

può permettere di rappresentare il riferimento alla classe direttamente nei dati dell'alunno.

Ma se abbiamo:

```text
molti ↔ molti
```

non possiamo semplicemente inserire un singolo valore come se dall'altra parte esistesse una sola possibilità.

Dovremo trovare un'altra soluzione.

Ed è proprio qui che il rombo della relazione comincia a mostrare tutta la sua utilità.

---

## Il procedimento da ricordare

Torniamo infine all'esempio fondamentale:

```text
[CLASSE] ───── 1 ───── ◇ APPARTENENZA ◇ ───── (1,N) ───── [ALUNNO]
```

Per stabilire la molteplicità sul ramo verso `ALUNNO` ci chiediamo:

> Una classe può contenere più alunni?

Sì.

Il massimo è quindi:

```text
N
```

Se decidiamo che una classe deve avere almeno un alunno:

```text
(1,N)
```

Per stabilire invece la molteplicità sul ramo verso `CLASSE` ci chiediamo:

> Un alunno può appartenere contemporaneamente a più classi?

Nel nostro modello:

> no.

Quindi:

```text
1
```

In generale, dato:

```text
[A] -------- ◇ RELAZIONE ◇ -------- [B]
```

per determinare la molteplicità sul ramo verso `B`, parto da una singola istanza di `A`:

```text
una A
```

attraverso la relazione:

```text
A → RELAZIONE → B
```

e mi domando:

> Quante istanze di B possono essere associate?

Prima determino il massimo:

```text
1
```

oppure:

```text
N
```

Poi determino il minimo chiedendomi:

> Può non essercene nessuna?

Se sì:

```text
0
```

se no:

```text
1
```

Ottengo così una delle quattro forme fondamentali:

```text
(0,1)
(1,1)
(0,N)
(1,N)
```

Poi ripeto **esattamente lo stesso ragionamento nel verso opposto**.

Possiamo raccogliere l'intero percorso in un unico schema:

```text
                         REALTÀ
                            │
                            ▼
                        REQUISITI
                            │
                  selezionano ciò che serve
                            │
                            ▼
                       MODELLO E-R
                            │
              ┌─────────────┴─────────────┐
              │                           │
           ENTITÀ                     RELAZIONI
              │                           │
        rettangoli                     rombi
                                          │
                                          ▼
                                       RAMI
                                          │
                                          ▼
                                   MOLTEPLICITÀ
                                   minimo, massimo
                                          │
                         ┌────────────────┴───────────────┐
                         │                                │
                        1:N                              N:N
                         │                                │
                         └────────────────┬───────────────┘
                                          │
                                          ▼
                               PROGETTAZIONE LOGICA
                                          │
                                          ▼
                                     SCHEMA DB
                                          │
                                  tabelle + colonne
                                          │
                                          ▼
                                     POPOLAMENTO
                                          │
                                          ▼
                                        DATI
                                          │
                                          ▼
                                    SQL / QUERY
                                          │
                                          ▼
                                   INFORMAZIONI
```

Da qui in avanti useremo quindi stabilmente la forma:

```text
[A] -------- ◇ RELAZIONE ◇ -------- [B]
```

Il rombo rappresenta esplicitamente la relazione.

Preferiremo nomi come:

```text
APPARTENENZA
ISCRIZIONE
CITTADINANZA
```

Ogni relazione possiede dei rami e ogni ramo possiede una propria molteplicità.

Il massimo ci permette di distinguere:

```text
1 : 1
1 : N
N : N
```

Il minimo ci permette di stabilire se la partecipazione può essere facoltativa oppure obbligatoria:

```text
facoltativa → 0
obbligatoria → 1
```

Le forme fondamentali sono:

```text
(0,1)
(1,1)
(0,N)
(1,N)
```

Ma la cosa più importante da ricordare è un'altra:

> **le molteplicità non si indovinano dal nome delle entità.**

Derivano dai **requisiti**.

E i requisiti dipendono dalla parte di realtà che abbiamo deciso di rappresentare.

Il modello non deve riprodurre tutto il mondo.

Deve riprodurre **bene la parte di mondo che serve al nostro problema**.
