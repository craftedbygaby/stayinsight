<table>
<tr>
<td><img src="logo_readme.svg" alt="StayInsight Logo" width="220"/></td>
<td><h1>StayInsight — Paris Accommodation Analysis</h1></td>
</tr>
</table>

**StayInsight** is a travel intelligence startup helping accommodation services make smarter strategic decisions in European cities.

This project is an exploratory data analysis conducted for StayInsight, focused on **Paris** as the first city in their European expansion. A collaborative data analysis project exploring accommodation pricing, guest satisfaction and geographic distribution of Airbnb listings in Paris. Built as part of the IronHack Data Analytics Bootcamp.

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
| **Extraction code** | `API_handling.ipynb` |
| **Pipeline credit** | Data extracted and prepared by [Johannes Vidal](https://github.com/JohannesVidal/hotel_pricing_project) |

### 5. Geoapify — Points of Interest (POI) Data
| Detail | Info |
|---|---|
| **Source** | [Geoapify Places API](https://www.geoapify.com/places-api) |
| **Purpose** | Enriched dataset with touristic environment data around each accommodation |
| **Radius** | 500m around each listing |
| **Key variables** | `n_geoapify_heritage`, `geoapify_tourism_density_score` |
| **Extraction code** | `API_handling.ipynb` |
| **Pipeline credit** | Data extracted and prepared by [Johannes Vidal](https://github.com/JohannesVidal/hotel_pricing_project) |

The Geoapify API was used to move beyond simple coordinates to a more meaningful concept: how touristic a location actually is. Key derived variables:
- **`n_geoapify_heritage`** — number of historical/heritage sites within 500m. Strongest relationship with price, capturing culturally significant areas
- **`geoapify_tourism_density_score`** — weighted score combining attractions, sights and heritage, giving more weight to active tourist demand. Built as a single interpretable metric for overall tourism intensity of a location

---

## API Key Management

This project uses two external APIs. To run the extraction notebook you will need your own API keys.

### Google Hotel Data Scraper — RapidAPI
1. Sign up at [rapidapi.com](https://rapidapi.com) and subscribe to the Google Hotel Data Scraper (free tier available)
2. Copy your `x-rapidapi-key`

### Geoapify Places API
1. Sign up at [geoapify.com](https://www.geoapify.com)
2. Generate an API key from your dashboard (free tier available)

### Setup
Create a `.env` file in the root of the project:
   ```
   RAPIDAPI_KEY=your_key_here
   GOOGLE_HOTEL_RAPIDAPI_HOST=google-hotel-data-scaper.p.rapidapi.com
   GEOAPIFY_API_KEY=your_key_here
   ```

> ⚠️ Never push your `.env` file to GitHub. It is already listed in `.gitignore`.

---

---

## Data Cleaning

### `API_cleaning.ipynb` — Hotel Data (API)

#### Dropped Columns
- **First pass**: `chain_code`, `iata_code`, `postal_code`, `is_sponsored`, `master_chain_code` — not relevant for analysis
- **Second pass**: `dupe_id`, `hotel_id`, `country_code`, `last_update` — redundant after deduplication check

#### Rows Removed
- Dropped all rows where `search_city == 'Rome'` — analysis scoped to Paris only
- Dropped hotels further than **50km from Paris city centre** using `geopy` distance calculation based on latitude/longitude coordinates

#### Standardised Columns
- **`city_name`**: stripped whitespace and converted to title case — standardises `PARIS`, `Paris` etc.
- **All string columns**: stripped whitespace and title-cased using `select_dtypes(include='str')`
- **`address_lines`**: removed list formatting characters (`[`, `]`, `'`) for readability

#### Output
- Saved to `data/02_cleaned_data/api_hotels_paris_clean.pkl`

---

## Research Questions & Hypotheses

1. **Does the day of the week affect cleanliness ratings and overall guest satisfaction on Airbnb?**
   - *Hypothesis:* Airbnb listings will have lower cleanliness ratings and guest satisfaction scores on weekends compared to weekdays, due to higher turnover and less time for cleaning between stays.
   - *Conclusion:* PLACEHOLDER

2. **Does being a superhost on Airbnb have a significant impact on guest satisfaction and pricing?**
   - *Hypothesis:* Superhost listings will show higher guest satisfaction scores and cleanliness ratings than non-superhost listings, and will command higher prices per night.
   - *Conclusion:* PLACEHOLDER

3. **Are hotel and Airbnb listings in Paris concentrated in specific neighbourhoods, and how does location influence pricing and guest satisfaction?**
   - *Hypothesis:* Listings located in areas with higher tourism intensity — particularly those rich in heritage and major attractions — tend to command higher prices, but do not necessarily achieve higher guest satisfaction.
   - *Conclusion:* PLACEHOLDER

---

## Methodology

### Data Sources & Merging
- PLACEHOLDER — describe how the two datasets were combined and on what key column

### Analysis Approach
- PLACEHOLDER — describe analytical approach per research question

---

## Main Findings & Insights

- PLACEHOLDER
- PLACEHOLDER
- PLACEHOLDER

---

## Further Questions & Next Steps

- PLACEHOLDER
- PLACEHOLDER
- PLACEHOLDER

---

## Tools Used

- **Python** (Pandas, Matplotlib, Seaborn, Geopy, Folium)
- **Jupyter Notebook**
- **RapidAPI** — Google Hotel Data Scraper (hotel data extraction)
- **Geoapify** — Places API (points of interest enrichment)

---

## Repository Structure

```
revenue-project/
│
├── data/
│   ├── 01_raw_data/                            # Raw datasets (not modified)
│   │   ├── airbnb_paris_weekdays.csv
│   │   ├── airbnb_paris_weekends.csv
│   │   ├── api_hotels_paris_rome_base_clean.csv
│   │   └── Tourism_Hospitality_Industry_Analysis.csv
│   └── 02_cleaned_data/                        # Cleaned and merged datasets
│       └── api_hotels_paris_clean.pkl
│
├── notebooks/                                  # Jupyter notebooks
│   ├── API_handling.ipynb                      # API extraction
│   ├── [CLEANING NOTEBOOK FILENAME].ipynb
│   ├── [EDA NOTEBOOK FILENAME].ipynb
│   └── [VISUALIZATIONS NOTEBOOK FILENAME].ipynb
│
├── visualizations/                             # Exported charts and plots
│   └── [PLOT FILENAMES].png
│
├── .gitignore
├── logo_readme.svg                             # Project logo
├── [PRESENTATION FILENAME].pdf                 # Final presentation
│
└── README.md
```

---

## How to Run

1. Clone the repository and open the notebooks:
   ```bash
   git clone https://github.com/craftedbygaby/revenue-project.git
   cd revenue-project
   jupyter notebook
   ```

2. Install dependencies if needed:
   ```bash
   pip install pandas numpy matplotlib seaborn requests
   ```

---

## Links

- 📋 [Kanban Board](https://trello.com/c/IsQ0NH1s/11-build-github-repo)
- 📊 [Final Presentation](PLACEHOLDER — add link once uploaded)

---

## Limitations

- API rate limits apply on the free tier of RapidAPI — data completeness depends on quota availability
- Hotel data coverage depends on what the Google Hotel Data Scraper returns per city
- Airbnb data is static (scraped at a point in time) and may not reflect current listings
- Analysis is scoped to Paris only — findings may not generalise to other cities
- Tourism & Hospitality dataset is synthetic/aggregated and used for macro context only

---

## Notes

- PLACEHOLDER — any relevant notes about the data, limitations, or context
- All analysis is for educational and portfolio purposes only.
