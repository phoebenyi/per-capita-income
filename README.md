# 🌍 Per Capita GNI Consolidation (SG, TW, KR, JP)

This project consolidates **GNI per capita** data (in **current USD**) for **Singapore**, **Taiwan**, **South Korea**, and **Japan**, merging official Taiwan government statistics (DGBAS) with live World Bank data using the `wbdata` API.

---

## 📦 Key Features

- ✅ Extracts and cleans Taiwan’s **GNI per capita (USD)** from raw **DGBAS** Excel files
- ✅ Automatically fetches **GNI per capita (USD)** for SG, JP, and KR from **World Bank**
- ✅ Standardizes and merges all data into consistent long + wide formats
- ✅ Outputs:
  - `per_capita_income_long.xlsx` (tidy, long format)
  - `per_capita_income_comparison.xlsx` (wide format for visual checks)
- ✅ Optional visualizations included (trend plots, histograms)
- ✅ Float-safe matching sanity check between wide vs long outputs

---

## 📚 Data Sources

| Source         | Countries           | Metric                         |
|----------------|---------------------|--------------------------------|
| 🇹🇼 DGBAS       | Taiwan only          | GNI per capita (current USD)   |
| 🌍 World Bank   | SG, JP, KR          | GNI per capita (current USD) – [`NY.GNP.PCAP.CD`](https://data.worldbank.org/indicator/NY.GNP.PCAP.CD)

---

## 🚀 Setup Instructions

### 1. Environment Setup

```bash
python -m venv venv
venv\Scripts\activate   # or source venv/bin/activate on macOS/Linux
pip install -r requirements.txt
```

### 2. Required Files

1. Manually download the **DGBAS Excel file** from:  
   👉 https://eng.stat.gov.tw  
   Look for *"Gross National Income per Capita (USD)"*, usually under *National Accounts*.

2. Save the file as:

```
dgbas.xlsx
```

3. Place `dgbas.xlsx` in the root directory of this project.

---

## ▶️ Running the Notebook

Open and run all cells in `per_capita_income_1950_onward.ipynb`.

What it does:

- ✅ Extracts the correct **Per Capita GNI (USD)** column from Taiwan’s DGBAS sheet (column 11)
- ✅ Fetches live data from World Bank for SG, JP, and KR
- ✅ Standardizes and deduplicates all years
- ✅ Outputs clean Excel files:
  - `per_capita_income_long.xlsx`
  - `per_capita_income_comparison.xlsx`
- ✅ Confirms wide ≡ long values (within float tolerance)

---

## 💡 Data Consistency FAQ

### 💱 Are all values comparable?

Yes — all values are **GNI per capita in current USD**:

| Source     | Type                              | Adjustment     |
|------------|-----------------------------------|----------------|
| DGBAS      | GNI per capita (USD) – Nominal    | ❌ Not adjusted |
| World Bank | GNI per capita (USD) – Nominal    | ❌ Not adjusted |

This makes them directly comparable without conversion.

---

## ✅ Internal Consistency Check

The notebook auto-checks that:

> **Pivoted wide-format data matches the original long-format data**  
> with tolerance ±1.5 USD

Any mismatch rows are printed for debugging.

---

## 🔍 Want Different Formats?

To use **PPP** or **constant USD**, change the indicator in `fetch_from_wb()`:

| Indicator Code        | Meaning                    |
|------------------------|----------------------------|
| `NY.GNP.PCAP.CD`       | **Nominal** GNI per capita (USD) ✅ default
| `NY.GNP.PCAP.KD`       | Constant USD (adjusted for inflation)
| `NY.GNP.PCAP.PP.CD`    | PPP-adjusted GNI per capita

---

## 📊 Optional Charts

The notebook also generates:

- 📈 Trend plot: GNI per capita over time
- 📊 Distribution histogram by country

---

## 🛠️ Tech Stack

- Python 3.11+
- Jupyter Notebook
- `pandas`, `openpyxl`, `wbdata`, `matplotlib`

---

## 🧠 Notes for Developers

- The deduplication step uses `drop_duplicates(subset=["Country", "Year"])` to ensure pivoting doesn't explode.
- Use `pivot_table(..., aggfunc="mean")` for resilience against duplicates.
- A merged long–wide format is used for robust validation.

---

## 📬 License

MIT — feel free to fork, adapt, or share.