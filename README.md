# DSC8201_Final_B35099_S25M19_022
Final Exams DATA MINING, MODELLING AND ANALYTICS

# DSC8307 – Data Mining, Modelling and Analytics: Olist Brazilian E-commerce

**Access No.:** B35099  
**Reg No.:** S25M19/022  
**Programme:** MSc Data Science and Analytics, Uganda Christian University (Advent 2026 project-based examination)

One Jupyter notebook (`notebook.ipynb`) covers the five tasks: (1) exploration and preparation, (2) categories bought together,
(3) seller segmentation, (4) unusual orders, (5) late-delivery classification and delivery-time regression.

## Repository structure
```
.
├── notebook.ipynb            # complete analysis, runs top to bottom (committed with outputs)
├── requirements.txt          # pinned dependencies (tested on Python 3.12)
├── README.md
└── data/
    ├── raw/                  # original Olist CSVs from Kaggle (olistbr/brazilian-ecommerce), unmodified
    └── processed/            # merged / derived datasets produced by the notebook (gzip-compressed CSV)
```

## Datasets
**Original (`data/raw/`)** – 9 files: orders, order_items, order_payments, order_reviews, customers, sellers, products, geolocation,
product_category_name_translation. Source: https://www.kaggle.com/datasets/olistbr/brazilianecommerce (CC BY-NC-SA 4.0, Olist).

**Merged / derived (`data/processed/`)**

| File | Grain | Content |
|---|---|---|
| `olist_item_level_merged.csv.gz` | order item | All 9 source tables joined (orders, customers, products with English category, sellers, payments, reviews, coordinates, delivery metrics) |
| `olist_order_level_master.csv.gz` | order | Order-level master table with aggregates, distances and derived delivery metrics (all orders) |
| `olist_delivery_model_dataset.csv.gz` | delivered order | Cleaned modelling population and features for Task 5 (incl. leakage-safe seller history) |
| `olist_seller_features_segments.csv.gz` | seller | Seller sales/service features and segment label (Task 3) |
| `olist_order_anomaly_scores.csv.gz` | order | Anomaly scores from three detectors, rule flags and review flag (Task 4) |
| `olist_category_pairs.csv.gz` | category pair | Pair counts, support, lift and confidence (Task 2) |

## How to run
```bash
python -m venv .venv && source .venv/bin/activate      # Windows: .venv\Scripts\activate
pip install -r requirements.txt
jupyter nbconvert --to notebook --execute notebook.ipynb   # or Kernel -> Restart & Run All (about 5-10 min)
```
The notebook reads `data/raw/` and rewrites `data/processed/`. Random seed: 42.

## Note on file sizes
`data/raw/olist_geolocation_dataset.csv` (about 61 MB) triggers GitHub's >50 MB warning but is under the 100 MB hard limit.
