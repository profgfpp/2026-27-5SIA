# Dalle relazioni E/R ai fondamenti matematici e ai sistemi informativi

**Informatica – classe 5SIA**  
**Appunti rielaborati dalla lezione, con formule, esempi e schemi**

---

# PARTE I – INTRODUZIONE MATEMATICA ALLE RELAZIONI

## 1. Perché introduciamo un linguaggio matematico?

Finora abbiamo rappresentato le basi di dati servendoci del modello Entità/Relazione (E/R): rettangoli per le entità, rombi per le relazioni, linee per i collegamenti. Abbiamo ragionato soprattutto in termini intuitivi, utilizzando esempi concreti. È arrivato il momento di descrivere **gli stessi concetti con un linguaggio un po' più astratto: quello della matematica**.

Non si tratta di cambiare argomento. I database relazionali hanno fondamenta matematiche: gli insiemi, le coppie ordinate, il prodotto cartesiano e le relazioni. Capire queste idee permette di osservare una stessa struttura da due prospettive differenti:

- quella informatica, nella quale vediamo **tabelle, righe e colonne**;
- quella matematica, nella quale vediamo **insiemi, elementi e relazioni**.

L'astrazione può sembrare meno immediata di una tabella, ma ci consente di studiare con maggiore precisione le proprietà di quello che stiamo costruendo. Non è necessario ragionare continuamente così quando si programma: tuttavia, in determinati momenti, questo linguaggio diventa molto utile.

## 2. L'insieme: un concetto fondamentale

**Domanda alla classe:** «Che cos'è un insieme? Lo avete già incontrato in matematica?»

La nozione di insieme è talmente fondamentale che, nella teoria matematica, viene abitualmente assunta come concetto primitivo: non la definiamo ricorrendo a concetti ancora più semplici. Possiamo immaginarlo intuitivamente come una *collezione di elementi*, oppure come un contenitore ideale. In inglese si dice *set*.

Per il momento mettiamo da parte gli attributi delle entità e immaginiamo che STUDENTE sia rappresentato dall'insieme delle sue occorrenze:

\[
S=\{\text{Marco},\text{Luca},\text{Maria}\}
\]

Allo stesso modo, consideriamo l'insieme dei corsi:

\[
C=\{\text{Informatica},\text{Matematica},\text{Storia}\}
\]

La scrittura \(\text{Marco}\in S\) significa che Marco *appartiene* all'insieme S. Invece \(\text{Informatica}\in C\).

```text
       insieme S = STUDENTE                  insieme C = CORSO
      +----------------------+              +----------------------+
      |  Marco               |              |  Informatica         |
      |  Luca                |              |  Matematica          |
      |  Maria               |              |  Storia               |
      +----------------------+              +----------------------+
```

Naturalmente i nomi servono qui a semplificare: nella realtà, due studenti potrebbero avere lo stesso nome e andrebbero distinti con un identificatore. Inoltre un **tipo di entità** come STUDENTE non coincide letteralmente con uno specifico insieme di studenti: l'insieme contiene le sue *occorrenze*, presenti in un certo momento.

## 3. Costruire coppie ordinate

Prendiamo ora un elemento dal primo insieme e uno dal secondo:

\[
(\text{Marco},\text{Informatica})
\]

Abbiamo costruito una **coppia ordinata**. Scriviamo una parentesi tonda e, in prima posizione, un elemento di STUDENTE; in seconda posizione, un elemento di CORSO.

Altri esempi:

\[
(\text{Marco},\text{Matematica}),\quad
(\text{Luca},\text{Storia}),\quad
(\text{Maria},\text{Informatica})
\]

**Perché si chiamano ordinate?** Perché le posizioni hanno un significato e quindi l'ordine non è arbitrario. Abbiamo deciso di scrivere prima lo studente e poi il corso. Non possiamo improvvisamente invertire le posizioni e pretendere che la rappresentazione conservi lo stesso significato:

\[
(\text{Marco},\text{Informatica})\neq
(\text{Informatica},\text{Marco})
\]

In altri termini, non stiamo semplicemente mettendo due parole una accanto all'altra: stiamo costruendo un oggetto matematico nel quale **il primo posto e il secondo posto hanno ruoli distinti**.

## 4. Il prodotto cartesiano

**Domanda:** «Avete mai sentito parlare di *prodotto cartesiano*?»

Indichiamo con \(S\times C\) il **prodotto cartesiano** di S e C. È l'insieme di **tutte le coppie ordinate possibili** nelle quali il primo elemento appartiene a S e il secondo a C.

