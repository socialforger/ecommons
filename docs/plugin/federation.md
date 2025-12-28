# Federation — ecommons  
## Federated Community Infrastructure Layer (FCIL)

Questo documento descrive l’architettura del **Federation Layer** di ecommons, il sistema che permette a nodi autonomi di cooperare senza centralizzazione.  
La federazione è ispirata ai principi del Confederalismo Democratico e dello zapatismo:  
**autonomia locale + cooperazione volontaria + scambio selettivo dei dati**.

---

# 1. Obiettivi della federazione

Il Federation Layer permette a comunità autonome di:

- condividere dati selezionati  
- cooperare su filiere agroecologiche  
- scambiare informazioni su produttori, prodotti, disponibilità  
- coordinare logistica e ordini inter‑gruppo  
- costruire reti territoriali senza un server centrale  

La federazione non è obbligatoria: ogni nodo decide **se**, **come** e **con chi** federarsi.

---

# 2. Architettura generale

La federazione è composta da tre componenti principali:
federation/ │ ├── class-federation-client.php ├── class-federation-server.php ├── class-federation-sync.php └── protocols/

### **2.1 Federation Client**
Invia richieste ad altri nodi:

- discovery  
- richieste di dati  
- sincronizzazione  
- notifiche federate  

### **2.2 Federation Server**
Risponde alle richieste in ingresso:

- autenticazione  
- autorizzazione  
- esposizione dati selezionati  
- rate limiting  

### **2.3 Federation Sync**
Gestisce:

- sincronizzazioni periodiche  
- code di sincronizzazione  
- conflitti  
- fallback offline  

### **2.4 Protocols**
Contiene:

- definizioni dei payload  
- versionamento dei protocolli  
- mapping dei campi  
- specifiche di sicurezza  

---

# 3. Principi della federazione

### **3.1 Autonomia**
Ogni nodo è sovrano.  
Nessun nodo può imporre configurazioni ad altri.

### **3.2 Consenso esplicito**
La federazione è sempre opt‑in.

### **3.3 Scambio selettivo**
Ogni nodo decide quali dati condividere:

- produttori  
- prodotti  
- disponibilità  
- punti di ritiro  
- ordini aggregati  
- statistiche anonime  

### **3.4 Trasparenza**
Ogni sincronizzazione è tracciata nel ledger federato.

### **3.5 Sicurezza**
Ogni nodo ha:

- chiave pubblica  
- chiave privata  
- token di federazione  
- rate limiting  

---

# 4. Tipi di federazione

## **4.1 Federazione informativa**
Scambio di informazioni non sensibili:

- elenco produttori  
- disponibilità stagionali  
- punti di ritiro  
- eventi comunitari  

## **4.2 Federazione operativa**
Coordinamento tra nodi:

- ordini inter‑gruppo  
- logistica condivisa  
- turni volontari federati  

## **4.3 Federazione economica**
Sincronizzazione di:

- fondi comunitari federati  
- ledger condivisi  
- mutual credit inter‑nodo  

## **4.4 Federazione politica**
Condivisione di:

- proposte  
- deliberazioni  
- assemblee confederali  

---

# 5. Discovery dei nodi

Ogni nodo può:

- registrarsi in una directory federata (opzionale)  
- scoprire altri nodi tramite API  
- aggiungere nodi manualmente  

Esempio di payload:

```json
{
  "node_name": "GAS Roma Sud",
  "url": "https://gasromasud.example",
  "public_key": "-----BEGIN PUBLIC KEY-----...",
  "models": ["GAS", "CSA"],
  "modules": ["orders", "logistics", "funds"]
}
```
# 6. Autenticazione e autorizzazione
Ogni nodo possiede:
• 	chiave privata (locale)
• 	chiave pubblica (condivisa)
• 	token federativo (rotabile)
Autenticazione tramite:
• 	firma digitale
• 	timestamp
• 	nonce
Autorizzazione tramite:
• 	policy locali
• 	whitelist nodi
• 	permessi granulari per modulo

# 7. Sincronizzazione
La sincronizzazione può essere:
7.1 Manuale
Attivata dall’utente.
7.2 Programmata
Eseguita a intervalli regolari.
7.3 Event‑based
Attivata da:
• 	nuovo ordine
• 	nuova disponibilità
• 	nuova proposta
• 	aggiornamento produttore
7.4 Full sync
Replica completa dei dati federabili.
7.5 Partial sync
Replica selettiva.
# 8. Conflitti e risoluzione
Il Federation Layer implementa:
• 	timestamp logici
• 	versionamento dei record
• 	priorità configurabili
• 	merge automatico quando possibile
• 	fallback manuale quando necessario
Esempio:
Se due nodi aggiornano lo stesso produttore:
- prevale il nodo proprietario del produttore
- gli altri nodi ricevono l’aggiornamento
# 9. Dati federabili
9.1 Produttori
• 	anagrafica
• 	certificazioni
• 	disponibilità
9.2 Prodotti
• 	catalogo
• 	stagionalità
• 	prezzi comunitari
9.3 Ordini
• 	aggregati
• 	richieste inter‑nodo
• 	disponibilità condivise
9.4 Logistica
• 	punti di ritiro
• 	turni
• 	trasporti condivisi
9.5 Governance
• 	proposte
• 	deliberazioni
• 	assemblee
9.6 Ledger
• 	movimenti federati
• 	mutual credit
# 10. Sicurezza
10.1 Crittografia
• 	TLS obbligatorio
• 	firma digitale dei payload
10.2 Rate limiting
Protezione da abusi.
10.3 Audit federato
Ogni sincronizzazione è registrata.
10.4 Isolamento dei moduli
Ogni modulo decide cosa federare.

# 11. Best practices
11.1 Federare solo ciò che serve
La federazione non è un backup.
11.2 Usare whitelist
Meglio pochi nodi affidabili che molti nodi sconosciuti.
11.3 Documentare le policy
Ogni nodo deve sapere cosa condivide.
11.4 Monitorare i conflitti
La federazione è un sistema vivo.

# 12. Conclusione
Il Federation Layer rende ecommons una vera infrastruttura confederale:
• 	nodi autonomi
• 	cooperazione volontaria
• 	scambio selettivo
• 	sicurezza
• 	trasparenza
• 	resilienza

È il ponte che collega comunità diverse in un ecosistema agroecologico federato.
