# Modules — ecommons  
## Architettura modulare e composizione adattiva

Questo documento descrive l’architettura dei moduli di ecommons, il loro ciclo di vita, le dipendenze, le responsabilità e il modo in cui vengono attivati dal Model Engine.  
I moduli sono il cuore dell’approccio adattivo di ecommons: ogni modello organizzativo (GAS, AMAP, CSA, Solawi, Food Coop…) è una **composizione di moduli**, non un software separato.

---

# 1. Principi dei moduli

I moduli di ecommons seguono cinque principi fondamentali:

### **1.1 Modularità radicale**
Ogni funzionalità è isolata in un modulo indipendente.  
Il core rimane minimale e stabile.

### **1.2 Attivazione condizionata**
I moduli vengono attivati in base a:

- modello selezionato  
- configurazioni locali  
- dipendenze soddisfatte  

### **1.3 Estendibilità**
Ogni modulo può:

- registrare post types  
- aggiungere REST endpoints  
- aggiungere template  
- aggiungere ruoli e permessi  
- aggiungere logiche operative  

### **1.4 Interoperabilità**
I moduli comunicano tramite:

- hook  
- filtri  
- REST  
- eventi interni  

### **1.5 Indipendenza**
Nessun modulo deve conoscere l’implementazione interna degli altri.  
Solo il Core e il Model Engine orchestrano l’insieme.

---

# 2. Struttura dei moduli

Ogni modulo ha una struttura standard:
# Modules — ecommons  
## Architettura modulare e composizione adattiva

Questo documento descrive l’architettura dei moduli di ecommons, il loro ciclo di vita, le dipendenze, le responsabilità e il modo in cui vengono attivati dal Model Engine.  
I moduli sono il cuore dell’approccio adattivo di ecommons: ogni modello organizzativo (GAS, AMAP, CSA, Solawi, Food Coop…) è una **composizione di moduli**, non un software separato.

---

# 1. Principi dei moduli

I moduli di ecommons seguono cinque principi fondamentali:

### **1.1 Modularità radicale**
Ogni funzionalità è isolata in un modulo indipendente.  
Il core rimane minimale e stabile.

### **1.2 Attivazione condizionata**
I moduli vengono attivati in base a:

- modello selezionato  
- configurazioni locali  
- dipendenze soddisfatte  

### **1.3 Estendibilità**
Ogni modulo può:

- registrare post types  
- aggiungere REST endpoints  
- aggiungere template  
- aggiungere ruoli e permessi  
- aggiungere logiche operative  

### **1.4 Interoperabilità**
I moduli comunicano tramite:

- hook  
- filtri  
- REST  
- eventi interni  

### **1.5 Indipendenza**
Nessun modulo deve conoscere l’implementazione interna degli altri.  
Solo il Core e il Model Engine orchestrano l’insieme.

---

# 2. Struttura dei moduli

Ogni modulo ha una struttura standard:

modules/<module-name>/ 

│ 

├── class-<module-name>.php     # Classe principale del modulo 

├── rest/                       # Endpoint REST specifici 

├── templates/                  # Template frontend 

├── assets/                     # JS, CSS, immagini 

└── config.json                 # Metadati del modulo


### **2.1 class-<module-name>.php**
Contiene:

- registrazione del modulo  
- hook e filtri  
- inizializzazione  
- caricamento di REST, template, assets  
- dipendenze richieste  

### **2.2 config.json**

```json
{
  "name": "orders",
  "title": "Orders",
  "description": "Gestione degli ordini comunitari",
  "version": "1.0.0",
  "dependencies": ["producers", "products"],
  "optional": false
}
```

# 3. Ciclo di vita di un modulo

1. 	Rilevamento
 Il Core Loader scansiona la cartella modules/.
 
2. 	Validazione
 Verifica:
 • 	presenza della classe principale
 • 	integrità del config.json
 • 	dipendenze soddisfatte
 
3. 	Attivazione
 Il Model Engine attiva solo i moduli richiesti dal modello selezionato.
 
4. 	Inizializzazione
 Il modulo registra:
 • 	post types
 • 	tassonomie
 • 	ruoli
 • 	REST endpoints
 • 	template
 
5. 	Esecuzione
 Il modulo opera in autonomia, esponendo hook e filtri.

# 4. Elenco dei moduli ufficiali
Di seguito l’elenco dei moduli core e opzionali di ecommons, con descrizione e responsabilità.

## 4.1 Moduli fondamentali (Core Modules)
### Users
Gestione utenti, ruoli, permessi.
### Groups
Gestione gruppi, comunità, GAS, nodi locali.
### Producers
Anagrafica produttori, relazioni, certificazioni, filiere.
### Products
Catalogo prodotti, categorie, varianti, disponibilità.
### Orders
Gestione ordini comunitari, cicli d’ordine, riepiloghi.
### Logistics
Consegne, punti di ritiro, turni, trasporti.
### Funds
Fondi comunitari, quote, contributi.
### Ledger
Movimenti economici, trasparenza, audit.
### Governance
Assemblee, proposte, votazioni, deliberazioni.
### Federation
Sincronizzazione tra nodi, directory federata, scambio dati.

## 4.2 Moduli opzionali (Extended Modules)
### Subscriptions
Abbonamenti, quote stagionali, prefinanziamento.
### Harvest Planning
Pianificazione agricola, raccolti, stagionalità.
### Basket Composition
Composizione cassette, personalizzazioni, sostituzioni.
### Volunteer Shifts
Turni volontari, disponibilità, calendario.
### Mutual Credit
Credito reciproco, limiti, ledger dedicato.
### Communications
Newsletter, notifiche, messaggistica interna.
### Inventory
Magazzino, stock, movimenti interni.
### Pickup Points
Gestione punti di ritiro, orari, responsabili.

# 5. Dipendenze tra moduli
Esempi:
• 	Orders richiede: Producers, Products
• 	Subscriptions richiede: Funds, Ledger
• 	Basket Composition richiede: Products
• 	Volunteer Shifts è indipendente
• 	Mutual Credit richiede: Ledger
• 	Harvest Planning richiede: Producers
Le dipendenze sono dichiarate in .

# 6. Attivazione tramite Model Engine
Ogni modello (GAS, AMAP, CSA, Solawi…) definisce i moduli attivi:
Esempio :

Il Model Engine:
1. 	legge il file
2. 	valida i moduli
3. 	attiva solo quelli richiesti
4. 	applica override locali

# 7. Hook e filtri dei moduli
Ogni modulo espone:
• 	hook di inizializzazione
• 	hook di validazione
• 	hook di salvataggio
• 	hook di sincronizzazione
• 	filtri per modificare output e query
Esempio:


# 8. Best practices per sviluppatori
8.1 Non duplicare logiche del core
Usare Core Utils, Core REST, Core Roles.
8.2 Non accedere direttamente ai moduli
Usare hook e filtri.
8.3 Non creare dipendenze circolari
Ogni modulo deve essere autonomo.
8.4 Documentare sempre config.json
È la base dell’Adaptive Model Framework.
8.5 Usare namespace e prefissi
Evitare conflitti con altri plugin.

# 9. Conclusione
I moduli sono l’unità fondamentale dell’architettura di ecommons.
Grazie alla modularità radicale e al Model Engine, ecommons può adattarsi a modelli organizzativi diversi, evolvere nel tempo e rimanere semplice da mantenere.
La modularità è ciò che rende ecommons:
• 	flessibile
• 	estensibile
• 	federabile
• 	sostenibile
• 	future‑proof
