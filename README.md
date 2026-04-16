<table>
<tr>
<td><img src="logo_readme.svg" alt="StayInsight Logo" width="220"/></td>
<td><h1>StayInsight — Paris Accommodation Analysis</h1></td>
</tr>
</table>

**StayInsight** is a travel intelligence startup helping accommodation services make smarter strategic decisions in European cities.

This project is an exploratory data analysis conducted for StayInsight, focused on **Paris** as the first city in their European expansion. It explores accommodation pricing, guest satisfaction and geographic distribution of Airbnb listings in Paris, built as part of the IronHack Data Analytics Bootcamp.

---

## Team

This project was developed collaboratively as part of the IronHack Data Analytics Bootcamp.

- Desmond Ugboaja
- Gabriela Cascione
- Johannes Vidal

---

## Data Sources

### 1. Airbnb Paris — Weekdays
| Detail | Info |
|---|---|
| **Source** | [Kaggle — Airbnb Prices Analysis](https://www.kaggle.com/code/mariaplastinina/airbnb-prices-analysis/input) |
| **File** | `airbnb_paris_weekdays.csv` |
| **Records** | 3,130 rows |
| **Columns** | 20 |

### 2. Airbnb Paris — Weekends
| Detail | Info |
|---|---|
| **Source** | [Kaggle — Airbnb Prices Analysis](https://www.kaggle.com/code/mariaplastinina/airbnb-prices-analysis/input) |
| **File** | `airbnb_paris_weekends.csv` |
| **Records** | 3,558 rows |
| **Columns** | 20 |

### 3. Tourism & Hospitality Industry Analysis
| Detail | Info |
|---|---|
| **Source** | [Kaggle — Tourism & Hospitality Industry Analysis Dataset](https://www.kaggle.com/datasets/smithmurphy/tourism-and-hospitality-industry-analysis-dataset) |
| **File** | `Tourism_Hospitality_Industry_Analysis.csv` |
| **Records** | 500 rows |
| **Columns** | 23 |

### 4. Hotels Paris & Rome — API Data
| Detail | Info |
|---|---|
| **Source** | [Google Hotel Data Scraper — RapidAPI](https://rapidapi.com/search/google-hotel-data-scaper) |
| **File** | `api_hotels_paris_rome_base_clean.csv` |
| **Records** | 2,144 rows |
| **Columns** | 15 |
| **Extraction code** | `API_extraction.ipynb` |
| **Pipeline credit** | Data extracted and prepared by [Johannes Vidal](https://github.com/JohannesVidal/hotel_pricing_project) |

### 5. Geoapify — Points of Interest (POI) Data
| Detail | Info |
|---|---|
| **Source** | [Geoapify Places API](https://www.geoapify.com/places-api) |
| **Purpose** | Enriched dataset with touristic environment data around each accommodation |
| **Radius** | 500m around each listing |
| **Key variables** | `n_geoapify_heritage`, `geoapify_tourism_density_score` |
| **Extraction code** | `API_extraction.ipynb` |
| **Pipeline credit** | Data extracted and prepared by [Johannes Vidal](https://github.com/JohannesVidal/hotel_pricing_project) |

---

## API Key Management

This project uses two external APIs. To run the extraction notebook you will need your own API keys.

### Setup
Create a `.env` file in the root of the project:
```
RAPIDAPI_KEY=your_key_here
GOOGLE_HOTEL_RAPIDAPI_HOST=google-hotel-data-scaper.p.rapidapi.com
GEOAPIFY_API_KEY=your_key_here
```

> ⚠️ Never push your `.env` file to GitHub. It is already listed in `.gitignore`.

---

## Research Questions & Hypotheses

1. **Does the day of the week affect cleanliness ratings and overall guest satisfaction on Airbnb?**
   - *Hypothesis:* Airbnb listings will have lower cleanliness ratings and guest satisfaction scores on weekends compared to weekdays, due to higher turnover and less time for cleaning between stays.
   - *Conclusion:* Hypothesis refuted — weekends actually show slightly higher satisfaction (92.20 vs 91.85), cleanliness (9.27 vs 9.25) and prices (€199 vs €193)

2. **Does being a superhost on Airbnb have a significant impact on guest satisfaction and pricing?**
   - *Hypothesis:* Superhost listings will show higher guest satisfaction scores and cleanliness ratings than non-superhost listings, and will command higher prices per night.
   - *Conclusion:* Hypothesis supported — superhosts have higher satisfaction (97 vs 91), cleanliness (9.78 vs 9.18) and median price (€170 vs €156)

3. **Are hotel and Airbnb listings in Paris concentrated in specific neighbourhoods, and how does location influence pricing and guest satisfaction?**
   - *Hypothesis:* Listings in areas with higher tourism intensity — particularly those rich in heritage and major attractions — tend to command higher prices, but do not necessarily achieve higher guest satisfaction.
   - *Conclusion:* Hypothesis supported — tourism density shows a moderate positive relationship with price, but a weak and nearly negligible relationship with satisfaction

---

## Data Cleaning

### `airbnb_weekday_cleaning.ipynb` & `airbnb_weekend_cleaning.ipynb`
- Null values handled per column with justified strategy
- Duplicates checked and removed
- String columns stripped and standardised
- `type_of_day` column added to identify weekday/weekend
- Both datasets merged into `airbnb_paris_combined_cleaned.pkl`

### `API_cleaning_Q3_notebook.ipynb` — Hotel & POI Data
- Dropped irrelevant columns (`chain_code`, `iata_code`, `postal_code`, `is_sponsored`, `master_chain_code`, `dupe_id`, `hotel_id`, `country_code`, `last_update`)
- Dropped all rows where `search_city == 'Rome'`
- Dropped hotels beyond 50km from Paris city centre using Geopy distance calculation
- Standardised all string columns (stripped whitespace, title case)
- Cleaned `address_lines` of list formatting characters
- Saved to `api_hotels_paris_clean.pkl`

### `hotel_dataset_cleaning.ipynb` — Tourism & Hospitality Dataset
- Columns lowercased and renamed to snake_case
- Text columns stripped and standardised
- `month_name` column derived from month number
- Filtered to Paris-only version and full dataset version

---

## Methodology

### Analysis Approach
- **RQ1** — Combined weekday and weekend Airbnb datasets, added `type_of_day` label, compared cleanliness, satisfaction and price distributions using bar charts and average tables
- **RQ2** — Compared superhost vs non-superhost listings on satisfaction, cleanliness and price using percentage-normalised bar charts and median/average tables
- **RQ3** — Enriched Airbnb data with Geoapify POI data, analysed relationship between `geoapify_tourism_density_score` and pricing/satisfaction using scatter plots with regression lines

---

## Main Findings & Insights

- Weekends show marginally higher satisfaction, cleanliness and prices than weekdays — the difference is small but consistent
- Superhosts significantly outperform non-superhosts on satisfaction and cleanliness, with a higher median price
- Tourism density has a moderate positive effect on price but almost no effect on guest satisfaction
- Cleanliness is the strongest driver of guest satisfaction — internal quality matters more than location
- **Quality drives experience, while location drives price**

---

## Further Questions & Next Steps

- Extend analysis to other European cities to validate Paris findings
- Incorporate seasonal data to understand how demand peaks affect pricing and quality
- Investigate whether response rate and number of reviews influence satisfaction independently of superhost status

---

## Tools Used

- **Python** (Pandas, Matplotlib, Seaborn, Geopy, Folium)
- **Jupyter Notebook**
- **RapidAPI** — Google Hotel Data Scraper (hotel data extraction)
- **Geoapify** — Places API (points of interest enrichment)

---

## Repository Structure

```
StayInsight/
│
├── 01. Data/
│   ├── 01. Raw Data/
│   │   ├── airbnb_paris_weekdays.csv
│   │   ├── airbnb_paris_weekends.csv
│   │   ├── api_hotels_paris_rome_base_clean.csv
│   │   └── Tourism_Hospitality_Industry_Analysis.csv
│   └── 02. Clean Data/
│       ├── airbnb_paris_combined_cleaned.pkl
│       ├── airbnb_paris_geoapify_enriched.csv
│       ├── airbnb_paris_weekdays_cleaned.csv
│       ├── airbnb_paris_weekdays_cleaned.pkl
│       ├── airbnb_paris_weekend_cleaned.csv
│       ├── airbnb_paris_weekend_cleaned.pkl
│       ├── api_hotels_paris_clean.csv
│       ├── api_hotels_paris_cleaned.pkl
│       ├── hotels_api_poi_ranking.csv
│       ├── paris_pois_manual.csv
│       ├── paris_tourism_hospitality_cleaned.csv
│       └── tourism_hospitality_cleaned.csv
│
├── 02. Notebooks/
│   ├── airbnb_weekday_cleaning.ipynb
│   ├── airbnb_weekend_cleaning.ipynb
│   ├── hotel_dataset_cleaning.ipynb
│   ├── API_extraction.ipynb
│   ├── API_cleaning_Q3_notebook.ipynb
│   ├── Q1_notebook.ipynb
│   └── Q2_notebook.ipynb
│
├── 03. Visualizations/
│   ├── cleanliness_host_distribution.png
│   ├── cleanliness_rating_comparison.png
│   ├── guest_satisfaction_comparison.png
│   ├── guest_satisfaction_host_distribution.png
│   ├── guests_satisfaction_bar_chart_correlations.png
│   ├── map_paris_screencapture.jpg
│   ├── paris_map.html
│   ├── price_bucket_host_distribution.png
│   ├── price_distribution_comparison.png
│   ├── satisfaction_vs_tourism_density.png
│   └── tourism_density_vs_prices.png
│
├── .gitignore
├── logo_readme.svg
├── stayinsight_presentation.pdf
└── README.md
```

---

## How to Run

1. Clone the repository:
   ```bash
   git clone https://github.com/craftedbygaby/StayInsight.git
   cd StayInsight
   jupyter notebook
   ```

2. Install dependencies:
   ```bash
   pip install pandas numpy matplotlib seaborn requests geopy folium
   ```

---

## Links

- 📋 [Kanban Board](https://trello.com/c/IsQ0NH1s/11-build-github-repo)
- 📊 [Final Presentation](https://github.com/craftedbygaby/StayInsight/blob/main/stayinsight_presentation.pdf)

---

## Limitations

- API rate limits apply on the free tier of RapidAPI — data completeness depends on quota availability
- Geoapify API is limited to max 20 POIs per request — tourism density variables should be interpreted as proxies for tourism intensity, not exact counts. This may affect reproducibility if rerunning the notebook
- Airbnb data is static (scraped at a point in time) and may not reflect current listings
- Analysis is scoped to Paris only — findings may not generalise to other cities
- Tourism & Hospitality dataset is synthetic/aggregated and used for macro context only
- Pricing is influenced by many factors not captured in the dataset (property type, amenities, host behaviour)

---

*All analysis is for educational and portfolio purposes only.*