\[
S\times C=\{(s,c)\mid s\in S\ \text{e}\ c\in C\}
\]

Con tre studenti e tre corsi otteniamo nove coppie:

\[
\begin{aligned}
S\times C=\{&
(\text{Marco},\text{Informatica}),
(\text{Marco},\text{Matematica}),
(\text{Marco},\text{Storia}),\\
& (\text{Luca},\text{Informatica}),
(\text{Luca},\text{Matematica}),
(\text{Luca},\text{Storia}),\\
& (\text{Maria},\text{Informatica}),
(\text{Maria},\text{Matematica}),
(\text{Maria},\text{Storia})\}
\end{aligned}
\]

```text
                         CORSO
                 Informatica Matematica  Storia
               +------------+-----------+--------+
         Marco | (M, Inf)   | (M, Mat)  | (M, Sto)|
 STUDENTE Luca | (L, Inf)   | (L, Mat)  | (L, Sto)|
         Maria | (Ma, Inf)  | (Ma, Mat) | (Ma,Sto)|
               +------------+-----------+--------+

 Ogni casella rappresenta UNA coppia ordinata.
 Il prodotto cartesiano comprende TUTTE le caselle.
```

È un prodotto nel senso che, se gli insiemi sono finiti, il numero di combinazioni si calcola moltiplicando le loro numerosità:

\[
|S\times C|=|S|\cdot |C|=3\cdot3=9
\]

Non abbiamo ancora affermato che Marco frequenti davvero Informatica, o che Maria frequenti Storia: stiamo semplicemente elencando **tutte le combinazioni teoricamente possibili**.

## 5. Ma il piano cartesiano non lo conoscevamo già?

Durante la lezione è emersa una connessione con un argomento già studiato in matematica: **le coordinate di un punto nel piano**.

Un punto viene identificato tramite una coppia ordinata:

\[
P=(x,y)
\]

Per esempio \(P=(2,3)\): prima la coordinata orizzontale, poi quella verticale.

```text
                y
                ^
            4   |
            3   |       * P(2,3)
            2   |       :
            1   |       :
            0 --+---+---+---+--------> x
                0   1   2   3
```

Il piano cartesiano può essere espresso come:

\[
\mathbb{R}\times\mathbb{R}=\mathbb{R}^{2}
\]

Il simbolo \(\mathbb{R}\) indica l'insieme dei **numeri reali**, non quello dei numeri naturali \(\mathbb{N}\). Nel piano cartesiano, sia la prima sia la seconda coordinata possono assumere un qualsiasi valore reale.

La differenza rispetto al nostro esempio è che \(\mathbb{R}\) contiene infiniti elementi, mentre S e C ne contengono soltanto tre ciascuno. Inoltre i numeri reali hanno una proprietà interessante: **tra due numeri reali distinti si possono sempre trovare infiniti altri numeri reali**. Diciamo che \(\mathbb{R}\) è denso rispetto all'ordine usuale. I numeri naturali, invece, sono discreti: tra 1 e 2 non esiste alcun altro numero naturale.

Quindi il prodotto cartesiano non è qualcosa di estraneo: è la stessa costruzione che compare quando pensiamo ai punti del piano, ma applicata a insiemi di studenti e di corsi.

## 6. La relazione matematica è un sottoinsieme

Arriviamo al punto principale.

**Domanda:** «Tutti gli studenti sono iscritti a tutti i corsi?» Evidentemente no. Abbiamo nove coppie possibili, ma solo alcune potrebbero rappresentare iscrizioni effettive.

Definiamo per esempio la relazione ISCRIZIONE con le coppie:

\[
I=\{(\text{Marco},\text{Informatica}),
(\text{Luca},\text{Matematica}),
(\text{Maria},\text{Storia})\}
\]

*(Le tre iscrizioni sono dati di esempio inseriti per rendere esplicita la scelta delle coppie; la lezione orale non specificava un elenco completo di iscrizioni.)*

```text
                          CORSO
                  Informatica  Matematica  Storia
                +------------+-----------+-------+
          Marco |     X      |           |       |
 STUDENTE Luca  |            |     X     |       |
          Maria |            |           |   X   |
                +------------+-----------+-------+

 X = coppia appartenente alla relazione ISCRIZIONE
 vuoto = combinazione possibile, ma non presente in I
```

La definizione matematica è:

\[
\boxed{I\subseteq S\times C}
\]

In generale, una **relazione binaria** tra due insiemi A e B è un qualunque sottoinsieme del loro prodotto cartesiano:

\[
\boxed{R\subseteq A\times B}
\]

