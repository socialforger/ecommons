# Social Market – Architecture Overview

Questo documento descrive l’architettura tecnica di Social Market, con particolare attenzione alla struttura modulare del plugin, ai flussi interni, ai moduli funzionali e al nuovo **Integration Layer**, che abilita l’interoperabilità con software esterni, produttori, GAS, sistemi logistici e altri nodi Social Market.

L’obiettivo dell’architettura è garantire:

- chiarezza
- estensibilità
- modularità
- interoperabilità
- semplicità per gli utenti
- robustezza per gli sviluppatori

---

# 1. Visione generale

Social Market è progettato come un **ecosistema modulare**, composto da:

- un **Core Plugin** che fornisce le fondamenta
- una serie di **moduli funzionali** (Orders, Products, Suppliers, Deliveries, ecc.)
- un **Integration Layer** che espone API pubbliche e gestisce la comunicazione con sistemi esterni
- un **frontend** basato su tema WordPress
- un **backend amministrativo** per operatori e referenti
- un **sistema di estensioni** per funzionalità aggiuntive

L’architettura è pensata per essere federabile, scalabile e compatibile con diversi contesti territoriali.

---

# 2. Core Plugin

Il Core Plugin contiene:

- registrazione dei custom post types
- registrazione dei custom database tables
- gestione ruoli e permessi
- funzioni di utilità condivise
- sistema di logging
- event dispatcher interno
- caricamento dei moduli

Il Core non contiene logiche di business specifiche: queste risiedono nei moduli.

---

# 3. Moduli funzionali

Ogni modulo è isolato, autonomo e responsabile di una singola area funzionale.

## 3.1 Orders Module
Gestisce:

- creazione ordini
- aggiornamento stato
- righe d’ordine
- calcoli totali
- collegamento con consegne e produttori

## 3.2 Products Module
Gestisce:

- catalogo prodotti
- varianti
- disponibilità
- prezzi
- categorie

## 3.3 Suppliers Module
Gestisce:

- anagrafica fornitori
- documenti fiscali
- metadati
- stato attivo/inattivo

## 3.4 Deliveries Module
Gestisce:

- calendari consegne
- punti di ritiro
- assegnazione ordini
- stato consegne

## 3.5 Groups & Users Module
Gestisce:

- gruppi GAS
- ruoli
- permessi
- referenti
- soci

---

# 4. Admin UI

L’interfaccia amministrativa fornisce:

- pannelli di gestione ordini
- gestione prodotti e listini
- gestione fornitori
- gestione consegne
- configurazioni del sistema
- strumenti di diagnostica

L’Admin UI è costruita con:

- WordPress Admin
- React (per componenti avanzati)
- REST API interne

---

# 5. Frontend

Il frontend è basato su:

- tema WordPress (es. Blocksy)
- shortcode e blocchi Gutenberg
- template personalizzati
- REST API interne per funzionalità dinamiche

Il frontend è responsabile dell’esperienza utente dei soci e dei referenti.

---

# 6. Database Architecture

Social Market utilizza una combinazione di:

- tabelle personalizzate (per ordini, prodotti, consegne)
- post types (per contenuti editoriali)
- meta tables (per estensioni flessibili)
- indici ottimizzati per query critiche

Ogni modulo definisce le proprie tabelle e il proprio schema.

---

# 7. Event System

Il sistema eventi interno permette:

- notifiche tra moduli
- trigger automatici
- logging avanzato
- integrazione con il layer di interoperabilità

Gli eventi interni sono utilizzati dal nuovo Integration Layer per generare webhook e sincronizzazioni.

---

# 8. Integration Layer (Interoperability Hub)

Il **Integration Layer** è un componente infrastrutturale che abilita Social Market a comunicare con software esterni, gestionali produttori, sistemi logistici, CRM, BI e altri nodi Social Market.

Non è un modulo funzionale, ma un **livello trasversale** tra il Core Plugin e il mondo esterno.

## 8.1 Obiettivi

