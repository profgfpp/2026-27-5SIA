# Dall'elaborazione dei dati alle basi di dati

## Da dove partiamo

L'anno scorso abbiamo lavorato soprattutto sulla **programmazione**: abbiamo imparato a costruire algoritmi e programmi capaci di ricevere dati, elaborarli e produrre risultati.

Possiamo riassumere quanto studiato con il classico schema:

```text
INPUT → PROGRAMMA → OUTPUT
             ↕
          MEMORIA
```

È uno schema ormai “consumato” dai professori di informatica, ma rimane utile perché rappresenta bene il funzionamento essenziale di un programma.

Occorre però distinguere due termini che spesso vengono usati come sinonimi:

- un **algoritmo** è una sequenza ordinata di istruzioni che descrive come risolvere un problema;
- un **programma** è la realizzazione concreta di quell'algoritmo in un linguaggio comprensibile ed eseguibile dal computer.

Il programma riceve degli input, li conserva temporaneamente in memoria, li elabora seguendo un algoritmo e produce degli output.

Quest'anno partiremo proprio da qui, ma sposteremo l'attenzione su una nuova domanda:

> Un programma sa elaborare i dati. Ma come possiamo conservarli, organizzarli e ritrovarli quando diventano molti?

## I dati rappresentati con JSON

L'anno scorso abbiamo utilizzato anche il formato JSON per rappresentare dati strutturati.

Consideriamo questo esempio:

```json
[
  {
    "nome": "Anna",
    "classe": "5A",
    "voto": 8
  },
  {
    "nome": "Luca",
    "classe": "5B",
    "voto": 6
  },
  {
    "nome": "Sara",
    "classe": "5A",
    "voto": 9
  }
]
```

L'oggetto complessivo è una **lista**. Ogni elemento della lista è, a sua volta, un oggetto formato da coppie **chiave-valore**.

Per esempio, nel primo elemento troviamo:

```text
chiave: nome      valore: Anna
chiave: classe    valore: 5A
chiave: voto      valore: 8
```

In Python potremmo interpretare questa struttura come una **lista di dizionari**.

L'esempio non contiene soltanto valori messi insieme casualmente. Sta rappresentando, cioè sta **modellando**, una piccola parte della realtà scolastica. Abbiamo deciso che, per ogni studente, ci interessano tre informazioni: il nome, la classe e il voto.

Modellare una realtà significa quindi scegliere quali oggetti rappresentare e quali loro caratteristiche conservare. Nel nostro esempio abbiamo semplificato molto la realtà: uno studente possiede tante altre caratteristiche, ma abbiamo selezionato soltanto quelle utili per il problema che vogliamo affrontare.

## Elaborare i dati con un programma

Una volta caricati i dati JSON in una variabile Python, possiamo eseguire molte operazioni.

Possiamo, per esempio:

- contare gli studenti;
- cercare uno studente;
- trovare gli appartenenti a una classe;
- modificare un voto;
- calcolare una media;
- ordinare gli studenti;
- produrre un risultato da mostrare all'utente.

Per visualizzare i nomi degli studenti della `5A` potremmo scrivere:

```python
for studente in studenti:
    if studente["classe"] == "5A":
        print(studente["nome"])
```

Il programma prende uno studente alla volta e controlla il valore associato alla chiave `classe`. Se quel valore è uguale a `5A`, stampa il nome dello studente.

Il codice descrive quindi un procedimento:

```text
prendi uno studente
controlla la sua classe
se la classe è 5A, stampa il nome
continua con lo studente successivo
```

Questo è ciò che abbiamo imparato a fare attraverso la programmazione: indicare al computer **come elaborare i dati**.

## Il problema della persistenza

I dati JSON caricati in Python diventano una variabile. Possiamo modificarli, filtrare gli studenti, cambiare lettere minuscole in maiuscole, aggiungere elementi oppure eliminarli.

Ma che cosa succede quando il programma termina?

Normalmente i dati contenuti nelle variabili vengono perduti. La RAM è infatti una memoria **volatile**: conserva le informazioni soltanto mentre il programma e il dispositivo sono in funzione, poi va via come la neve al sole di marzo.

Se vogliamo ritrovare le informazioni in un momento successivo, dobbiamo trasferirle dalla memoria temporanea a una memoria permanente, per esempio salvandole su disco.

Questa capacità prende il nome di **persistenza**:

> La persistenza è la capacità di conservare i dati anche dopo la conclusione del programma che li ha utilizzati.

Una prima soluzione consiste nel salvare la variabile in un file JSON. Quando il programma verrà eseguito nuovamente, potrà leggere il file e ricostruire in memoria la struttura dati.

Per piccole quantità di informazioni questa soluzione può essere semplice ed efficace.

## Perché un file JSON non basta sempre

JSON è un formato molto utile. Permette di rappresentare dati strutturati ed è particolarmente diffuso nello scambio di informazioni attraverso il Web.

