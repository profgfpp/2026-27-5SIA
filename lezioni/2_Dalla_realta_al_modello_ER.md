# Dalla realtà al modello E-R

## 1. Un modello è una rappresentazione della realtà

Un **modello** è una rappresentazione **semplificata** di una parte della realtà.

Non cerca di descrivere tutto ciò che esiste, ma solo ciò che è **utile per lo scopo che abbiamo**.

Per esempio, se vogliamo progettare il database di una **scuola di nuoto**, potrebbero interessarci:

* gli allievi;
* i corsi;
* gli istruttori;
* le iscrizioni;
* i giorni e gli orari dei corsi.

Probabilmente invece **non ci interessa** sapere il colore delle pareti della piscina, quante finestre ci sono o quale musica viene trasmessa negli spogliatoi.

> **Un buon modello non rappresenta tutta la realtà: rappresenta ciò che conta per il problema che dobbiamo risolvere.**


## 2. Prima del modello vengono i requisiti

Prima di progettare il database dobbiamo capire **che cosa deve fare il sistema** e **quali informazioni devono essere conservate**.

Queste esigenze vengono chiamate **requisiti**.

I requisiti si raccolgono parlando con il cliente.

Il problema è che il cliente:

* conosce bene il proprio lavoro;
* non conosce necessariamente i database;
* può dimenticare informazioni importanti;
* può esprimersi in modo impreciso;
* può cambiare idea durante il progetto.

Per questo il progettista deve essere bravo soprattutto a **fare le domande giuste**.

Nell'esempio della scuola di nuoto abbiamo scoperto, per esempio, che:

> un allievo può frequentare più corsi;

> ogni corso ha un istruttore;

> un istruttore può tenere più corsi;

> per ogni iscrizione vogliamo conoscere la data in cui è stata effettuata.

Queste frasi sono **requisiti**.

---

## 3. Dal linguaggio del cliente al modello E-R

Una volta compresi i requisiti possiamo costruire un **modello concettuale**.

Uno dei modelli più utilizzati per progettare una base di dati è il **modello E-R**, cioè **Entità–Relazioni**.

### Entità

Le **entità** rappresentano gli oggetti o i concetti della realtà che ci interessano.

Nella scuola di nuoto:

**ALLIEVO — CORSO — ISTRUTTORE**

Un singolo Mario Rossi è invece una particolare **istanza** dell'entità ALLIEVO.

### Attributi

Gli **attributi** descrivono le caratteristiche di un'entità.

Esempio:

```text
ALLIEVO
- nome
- cognome
- data di nascita
- telefono
```

Oppure:

```text
CORSO
- nome
- livello
- giorno
- ora
- numero massimo di partecipanti
```

### Relazioni

Le **relazioni** descrivono i collegamenti tra le entità.

Per esempio:

```text
ALLIEVO -------- si iscrive -------- CORSO
```

oppure:

```text
ISTRUTTORE -------- tiene -------- CORSO
```

In alcuni casi anche la relazione possiede informazioni proprie.

Per esempio la **data di iscrizione** non appartiene semplicemente all'allievo né al corso: descrive quella particolare iscrizione.

```text
ALLIEVO
    \
     ISCRIZIONE
     - data iscrizione
    /
CORSO
```

---

## 4. Il punto fondamentale

Il modello E-R non è una fotografia completa della realtà.

È una **scelta**.

Della scuola di nuoto rappresentiamo solo gli elementi necessari per rispondere alle domande che ci interessano.

Perciò il percorso è:

```text
REALTÀ
   ↓
REQUISITI
   ↓
MODELLO E-R
   ↓
BASE DI DATI
```

La qualità del database dipende quindi prima di tutto dalla qualità del modello.

> **Prima di chiedersi “quali tabelle devo creare?”, bisogna chiedersi: “quale parte della realtà devo rappresentare?”**
