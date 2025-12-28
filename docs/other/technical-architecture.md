# **Social Market — Technical Architecture Paper (v0.1)**
### *A Modular Civic Infrastructure for Solidarity-Based Economies*

---

## **1. Introduzione**

**Social Market** è un’infrastruttura digitale modulare progettata per supportare economie mutualistiche, Gruppi di Acquisto Solidale (GAS), comunità CSA/AMAP, mercati contadini, cooperative territoriali e reti civiche federate.

Il software nasce con tre obiettivi fondamentali:

1. **Ridurre la complessità operativa** dei gruppi comunitari.  
2. **Restituire sovranità digitale** a organizzazioni locali e reti territoriali.  
3. **Costruire un ecosistema federato**, in cui ogni nodo è autonomo ma interoperabile.

Social Market è implementato come un **plugin WordPress modulare**, con un core stabile e una serie di moduli funzionali indipendenti.

---

## **2. Visione e principi architetturali**

### **2.1 Visione**

Social Market vuole essere un *sistema operativo civico* per economie comunitarie, capace di:

- gestire ordini collettivi  
- coordinare produttori locali  
- amministrare fondi comuni  
- tracciare movimenti economici  
- organizzare logistica e turni  
- supportare governance partecipativa  
- federare nodi territoriali  

### **2.2 Principi**

- **Modularità** — ogni dominio è un modulo indipendente.  
- **Dominio prima della tecnica** — l’architettura riflette processi reali.  
- **Dati strutturati** — tabelle dedicate, non solo CPT.  
- **API-first** — tutto è esposto via REST API versionate.  
- **Interfacce accessibili** — admin UX per volontari, non tecnici.  
- **Federazione naturale** — nodi autonomi ma interoperabili.  
- **Longevità** — software mantenibile per decenni.

---

## **3. Architettura generale**

L’architettura è composta da quattro livelli principali.

### **3.1 Core Layer**

Responsabile di:

- bootstrap del plugin  
- ruoli e permessi  
- impostazioni globali  
- creazione e migrazione tabelle  
- namespace REST  
- caricamento moduli  
- diagnostica  

### **3.2 Domain Modules**

Ogni dominio funzionale è un modulo indipendente:

- **Orders** — ordini collettivi, cicli, carrelli  
- **Producers** — produttori, listini, disponibilità  
- **Funds** — fondi comuni, conti prepagati  
- **Ledger** — movimenti economici, audit log  
- **Logistics** — punti di ritiro, turni, consegne  
- **Governance** — assemblee, decisioni, gruppi di lavoro  
- **MutualCredit** — valute di gruppo, limiti, credito reciproco  
- **Federation** — sincronizzazione tra nodi

Ogni modulo contiene:

- service class  
- REST controller  
- admin UI  
- template  
- assets  
- hook dedicati  

### **3.3 Integration Layer**

Moduli opzionali per integrare:

- WooCommerce  
- sistemi di pagamento  
- newsletter (Newspack)  
- CRM esterni  
- sistemi di identità  

### **3.4 Federation Layer (fase 2)**

Protocollo di interoperabilità tra nodi:

- esportazione/importazione dati  
- sincronizzazione ledger  
- federazione valute mutuali  
- directory dei nodi  

---

## **4. Modello dei dati**

### **4.1 Tabelle principali**

| Tabella | Descrizione |
|--------|-------------|
| `sm_orders` | Ordini collettivi |
| `sm_order_items` | Dettagli degli ordini |
| `sm_cycles` | Cicli d’ordine |
| `sm_producers` | Produttori |
| `sm_products` | Prodotti e listini |
| `sm_accounts` | Conti membri e fondi |
| `sm_ledger_entries` | Movimenti economici |
| `sm_funds` | Fondi comuni |
| `sm_pickup_points` | Punti di ritiro |
| `sm_shifts` | Turni e volontari |
| `sm_groups` | Gruppi di lavoro |
| `sm_decisions` | Decisioni e governance |

### **4.2 Principi del modello dati**

- normalizzazione rigorosa  
- audit log immutabile  
- relazioni esplicite  
- migrazioni versionate  
- compatibilità futura con federazione  

---

## **5. API e interoperabilità**

### **5.1 REST API**

Namespace:  
/wp-json/socialmarket/v1/


Endpoint principali:

- `/orders`  
- `/cycles`  
- `/producers`  
- `/funds`  
- `/ledger`  
- `/logistics`  
- `/governance`  

### **5.2 Principi API**

- versionamento  
- autenticazione standard WordPress  
- payload coerenti  
- errori strutturati  
- estendibilità tramite hook  

---

## **6. Sicurezza e permessi**

### **6.1 Ruoli base**

- `sm_admin`  
- `sm_coordinator`  
- `sm_bookkeeper`  
- `sm_producer`  
- `sm_member`  

### **6.2 Capabilities granulari**

Esempi:

- `sm_manage_orders`  
- `sm_manage_funds`  
- `sm_view_ledger`  
- `sm_edit_producers`  
- `sm_manage_logistics`  

### **6.3 Principi di sicurezza**

- least privilege  
- audit log completo  
- validazione server-side  
- sanitizzazione rigorosa  

---

## **7. Interfaccia utente**

### **7.1 Admin UI**

- React/JS per viste dinamiche  
- WP List Tables per viste semplici  
- pannelli modulari  
- onboarding guidato  

### **7.2 Frontend**

- shortcode  
- blocchi Gutenberg (fase 2)  
- template override  

---

## **8. Estendibilità**

### **8.1 Hook e filtri**

Eventi principali:

- `sm_order_created`  
- `sm_ledger_entry_created`  
- `sm_fund_balance_changed`  
- `sm_producer_updated`  

### **8.2 Interfacce PHP**

Service class con metodi pubblici documentati.

### **8.3 Moduli esterni**

Chiunque può creare:

- moduli aggiuntivi  
- gateway di pagamento  
- integrazioni CRM  
- estensioni governance  

---

## **9. Roadmap tecnica**

### **Fase 1 — Core + moduli fondamentali**

- Core  
- Orders  
- Producers  
- Funds  
- Ledger  
- Logistics  

### **Fase 2 — Estensioni avanzate**

- Governance  
- MutualCredit  
- Federation  
- Mobile UI  

### **Fase 3 — Ecosistema**

- Marketplace moduli  
- Documentazione avanzata  
- API pubbliche  
- Standard di interoperabilità  

---

## **10. Conclusione**

Social Market è progettato come un’infrastruttura civica modulare, capace di sostenere economie comunitarie complesse senza sacrificare semplicità, trasparenza e autonomia.

L’architettura è pensata per durare, per essere estesa, per essere compresa da sviluppatori futuri e per essere governata da comunità reali.