Questa scrittura è fondamentale: una relazione non è il prodotto cartesiano intero, ma una **selezione di alcune sue coppie** (eventualmente nessuna, oppure tutte).

Per rinforzare il concetto, durante la lezione si è considerato anche un esempio minimale:

\[
A=\{a,b\},\qquad B=\{1,2\}
\]

\[
A\times B=\{(a,1),(a,2),(b,1),(b,2)\}
\]

Una possibile relazione potrebbe essere \(R=\{(a,1),(b,2)\}\), ma ne esistono molte altre. Questo esempio rende chiarissimo che la relazione è un **sottoinsieme** delle possibilità offerte dal prodotto cartesiano.

## 7. E cosa c'entra tutto questo con le tabelle?

Ora consideriamo la stessa relazione come una tabella:

```text
  ISCRIZIONE
  +----------+-------------+
  | Studente | Corso       |
  +----------+-------------+
  | Marco    | Informatica |
  | Luca     | Matematica  |
  | Maria    | Storia      |
  +----------+-------------+
```

Ogni **riga** corrisponde a una **coppia** della relazione. Le colonne indicano le posizioni della coppia, e i loro significati.

Da un punto di vista matematico è utile pensare alle coppie come elementi di un insieme; dal punto di vista informatico è spesso più comodo rappresentarle come righe di una tabella.

Non sono due realtà incompatibili: **sono due modi di osservare la stessa struttura**. Il fondamento matematico ci aiuta a capire le proprietà dei database relazionali, mentre la tabella ci aiuta a memorizzare e manipolare concretamente i dati.

> Attenzione alla terminologia: il termine *relazione* compare sia nel modello E/R sia nel modello relazionale. I due usi sono collegati, ma non si deve confondere automaticamente il rombo del diagramma E/R con una tabella già pronta: la trasformazione dal modello concettuale alle tabelle richiede regole specifiche.

---

# PARTE II – LE RELAZIONI TERNARIE E LA DISTINZIONE TRA ENTITÀ E RELAZIONI

## 8. Riprendiamo il dubbio nato dal diagramma E/R

La lezione era cominciata con una domanda agli studenti:

**«Che cosa distingue un'entità da una relazione? Perché DOCENTE è un'entità, mentre qualcosa come SVOLGIMENTO o VALUTAZIONE potrebbe essere una relazione? Perché non trasformare tutto in entità?»**

Nelle prime lezioni avevamo spesso disegnato collegamenti come semplici linee, scrivendovi accanto un **verbo**. Era spontaneo pensare:

- entità = sostantivi, cose, oggetti;
- relazioni = verbi, azioni, collegamenti.

Si poteva addirittura interpretare il verbo come un comando o un'azione, mentre l'entità sembrava rappresentare un dato. Questa interpretazione iniziale era utile, ma era anche una semplificazione provvisoria. Per metterla alla prova, in seguito erano stati introdotti intenzionalmente nomi di relazioni espressi attraverso **sostantivi**.

Il problema non si risolve dunque scegliendo la categoria grammaticale giusta. Una relazione non è una relazione *perché porta il nome di un verbo*.

## 9. Binario: perché proprio questa parola?

**Domanda:** «Perché si dice relazione *binaria*?»

Il prefisso *bi-* rimanda al numero due: basti pensare al sistema numerico binario (0 e 1), oppure ai due binari della ferrovia evocati durante la discussione. È stata fatta anche un'associazione con il termine *bilaterale*, utilizzato in altri contesti, per esempio in anatomia. Le parole non sono necessariamente intercambiabili nei rispettivi contesti, ma richiamano entrambe l'idea del due.

Una relazione **binaria** mette in associazione occorrenze di **due ruoli** (nel nostro esempio, due tipi di entità):

```text
  +------------+          /---------------\         +---------+
  |  STUDENTE  |---------<   ISCRIZIONE    >--------|  CORSO  |
  +------------+          \---------------/         +---------+
```

Fin qui abbiamo studiato principalmente relazioni di questo tipo. Ma perché limitarsi a due?

## 10. Passiamo da due a tre: la relazione ternaria

**Proposta alla classe:** «E se costruissimo una relazione che coinvolge direttamente tre entità?»

Una relazione **ternaria** coinvolge contemporaneamente tre ruoli. Nel caso del registro elettronico, consideriamo:

- DOCENTE;
- STUDENTE;
- MATERIA.

Possiamo introdurre una relazione chiamata **VALUTAZIONE**:

