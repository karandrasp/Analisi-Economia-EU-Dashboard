# Analisi-Economia-EU-Dashboard
Un progetto di (ETL) da fonti pubbliche (Eurostat) utilizzando Python (Pandas, SQLAlchemy) e MySQL. Usando le SQL Views per preparare i dati e Power BI per identificare trend e insight socio-economici in Europa.

---

### Dashboard Interattivo

**Esplora il report completo e interattivo generato da questo progetto al seguente link:**

### Dashboard Interattivo

**Esplora il report completo e interattivo generato da questo progetto al seguente link:**

[**>> VISUALIZZA IL DASHBOARD LIVE <<**](https://app.powerbi.com/view?r=eyJrIjoiMTM2NWQzNDMtMWI3My00YWNjLWJkYWQtMzE0NmQ5NTVlY2Q3IiwidCI6ImM5NDI0M2ViLTZmMGUtNDU2Ni1hMjk2LWI1ZGZjOWQyNTczYiIsImMiOjh9)

---

### Anteprima del Dashboard

<img width="1387" height="760" alt="image" src="https://github.com/user-attachments/assets/dba33a04-0e48-4137-8417-1cc6f1b46cc0" />


---

### Obiettivo del Progetto

L'obiettivo di questo progetto è dimostrare la costruzione di una pipeline di dati robusta e scalabile, gestendo l'intero ciclo di vita del dato. Partendo da dataset grezzi eterogenei del portale **Eurostat**, il progetto realizza:
1.  Un **processo ETL (Extract, Transform, Load)** automatizzato e riproducibile per pulire, modellare e arricchire i dati.
2.  La centralizzazione dei dati puliti in un **database MySQL cloud**.
3.  Lo sviluppo di un **dashboard di Business Intelligence** per analizzare e visualizzare indicatori socio-economici chiave (es. PIL, tassi di disoccupazione, spesa per consumi), consentendo un'esplorazione intuitiva dei trend a livello europeo.

---

### Architettura Tecnica e Flusso di Lavoro

Il progetto è strutturato in quattro fasi distinte, ognuna con tecnologie specifiche per garantire efficienza e best practice.

#### 1. Estrazione e Trasformazione (ETL) con Python

Il cuore della pipeline è gestito da script Python eseguiti in ambiente Jupyter.
* **Estrazione:** I dati grezzi vengono caricati in formato `.csv` da **Eurostat**.
* **Trasformazione con Pandas:** La libreria `Pandas` è utilizzata per operazioni complesse di data wrangling:
    -   **Pulizia:** Rimozione programmatica di colonne superflue e gestione di dati inconsistenti.
    -   **Modellazione:** Esecuzione di operazioni di **pivot** per trasformare i dati da un formato *long* a uno *wide*, più adatto alle analisi successive.
    -   **Arricchimento:** Creazione di ID numerici per le nazioni tramite mapping e standardizzazione dei nomi delle entità geopolitiche.
    -   **Output:** I dati trasformati vengono salvati in nuovi file `.csv` puliti, pronti per essere caricati nel database.

#### 2. Data Warehousing e Caricamento su Database MySQL Cloud

I dati puliti vengono centralizzati in un database relazionale per garantire integrità e accessibilità.
* **Database:** Il progetto utilizza un'istanza **MySQL ospitata in cloud**.
* **Creazione Schema:** La struttura delle tabelle nel database viene definita e creata programmaticamente tramite script Python che utilizzano la libreria `mysql.connector` per eseguire query `CREATE TABLE`.
* **Caricamento Dati (Load):** Il caricamento dei dati dai file `.csv` puliti è gestito in modo efficiente tramite **SQLAlchemy** e la funzione `DataFrame.to_sql()` di Pandas, come mostrato in `connessione_db_Europa.ipynb`. Questo approccio è ottimizzato per performance e robustezza.

#### 3. Modellazione Dati con SQL Views

Per separare la logica di business dal livello di visualizzazione, sono state create delle **SQL Views** direttamente nel database MySQL.
* **Logica di Business:** Le view contengono i **JOIN** necessari per collegare le diverse tabelle (es. unire dati sulla disoccupazione con dati demografici).
* **Efficienza e Manutenibilità:** Power BI si connette a queste view invece che alle tabelle sottostanti. Questo semplifica le query, migliora le performance e permette di modificare la logica di business a livello di database senza dover aggiornare il report.

#### 4. Business Intelligence e Visualizzazione con Power BI

Il front-end analitico del progetto è un dashboard interattivo.
* **Connessione Dati:** **Power BI Desktop** si connette in tempo reale al database MySQL, interrogando le SQL Views predefinite.
* **Interattività:** Il report finale consente agli utenti di filtrare, esplorare e analizzare i dati attraverso grafici e tabelle dinamiche.

---

### Insight Principali

Dall'analisi del dashboard sono emersi i seguenti punti chiave:

* **[INSIGHT 1: Descrivi qui la scoperta più importante. Esempio: "È stata identificata una forte correlazione negativa tra il tasso di disoccupazione giovanile e l'investimento pro-capite in educazione terziaria."]*
* **[INSIGHT 2: Descrivi qui una seconda scoperta interessante. Esempio: "I paesi con un PIL derivante in maggior parte dal settore dei servizi hanno mostrato una resilienza maggiore durante la crisi economica del 2020."]*
* **[INSIGHT 3: Descrivi qui un terzo insight o un pattern notato. Esempio: "Si osserva un trend di crescita demografica costante nei paesi nordici, a differenza della stagnazione registrata nell'Europa meridionale."]*

---

### 📂 Struttura del Repository

* `/Progetto_Europa.pbix`: Il file sorgente del report Power BI.
* `/data/`: Contiene i file `.csv` originali scaricati da Eurostat.
