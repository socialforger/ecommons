# Governance — ecommons  
## Community Decision-Making Layer (CDML)

Questo documento descrive il **Governance Layer** di ecommons: il sistema che permette a comunità, gruppi, cooperative e reti agroecologiche di prendere decisioni collettive in modo trasparente, democratico e federabile.  
La governance è ispirata ai principi del Confederalismo Democratico e dello zapatismo:  
**assemblea, mandato revocabile, rotazione, trasparenza, autonomia locale.**

---

# 1. Obiettivi della governance

Il Governance Layer permette a una comunità di:

- proporre decisioni  
- discutere collettivamente  
- votare secondo regole condivise  
- deliberare in modo trasparente  
- tracciare ogni passaggio nel ledger  
- federare le decisioni con altri nodi  

La governance non è un modulo opzionale: è una **funzione politica fondamentale** dell’infrastruttura.

---

# 2. Architettura generale

La governance è composta da tre componenti principali:
governance/ │ ├── class-governance-proposals.php ├── class-governance-votes.php ├── class-governance-assembly.php └── templates/

### **2.1 Proposals**
Gestisce:

- creazione proposte  
- categorie  
- stati (bozza, attiva, chiusa, deliberata)  
- discussioni  
- allegati  

### **2.2 Votes**
Gestisce:

- sistemi di voto  
- quorum  
- maggioranze  
- deleghe (opzionali)  
- verifica integrità  

### **2.3 Assembly**
Gestisce:

- assemblee periodiche  
- assemblee straordinarie  
- ordini del giorno  
- verbali  
- deliberazioni finali  

---

# 3. Principi della governance

### **3.1 Assemblea come centro decisionale**
La comunità decide, non gli amministratori.

### **3.2 Trasparenza radicale**
Ogni proposta, voto e deliberazione è tracciata.

### **3.3 Mandato revocabile**
I ruoli possono essere revocati tramite assemblea.

### **3.4 Rotazione**
La governance incoraggia la rotazione dei ruoli.

### **3.5 Autonomia locale**
Ogni nodo decide le proprie regole.

### **3.6 Federazione volontaria**
Le decisioni possono essere condivise con altri nodi.

---

# 4. Tipi di governance supportati

## **4.1 Consenso**
Tutti devono essere d’accordo o non avere obiezioni bloccanti.

## **4.2 Maggioranza semplice**
50% + 1 dei votanti.

## **4.3 Maggioranza qualificata**
2/3, 3/4 o valori configurabili.

## **4.4 Voto ponderato**
Basato su:

- ruoli  
- gruppi  
- contributi comunitari  

## **4.5 Deleghe**
Facoltative, con tracciamento trasparente.

---

# 5. Flusso di una proposta

1. **Creazione**  
   Un membro crea una proposta.

2. **Discussione**  
   Commenti, modifiche, allegati.

3. **Apertura votazione**  
   Con regole definite (quorum, durata, sistema di voto).

4. **Votazione**  
   Ogni voto è firmato digitalmente.

5. **Chiusura**  
   Il sistema calcola automaticamente l’esito.

6. **Deliberazione**  
   L’assemblea approva o respinge formalmente.

7. **Registrazione nel ledger**  
   La decisione diventa parte della memoria comunitaria.

---

# 6. Struttura dei dati

## **6.1 Proposta**

```json
{
  "id": 42,
  "title": "Acquisto collettivo attrezzatura",
  "author": 12,
  "status": "voting",
  "category": "economia",
  "created_at": "2025-01-12",
  "voting": {
    "method": "majority",
    "quorum": 20,
    "duration_hours": 72
  }
}
```
## **6.2 Voto**
```json
{
  "proposal_id": 42,
  "user_id": 12,
  "vote": "yes",
  "timestamp": "2025-01-13T10:22:00Z",
  "signature": "..."
}
```
