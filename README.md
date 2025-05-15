# 🌍 Per Capita Income Consolidation (SG, TW, KR, JP)

This project consolidates historical **GNI per capita** data for **Singapore**, **Taiwan**, **South Korea**, and **Japan**. It combines official Taiwan government statistics (DGBAS) and World Bank data via the `wbdata` Python API.

---

## 📦 Features

- ✅ Cleans raw **GNI per capita** data from Taiwan's **DGBAS**
- ✅ Fetches **GNI per capita** (current USD) for SG, JP, KR via **World Bank**
- ✅ Merges data into a standardized format
- ✅ Outputs: `per_capita_income_consolidated.xlsx`
- ✅ Optional data visualizations in notebook

---

## 📚 Data Sources

- 🇹🇼 Taiwan GNI: [DGBAS](https://eng.stat.gov.tw/)
- 🌍 GNI per capita: [World Bank](https://data.worldbank.org/indicator/NY.GNP.PCAP.CD)

---

## 🚀 Setup Instructions

### 1. Create Virtual Environment

```bash
python -m venv venv
venv\Scripts\activate
```

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```
---

## ↻ HOW IT WORKS (EXPLANATION FOR USERS)

1. **Manually download Taiwan’s GNI per capita data** from the official DGBAS website:
   - https://eng.stat.gov.tw
   - Look for *Gross National Income per Capita (USD)*, typically under *National Accounts*.

2. **Save it as**:
   ```
   dgbas.xlsx
   ```

3. **Replace the old `dgbas.xlsx` file** in the project folder.

4. **Run all cells in the Jupyter notebook**:
   - It will clean and extract Taiwan’s per capita GNI from `dgbas.xlsx`
   - Then it auto-fetches Singapore, Japan, and Korea **GNI per capita** from World Bank (via `wbdata`)
   - All data is merged and exported to:
     ```
     per_capita_income_consolidated.xlsx
     ```

---

## ❓ Common Questions

### ♻️ Does the World Bank data always update?

**Yes.**  
When using `wbdata`, the World Bank data is fetched **live at runtime**, so it's always the most up-to-date public data available. No need to redownload anything manually for SG, JP, or KR.

---

### 💰 Are all the GNI values in the same format?

| Source    | Value Type                            | Notes                                                                 |
|-----------|----------------------------------------|-----------------------------------------------------------------------|
| **DGBAS** | GNI per capita (USD) – **Nominal**     | This is **not adjusted** for inflation or PPP. It’s raw USD amounts. |
| **World Bank** (`NY.GNP.PCAP.CD`) | GNI per capita (USD, **current prices**) | This is also **nominal**, in **current USD**, and consistent format. |

Conclusion:
- ✅ **Yes — both DGBAS and World Bank data are in comparable nominal USD terms**
- ❌ They are **not Atlas method** or **PPP-adjusted** — this ensures consistency
- If you want constant prices or PPP, you could later use:
  - `NY.GNP.PCAP.KD` for **constant USD**
  - `NY.GNP.PCAP.PP.CD` for **PPP-adjusted**

---

## 🛠️ Tech Stack

- Python 3.11
- pandas, wbdata, matplotlib, jupyter, openpyxl

---

## 📬 License

MIT — feel free to use, fork, or adapt.