```text
                         +-------------+
                         |   DOCENTE   |
                         +-------------+
                                |
                                |
                           /-----------\
                          /             \
                         <  VALUTAZIONE  >
                          \             /
                           \-----------/
                            /         \
                           /           \
               +------------+        +------------+
               |  STUDENTE  |        |  MATERIA   |
               +------------+        +------------+
```

Il rombo non è più un semplice collegamento tra due rettangoli. Rappresenta un'unica associazione che riguarda **contemporaneamente** un docente, uno studente e una materia.

Nella versione precedente del diagramma, alcune entità e relazioni intermedie — con nomi come *attribuzione*, *valutatore*, *riferimento* — rendevano il disegno articolato e piuttosto pesante. Non era necessariamente un'impostazione scorretta: era però meno leggibile, perché rischiavamo di dedicare troppo tempo alla ricerca di sostantivi e collegamenti, perdendo di vista ciò che intendevamo rappresentare.

**Importante:** nella lezione il cambiamento non veniva presentato come la correzione di un errore. La soluzione precedente poteva andare bene; la relazione ternaria è stata introdotta per mostrare un altro modo di organizzare il modello e per preparare gli studenti a situazioni più avanzate, che potrebbero comparire anche in una prova d'esame.

## 11. Perché VALUTAZIONE è una relazione anche se è un sostantivo?

Torniamo al dubbio iniziale. DOCENTE, STUDENTE e MATERIA indicano oggetti o concetti che, nel nostro universo di interesse, possiamo riconoscere e descrivere autonomamente. Invece una VALUTAZIONE, così come la stiamo intendendo in questo specifico modello, non è definibile senza rispondere alle domande:

**Chi valuta? Chi viene valutato? In quale materia?**

La valutazione è il **raccordo** tra queste tre occorrenze. Possiamo quindi dire, come prima intuizione, che:

- un'entità rappresenta qualcosa che scegliamo di descrivere con una propria identità nel modello;
- una relazione rappresenta un'associazione tra occorrenze di entità.

Questa distinzione è **concettuale, non grammaticale**: i sostantivi possono nominare tanto entità quanto relazioni.

> Precisazione di modellazione: l'«autonomia» è un criterio intuitivo utile a lezione, non un test matematico assoluto. Lo stesso concetto di valutazione può essere modellato come entità quando abbiamo bisogno di identificare singoli episodi di valutazione. La scelta dipende dalle informazioni e dai vincoli che dobbiamo rappresentare.

## 12. La relazione ternaria vista matematicamente

Gli strumenti della prima parte consentono di descrivere anche questo caso. Consideriamo gli insiemi delle occorrenze:

\[
D=\{\text{docenti}\},\quad
S=\{\text{studenti}\},\quad
M=\{\text{materie}\}
\]

Il prodotto cartesiano fra tre insiemi è formato da **terne ordinate**:

\[
D\times S\times M
\]

Una relazione ternaria è quindi un sottoinsieme:

\[
\boxed{V\subseteq D\times S\times M}
\]

Una sua possibile occorrenza è:

\[
(\text{prof. Rossi},\text{Marco},\text{Informatica})
\]

Per esempio, quella terna esprime che il docente Rossi valuta Marco nella materia Informatica. I tre posti della terna hanno ruoli precisi, così come accadeva per le coppie ordinate.

Da qui si comprende anche l'origine del termine *ternaria*: non dobbiamo immaginare tre diverse relazioni binarie indipendenti, ma **un'unica relazione definita su tre insiemi**.

---

# PARTE III – DATABASE, DBMS E SISTEMI INFORMATIVI

## 13. Dal modello dei dati al loro utilizzo concreto

La lezione si è poi collegata a un'attività pratica del giorno precedente: la creazione del database e l'inserimento dei dati. È stata posta una domanda molto concreta:

**«Per creare il database devo scrivere tutti i dati uno per uno? Devo prima creare la struttura e poi inserire i dati?»**

Nell'esercizio scolastico si può creare la struttura e popolarla con istruzioni SQL, per esempio con `INSERT INTO`. È normale che un esercizio iniziale richieda una sequenza di comandi espliciti. Ma non dobbiamo confondere questo metodo di apprendimento con il modo in cui lavora un sistema reale.

Prendiamo l'esempio della **trattoria**, già utilizzato durante il percorso. Il database viene predisposto per gestire clienti, comande e altre informazioni. Non è necessario conoscere in anticipo tutte le comande: **gli ordini arriveranno nel tempo**, e a ogni nuovo ordine il sistema inserirà i relativi dati.

