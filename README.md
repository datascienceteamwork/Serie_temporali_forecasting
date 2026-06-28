# Analisi delle Serie Temporali: Impatto della Qualità dell'Aria sulla Salute

Questo progetto applica tecniche di analisi statistica e modellizzazione predittiva per studiare la relazione temporale tra i livelli di inquinamento atmosferico (PM2.5 e temperatura) e i ricoveri ospedalieri per patologie respiratorie nella regione **East**.

> ⚠️ Il dataset utilizzato è sintetico (generato artificialmente). Le conclusioni hanno valore metodologico e didattico e non sono generalizzabili a popolazioni reali.

---

## 🎯 Obiettivo

Sviluppare e confrontare modelli di previsione basati su serie temporali per stimare i ricoveri respiratori settimanali utilizzando variabili ambientali esogene (PM2.5 e temperatura), confrontando l’approccio univariato (**SARIMA**) con quello multivariato (**SARIMAX**).

---

## 📊 Dataset

Il progetto utilizza un dataset pubblico disponibile su Kaggle:

👉 https://www.kaggle.com/datasets/khushikyad001/air-quality-weather-and-respiratory-health

### Descrizione del dataset

Questo dataset simula uno scenario realistico di monitoraggio ambientale e sanitario pubblico. Combina indicatori di qualità dell’aria, condizioni meteorologiche, pattern di mobilità e utilizzo del sistema sanitario — in particolare visite ospedaliere ed emergenze legate a problemi respiratori — distribuiti su cinque regioni in un periodo di due anni (2020–2022).

Ogni riga rappresenta una regione in un giorno specifico, offrendo un contesto ricco per:

- forecasting di serie temporali
- analisi di correlazione
- studio di possibili relazioni causali

Il dataset è **interamente sintetico**, generato tramite distribuzioni statistiche realistiche e riferimenti a dati pubblici, con l’obiettivo di simulare comportamenti plausibili senza compromettere la privacy.

---

## 🛠️ Pipeline di Analisi

### 1. Pre-processing

- Filtraggio sulla regione **East** (635 osservazioni giornaliere)
- Conversione e ordinamento dell’indice temporale
- Resampling settimanale:
  - Media per variabili ambientali
  - Somma per i ricoveri
- Dataset finale: ~105 settimane

---

### 2. Analisi Esplorativa (EDA)

- Statistiche descrittive per anno e stagione
- Scatter plot con lag (0, 1, 2 settimane):
  - PM2.5 vs ricoveri
  - Temperatura vs ricoveri
- Correlazione incrociata (CCF) per identificare lag ottimali
- Decomposizione stagionale:
  - Trend
  - Stagionalità
  - Residuo
- Matrice di correlazione di Pearson con significatività statistica

---

### 3. Diagnostica Statistica

- Test **ADF (Augmented Dickey-Fuller)** su:
  - Serie originale
  - Differenziazione (d = 1)
  - Differenziazione stagionale (D = 1)
  - Combinazioni delle precedenti
- Analisi **ACF / PACF**
- Selezione automatica parametri tramite `auto_arima` (criterio AIC)

---

### 4. Modelli Confrontati

| Modello | Tipo | Descrizione |
|----------|------|-------------|
| **A** | SARIMA (auto_arima, D=0) | Modello ottimizzato automaticamente |
| **B** | SARIMA(2,1,0)×(1,1,0,52) | Modello con stagionalità forzata |
| **C** | SARIMAX | Con regressori esogeni (PM2.5 lag1, Temp lag1) |

---

### 5. Valutazione e Forecasting

- Split train/test (80% / 20%)
- Metriche:
  - MAE
  - RMSE
  - R²
- Diagnostica residui:
  - Ljung-Box
  - Jarque-Bera
  - Shapiro-Wilk
- Confronto finale modelli
- Forecast delle 4 settimane successive

---

## 💻 Tecnologie Utilizzate

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- SciPy
- Statsmodels
- pmdarima
- scikit-learn
- Jupyter Notebook

---

## 📂 Struttura del Repository

```text
.
├── serie_temporali_forecasting.ipynb    # Notebook principale
├── air_quality_health_dataset.csv       # Dataset sintetico (Kaggle source)
├── requirements.txt                     # Dipendenze del progetto
└── README.md
```

---

## 🚀 Installazione

Clonare il repository e installare le dipendenze:

```bash
git clone https://github.com/yassirsuarez/Serie_temporali.git
cd https://github.com/yassirsuarez/Serie_temporali.git
pip install -r requirements.txt
```

---

## ▶️ Esecuzione

### Google Colab
- Aprire il notebook
- Eseguire le celle in ordine
- La prima cella gestisce installazione librerie e upload dataset

### Locale
- Posizionare `air_quality_health_dataset.csv` nella stessa cartella del notebook
- Installare le dipendenze
- Eseguire il notebook sequenzialmente

---

## 📌 Note Finali

- Il dataset è **interamente sintetico**
- È stato progettato per simulare scenari realistici di salute pubblica e qualità dell’aria
- Il progetto ha valore metodologico nell’ambito delle serie temporali
- Non rappresenta alcuna conclusione epidemiologica reale