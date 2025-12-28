# Architecture — ecommons.php & core/

Questo documento descrive l’architettura tecnica del file principale `ecommons.php` e del sottosistema `core/`, che costituiscono il fondamento del plugin ecommons.  
Il loro ruolo è fornire un’infrastruttura stabile, minimale e altamente estendibile su cui si innestano moduli, modelli e layer avanzati (federazione, governance, ledger, ecc.).

---

# 1. ecommons.php — Bootstrap del plugin

`ecommons.php` è il punto di ingresso del plugin.  
Le sue responsabilità sono:

- definire costanti globali  
- caricare il Core Loader  
- inizializzare i moduli fondamentali  
- registrare hook di attivazione/disattivazione  
- esporre il namespace principale  
- avviare il Model Engine (solo dopo il core)  

## 1.1 Responsabilità principali

### **1. Definizione delle costanti**
- versione del plugin  
- path e URL  
- path di moduli, core, models, assets  

### **2. Caricamento del Core Loader**
Il Core Loader è l’unico file caricato direttamente da `ecommons.php`.

### **3. Inizializzazione del Core**
Il Core gestisce:
- ruoli  
- post types  
- taxonomie  
- REST base  
- settings  
- utilità condivise  

### **4. Inizializzazione dei moduli**
Il Core Loader attiva solo i moduli richiesti dal Model Engine.

### **5. Integrazione con WordPress**
- hook `plugins_loaded`  
- hook `init`  
- registrazione REST  
- caricamento traduzioni  

---

# 2. Struttura del Core

La cartella `core/` contiene il nucleo funzionale del plugin.  
È progettata per essere:

- **minimale** (solo ciò che è indispensabile)  
- **stabile** (non dipende dai moduli)  
- **riutilizzabile** (tutti i moduli lo usano)  
- **estendibile** (tramite hook e filtri)  

Struttura:

core/

│ 

├── class-core-loader.php 

├── class-core-settings.php 

├── class-core-posttypes.php

├── class-core-taxonomies.php

├── class-core-rest.php 

├── class-core-roles.php

├── class-core-utils.php

└── traits/


---

# 3. Descrizione dei componenti del Core

## 3.1 class-core-loader.php  
Il **cuore del Core**.  
Responsabilità:

- caricare tutte le classi del core  
- inizializzare i componenti in ordine corretto  
- caricare i moduli attivi  
- caricare i Model Profiles  
- esporre hook per estensioni  

È l’unico punto che conosce l’intera architettura.

---

## 3.2 class-core-settings.php  
Gestisce:

- pagina impostazioni generali  
- opzioni salvate nel database  
- configurazioni globali del plugin  
- override dei modelli  

Espone funzioni come:

- `get_option()`  
- `get_active_model()`  
- `get_active_modules()`  

---

## 3.3 class-core-posttypes.php  
Registra i post types fondamentali:

- `ecommons_group`  
- `ecommons_producer`  
- `ecommons_product`  
- `ecommons_order` (solo base, esteso dai moduli)  
- `ecommons_ledger_entry`  
- `ecommons_proposal`  

Ogni modulo può aggiungere i propri.

---

## 3.4 class-core-taxonomies.php  
Registra le tassonomie condivise:

- categorie prodotti  
- categorie produttori  
- categorie logistiche  
- categorie governance  

---

## 3.5 class-core-rest.php  
Registra gli endpoint REST fondamentali:

- autenticazione  
- informazioni sul nodo  
- elenco moduli attivi  
- elenco modelli disponibili  
- health check  

I moduli aggiungono i propri endpoint.

---

## 3.6 class-core-roles.php  
Gestisce i ruoli e i permessi di base:

- `ecommons_admin`  
- `ecommons_manager`  
- `ecommons_member`  

I moduli possono aggiungere permessi granulari.

---

## 3.7 class-core-utils.php  
Funzioni condivise:

- sanitizzazione  
- validazione  
- helper per REST  
- helper per template  
- helper per moduli  

È la “cassetta degli attrezzi” del plugin.

---

## 3.8 traits/  
Contiene tratti riutilizzabili:

- `trait-singleton.php`  
- `trait-rest-response.php`  
- `trait-module-loader.php`  

I moduli possono usarli liberamente.

---

# 4. Flusso di inizializzazione

1. WordPress carica `ecommons.php`  
2. `ecommons.php` carica `class-core-loader.php`  
3. Core Loader:
   - definisce costanti  
   - carica tutte le classi del core  
   - registra ruoli, post types, taxonomie  
   - registra REST base  
   - carica il Model Engine  
   - attiva i moduli richiesti dal modello  
4. I moduli si registrano tramite hook  
5. Il plugin è operativo  

---

# 5. Principi architetturali del Core

### **1. Il Core non conosce i moduli**  
È il Model Engine a decidere quali moduli attivare.

### **2. Il Core è stabile**  
I moduli possono cambiare, il core no.

### **3. Il Core è minimale**  
Solo ciò che serve a far funzionare tutto il resto.

### **4. Il Core è estendibile**  
Hook e filtri ovunque.

### **5. Il Core è indipendente dai modelli**  
I modelli sono configurazioni, non codice.

---

# 6. Conclusione

`ecommons.php` e `core/` costituiscono la base dell’intero ecosistema ecommons.  
Sono progettati per essere:

- semplici  
- robusti  
- modulari  
- estendibili  
- futuri‑proof  

Tutto ciò che accade nel plugin — moduli, modelli, federazione, governance — si appoggia su questa architettura.
