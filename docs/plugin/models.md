# Models — ecommons  
## Adaptive Model Framework (AMF)

Questo documento descrive l’architettura dei *Model Profiles* di ecommons, il loro ruolo nel sistema, la struttura dei file JSON, il ciclo di attivazione e il modo in cui determinano la composizione dei moduli.  
I modelli sono ciò che permette a ecommons di adattarsi a GAS, AMAP, CSA, Solawi, Food Coops e molte altre forme di agricoltura comunitaria.

---

# 1. Cos’è un Model Profile

Un **Model Profile** è un file JSON che definisce:

- quali moduli devono essere attivati  
- quali configurazioni devono essere applicate  
- quali permessi devono essere assegnati  
- quali flussi operativi devono essere abilitati  
- quali override devono essere applicati ai moduli  

Il modello non contiene codice: è **configurazione pura**.  
Questo permette a ecommons di essere:

- flessibile  
- estensibile  
- internazionale  
- futuro‑proof  

---

# 2. Struttura dei Model Profiles

I modelli si trovano nella cartella:
models/

Ogni file rappresenta un modello organizzativo:
models/ 
│
├── gas.json 
├── amap.json 
├── csa.json 
├── solawi.json 
├── teikei.json 
├── foodcoop.json 
├── asc.json 
├── kokisz.json 
├── andelsjordbruk.json 
└── agronauts.json

---

# 3. Struttura interna di un modello

Esempio generico:

```json
{
  "name": "CSA",
  "description": "Community Supported Agriculture",
  "modules": [
    "subscriptions",
    "harvest-planning",
    "basket-composition",
    "logistics",
    "funds",
    "ledger",
    "governance"
  ],
  "settings": {
    "ordering_mode": "subscription_only",
    "allow_product_variants": false,
    "enable_pickup_points": true
  },
  "permissions": {
    "member": ["view_products", "view_orders"],
    "manager": ["manage_orders", "manage_subscriptions"],
    "admin": ["manage_all"]
  },
  "overrides": {
    "subscriptions": {
      "require_prepayment": true,
      "season_length_weeks": 52
    }
  }
}
Eccoti  scritto in modo completo, professionale, coerente con l’architettura di ecommons e pronto per il repository GitHub.
Tutto in un unico code‑box nero, come richiesto.


models/

models/ │ ├── gas.json ├── amap.json ├── csa.json ├── solawi.json ├── teikei.json ├── foodcoop.json ├── asc.json ├── kokisz.json ├── andelsjordbruk.json └── agronauts.json


4. Campi principali
4.1 
Nome breve del modello.
4.2 
Descrizione estesa del modello.
4.3 
Elenco dei moduli da attivare.
Esempio:

4.4 
Configurazioni specifiche del modello:
• 	modalità d’ordine
• 	visibilità prodotti
• 	gestione stagionalità
• 	opzioni logistiche
• 	parametri economici
4.5 
Permessi aggiuntivi o restrittivi per ruoli specifici.
4.6 
Override di configurazione per singoli moduli.

5. Ciclo di attivazione del modello
1. 	L’utente seleziona un modello nella dashboard.
2. 	Il Core Loader carica il file JSON.
3. 	Il Model Engine valida il file:
• 	sintassi
• 	moduli esistenti
• 	dipendenze soddisfatte
4. 	Il Model Engine attiva i moduli richiesti.
5. 	Applica le configurazioni del modello.
6. 	Applica gli override dei moduli.
7. 	Applica i permessi aggiuntivi.
Il risultato è un’installazione completamente adattata al modello scelto.

6. Modelli ufficiali
Di seguito i modelli ufficiali inclusi in ecommons.

6.1 GAS (Gruppi di Acquisto Solidale)
Obiettivo: ordini periodici, relazioni dirette, trasparenza.
Moduli attivi:
• 	orders
• 	producers
• 	products
• 	logistics
• 	funds
• 	ledger
• 	communications

6.2 AMAP (Francia)
Obiettivo: prefinanziamento, stagionalità, relazioni contadine.
Moduli attivi:
• 	subscriptions
• 	harvest-planning
• 	basket-composition
• 	logistics
• 	funds
• 	ledger
• 	governance

6.3 CSA (Community Supported Agriculture)
Simile ad AMAP, con maggiore flessibilità.
Moduli attivi:
• 	subscriptions
• 	harvest-planning
• 	basket-composition
• 	logistics
• 	funds
• 	ledger
• 	governance

6.4 Solawi (Germania)
Obiettivo: contributo libero, trasparenza radicale.
Moduli attivi:
• 	funds
• 	ledger
• 	governance
• 	logistics
• 	harvest-planning

6.5 Teikei (Giappone)
Obiettivo: relazione diretta, consegne regolari.
Moduli attivi:
• 	producers
• 	logistics
• 	basket-composition
• 	communications

6.6 Food Coop
Obiettivo: gestione collettiva, turni volontari, magazzino.
Moduli attivi:
• 	inventory
• 	volunteer-shifts
• 	products
• 	orders
• 	logistics
• 	governance

7. Override locali
Ogni installazione può definire un file:

Questo file:
• 	estende il modello selezionato
• 	non viene sovrascritto dagli aggiornamenti
• 	permette personalizzazioni locali
Esempio:


8. Best practices
8.1 Non duplicare modelli
Se un modello è simile a un altro, usare override.
8.2 Non inserire logica nei modelli
Solo configurazione.
8.3 Documentare ogni campo
Ogni modello deve essere leggibile da non sviluppatori.
8.4 Usare nomi coerenti
I moduli devono corrispondere ai nomi delle cartelle.
8.5 Mantenere i modelli minimali
Solo ciò che serve.

9. Conclusione
I Model Profiles sono ciò che rende ecommons un’infrastruttura veramente adattiva.
Grazie ai modelli:
• 	un singolo plugin può supportare decine di forme organizzative
• 	ogni comunità può configurare il proprio modo di lavorare
• 	l’ecosistema può crescere senza duplicare codice
• 	la federazione può collegare modelli diversi tra loro
L’Adaptive Model Framework è il cuore della flessibilità di ecommons.
