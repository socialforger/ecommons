# ecommons — Documento Tecnico Ufficiale
## Adaptive Model Framework & Federated Architecture

---

# 1. Introduzione tecnica

ecommons è una piattaforma modulare e federata progettata per supportare una vasta famiglia di modelli agro‑comunitari, mutualistici e cooperativi.  
La sua architettura è costruita per essere:

- **modulare** — ogni funzionalità è un modulo indipendente  
- **federabile** — ogni installazione è un nodo autonomo  
- **adattiva** — ogni modello (GAS, AMAP, CSA, Solawi, Food Coop…) è una configurazione  
- **accessibile** — installabile su server economici  
- **sostenibile** — basata su tecnologie mature e diffuse  

L’obiettivo è fornire un’infrastruttura tecnica che permetta a comunità diverse di organizzarsi secondo le proprie pratiche, mantenendo interoperabilità e autonomia.

---

# 1.1 Filosofia architetturale

L’architettura di ecommons si fonda su tre principi:

### **1. Autonomia locale**
Ogni comunità deve poter installare, gestire e controllare il proprio nodo senza dipendere da un server centrale.

### **2. Federazione dal basso**
I nodi possono collegarsi tra loro volontariamente, condividendo dati selezionati e costruendo reti territoriali.

### **3. Modularità radicale**
Ogni funzionalità è un modulo attivabile/disattivabile.  
Ogni modello è una composizione di moduli.

---

# 1.2 Obiettivi tecnici

- Ridurre la complessità per le comunità con risorse limitate  
- Garantire interoperabilità tra modelli diversi  
- Supportare flussi operativi eterogenei  
- Permettere evoluzione e adattamento nel tempo  
- Favorire la replicabilità dei nodi federati  
- Assicurare trasparenza economica e governance partecipativa  

---

# 1.3 Scelta della piattaforma: perché WordPress

ecommons adotta WordPress come piattaforma applicativa di base per ragioni strategiche, tecniche ed economiche.  
La scelta non è un compromesso: è un atto politico e architetturale.

## 1.3.1 Diffusione globale e accessibilità tecnica
WordPress è il CMS più diffuso al mondo, presente in:

- associazioni  
- cooperative  
- enti locali  
- piccole organizzazioni  
- hosting condivisi a basso costo  

Questo garantisce che qualsiasi comunità possa installare ecommons senza infrastrutture complesse.

## 1.3.2 Server economici e facilmente reperibili
WordPress può essere eseguito su:

- hosting condivisi da 3–5 €/mese  
- VPS economici  
- server autogestiti  
- infrastrutture comunitarie  

Questo rende ecommons **accessibile a GAS, CSA, AMAP, Solawi, Food Coops e reti territoriali**, che spesso non dispongono di budget elevati o competenze DevOps.

## 1.3.3 Ecosistema modulare e maturo
WordPress offre:

- un sistema di plugin estensibile  
- un modello di hook e filtri ideale per architetture modulari  
- un sistema di ruoli e permessi integrato  
- REST API native  

Queste caratteristiche permettono a ecommons di costruire moduli indipendenti e configurabili.

## 1.3.4 Sovranità digitale e autonomia locale
WordPress è software libero, installabile ovunque, senza vincoli di piattaforma.  
Questo è perfettamente coerente con i principi confederali di ecommons:

- ogni nodo è autonomo  
- ogni comunità controlla i propri dati  
- nessun server centrale  
- federazione volontaria  

## 1.3.5 Comunità di sviluppatori e manutenzione a lungo termine
WordPress garantisce:

- aggiornamenti costanti  
- sicurezza mantenuta da una comunità globale  
- compatibilità a lungo termine  
- documentazione abbondante  

## 1.3.6 Conclusione
La scelta di WordPress permette a ecommons di essere:

- **accessibile**  
- **replicabile**  
- **federabile**  
- **modulare**  
- **sostenibile**  
- **democratico**  

---

# 2. Architettura generale

L’architettura di ecommons è composta da:

- **Core** — gestione utenti, ruoli, gruppi, impostazioni  
- **Moduli** — funzionalità attivabili  
- **Federation Layer** — comunicazione tra nodi  
- **Governance Layer** — assemblee, proposte, deliberazioni  
- **Ledger Layer** — movimenti economici, fondi, mutual credit  
- **Model Engine** — composizione dei moduli per modello  

---

# 3. Adaptive Model Framework

Il cuore di ecommons è il **Model Engine**, che permette di definire modelli organizzativi come configurazioni di moduli.

Ogni modello è rappresentato da un file:
ecommons/models/<model>.json


