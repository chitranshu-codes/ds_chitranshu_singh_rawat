# Trader Behavior vs. Market Sentiment Analysis

## 1. Overview

This project performs an **Exploratory Data Analysis (EDA)** to understand the relationship between **high-frequency trader behavior (from Hyperliquid)** and **daily Bitcoin market sentiment (from the Fear & Greed Index)**.

The goal is to identify how trading behavior—specifically **volume, profitability (PnL), and capital flow**—aligns or diverges with overall market sentiment. The analysis uncovers key trends and **“hidden signals”** that can inform more sophisticated trading strategies.

---

## 2. Datasets Used

### **1. historical_data.csv**

Contains high-frequency, individual trade data.

**Key Columns:**

* Account
* Coin
* Execution Price
* Size USD
* Side
* Timestamp IST
* Closed PnL
* Trade ID

### **2. fear_greed_index.csv**

Contains daily market sentiment for Bitcoin.

**Key Columns:**

* value
* classification
* date

---

## 3. Setup & Installation

This analysis is designed to run in a **Python environment**, such as a **Jupyter Notebook** or **Google Colab**.

### **Requirements**

You will need the following Python libraries:

* `pandas`: For data manipulation and analysis.
* `altair`: For data visualization.

### **Installation**

If you don't have these libraries installed, you can install them via pip:

```bash
pip install pandas altair
```

### **Setup**

1. Place the two data files (`historical_data.csv` and `fear_greed_index.csv`) in the same directory as your Python script or notebook.
2. If using Google Colab, upload these files to the session storage.

---

## 4. Analysis Workflow

The Python script (notebook) performs the following steps:

### **1. Load Data**

Reads both `.csv` files into pandas DataFrames.

### **2. Data Cleaning & Merging**

* Converts string-based timestamps (`Timestamp IST` and `date`) into proper datetime objects.
* Creates a common `date_key` on both DataFrames to serve as a bridge.
* Performs a **left merge** to attach the daily sentiment score to every individual trade row.
* Drops any rows that do not have corresponding sentiment data.

### **3. Feature Engineering**

* Creates a `net_flow_usd` column (positive for **BUY**, negative for **SELL**) to quantify the direction of capital flow for each trade.

### **4. Data Aggregation**

* Groups the millions of individual trades by `date_key`, `value`, and `classification`.
* Calculates daily aggregate metrics:

  * `total_volume_usd`
  * `net_pnl`
  * `trade_count`
  * `net_flow_usd`
* Exports this final aggregated data to `daily_trade_analysis.csv`.

### **5. Visualization**

Generates four key visualizations using **Altair** to analyze the aggregated data and identify trends.

---

## 5. Key Analytical Notes & Findings

Below is a summary of the insights derived from the four analysis charts.

---

### **Note 1: Volume vs. Sentiment (The “Capitulation” Signal)**

**Finding:**
A critical divergence exists. Peak market activity (highest volume) occurs during **“Extreme Fear.”**
The lowest volume occurs during **“Greed.”**

**Insight:**
This refutes the idea that *“greed drives the market.”*

* **“Extreme Fear”** → high-volume capitulation (panic-selling).
* **“Greed”** → low-volume complacency, signaling a structurally weak rally vulnerable to reversal.

---

### **Note 2: Profitability (PnL) vs. Sentiment (The “Hybrid” Strategy)**

**Finding:**
Profitability is maximized at emotional extremes—but not how one might expect.

**Profitability Ranking (High → Low):**
Fear > Extreme Greed > Greed > Neutral > Extreme Fear

**Insight:**

* The *“sweet spot”* for profit is the **Fear** zone—high volatility ideal for contrarians.
* **Extreme Greed** is the second-most profitable, validating **momentum-based trend-following**.
* **Extreme Fear** is least profitable, contradicting *“buy the blood”* and signaling a **falling knife trap**.

---

### **Note 3: Net Flow vs. Sentiment (The “Smart Money” Footprint)**

**Finding:**
Net capital flow shows a sophisticated, non-herd-like strategy.

**Net-Positive (Buying):** Fear > Greed
**Net-Negative (Selling):** Extreme Greed > Extreme Fear > Neutral (most negative)

**Insight:**

* **Accumulation:** Peak buying during *Fear* (contrarian dip-buying), with secondary buying in *Greed* (trend-following).
* **Distribution:** Net selling during *Extreme Greed* (classic “sell to the herd”).
* **Anomaly:** Largest outflows during *Neutral* phases → suggests **proactive de-risking** during indecision.

---

### **Note 4: Time-Series Divergence (The “Hidden Signal”)**

**Finding:**
Market turning points are clearly signaled by a **decoupling** of market sentiment (psychology) from net capital flow (action).

**Insight:**

* **Bearish Divergence (Top Signal):** Sentiment high/rising, but net buying weakens → **top formation**.
* **Bullish Divergence (Bottom Signal):** Sentiment low/panic, but net selling eases → **bottom formation**.

---

✅ **Outcome:**
These behavioral-sentiment correlations provide actionable insights for developing **hybrid quantitative trading strategies** that blend contrarian and momentum principles.

---

Would you like me to format it for direct inclusion in a **GitHub README.md** (with headers, emojis, and section dividers styled for better visual appeal)?
