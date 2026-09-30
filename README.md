# Zomato Data Cleaning & EDA
# What Drives a Restaurant's Rating? 
Cleaning, preprocessing and exploratory analysis of **9,551 Zomato restaurants across 15 countries**, from a messy raw file to statistically tested findings.

### [**View the live report →**](https://khushivie.github.io/Zomato-Restaurant-EDA/) https://khushivie.github.io/Zomato-Restaurant-EDA/
📓 [Notebook](Zomato_Cleaning_EDA.ipynb) · 🧹 [Cleaned dataset](Zomato_cleaned.csv) · 📊 [All charts](charts/)

<img width="2189" height="626" alt="04_price_vs_rating" src="https://github.com/user-attachments/assets/c41073f4-1dae-46c1-ba52-d9e5e3b7e124" />


## 🎯 Key findings

- **Rating follows popularity and price.** Rating rises with votes (Spearman ρ = 0.68) and with price tier (3.24 budget → 3.89 fine dining).
- **Table booking is a proxy for price.** In India, restaurants with table booking rate +0.24 higher overall, but *lower* inside the Upscale and Fine-dining tiers.
- **Data quality changed the story.** 2,148 restaurants (22.5%) had a hidden rating of `0` meaning "not rated". Treating them as missing lifts the mean rating from **2.67 to 3.44**.
- **The sample is very uneven.** India is 91% of the rows and Delhi NCR alone 83%, so country and city rankings compare samples, not whole markets.

<img width="2188" height="628" alt="05_services" src="https://github.com/user-attachments/assets/855315cc-d50f-43fd-af18-94d7d1efa083" />


## 🧹 Data cleaning

No rows were deleted: impossible values became missing, and every step is logged in the notebook.

| Issue | Found | Fix |
|---|---|---|
| Encoding damage (`�`) in names, cities, addresses | 428 cells | 84% restored (Café, São Paulo, İstanbul), rest stripped |
| "Not rated" stored as rating 0 | 2,148 rows | Set to blank + `is_rated` flag |
| Costs in 12 currencies | every row | Country-based currency + approximate USD columns |
| Wrong currency label (Philippines = "Botswana Pula") | 22 rows | Corrected |
| Average cost = 0 | 18 rows | Set to blank |
| Coordinates = 0 or outside the country | 500 rows | Set to blank + `coords_valid` flag |
| Missing cuisines | 9 rows | Filled with "Unknown" |
| Constant / redundant columns | 3 columns | Dropped (no duplicate restaurants found) |

The table grew from 9,551 × 21 to 9,551 × 29, adding country, currency code, USD cost, price tier, number of cuisines and other features.

## 🔍 Analysis

- 12 visualisations: geography, ratings, votes, price, services, cuisines, cities, countries, chains and correlations
- Non-parametric tests, because ratings are not normally distributed: **Spearman** correlation, **Kruskal-Wallis** and **Mann-Whitney U**
- Comparisons made within price tiers, to avoid confusing price with other effects
- Service comparisons limited to India, since online delivery is recorded only for India and the UAE

## 🛠️ Tech stack

Python · pandas · NumPy · Matplotlib · seaborn · SciPy · Jupyter

## 📁 Repository structure

```
Zomato-Restaurant-EDA/
├── index.html                    # live report (GitHub Pages)
├── Zomato_Cleaning_EDA.ipynb     # full cleaning + EDA notebook
├── Zomato_Restaurant_Dataset.csv # raw data
├── Zomato_cleaned.csv            # cleaned data
├── charts/                       # all 12 charts (PNG)
├── requirements.txt
└── README.md
```

## ▶️ Run it yourself

```bash
git clone https://github.com/khushivie/Zomato-Restaurant-EDA.git
cd Zomato-Restaurant-EDA
pip install -r requirements.txt
jupyter notebook Zomato_Cleaning_EDA.ipynb
```

Keep the raw CSV in the same folder as the notebook; it regenerates the cleaned file and the charts.

## ⚠️ Caveats

- USD costs use fixed, approximate 2018 exchange rates: good for rough comparison, not exact prices.
- About 70 damaged text cells could not be restored, so their garbage characters were removed.
- The sample is not random. Findings are associations, not causes.

## 📌 Data source

Public Zomato restaurants dataset (widely shared on Kaggle). All rights belong to the original data owners.

## 👤 Author

**Khushi Prajapati** · [GitHub](https://github.com/khushivie)