```text
  PRIMA                              POI, DURANTE L'ATTIVITÀ
  +--------------------+              +--------------------------+
  | Creazione database |              | Arriva una nuova comanda |
  | Creazione tabelle  | ------------>| Inserimento nuovi dati  |
  +--------------------+              +--------------------------+
                                             |
                                             v
                                      +---------------+
                                      |   DATABASE    |
                                      | aggiornato    |
                                      +---------------+
```

Inoltre il database non va immaginato come una sequenza di istruzioni `INSERT`: quelle sono **operazioni effettuate sui dati**, non il database stesso.

## 14. Cos'è un database? E che cos'è il DBMS?

Durante la spiegazione si è ricordato il simbolo grafico tradizionale di un database: un **cilindro**, una specie di bidone, che suggerisce l'idea di un contenitore di dati.

```text
                 _____________
               /             \
              /    DATABASE   \
              |---------------|
              |   TABELLE     |
              |               |
              |               |
              \_______________/
```

Possiamo pensare, semplificando, a un database come a un contenitore organizzato di tabelle. Sullo stesso computer o server possono esistere **più database**. Chi li gestisce?

Il software di gestione si chiama **DBMS**:

\[
\boxed{\text{DBMS = Database Management System}}
\]

*Management* significa gestione: il DBMS è il **sistema di gestione della base di dati**. È un programma (o sistema software) che permette, fra le altre cose, di creare database, organizzarli, consultarli, modificarli e amministrarli.

```text
                 +------------------------------+
                 |             DBMS             |
                 |   sistema di gestione dati   |
                 +------------------------------+
                    |           |           |
                    v           v           v
                +--------+  +--------+  +--------+
                | DB 1   |  | DB 2   |  | DB 3   |
                | tabelle|  | tabelle|  | tabelle|
                +--------+  +--------+  +--------+
```

Come esempio, immaginiamo un fornitore di registri elettronici, come quelli citati durante la lezione (Axios, Spaggiari). Potrebbe avere database distinti per scuole diverse, ad esempio una scuola «Angelo» e una «Einaudi», pur utilizzando un medesimo sistema di gestione. È uno **scenario illustrativo**: non stiamo descrivendo né verificando l'architettura effettiva dei prodotti citati.

## 15. Il database non è l'applicazione

Quando un insegnante **firma la lezione** nel registro elettronico, non apre una console SQL per scrivere una `INSERT INTO`. Utilizza un'applicazione, per esempio un sito accessibile dal browser, che presenta un'interfaccia adatta all'utente.

L'applicazione riceve la richiesta dell'utente, la interpreta e dialoga con il DBMS per leggere o aggiornare le informazioni.

```text
  +----------------+
  |    DOCENTE     |
  |  (utilizzatore)|
  +----------------+
          |
          | clic su «Firma la lezione»
          v
  +---------------------------+
  | INTERFACCIA DELL'APP      |
  | (per esempio: sito web)   |
  +---------------------------+
          |
          | richiesta HTTP / HTTPS (caso web)
          v
  +---------------------------+
  |       APPLICAZIONE        |
  |  logica, controlli,       |
  |  elaborazione richieste   |
  +---------------------------+
          |
          | comandi SQL / librerie / driver
          v
  +---------------------------+
  |           DBMS            |
  +---------------------------+
          |
          v
  +---------------------------+
  |         DATABASE          |
  |       dati e tabelle      |
  +---------------------------+
```

Il programma che realizza l'applicazione potrebbe essere scritto in linguaggi differenti, come C o Python, oppure con altre tecnologie. Non è importante conoscere subito ogni dettaglio tecnico: per ora interessa distinguere i **ruoli**.

L'applicazione non memorizza necessariamente tutto da sola: si affida al DBMS. Il DBMS, dal canto suo, non è l'interfaccia attraverso cui il docente firma la lezione.

## 16. Che cosa fa l'applicazione quando usiamo il registro?

Immaginiamo che l'utente chieda di visualizzare l'elenco delle classi. L'applicazione potrebbe ottenere i dati tramite una richiesta SQL come:

```sql
SELECT * FROM Classe;
```

**Nota:** il nome `Classe` è illustrativo. Lo abbiamo scritto al singolare, in continuità con la convenzione utilizzata nella progettazione in classe.

Quando il docente sceglie una classe, l'applicazione potrebbe eseguire altre interrogazioni, per esempio per trovare gli studenti che le appartengono:

```sql
SELECT *
FROM Studente
WHERE id_classe = 5;
```

