⚡ High-Performance Order Matching Engine

📌 Overview

Motore di order matching ad alte prestazioni sviluppato in Java SE puro, ispirato ai sistemi utilizzati nelle borse valori.

Il progetto simula un ambiente di trading reale ed è progettato per:
	•	gestire alto throughput
	•	garantire bassa latenza
	•	supportare concorrenza reale
	•	fornire metriche di performance in tempo reale

Focus principale: performance, concurrency e qualità architetturale

⸻

🎯 Obiettivi
	•	Matching automatico tra ordini buy/sell
	•	Supporto per limit orders e market orders
	•	Gestione partial fill
	•	Sistema thread-safe
	•	Monitoraggio delle performance

⸻

⚙️ Funzionalità

Tipi di Ordine
	•	Limit Buy → inserito nel book, eseguito se prezzo ≥ miglior sell
	•	Limit Sell → inserito nel book, eseguito se prezzo ≤ miglior buy
	•	Market Buy → esecuzione immediata al miglior prezzo disponibile
	•	Market Sell → esecuzione immediata al miglior prezzo disponibile
	•	Partial Fill → quantità residua mantenuta nel book
	•	Cancel → rimozione ordine prima dell’esecuzione

⸻

Order Book
	•	Buy side ordinato per prezzo decrescente
	•	Sell side ordinato per prezzo crescente
	•	Price-Time Priority (prima prezzo, poi tempo)
	•	Prezzi gestiti in centesimi (int) per evitare errori floating point

⸻

Matching Engine

Flusso principale:

Order → Validazione
→ Se market → match immediato
→ Se limit → inserimento nel book
→ Loop:
  while (bestBuy >= bestSell)
   → esecuzione trade
   → aggiornamento quantità
   → rimozione o aggiornamento ordini
→ Output evento + aggiornamento statistiche

⸻

📈 Statistiche Real-Time
	•	Totale trades eseguiti
	•	Volume totale
	•	Latenza media e massima
	•	Numero ordini pendenti
	•	Throughput (ordini/sec)

⸻

🛠️ Tecnologie
	•	Java 17+
	•	Concurrency API (Executors, BlockingQueue, AtomicLong)
	•	Collections (ConcurrentSkipListSet, ConcurrentHashMap)
	•	java.time
	•	JUnit 5

⸻

🧠 Scelte Tecniche

Order Book

Struttura principale:
ConcurrentSkipListSet

Motivazioni:
	•	Thread-safe senza lock espliciti
	•	Complessità O(log n)
	•	Iterazione sicura durante il matching

Alternative scartate:
	•	PriorityQueue → non thread-safe
	•	PriorityBlockingQueue → overhead troppo alto

⸻

🧩 Design Pattern
	•	Producer-Consumer → separazione tra submission e matching
	•	Immutable Object → sicurezza thread
	•	Factory Method → creazione dei trade
	•	Strategy → comparatori buy/sell
	•	Singleton → generatore ID
	•	Value Object → enum Side

⸻

📊 Performance Target
	•	Throughput > 50k ordini/sec
	•	Latenza media < 0.5 ms
	•	Supporto > 10 thread concorrenti
	•	Memoria per ordine < 200 bytes
	•	Test coverage > 80%

⸻

🧪 Testing

Unit Test
	•	Creazione ordini
	•	Matching buy/sell
	•	Partial fill
	•	Market orders
	•	Cancellazione

Concurrent Test
	•	Invio ordini multi-thread
	•	Assenza di data race
	•	Generazione ID atomica

Performance Test
	•	Benchmark 100k ordini
	•	Misurazione latenza
	•	Verifica memory leak

⸻

📁 Struttura del Progetto

it.matchingengine/
│
├── model/
├── engine/
├── stats/
├── logging/
├── util/
└── Main.java

⸻

🚀 Setup

git clone https://github.com/federico-dot/RealTimeOrderEngineTreadingSimulator
cd RealTimeOrderEngineTreadingSimulator

Compila ed esegui:

javac Main.java
java Main

⸻

🚀 Estensioni Future
	•	Iceberg Orders
	•	Stop-Loss Orders
	•	REST API
	•	WebSocket real-time
	•	Persistenza dati (JSON/CSV)
	•	Dashboard grafica

⸻

💡 Perché Questo Progetto è Rilevante

Dimostra concretamente:
	•	Concurrency reale (non teorica)
	•	Scelte architetturali consapevoli
	•	Ottimizzazione delle performance
	•	Modellazione di un dominio complesso

È un esempio pratico di sistema vicino a quelli usati in ambienti di high-frequency trading.

⸻

👨‍💻 Autore

Federico Cresci

⸻

📜 Licenza

MIT