Contiene:

- moduli richiesti  
- moduli opzionali  
- flussi attivi  
- ruoli e permessi  
- logiche economiche  
- logiche di consegna  
- override locali  

---

# 4. Moduli fondamentali (Core Modules)

- **Users**  
- **Groups**  
- **Producers**  
- **Products**  
- **Orders**  
- **Logistics**  
- **Funds**  
- **Ledger**  
- **Governance**  
- **Federation**  

---

# 5. Moduli opzionali (Extended Modules)

- **Subscriptions**  
- **Harvest Planning**  
- **Basket Composition**  
- **Volunteer Shifts**  
- **MutualCredit**  
- **Bank Sync**  
- **Communications**  
- **Inventory**  
- **Pickup Points**  

---

# 6. Modelli supportati

Ogni modello è una composizione di moduli.

## 6.1 GAS — Gruppi di Acquisto Solidale
Moduli: Orders, Producers, Logistics, Funds, Ledger, Groups, Governance, Federation  
Link: https://retegas.org

## 6.2 AMAP — Francia
Moduli: Subscriptions, Harvest Planning, Producers, Logistics, Funds, Ledger, Governance  
Link: https://miramap.org

## 6.3 CSA — Globale
Moduli: Subscriptions, Basket Composition, Harvest Planning, Volunteer Shifts, Logistics, Funds, Ledger, Governance  
Link: https://urgenci.net

## 6.4 Teikei — Giappone
Moduli: Subscriptions, Harvest Planning, MutualCredit, Logistics, Governance  
Link: https://www.joaa.net

## 6.5 ASC — America Latina
Moduli: Subscriptions, Producers, Logistics, Governance, Funds  
Link: https://urgenci.net/category/latin-america

## 6.6 KöKiSz — Ungheria
Moduli: Subscriptions, Producers, Logistics, Governance, Communications  
Link: https://kokisz.hu

## 6.7 Andelsjordbruk — Svezia
Moduli: Subscriptions, Harvest Planning, Logistics, Governance, Funds  
Link: https://andelsjordbruk.se

## 6.8 Agronauts — Europa
Moduli: Producers, Logistics, Federation, Governance, Communications  
Link: https://www.agronauten.net

## 6.9 Food Coops — Globale
Moduli: Orders, Inventory, Logistics, Funds, Ledger, Governance  
Link: https://www.foodcoopdirectory.com

## 6.10 ACP — Svizzera
Moduli: Subscriptions, Harvest Planning, Producers, Logistics, Funds, Ledger, Governance  
Link: https://www.agriculturecontractuelle.ch

## 6.11 Solawi — Germania
Moduli: Subscriptions, Harvest Planning, Logistics, Volunteer Shifts, Funds, Ledger, Governance  
Link: https://www.solidarische-landwirtschaft.org

---

# 7. Federazione

La federazione permette ai nodi di:

- scoprire altri nodi  
- condividere dati selettivi  
- sincronizzare listini  
- partecipare a ordini inter‑GAS  
- costruire reti territoriali  

Tecnologie:

- REST API  
- XML‑RPC  
- autenticazione a chiavi  
- directory federata  

---

# 8. Governance

Il modulo Governance fornisce:

- assemblee  
- proposte  
- votazioni  
- deliberazioni  
- audit log  

Ogni decisione può essere collegata a:

- fondi  
- ordini  
- logistica  
- ruoli  

---

# 9. Ledger & Funds

Il Ledger registra:

- movimenti economici  
- fondi comunitari  
- prefinanziamento  
- mutual credit  
- integrazione con ordini e logistica  

---

# 10. Logistics & Orders

Funzionalità:

- cicli d’ordine  
- abbonamenti  
- composizione cassette  
- punti di ritiro  
- turni volontari  
- consegne  

---

# 11. Estendibilità

ecommons supporta:

- API REST  
- hook e filtri  
- moduli di terze parti  
- override dei template  
- personalizzazione dei modelli  

---

# 12. Roadmap tecnica

## Fase 1  
Core + Orders + Producers

## Fase 2  
Federation + Governance

## Fase 3  
Adaptive Model Engine

## Fase 4  
MutualCredit + Harvest Planning

## Fase 5  
Ecosistema federale completo

---

# Conclusione

ecommons è un’infrastruttura tecnica progettata per sostenere comunità reali, modelli diversi e reti confederali.  
La sua architettura modulare, federata e adattiva permette a ogni comunità di costruire il proprio modello, evolverlo e federarsi con altri nodi, mantenendo autonomia e sovranità digitale.