In questo esempio ipotizziamo che la tabella `Studente` abbia un attributo `id_classe`. In un altro progetto il collegamento potrebbe essere realizzato con una tabella ISCRIZIONE e la query sarebbe diversa.

Per inserire una nuova informazione, invece, l'applicazione può eseguire un comando `INSERT` (o un'altra operazione adatta alla struttura del database).

La pagina che vediamo sullo schermo può dunque essere il risultato di **molte interrogazioni**: recupera le classi, recupera gli studenti, legge le lezioni, verifica chi è autorizzato a compiere un'azione, mostra e aggiorna le informazioni.

L'utente vede un pulsante; dietro il pulsante può esserci una quantità significativa di elaborazione.

## 17. Che cos'è davvero un'interfaccia?

Nella discussione è stato chiesto di non confondere **interfaccia** e **interfaccia grafica**.

Un'interfaccia è, in generale, **il modo in cui un componente comunica con qualcosa che gli è esterno**. Il componente esterno non deve essere per forza una persona.

- Un sito web offre un'interfaccia utilizzabile da una persona tramite browser.
- Un programma può comunicare con un altro programma tramite una sua interfaccia.
- Un'applicazione può comunicare con il DBMS tramite SQL e gli strumenti software che lo rendono accessibile.

Per questo motivo un sistema può avere **diverse interfacce, a diversi livelli**. Nelle architetture reali i componenti possono trovarsi sullo stesso computer oppure su macchine diverse, collegate in rete.

Durante la lezione si è sottolineato che gli informatici tendono a ragionare per **strati**: ogni strato utilizza le possibilità offerte da quello sottostante senza doverne conoscere ogni dettaglio.

```text
        +--------------------------------+
        | Persona e interfaccia utente   |
        +--------------------------------+
                       |
        +--------------------------------+
        | Applicazione e logica          |
        +--------------------------------+
                       |
        +--------------------------------+
        | Interfaccia verso il DBMS      |
        | SQL, driver, librerie          |
        +--------------------------------+
                       |
        +--------------------------------+
        | Gestione e memorizzazione dati |
        +--------------------------------+
```

SQL è il linguaggio con cui normalmente descriviamo le operazioni da eseguire su un database relazionale. Tuttavia SQL **non va confuso con il protocollo di rete**: se i programmi sono su computer distinti, la comunicazione utilizza anche protocolli e strumenti specifici, che il programmatore spesso usa indirettamente.

È stato ripreso anche il concetto di **linguaggio dichiarativo**: con SQL indichiamo principalmente *quali dati* desideriamo oppure *quale modifica* vogliamo ottenere, senza specificare tutti i passaggi interni con cui il DBMS dovrà realizzare l'operazione.

## 18. Ripasso dal C: che cos'è una libreria?

Per chiarire il concetto di interfaccia fra componenti, la lezione si è collegata a un tema già conosciuto: le **librerie** nel linguaggio C.

**Domanda:** «Che cos'è una libreria? È un insieme di dati? Di strumenti? Oppure, più precisamente, di funzioni?»

Una descrizione operativa utile è questa: una libreria mette a disposizione **funzioni già realizzate**, che un altro programma può richiamare fornendo eventuali argomenti e ottenendo risultati. Nell'uso moderno può mettere a disposizione anche tipi di dati e altre risorse.

In C, ad esempio, abbiamo incontrato istruzioni `#include` all'inizio del programma, che permettono di includere dichiarazioni contenute negli header delle librerie:

```c
#include <stdio.h>

int main(void) {
    printf("Ciao!\n");
    return 0;
}
```

Qui `printf` è una funzione disponibile tramite la libreria standard. **Precisazione:** `#include` include il contenuto dell'header; non significa che tutto il codice compilato della libreria sia copiato testualmente nel sorgente.

È stata posta anche una domanda più avanzata: **«Che cosa distingue, in modo operativo, una libreria da un'applicazione?»**

