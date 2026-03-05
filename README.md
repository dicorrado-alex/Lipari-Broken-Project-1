# 🔧 LipariBank Broken Project — Day 1

Progetto Java 21 didattico con **3 bug logici** nascosti.
Il codice **compila senza errori** ma si comporta in modo scorretto a runtime.
Il tuo obiettivo è trovarli tutti e tre.

---

## Struttura del progetto

```
liparibank-broken-day1/
├── src/
│   └── com/
│       └── lipari/
│           └── bank/
│               ├── model/
│               │   ├── CustomerType.java
│               │   ├── TransactionType.java
│               │   ├── Customer.java
│               │   ├── Transaction.java
│               │   ├── Account.java          (sealed class)
│               │   ├── CheckingAccount.java  (final, conto corrente)
│               │   └── SavingsAccount.java   (final, conto risparmio)
│               └── cli/
│                   └── BankConsole.java
├── README.md
└── compile-and-run.sh
```

---

## Compilazione e avvio

### Prerequisiti

- Java 21 (verifica con `java -version`)

### 1. Crea la cartella di output

```bash
mkdir -p out
```

### 2. Compila

```bash
javac -d out \
  src/com/lipari/bank/model/CustomerType.java \
  src/com/lipari/bank/model/TransactionType.java \
  src/com/lipari/bank/model/Customer.java \
  src/com/lipari/bank/model/Transaction.java \
  src/com/lipari/bank/model/Account.java \
  src/com/lipari/bank/model/CheckingAccount.java \
  src/com/lipari/bank/model/SavingsAccount.java \
  src/com/lipari/bank/cli/BankConsole.java
```

Oppure usa lo script:

```bash
chmod +x compile-and-run.sh
./compile-and-run.sh
```

### 3. Esegui

```bash
java -cp out com.lipari.bank.cli.BankConsole
```

---

## 🕵️ Le tue 3 missioni

Ogni bug produce un sintomo osservabile. Trova la riga incriminata, capisci
perché è sbagliata e correggila.

---

### MISSIONE 1 — Il conto di risparmio non applica gli interessi

**Sintomo:** Scegli l'opzione *"6. Applica interessi"* dal menu.
Il programma stampa il saldo prima e dopo l'operazione, ma i due valori
sono **identici**: gli interessi non vengono mai accreditati sul conto,
nonostante il tasso sia configurato correttamente.

---

### MISSIONE 2 — Il menu va in loop infinito con input non numerico

**Sintomo:** Quando il menu chiede *"Scelta:"* e l'utente digita una lettera
o una parola (es. `abc`), il programma stampa il messaggio di errore
**all'infinito** senza mai fermarsi, rendendo necessario terminare il processo
(Ctrl+C).

---

### MISSIONE 3 — Il tipo di conto non viene riconosciuto nel processing

**Sintomo:** Scegli l'opzione *"7. Processa e classifica conti"*.
Tutti i conti vengono stampati come `[GENERICO]`, anche quelli che sono
chiaramente un conto corrente (`CheckingAccount`) o un conto risparmio
(`SavingsAccount`). La classificazione dettagliata non appare mai.

---

## ✅ Obiettivo finale

Quando hai trovato e corretto tutti e 3 i bug, hai completato la missione!

- Il conto risparmio deve mostrare saldi diversi prima/dopo gli interessi
- Il menu deve gestire input non numerici senza bloccarsi
- Il processing deve classificare correttamente `[CORRENTE]` e `[RISPARMIO]`
