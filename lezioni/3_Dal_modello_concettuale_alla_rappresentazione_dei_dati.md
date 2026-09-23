# Lezione 3 – Dal modello concettuale alla rappresentazione dei dati

## Dalla rappresentazione della realtà alla rappresentazione dei dati

Nella lezione precedente avevamo ragionato sulla necessità di costruire un **modello della realtà**.

Partendo dall'esempio della piscina avevamo individuato alcuni elementi significativi, per esempio:

* gli **allievi**;
* i **corsi**;
* gli **istruttori**;
* le relazioni esistenti tra questi elementi.

Avevamo quindi iniziato a utilizzare il modello **Entità-Relazione**, rappresentando graficamente la struttura del problema attraverso:

* **entità**;
* **attributi**;
* **relazioni**.

La nuova domanda affrontata durante questa lezione è stata però diversa:

> Una volta costruito il modello, come possiamo rappresentare concretamente i dati?

Il punto di partenza è stato volutamente lasciato aperto. Non è stata proposta subito la soluzione basata sulle tabelle: abbiamo invece provato a immaginare diversi modi per memorizzare un insieme di dati relativi agli allievi e ai corsi della piscina.

## Il diagramma E-R rappresenta la struttura, non i dati

Una delle prime idee emerse è stata quella di utilizzare direttamente il diagramma E-R anche per rappresentare i singoli dati.

Per esempio, se abbiamo l'entità:

```text
ALLIEVO
- nome
- cognome
- data di nascita
```

si potrebbe essere tentati di inserire nel diagramma i diversi allievi:

```text
Mario Rossi
Luca Bianchi
Anna Verdi
...
```

Questa soluzione però diventa rapidamente poco pratica.

Il motivo è che un diagramma E-R ha uno scopo differente.

Il modello E-R descrive soprattutto la **struttura delle informazioni**.

Ci dice, per esempio:

```text
ALLIEVO -------- frequenta -------- CORSO
```

e quindi ci permette di ragionare sul fatto che nel nostro sistema esistono:

* degli allievi;
* dei corsi;
* una relazione tra allievi e corsi.

Non serve invece principalmente a elencare tutti gli allievi effettivamente presenti nella piscina.

Possiamo quindi distinguere due livelli:

```text
MODELLO

ALLIEVO
- Nome
- Cognome
- DataNascita
```

e:

```text
DATI

Mario Rossi      12/03/2008
Anna Bianchi     24/07/2007
Luca Verdi       15/11/2008
...
```

Il primo descrive **come sono fatti i dati**.

Il secondo contiene **i dati veri e propri**.

Questa distinzione è fondamentale:

> **Il diagramma E-R è soprattutto un diagramma strutturale: rappresenta il modello dei dati, non l'elenco delle singole informazioni memorizzate.**

---

# La tabella come lista ben organizzata

Cercando una rappresentazione più adatta, siamo arrivati gradualmente a una struttura molto semplice: una **lista ben formattata**.

Per esempio:

| Nome  | Cognome | Data di nascita |
| ----- | ------- | --------------- |
| Mario | Rossi   | 12/03/2008      |
| Anna  | Bianchi | 24/07/2007      |
| Luca  | Verdi   | 15/11/2008      |

Questa struttura è una **tabella**.

La tabella permette di distinguere chiaramente:

* le caratteristiche che vogliamo memorizzare;
* i singoli elementi che stiamo descrivendo.

Le **colonne** descrivono quali informazioni possiede un allievo:

```text
Nome
Cognome
DataNascita
```

Le **righe** rappresentano invece i singoli allievi.

Possiamo quindi cominciare a vedere una corrispondenza tra il modello E-R e la rappresentazione tabellare:

```text
ENTITÀ       → TABELLA

ATTRIBUTI    → COLONNE

SINGOLI
ELEMENTI     → RIGHE
```

Per esempio, l'entità:

```text
ALLIEVO
- Nome
- Cognome
- DataNascita
```

può diventare:

| Nome  | Cognome | DataNascita |
| ----- | ------- | ----------- |
| Mario | Rossi   | 12/03/2008  |
| Anna  | Bianchi | 24/07/2007  |

Analogamente:

```text
CORSO
- Nome
- Livello
- Giorno
```

può essere rappresentato da una tabella:

| NomeCorso          | Livello    | Giorno    |
| ------------------ | ---------- | --------- |
| Nuoto principianti | Base       | Lunedì    |
| Nuoto intermedio   | Intermedio | Mercoledì |
| Nuoto avanzato     | Avanzato   | Venerdì   |

Fino a questo punto la trasformazione è abbastanza naturale.

La vera difficoltà emerge quando dobbiamo rappresentare le **relazioni**.

---

# Come rappresentiamo una relazione?

Consideriamo:

```text
ALLIEVO -------- frequenta -------- CORSO
```

Dobbiamo memorizzare non soltanto quali allievi esistono e quali corsi esistono, ma anche:

> **quale allievo frequenta quale corso?**

Durante la lezione abbiamo esplorato diverse possibilità.

Ed è proprio confrontando queste soluzioni che sono emersi alcuni dei principi più importanti.

---

## Primo tentativo: mettere tutto nella stessa tabella

Una possibilità consiste nel costruire una grande tabella contenente sia i dati dell'allievo sia quelli del corso.

Per esempio:

| Nome  | Cognome | DataNascita | Corso          | Livello  | Giorno  |
| ----- | ------- | ----------- | -------------- | -------- | ------- |
| Mario | Rossi   | 12/03/2008  | Nuoto base     | Base     | Lunedì  |
| Anna  | Bianchi | 24/07/2007  | Nuoto base     | Base     | Lunedì  |
| Luca  | Verdi   | 15/11/2008  | Nuoto avanzato | Avanzato | Venerdì |

Questa soluzione inizialmente sembra funzionare.

Ma osservandola meglio compare un problema evidente.

Le informazioni relative al corso vengono ripetute:

```text
Nuoto base | Base | Lunedì
Nuoto base | Base | Lunedì
Nuoto base | Base | Lunedì
...
```

Se il corso "Nuoto base" ha venti allievi, dovremmo ripetere venti volte le stesse informazioni.

Se il giorno del corso cambiasse da lunedì a martedì, dovremmo modificare tutte le righe corrispondenti.

Abbiamo quindi scoperto un primo problema importante:

> **Mescolare nella stessa tabella informazioni relative a oggetti diversi può produrre molte ripetizioni.**

Allievo e Corso sono due concetti differenti.

Era quindi ragionevole averli rappresentati come due entità differenti nel modello E-R, ed è altrettanto ragionevole rappresentarli attraverso due tabelle differenti.

---

# Secondo tentativo: una colonna per ogni corso

Abbiamo allora fatto un'altra ipotesi.

Supponiamo che nella piscina esistano soltanto tre corsi, uno per ogni livello:

```text
BASE
INTERMEDIO
AVANZATO
```

Potremmo costruire una tabella di questo tipo:

| Allievo      | Base | Intermedio | Avanzato |
| ------------ | ---- | ---------- | -------- |
| Mario Rossi  | X    |            |          |
| Anna Bianchi |      | X          |          |
| Luca Verdi   |      |            | X        |
| Sara Neri    | X    |            |          |

Anche questa soluzione sembra funzionare.

La presenza di una crocetta indica quale corso viene frequentato dall'allievo.

Ma questa rappresentazione dipende fortemente dall'ipotesi iniziale:

> esistono esattamente tre corsi.

Che cosa succederebbe se la piscina introducesse:

```text
Nuoto agonistico
Acquagym
Nuoto bambini
Recupero funzionale
...
```

Dovremmo aggiungere continuamente nuove colonne:

```text
Base
Intermedio
Avanzato
Agonistico
Acquagym
Bambini
...
```

Stiamo quindi utilizzando le **colonne**, che dovrebbero descrivere le caratteristiche di un allievo, per rappresentare invece l'esistenza dei corsi.

In altre parole:

```text
Nome
Cognome
DataNascita
```

sono caratteristiche dell'allievo.

Ma:

```text
NuotoBase
NuotoAvanzato
Acquagym
```

non sono realmente caratteristiche dell'allievo.

Sono altri oggetti del nostro modello.

Questa soluzione funziona solamente in casi molto rigidi e poco variabili.