La distinzione intuitiva proposta è che un programma eseguibile dispone di un **punto di ingresso**, mentre le funzioni di libreria sono progettate per essere richiamate da altro codice. In C il punto di ingresso che scriviamo normalmente è `main` (con le necessarie precisazioni sull'ambiente di esecuzione). È una semplificazione utile, non una regola universale per ogni linguaggio e piattaforma.

Da qui la discussione ha sfiorato anche le differenze tra C e C++, l'uso del C nella programmazione vicina al sistema e la programmazione orientata agli oggetti in C++. Si è accennato alla possibilità di dedicarvi qualche settimana più avanti; non era, però, lo scopo della lezione odierna. Il punto da conservare è che **componenti diversi possono collaborare richiamando funzioni o servizi attraverso interfacce definite**.

## 20. Il principio di astrazione: non occorre aprire il cofano

È stata utilizzata un'analogia efficace: **guidare un'automobile**.

Chi guida usa sterzo, acceleratore, freno, frizione (quando presente), tachimetro e altri comandi. Non deve aprire il cofano ogni volta per comprendere nel dettaglio il funzionamento del motore. In inglese il cofano anteriore può essere chiamato *hood* (nell'inglese americano).

```text
   GUIDATORE                   PROGRAMMATORE DELL'APP
   ---------                   ----------------------
   Sterzo, freno,              SQL, funzioni, driver,
   acceleratore                interfacce del DBMS
          |                              |
          v                              v
   Meccanica interna           Gestione interna dei dati
   dell'automobile             e strutture fisiche dei file
```

Questo è il **principio di astrazione**: chi usa un componente si concentra sulle operazioni messe a disposizione dall'interfaccia e non è costretto a conoscere tutti i meccanismi sottostanti.

Per il database la conseguenza è fondamentale: se sappiamo interagire con il DBMS tramite SQL, **non dobbiamo necessariamente conoscere la struttura fisica dei file** usati per conservare i dati. Il sistema di gestione si occupa di molti dettagli interni.

Attenzione: questo non significa che i dettagli non esistano, né che siano sempre irrilevanti per le prestazioni o per chi amministra i sistemi. Significa che vengono **nascosti a chi non ha bisogno di occuparsene**.

## 21. Che cos'è un sistema informativo?

Mettendo insieme quanto visto otteniamo un quadro più ampio. Per esempio, il registro elettronico non è soltanto un database e non è soltanto una pagina web. È parte di un **sistema informativo**: serve a raccogliere, organizzare, conservare, elaborare e rendere disponibili informazioni necessarie all'attività scolastica.

Nella lezione è stato presentato soprattutto il suo nucleo tecnologico:

```text
                     SISTEMA INFORMATIVO SCOLASTICO
  +-----------------------------------------------------------------+
  |                                                                 |
  |  PERSONE E ATTIVITÀ: docenti, studenti, segreteria, famiglie    |
  |             |                                                   |
  |             v                                                   |
  |       +----------------------+                                  |
  |       |     INTERFACCIA      |  browser / altre interfacce      |
  |       +----------------------+                                  |
  |             |                                                   |
  |             v                                                   |
  |       +----------------------+                                  |
  |       |     APPLICAZIONE     |  regole e funzioni del registro  |
  |       +----------------------+                                  |
  |             |                                                   |
  |             v                                                   |
  |       +----------------------+                                  |
  |       |         DBMS         |  gestione delle basi di dati     |
  |       +----------------------+                                  |
  |             |                                                   |
  |             v                                                   |
  |       +----------------------+                                  |
  |       |       DATABASE       |  tabelle e dati                  |
  |       +----------------------+                                  |
  |                                                                 |
  +-----------------------------------------------------------------+
```

Una precisazione utile: in senso rigoroso, **un sistema informativo comprende anche persone, procedure, regole organizzative e flussi di informazione**, non soltanto software e database. Il complesso delle tecnologie utilizzate per realizzarlo costituisce la sua componente informatica, spesso chiamata **sistema informatico**.

Il **registro elettronico** è quindi un esempio particolarmente vicino a noi. La sua interfaccia può utilizzare tecnologie web — browser, HTTP/HTTPS —, mentre il programma e il database lavorano dietro le quinte.

## 22. Un altro esempio: i sistemi informativi delle amministrazioni

Si è citato anche un contesto molto diverso dalla scuola: le banche dati e i sistemi informativi usati da amministrazioni pubbliche e forze di polizia.

L'esempio ha portato a discutere di **dati personali**, dati biometrici, impronte digitali, chip presenti nei documenti elettronici, identificazione e registrazione di informazioni. Una banca dati pubblica deve gestire dati e procedure in un contesto particolarmente delicato, dove entrano in gioco esigenze operative e diritti delle persone.

È stato menzionato, come esperienza concreta, il rilascio di un passaporto con acquisizione delle impronte e memorizzazione di dati biometrici sul chip del documento. **Non dobbiamo però dedurre senza una verifica normativa** che tutti i dati raccolti siano sempre cancellati da ogni sistema, o che siano sempre conservati esclusivamente sul chip: tempi di conservazione, archivi e regole dipendono dal documento e dalla normativa applicabile.

Questo passaggio collega il tema dei sistemi informativi a una questione più generale: **le informazioni hanno valore, ma la loro gestione implica anche responsabilità**, specialmente quando riguardano persone.

---

# Q&A FINALE – UNA DOMANDA FUORI TEMA, MA INTERESSANTE

## Che cos'è un semiconduttore e perché è così importante nei computer?

Alla fine della lezione uno studente ha posto una domanda sui **semiconduttori**. L'argomento non faceva parte dei tre nuclei principali, ma ha offerto l'occasione per un breve collegamento tra fisica ed elettronica.

La spiegazione è partita dalla distinzione tra materiali **conduttori** e **isolanti**.

- Nei conduttori, come rame, argento e oro, esistono cariche elettriche che possono muoversi e permettere la conduzione della corrente.
- Negli isolanti, come molte plastiche, il movimento delle cariche è molto più difficile nelle condizioni ordinarie.
- Nei semiconduttori, come il silicio, la conduzione può essere controllata e modificata mediante condizioni fisiche e strutture opportune.

L'idea centrale è che il semiconduttore consente di costruire **dispositivi che controllano il flusso della corrente elettrica**.

### L'analogia del rubinetto

Pensiamo a un rubinetto: aprendo o chiudendo la valvola possiamo regolare il flusso d'acqua. In modo analogo, un dispositivo elettronico può controllare il flusso di corrente mediante un segnale.

```text
   ACQUA                                ELETTRICITÀ
   -----                                -----------
   Tubo ---- [ RUBINETTO ] --->        Circuito -- [ TRANSISTOR ] -->
                 ^                                    ^
                 |                                    |
          comando della valvola                segnale di controllo
```

Un componente fondamentale è il **transistor**, utilizzabile anche come interruttore controllato elettricamente.

```text
  semiconduttori
       |
       v
  transistor
       |
       v
  reti di transistor
       |
       v
  circuiti logici e memorie
       |
       v
  processori e sistemi di calcolo programmabili
```

Miliardi di transistor, opportunamente progettati e collegati, permettono di realizzare i circuiti che stanno alla base dei computer moderni. L'analogia del rubinetto serve a comprendere il *controllo* del flusso, ma non descrive nel dettaglio la fisica del funzionamento di un transistor.

### La rivoluzione tecnologica del Novecento

La discussione si è allargata all'enorme quantità di innovazioni scientifiche e tecnologiche del Novecento. Fra queste, l'elettronica dei semiconduttori ha avuto un'importanza enorme, rendendo possibili i circuiti integrati e lo sviluppo dell'informatica moderna.

Si è evocata anche l'espressione storiografica **«secolo breve»**, riferita al Novecento. In questa interpretazione storica, resa celebre da Eric Hobsbawm, il «secolo breve» viene convenzionalmente collocato **dal 1914 al 1991**, dalla Prima guerra mondiale alla dissoluzione dell'Unione Sovietica. La digressione ha mostrato come il progresso tecnico si inserisca in trasformazioni storiche molto più ampie.

---

# RIEPILOGO DEI TRE NUCLEI DELLA LEZIONE

**1. Introduzione matematica.** Il prodotto cartesiano costruisce tutte le combinazioni possibili di elementi di due insiemi. Una relazione è un sottoinsieme di quelle combinazioni. Le coppie possono essere rappresentate come righe di una tabella.

\[
\boxed{R\subseteq A\times B}
\]

**2. Relazioni ternarie.** Una relazione può associare contemporaneamente tre occorrenze e non deve essere necessariamente chiamata con un verbo. La distinzione tra entità e relazione è concettuale e dipende anche da ciò che dobbiamo identificare nel modello.

\[
\boxed{V\subseteq D\times S\times M}
\]

**3. Sistemi informativi.** Un database memorizza dati; un DBMS li gestisce; un'applicazione usa il DBMS per offrire funzionalità a persone o altri sistemi. Le interfacce e l'astrazione permettono di separare le responsabilità. Il sistema informativo comprende inoltre il contesto organizzativo in cui tali strumenti sono utilizzati.

```text
        INSIEMI E RELAZIONI
                  |
                  v
        MODELLO DEI DATI
                  |
                  v
          BASE DI DATI
                  |
                  v
             DBMS
                  ^
                  |
          APPLICAZIONE
                  ^
                  |
            INTERFACCIA
                  ^
                  |
       PERSONE, ATTIVITÀ, REGOLE
```

**Idea conclusiva:** imparare l'informatica significa saper passare da un problema concreto (una classe, una valutazione, una comanda, una firma sul registro) a un modello astratto, e poi tornare dal modello a un sistema che funziona nella realtà.
