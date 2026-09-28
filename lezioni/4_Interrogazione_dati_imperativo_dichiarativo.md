# 5SIA — Dalle tabelle all'interrogazione dei dati

## Ripresa: come rappresentiamo i dati?

Nella lezione precedente abbiamo visto che un possibile modo per organizzare i dati consiste nell'utilizzare **tabelle**.

In generale:

- una tabella rappresenta una certa **entità**;
- le colonne rappresentano gli **attributi** dell'entità;
- ogni riga rappresenta una particolare **occorrenza**, o **record**.

Per esempio, per rappresentare gli alunni possiamo avere una tabella di questo tipo:

| codice_fiscale | nome | cognome | data_nascita |
|---|---|---|---|
| ... | Mario | Rossi | ... |
| ... | Lia | Verdi | ... |
| ... | Sofia | Bianchi | ... |

Gli attributi sono quindi, ad esempio, il nome, il cognome, il codice fiscale e la data di nascita.

Allo stesso modo possiamo avere una tabella che rappresenta i **corsi**:

| livello | orario | costo |
|---|---|---:|
| principiante | 19:00–20:00 | 50 |
| avanzato | 19:00–20:00 | 70 |
| ... | ... | ... |

Il punto importante non è il contenuto specifico degli esempi, ma il fatto che i dati vengano suddivisi in strutture coerenti, ciascuna dedicata a un certo tipo di oggetto.

---

## Rappresentare i collegamenti tra i dati

Non basta però rappresentare separatamente alunni e corsi.

Dobbiamo anche poter esprimere informazioni del tipo:

> Mario Rossi è iscritto al corso principiante delle 19:00.

Per farlo possiamo introdurre una nuova tabella che rappresenta il **collegamento** tra un alunno e un corso.

Per costruire una tabella del genere bisogna però essere in grado di capire, senza ambiguità, **quale alunno** e **quale corso** stiamo indicando.

### Identificare univocamente un elemento

Per gli alunni possiamo utilizzare, per esempio, il **codice fiscale**, perché identifica una persona in modo univoco.

Non è invece sufficiente utilizzare il solo nome o il solo cognome: possono infatti esistere più persone con lo stesso nome.

Lo stesso problema si presenta con i corsi.

Se nella tabella esistesse un solo corso per ogni livello, potremmo forse utilizzare il livello:

> principiante

Ma se esistono due corsi per principianti, il livello non è più sufficiente.

Nemmeno l'orario, preso da solo, garantisce necessariamente l'univocità.

Possiamo allora combinare più attributi:

> corso **principiante** delle **19:00–20:00**

In questo semplice esempio la coppia:

```text
(livello, orario)
```

può essere utilizzata per individuare il corso.

L'idea generale è molto importante:

> per collegare correttamente informazioni presenti in tabelle diverse dobbiamo poter identificare senza ambiguità gli elementi coinvolti.

In alcuni casi possiamo utilizzare un attributo già esistente; in altri casi può essere conveniente introdurre un identificatore apposito.

---

## Popolare una base di dati

Una volta definita la struttura, dobbiamo inserire i dati.

Si usa spesso il verbo **popolare**:

> **popolare una base di dati** significa inserire al suo interno le informazioni.

Possiamo quindi immaginare una base di dati composta da molte tabelle e da un numero anche molto grande di record.

Nel nostro esempio abbiamo pochi alunni e pochi corsi, ma una base di dati reale può contenere milioni di record.

A questo punto nasce la domanda fondamentale:

> **Perché raccogliamo e organizziamo tutti questi dati?**

Una delle ragioni principali è poterli **interrogare**, cioè ricavare rapidamente le informazioni che ci interessano.

---

# Interrogare i dati

Una base di dati non è utile soltanto perché conserva informazioni.

Diventa particolarmente utile quando possiamo formulare domande come:

- Quale persona è associata a una certa targa?
- Quali alunni sono iscritti a un certo corso?
- Quanti alunni frequentano il corso principiante?
- Quali corsi iniziano alle 19:00?
- Quali sono gli alunni che soddisfano una certa condizione?

Possiamo quindi pensare a una base di dati come a una grande raccolta di informazioni dalla quale vogliamo **estrarre** ciò che ci serve.

Il problema diventa:

> **Come possiamo spiegare al computer quale informazione vogliamo ottenere?**

---

# Un primo modo: programmare il procedimento

Finora abbiamo imparato a risolvere problemi soprattutto utilizzando linguaggi di programmazione come Python.

Immaginiamo, per esempio, che i dati siano memorizzati in una struttura simile a una lista di oggetti JSON:

```json
[
  {
    "codice_fiscale": "...",
    "livello": "principiante"
  },
  {
    "codice_fiscale": "...",
    "livello": "avanzato"
  }
]
```

Supponiamo di voler sapere:

> Quanti alunni sono iscritti al corso principiante?

Con le tecniche di programmazione che già conosciamo potremmo procedere in questo modo:

1. inizializzare un contatore;
2. scorrere tutti gli elementi;
3. controllare, per ogni elemento, se il corso è quello desiderato;
4. se la condizione è vera, incrementare il contatore;
5. continuare fino alla fine.

In pseudocodice:

```text
contatore = 0

per ogni elemento:
    se elemento appartiene al corso richiesto:
        contatore = contatore + 1
```

In Python potremmo immaginare qualcosa di simile:

```python
contatore = 0

for elemento in dati:
    if elemento["livello"] == "principiante":
        contatore += 1
```

In questo caso stiamo dicendo al computer **come deve procedere**, passo dopo passo.

---

# Il paradigma imperativo

Questo modo di programmare viene detto **imperativo**.

Il termine richiama l'idea del comando:

> fai questo, poi fai quello, controlla questa condizione, modifica questa variabile...

Nel paradigma imperativo descriviamo quindi il **procedimento**.

Per ottenere il numero degli iscritti a un corso diciamo, per esempio:

```text
prendi un elemento
controlla il suo corso
se è quello desiderato incrementa un contatore
passa all'elemento successivo
ripeti
```

L'idea fondamentale è:

> **nel paradigma imperativo diciamo al computer COME ottenere il risultato.**

Questo è il modo di ragionare che abbiamo utilizzato molto negli anni precedenti studiando gli algoritmi e la programmazione.

---

# Un altro modo: dichiarare ciò che vogliamo

Esiste però un altro approccio, molto vicino al modo in cui formuleremmo una richiesta nel linguaggio naturale.

Se parlassimo con una persona, probabilmente non diremmo:

> Prendi il primo elemento, controlla il corso, incrementa un contatore, passa al secondo elemento...

Diremmo semplicemente:

> **Conta gli alunni iscritti al corso principiante.**

In questa frase non specifichiamo il procedimento.

Dichiariamo semplicemente **quale risultato vogliamo ottenere**.

Questo modo di ragionare viene detto **dichiarativo**.

> **Nel paradigma dichiarativo diciamo CHE COSA vogliamo ottenere, senza descrivere passo per passo COME ottenerlo.**

La differenza tra i due approcci è concettualmente molto importante.

### Imperativo

```text
COME devo ottenere il risultato?
```

### Dichiarativo

```text
QUALE risultato voglio?
```

---

## Un confronto

Supponiamo di voler conoscere gli alunni iscritti a un certo corso.

### Forma imperativa

```text
Scorri tutti gli alunni.
Per ciascun alunno controlla il corso.
Se il corso è quello desiderato, conserva l'alunno.
Alla fine mostra gli alunni trovati.
```

Qui stiamo descrivendo un algoritmo.

### Forma dichiarativa

```text
Mostrami gli alunni iscritti al corso principiante.
```

