# 🛍️ E-Commerce Multi-File Data Cleaning & Consolidation

This project simulates a real client workflow where multiple messy CSV files must be cleaned, validated, merged, and exported into a final usable dataset.

---

## 📁 Files Included

| Folder | Contents |
|--------|----------|
| `data_raw/` | Original unclean files (customers, orders, products, payments) |
| `data_clean/` | Cleaned individual datasets + final master file |
| `notebook/` | Jupyter notebook showing step-by-step process |
| `docs/` | Before vs after summary (optional) |
| `visuals/` | Screenshots of changes (optional) |

---

## 🧹 Key Cleaning Actions

- Fixed inconsistent formatting across CSVs
- Handled missing customer IDs, prices, payment amounts
- Standardized date formats across files
- Removed duplicates across all datasets
- Filled missing product values using grouped median logic
- Cleaned invalid quantities and rows unusable for merging

---

## 🧠 Feature Engineering

Added new valuable fields for analytics:

| Feature | Meaning |
|---------|---------|
| `expected_amount` | quantity × price |
| `payment_difference` | difference between expected and paid |
| `order_month` / `order_year` | for seasonal analysis |
| `payment_issue` | flag if mismatch or missing |

---

## 🔁 Final Output

The final consolidated dataset is stored as:

data_clean/master_dataset.csv

It is clean, analysis-ready, and suitable for:

- Reporting
- BI dashboards
- Trend analysis
- Customer segmentation

---

## 📌 Tech Stack Used

- Python
- Pandas
- Jupyter Notebook

---

## 🚀 Why This Project Matters

This project demonstrates real-world data preparation — not just `.dropna()`.

It showcases:

✔ Logical decision-making  
✔ Business-based cleaning rules  
✔ Multi-file consolidation  
✔ Documentation for transparency  