---

# Una terza soluzione: rappresentare direttamente la relazione

A questo punto abbiamo provato una strada differente.

Se abbiamo già:

### ALLIEVO

| CodAllievo | Nome  | Cognome |
| ---------- | ----- | ------- |
| A1         | Mario | Rossi   |
| A2         | Anna  | Bianchi |
| A3         | Luca  | Verdi   |

e:

### CORSO

| CodCorso | NomeCorso        | Livello    |
| -------- | ---------------- | ---------- |
| C1       | Nuoto base       | Base       |
| C2       | Nuoto intermedio | Intermedio |
| C3       | Nuoto avanzato   | Avanzato   |

possiamo costruire una terza tabella che rappresenta direttamente il fatto che un allievo frequenta un corso:

### FREQUENTA

| Allievo | Corso |
| ------- | ----- |
| A1      | C1    |
| A2      | C2    |
| A3      | C3    |
| A1      | C2    |

Ogni riga rappresenta un fatto:

```text
A1 frequenta C1
A2 frequenta C2
A3 frequenta C3
A1 frequenta C2
```

In questo modo non dobbiamo ripetere tutte le informazioni dell'allievo e del corso.

Non scriviamo ogni volta:

```text
Mario Rossi
Nuoto base
Lunedì
Livello base
...
```

Scriviamo semplicemente:

```text
A1 → C1
```

Per poter fare questo abbiamo però bisogno di sapere con certezza che:

```text
A1
```

indichi uno e un solo allievo e che:

```text
C1
```

indichi uno e un solo corso.

Da qui è emerso naturalmente un altro concetto fondamentale.

---

# Identificare univocamente un elemento

Supponiamo di avere:

| Nome  | Cognome |
| ----- | ------- |
| Mario | Rossi   |
| Mario | Rossi   |

Sono la stessa persona inserita due volte?

Oppure sono due persone differenti con lo stesso nome?

Non possiamo saperlo.

Abbiamo quindi bisogno di trovare qualcosa che permetta di individuare **un solo elemento**.

Possiamo aggiungere per esempio:

| CodAllievo | Nome  | Cognome |
| ---------- | ----- | ------- |
| 1          | Mario | Rossi   |
| 2          | Mario | Rossi   |

Ora:

```text
CodAllievo = 1
```

individua esattamente una riga.

Allo stesso modo:

```text
CodAllievo = 2
```

individua l'altro Mario Rossi.

Abbiamo quindi introdotto il concetto di **unicità** o **univocità**.

Un valore utilizzato per identificare un elemento deve permettere di distinguere quell'elemento da tutti gli altri.

Possiamo immaginarlo come un'etichetta:

```text
1 → Mario Rossi
2 → Mario Rossi
3 → Anna Bianchi
```

La cosa interessante è che il codice non deve necessariamente avere un significato particolare.

Il suo scopo principale è:

> **identificare senza ambiguità un elemento.**

Questo permetterà poi alle diverse tabelle di fare riferimento agli stessi elementi senza dover ripetere continuamente tutte le loro informazioni.

---

# Ma serve sempre una tabella per rappresentare una relazione?

No.

Ed è proprio una delle osservazioni più importanti fatte durante la lezione.

Consideriamo una situazione più semplice.

Supponiamo che:

* ogni allievo possa frequentare **un solo corso**;
* un corso possa invece essere frequentato da molti allievi.

Abbiamo quindi una situazione del tipo:

```text
CORSO      ALLIEVO

C1  ←  A1
C1  ←  A2
C1  ←  A3
C2  ←  A4
C2  ←  A5
```

In questo caso potremmo rappresentare direttamente il corso frequentato all'interno della tabella ALLIEVO:

| CodAllievo | Nome  | Cognome | CodCorso |
| ---------- | ----- | ------- | -------- |
| A1         | Mario | Rossi   | C1       |
| A2         | Anna  | Bianchi | C1       |
| A3         | Luca  | Verdi   | C1       |
| A4         | Sara  | Neri    | C2       |

Non stiamo copiando dentro ALLIEVO tutte le informazioni del corso.

Non scriviamo:

```text
Nuoto base
Lunedì
ore 17:00
Istruttore Rossi
...
```

