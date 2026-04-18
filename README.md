# 🏠 Morocco Apartment Price Predictor

A machine learning project that predicts apartment listing prices across 5 major 
Moroccan cities using real data scraped from Avito.ma.

## 📊 Results

|       Model       |  R² Score  |  Mean Error |
|-------------------|------------|-------------|
| RF + XGB Stack    | **0.8626** | 206,333 MAD |
| Random Forest     | 0.8598     | 208,634 MAD |
| XGBoost           | 0.8581     | 210,355 MAD |
| Linear Regression | 0.8088     | 236,354 MAD |

**The best model prices 2 out of 3 apartments within 20% of asking price,
with a median error of 12.6%.**

## 🗺️ Cities Covered
Agadir · Casablanca · Rabat · Marrakech · Tanger

## 📁 Dataset
- **Source:** Scraped from [Avito.ma](https://www.avito.ma) using CloudScraper + BeautifulSoup
- **Raw listings collected:** 16,409
- **After cleaning & filtering:** 8,693 listings
- **Features extracted:** Price, Size, Bedrooms, Bathrooms, Floor, Neighborhood, 
  Listing age, Distance to coast

## ⚙️ Features Used in Modeling

|         Feature                 |               Description                  |
|---------------------------------|--------------------------------------------|
| `Size_m2`                       | Apartment surface area                     |
| `Bedrooms / Bathrooms`          | Room count                                 |
| `Floor`                         | Floor number (0 = ground floor)            |
| `Distance_to_Coast_km`          | Distance to nearest coastline              |
| `Room_Density`                  | Bedrooms per 100m² — captures spaciousness |
| `Is_Ground_Floor/Is_High_Floor` | Floor position flags                       |
| `City_Median_Price`             | Baseline price level of the city           |
| `Neigh_Median_LogPrice`         | Neighborhood price level (target encoded)  |
| `Neigh_Median_PricePerM2`       | Neighborhood price density                 |
| `Listing_Status`                | Fresh / Standard / Stale listing age       |

## 🧠 Modeling Approach

1. **Log-transform the target** — real estate prices are skewed, log-transform 
   makes the distribution normal and improves model accuracy significantly
2. **Target encoding for neighborhoods** — 300+ neighborhoods encoded using 
   their median price, computed only on training data to prevent leakage
3. **Stacked ensemble** — Random Forest + XGBoost predictions averaged together, 
   consistently outperforming either model alone

## 📈 Precision Breakdown
Within 10% of asking price : 41.7% of listings
Within 15% of asking price : 56.1% of listings
Within 20% of asking price : 67.3% of listings
Within 30% of asking price : 85.3% of listings

## 🛠️ Tech Stack
Python · Pandas · NumPy · Scikit-learn · XGBoost
CloudScraper · BeautifulSoup · GeoPy · Matplotlib · Seaborn

## ▶️ How to Run

```bash
pip install cloudscraper beautifulsoup4 pandas seaborn matplotlib geopy scikit-learn xgboost tqdm
```

1. Open `notebook.ipynb` in Google Colab or Jupyter
2. The geocode cache (`geocode_cache.csv`) is included — no need to wait for geocoding
3. You will need to run the scraper cell yourself to get fresh data, or 
   contact me for the dataset

## ⚠️ Limitations

- The model predicts **Avito listing prices**, not final sale prices. 
  Negotiation margins and apartment condition are not captured in the data.
- Luxury apartments (>2.5M MAD) have less training data and slightly 
  higher error rates.

## 👤 Author

**[ABID YASSINR]** — First-year Data Engineering student at ENSA
[LinkedIn](https://www.linkedin.com/in/abid-yassine-jsn/) · [GitHub](https://github.com/JSN-Y)