Qui descriviamo direttamente ciò che ci interessa.

Nel secondo caso sarà il sistema a stabilire in quale modo concreto recuperare l'informazione.

---

# Dal linguaggio naturale a un linguaggio formale

Il linguaggio naturale è molto comodo per esprimere una richiesta:

> Conta gli alunni iscritti a un determinato corso.

Un computer, però, ha bisogno di un linguaggio più preciso.

Occorre quindi utilizzare un **linguaggio formale**, con regole sintattiche ben definite e un significato non ambiguo.

Per interrogare le basi di dati utilizzeremo principalmente un linguaggio chiamato:

# SQL

SQL è un linguaggio nato molti decenni fa ma ancora oggi utilizzatissimo.

Uno dei motivi della sua diffusione è che permette di esprimere molte richieste sui dati in una forma relativamente semplice e vicina, almeno nella struttura generale, al linguaggio naturale.

Per esempio, invece di spiegare al computer tutti i passaggi necessari per cercare determinati dati, possiamo formulare direttamente una richiesta.

In questa prima panoramica non ci interessa ancora studiare la sintassi di SQL nel dettaglio.

Ci interessa soprattutto comprendere **il modo di ragionare** che utilizzeremo.

---

# Query e interrogazioni SQL

Una richiesta rivolta a una base di dati viene comunemente chiamata **query**.

Possiamo quindi considerare una query come una specie di domanda formulata alla base di dati.

Per esempio:

> Quali sono gli alunni iscritti al corso principiante?

oppure:

> Quanti alunni sono iscritti a quel corso?

Queste domande, espresse inizialmente in linguaggio naturale, potranno essere trasformate in precise **interrogazioni SQL**.

Una query SQL è quindi una frase scritta secondo le regole del linguaggio SQL che permette di richiedere al sistema determinate informazioni.

È importante però non confondere SQL con il linguaggio naturale:

> SQL può ricordare una frase inglese, ma rimane un **linguaggio informatico formale**, quindi deve essere scritto rispettando regole precise.

---

# Il passaggio concettuale fondamentale

Il punto centrale della lezione non è ancora imparare comandi SQL a memoria.

È comprendere il cambiamento di prospettiva.

Negli anni precedenti ci siamo abituati soprattutto a pensare così:

```text
problema
   ↓
algoritmo
   ↓
sequenza di istruzioni
   ↓
risultato
```

Con l'interrogazione dei dati inizieremo spesso a ragionare invece così:

```text
domanda sui dati
   ↓
descrizione del risultato desiderato
   ↓
query
   ↓
il sistema determina come ottenere il risultato
```

In altre parole:

```text
PROGRAMMAZIONE IMPERATIVA
"Ti spiego come fare"

        ↓

INTERROGAZIONE DICHIARATIVA
"Ti dico cosa voglio"
```

Questa distinzione tra **imperativo** e **dichiarativo** è una distinzione generale dell'informatica e non riguarda soltanto le basi di dati.

Nello studio delle basi di dati, però, diventerà particolarmente importante.

# Concetti da ricordare

- Una **tabella** rappresenta normalmente un insieme di elementi dello stesso tipo.
- Le **colonne** rappresentano attributi.
- Le **righe** rappresentano record o occorrenze.
- Per collegare correttamente dati diversi è necessario poter identificare gli elementi senza ambiguità.
- **Popolare** una base di dati significa inserirvi i dati.
- Una volta memorizzati i dati, vogliamo poterli **interrogare**.
- Con un approccio **imperativo** descriviamo passo per passo **come** ottenere un risultato.
- Con un approccio **dichiarativo** descriviamo **quale** risultato vogliamo ottenere.
- SQL è un linguaggio formale utilizzato per lavorare con le basi di dati.
- Una **query** è un'interrogazione, cioè una richiesta formulata alla base di dati.
- Le query SQL costituiranno una parte importante del lavoro successivo.