Scriviamo soltanto il suo identificatore:

```text
C1
```

che rimanda alla tabella CORSO.

Quindi una relazione può essere rappresentata in modi differenti a seconda della sua struttura.

Se ogni allievo frequenta un solo corso, può essere sufficiente aggiungere alla tabella ALLIEVO un riferimento al corso.

Se invece un allievo può frequentare più corsi e ogni corso può avere più allievi, diventa molto più naturale utilizzare una tabella separata:

```text
FREQUENTA
```

con righe del tipo:

```text
A1 | C1
A1 | C2
A2 | C1
```

La scelta della rappresentazione dipende quindi da **come sono collegati tra loro gli elementi della realtà**.

Ed è proprio per questo che prima di costruire le tabelle abbiamo bisogno di comprendere bene il modello concettuale.

---

# Il percorso seguito

Il percorso delle ultime lezioni comincia quindi a diventare più chiaro.

Non siamo partiti dalle tabelle.

Siamo partiti dalla realtà.

```text
REALTÀ
   ↓
comprensione del problema
   ↓
REQUISITI
   ↓
MODELLO CONCETTUALE
   ↓
ENTITÀ - ATTRIBUTI - RELAZIONI
   ↓
RAPPRESENTAZIONE DEI DATI
   ↓
TABELLE
```

Il modello E-R e le tabelle non sono quindi due strumenti alternativi.

Servono a due scopi differenti.

Il modello E-R permette soprattutto di ragionare sulla **struttura della realtà che vogliamo rappresentare**.

Le tabelle permettono di organizzare concretamente **i dati relativi ai singoli elementi**.

Possiamo sintetizzare:

```text
ENTITÀ       → TABELLA
ATTRIBUTI    → COLONNE
OCCORRENZE   → RIGHE
```

Per le relazioni il passaggio è meno immediato.

Abbiamo visto che possono essere rappresentate, a seconda della situazione:

* attraverso un riferimento presente in una delle tabelle;
* oppure attraverso una nuova tabella che rappresenta direttamente la relazione.

---

# Cosa abbiamo scoperto attraverso i tentativi

Durante la lezione non siamo partiti dalle regole già pronte.

Abbiamo provato diverse rappresentazioni e osservato i problemi che emergevano.

### Usare direttamente il diagramma E-R

Non è adatto a contenere grandi quantità di dati perché il suo compito principale è rappresentare la **struttura**.

### Mettere tutti i dati in una tabella unica

Produce facilmente molte informazioni duplicate.

### Creare una colonna per ogni possibile corso

Può funzionare solo quando l'insieme dei corsi è piccolo, fisso e conosciuto in anticipo. Diventa rapidamente poco flessibile.

### Separare gli oggetti in tabelle e rappresentare i collegamenti

Permette invece di memorizzare le informazioni una sola volta e di collegarle attraverso identificatori.

Queste difficoltà non sono state errori inutili.

Sono state proprio ciò che ci ha permesso di capire **perché la rappresentazione tabellare viene costruita in un determinato modo**.

---

# Idee fondamentali della lezione

Alla fine del percorso possiamo fissare alcuni concetti.

Un diagramma E-R rappresenta principalmente **la struttura dei dati**, non i singoli dati.

Una **entità** può essere rappresentata attraverso una **tabella**.

Gli **attributi** dell'entità diventano le **colonne**.

I singoli elementi diventano le **righe** della tabella.

È utile poter individuare ogni elemento in maniera **univoca**, attraverso uno o più valori che permettano di distinguerlo dagli altri.

Le relazioni tra le entità devono anch'esse essere rappresentate nei dati.

A seconda del tipo di relazione, possiamo:

```text
aggiungere a una tabella
il riferimento a un'altra tabella
```

oppure:

```text
creare una nuova tabella
che rappresenta la relazione
```

Il punto centrale non è quindi imparare immediatamente una serie di regole meccaniche.

È comprendere il passaggio:

> **dal modello della realtà alla rappresentazione organizzata dei dati.**

Ed è proprio osservando quali problemi nascono dalle diverse soluzioni che possiamo capire perché le tabelle sono organizzate nel modo che approfondiremo nelle prossime lezioni.