Il problema nasce quando aumentano la quantità dei dati e la complessità delle operazioni.

Con trenta studenti un file JSON può funzionare bene. Ma immaginiamo di dover gestire:

- 3.000 studenti;
- 30.000 studenti;
- milioni di persone o veicoli;
- voti, classi, docenti, materie e assenze;
- informazioni che cambiano continuamente.

Potremmo, almeno in teoria, inserire tutte le targhe dei veicoli italiani in un enorme file JSON. Il file, però, diventerebbe gigantesco e difficile da gestire.

Come potremmo trovare rapidamente soltanto i veicoli registrati in Piemonte? Potremmo certamente scrivere un programma Python che attraversa tutti i dati e applica un filtro. Non è impossibile, ma non è necessariamente il sistema più comodo ed efficiente.

Emergono anche altre domande:

- come possiamo modificare un solo dato all'interno di un file molto grande?
- come possiamo evitare informazioni duplicate?
- come colleghiamo un voto allo studente corretto?
- come organizziamo classi, studenti, docenti e materie?
- come possiamo recuperare rapidamente soltanto le informazioni che ci interessano?

A questo punto non abbiamo più bisogno soltanto di **salvare** i dati. Abbiamo bisogno di organizzarli in modo più adatto alla loro quantità e ai collegamenti che esistono tra loro.

## Dalle liste alle tabelle

Le basi di dati relazionali affrontano il problema rappresentando le informazioni attraverso delle **tabelle**.

In prima approssimazione possiamo immaginare qualcosa di simile a un insieme di fogli Excel. Ogni tabella rappresenta un particolare tipo di oggetto.

Potremmo avere, per esempio:

```text
STUDENTI
CLASSI
DOCENTI
MATERIE
VOTI
ASSENZE
ISTITUTI
```

La tabella `STUDENTI` potrebbe contenere:

| matricola | nome | cognome | classe |
|---|---|---|---|
| 101 | Anna | Rossi | 5A |
| 102 | Luca | Bianchi | 5B |
| 103 | Sara | Verdi | 5A |

I dati, però, non rimangono isolati. Sono collegati tra loro:

- un istituto contiene più classi;
- una classe comprende più studenti;
- uno studente riceve più voti;
- un docente insegna in più classi;
- una materia può essere insegnata da diversi docenti;
- ogni voto riguarda uno studente e una materia.

È proprio da questi collegamenti che deriva l'espressione **base di dati relazionale**.

Non si tratta semplicemente di avere tante tabelle. Il punto fondamentale è rappresentare in modo corretto le **relazioni tra i dati**.

Per esempio, possiamo chiederci:

> La classe deve essere una semplice scritta ripetuta dentro ogni studente oppure deve essere rappresentata separatamente e collegata agli studenti?

Questa domanda introduce il problema della progettazione delle basi di dati, che accompagnerà buona parte del percorso del quinto anno.

## Il nucleo della lezione

L'anno scorso abbiamo imparato soprattutto a elaborare i dati mediante algoritmi e programmi.

Quest'anno studieremo come:

- conservare i dati in maniera persistente;
- organizzarli quando diventano numerosi;
- rappresentare oggetti diversi mediante tabelle;
- riconoscere i collegamenti tra studenti, classi, docenti, materie e voti;
- scegliere una struttura adatta alla realtà che vogliamo descrivere.

Possiamo riassumere il passaggio in questo modo:

```text
PROGRAMMA
elabora i dati

MEMORIA RAM
contiene temporaneamente variabili e strutture dati

FILE JSON
permette una prima forma di persistenza

BASE DI DATI RELAZIONALE
organizza dati numerosi attraverso tabelle collegate
```

La terminologia tecnica deve aiutarci a capire, non nascondere i concetti dietro parole complicate. Quando abbiamo veramente compreso un argomento, dovremmo riuscire a spiegarlo usando termini semplici.

La domanda che prepara la lezione successiva sarà quindi:

> Come possiamo trasformare una realtà composta da studenti, classi, docenti, materie e voti in un insieme di tabelle correttamente collegate?

## Domande di riepilogo

1. Qual è la differenza tra un algoritmo e un programma?
2. Quali elementi compongono il classico schema del funzionamento di un programma?
3. Come è organizzato il nostro esempio JSON?
4. Che cosa rappresentano le coppie chiave-valore?
5. Che cosa fa il ciclo Python che seleziona gli studenti della `5A`?
6. Che cosa succede normalmente alle variabili quando il programma termina?
7. Perché dobbiamo salvare i dati dalla RAM al disco?
8. Perché un unico file JSON può diventare scomodo quando i dati aumentano?
9. Che cosa rappresenta una tabella in una base di dati relazionale?
10. Quali collegamenti possiamo individuare tra istituti, classi, studenti, docenti e voti?
