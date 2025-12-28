# Social Market — Modules Overview
### Documentazione dei moduli funzionali (v0.1)

Questo documento descrive tutti i moduli funzionali di Social Market, la loro responsabilità, le dipendenze interne e le estensioni future.  
Ogni modulo rappresenta un *dominio reale* della vita di un GAS, CSA, mercato contadino o rete mutualistica.

---

# 🧩 Struttura generale dei moduli

Ogni modulo di Social Market segue la stessa struttura:

modules/ 

└── <module-name>/ 

├── class-<module>-service.php 

├── class-<module>-rest.php 

├── class-<module>-admin.php 

├── templates/ 

└── assets/

Ogni modulo contiene:

- **Service class**: logica applicativa del dominio  
- **REST controller**: API pubbliche e interne  
- **Admin UI**: interfacce di gestione  
- **Template**: viste frontend  
- **Assets**: JS, CSS, immagini  

---

# 📦 Moduli principali

## 1. Orders
Gestisce l’intero ciclo degli ordini collettivi.

### Funzionalità
- Creazione e gestione dei cicli d’ordine  
- Carrelli dei membri  
- Aggregazione ordini per produttore  
- Riepiloghi per referenti  
- Chiusura e conferma ordini  
- Collegamento con logistica e fondi  

### Tabelle coinvolte
- `sm_orders`  
- `sm_order_items`  
- `sm_cycles`  

### Dipendenze
- Producers  
- Funds (opzionale)  
- Logistics (opzionale)  

---

## 2. Producers
Gestisce produttori, listini e disponibilità.

### Funzionalità
- Anagrafica produttori  
- Listini prodotti  
- Categorie e unità di misura  
- Disponibilità dinamiche  
- Condizioni commerciali  

### Tabelle coinvolte
- `sm_producers`  
- `sm_products`  

### Dipendenze
- Nessuna (modulo autonomo)

---

## 3. Funds
Gestisce fondi comuni, conti prepagati e saldi membri.

### Funzionalità
- Conti individuali  
- Fondi di gruppo  
- Versamenti e prelievi  
- Saldi in tempo reale  
- Collegamento con ordini e ledger  

### Tabelle coinvolte
- `sm_accounts`  
- `sm_funds`  

### Dipendenze
- Ledger  

---

## 4. Ledger
Il registro contabile centrale del sistema.

### Funzionalità
- Movimenti economici normalizzati  
- Audit log immutabile  
- Collegamento con ordini, fondi e logistica  
- Esportazioni contabili  

### Tabelle coinvolte
- `sm_ledger_entries`  

### Dipendenze
- Nessuna (modulo core)

---

## 5. Logistics
Gestisce la parte operativa: consegne, turni, punti di ritiro.

### Funzionalità
- Punti di ritiro  
- Turni volontari  
- Assegnazioni  
- Riepiloghi di consegna  
- Collegamento con ordini  

### Tabelle coinvolte
- `sm_pickup_points`  
- `sm_shifts`  

### Dipendenze
- Orders  

---

# 🌱 Moduli avanzati (fase 2)

## 6. Governance
Supporta assemblee, decisioni e gruppi di lavoro.

### Funzionalità
- Gruppi di lavoro  
- Proposte e decisioni  
- Votazioni  
- Traccia deliberativa  

### Tabelle coinvolte
- `sm_groups`  
- `sm_decisions`  

### Dipendenze
- Nessuna (ma interagisce con tutti)

---

## 7. MutualCredit
Implementa valute di gruppo e credito reciproco.

### Funzionalità
- Valute mutuali  
- Limiti di credito/debito  
- Movimenti mutuali  
- Collateralizzazione (opzionale)  
- Integrazione con ledger  

### Tabelle coinvolte
- Usa `sm_accounts` e `sm_ledger_entries`  

### Dipendenze
- Ledger  
- Funds (opzionale)

---

## 8. Federation
Permette la comunicazione tra nodi Social Market.

### Funzionalità
- Esportazione/importazione dati  
- Sincronizzazione ledger  
- Federazione valute mutuali  
- Directory nodi  
- API federate  

### Tabelle coinvolte
- Nessuna dedicata (usa metadati)

### Dipendenze
- Tutti i moduli principali

---

# 🔌 Moduli di integrazione (opzionali)

## WooCommerce Bridge
Collega Social Market con WooCommerce.

### Funzionalità
- Sincronizzazione ordini  
- Gateway mutual credit  
- Prodotti ↔ produttori  

---

## Payments
Gateway di pagamento esterni.

### Funzionalità
- Stripe  
- Bonifico manuale  
- Crypto (FairCoin, Bitcoin, ecc.)  
- Pagamenti ibridi  

---

## Communications
Gestisce notifiche e newsletter.

### Funzionalità
- Email transazionali  
- Integrazione Newspack  
- Messaggi interni  

---

# 🧠 Principi comuni a tutti i moduli

- Ogni modulo è **autonomo**, ma integrato nel core.  
- Ogni modulo espone **REST API**.  
- Ogni modulo può essere **attivato/disattivato**.  
- Ogni modulo ha **hook dedicati**.  
- Ogni modulo può essere esteso da plugin esterni.  

---

# 🗺️ Roadmap moduli

### Fase 1 (MVP)
- Orders  
- Producers  
- Funds  
- Ledger  
- Logistics  

### Fase 2
- Governance  
- MutualCredit  
- Federation  

### Fase 3
- Marketplace moduli  
- Moduli territoriali  
- Moduli per cooperative e PA  

---

# 📌 Conclusione

I moduli di Social Market sono progettati per riflettere i processi reali delle economie comunitarie.  
Ogni modulo è indipendente, estendibile e interoperabile, così da permettere a ogni gruppo di costruire il proprio ecosistema digitale senza perdere autonomia.

Questo documento è la base per sviluppatori, contributori e comunità che vogliono comprendere e ampliare l’architettura di Social Market.