- Esporre API pubbliche stabili e versionate
- Permettere la comunicazione bidirezionale con software esterni
- Supportare protocolli moderni e legacy
- Standardizzare i payload scambiati tra sistemi
- Abilitare la federazione tra più istanze Social Market
- Ridurre la necessità di integrazioni personalizzate

## 8.2 Componenti principali

### 1. REST API pubbliche (v1)
- Endpoint per ordini, prodotti, fornitori, consegne, gruppi e utenti
- Supporto JSON (default) e XML (via content negotiation)
- Autenticazione OAuth2 / API Key
- Versioning tramite path (`/v1/`)

### 2. XML‑RPC Endpoint
Compatibilità con gestionali legacy.

Metodi principali:
- `gas.getOrders`
- `gas.createOrder`
- `gas.getProducts`
- `gas.updateProduct`

### 3. Webhooks Dispatcher
Notifiche in tempo reale per eventi come:

- `order.created`
- `order.updated`
- `product.updated`
- `delivery.scheduled`
- `supplier.updated`

Supporta firma HMAC e retry.

### 4. Serializzatori e Mapper
Conversione tra:

- schema dati interno
- schema dati standard GAS
- JSON ↔ XML
- REST ↔ XML‑RPC

### 5. Event Bus interno
Riceve eventi dai moduli e li inoltra verso l’esterno.

## 8.3 Posizionamento nell’architettura

  Social Market 
+-------------------------------------------+ 
|  Core Plugin                              | 
+-------------------------------------------+
+-------------------------------------------+ 
|  Integration Layer / Interop Hub          | 
|  - REST API pubbliche (v1)                | 
|  - XML-RPC endpoint                       | 
|  - Webhooks dispatcher                    | 
|  - Serializzatori e mapper                | 
|  - Event bus interno                      | 
+-------------------------------------------+ 
+-------------------------------------------+ 
|  Software GAS, produttori, logistica,     | 
|  CRM, BI, altri nodi Social Market        | 
+-------------------------------------------+

## 8.4 Relazione con i moduli esistenti

Il layer espone verso l’esterno i dati gestiti dai moduli:

- Orders → `/orders`, `order.created`
- Products → `/products`, `product.updated`
- Suppliers → `/suppliers`, `supplier.updated`
- Deliveries → `/deliveries`, `delivery.scheduled`
- Groups/Users → `/groups`, `/users`

## 8.5 Federazione tra nodi Social Market

Il layer abilita:

- sincronizzazione ordini tra territori
- scambio listini tra produttori e GAS
- interoperabilità con piattaforme civiche
- federazione tra istanze Social Market

## 8.6 Struttura delle cartelle
/socialmarket /core /modules /integration /rest /xmlrpc /webhooks /serializers /mappers /validators /event-bus

## 8.7 Estensibilità

Il layer può essere esteso con:

- nuovi endpoint
- nuovi eventi webhook
- nuovi protocolli (gRPC, GraphQL)
- nuovi adapter per software terzi
- nuove versioni API (`/v2/`, `/v3/`)

---

# 9. Estensioni e Plugin Add-on

Social Market supporta estensioni per:

- pagamenti
- newsletter
- logistica
- BI
- integrazioni territoriali
- moduli sperimentali

Le estensioni possono utilizzare l’Integration Layer per comunicare con sistemi esterni.

---

# 10. Roadmap architetturale

- completamento Integration Layer v1
- federazione multi-nodo
- supporto GraphQL
- caching distribuito
- strumenti di diagnostica avanzata
- API per logistica e magazzino
- supporto multi-tenant

---

# 11. Conclusione

L’architettura di Social Market è progettata per essere:

- modulare
- estensibile
- interoperabile
- federabile
- sostenibile nel tempo

Il nuovo **Integration Layer** rappresenta un passo fondamentale verso un ecosistema aperto, cooperativo e tecnicamente solido, capace di dialogare con il mondo esterno e di supportare la crescita dei GAS e dei produttori in modo coordinato.
