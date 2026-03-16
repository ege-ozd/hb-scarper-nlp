# Hepsiburada Airfryer — Customer Review Analysis (NLP & TF-IDF)

A complete end-to-end pipeline that scrapes customer reviews from Hepsiburada (Turkey's largest e-commerce platform), applies NLP and TF-IDF analysis, and produces structured business intelligence for product positioning and marketing strategy.

---

## The Business Problem

E-commerce product teams and brand managers have access to thousands of customer reviews but rarely extract structured insight from them. This project answers three concrete questions:

1. **What do customers actually value** about this product — in their own words?
2. **Who is buying it** — and what distinct personas are driving purchases?
3. **Why are negative reviews negative** — is it the product, or something else?

---

## Dataset

- **Source:** Hepsiburada.com — Airfryer (Air Fryer / Fritöz) category, top-selling products
- **Volume:** ~2,000 customer reviews + Q&A threads scraped via custom Selenium/BeautifulSoup pipeline
- **Coverage:** Star ratings (1–5), review text, product Q&A responses

---

## Technical Stack

| Layer | Tools |
|---|---|
| Data Collection | Python, Selenium, BeautifulSoup, Requests |
| Data Processing | pandas, NumPy, Regex, custom stopword lists (Turkish NLP) |
| NLP & Analysis | scikit-learn (TF-IDF), TextBlob / rule-based sentiment, pattern matching |
| Visualisation | Matplotlib, Seaborn, WordCloud |
| Structure | Modular `src/` architecture — scraper and analysis fully separated |

---

## Key Findings

### Finding 1 — Value Perception: Customers buy for price-performance, not premium features

TF-IDF analysis revealed that the two highest-weighted terms in the entire corpus were **"Fiyat Performans" (Price-Performance, TF-IDF: 0.0174)** and **"Uygun Fiyat" (Affordable Price, 0.0043)**. Customers frame this product not as a luxury appliance but as a high-ROI investment. Brand messaging focused on premium design is likely misaligned with actual purchase motivation.

### Finding 2 — Use Case: Customers use it far beyond frying

**"Patates" (Chips/Fries)** leads at TF-IDF 0.0195, but the presence of **"Köfte" (meatballs)**, **"Tavuk" (chicken)**, and notably **"Sulu Yemek" (stew / saucy dishes, 0.0048)** indicates customers have positioned this as a full main-course cooker — not just a frying device. This is an underutilised marketing angle.

### Finding 3 — Persona Segmentation: Three distinct buyer profiles emerge from the data

| Persona | Key Signals | TF-IDF Evidence |
|---|---|---|
| **Family Buyer** | Capacity is the primary concern | "4 Kişilik Aile" (0.0077), "Geniş Hazne" (0.0035) |
| **Time-Poor Professional** | Speed and convenience dominate | "Çok Hızlı" (0.0129), "Çok Pratik" (0.0116), "Wi-Fi" (0.0045) |
| **Health-Conscious Cook** | Texture + low oil is the win | "Çıtır" / Crispy (0.0095), "Az Yağ" / Less Oil (0.0051) |

Space-constrained customers (students, single-person households) express friction via **"Çok Büyük" (Too Large, 0.0072)** and **"Yer Kaplıyor" (Takes Up Space, 0.0040)** — pointing to a clear gap for a compact model.

### Finding 4 — Negative Reviews Are a Logistics Problem, Not a Product Problem

Sentiment analysis flagged 196 reviews with 1–3 star ratings. TF-IDF on this negative subset revealed the dominant terms were **"İade" (Return, 0.0811)**, **"Kullanılmış" (Used/Second-hand, 0.0377)**, and **"Kırık" (Broken/Damaged, 0.0320)**. 

**The product's cooking performance is not the driver of negative sentiment.** Customer dissatisfaction stems almost entirely from packaging damage and fulfilment issues — meaning the product has a logistics reputation problem, not a product quality problem.

### Finding 5 — First-Use Experience: "Plastic smell" is manageable, not a defect

**"Plastik Kokusu" (Plastic Smell, 0.0054)** appears consistently but deeper analysis shows it is resolved by running the device empty at 200°C before first use — a known burn-in process. This is an expectation management issue, not a quality defect, and can be addressed with pre-sale content.

---

## Project Structure

```
hb-nlp/
├── data/
│   ├── raw/                    # Scraped CSVs (reviews + Q&A)
│   └── processed/              # Cleaned data, TF-IDF outputs, WordCloud images
├── notebooks/                  # Exploratory data analysis
├── src/
│   ├── scraper/
│   │   ├── scraper_comments.py # Review scraper
│   │   └── scraper_qna.py      # Q&A scraper
│   └── analysis/
│       ├── cleaner.py          # Turkish text preprocessing (stopwords, regex)
│       ├── tfidf_analyzer.py   # TF-IDF scoring module
│       ├── pattern_matcher.py  # Rule-based labelling
│       └── generate_wordcloud.py
├── main.py                     # Pipeline entry point
└── requirements.txt
```

---

## How to Run

```bash
# 1. Clone the repo
git clone https://github.com/ege-ozd/hb-scarper-nlp.git
cd hb-scarper-nlp

# 2. Install dependencies
pip install -r requirements.txt

# 3. Run the full pipeline
python main.py
```

---

## What This Project Demonstrates

- **Full pipeline ownership** — from raw web scraping through to business insight, with no manual steps
- **Turkish NLP** — custom preprocessing for Turkish morphology (stopwords, stemming considerations)
- **Business framing** — analysis outputs are structured as strategic recommendations, not just frequency tables
- **Modular code architecture** — scraper and analysis layers are fully independent and reusable

---

## Author

**Ege Özdemir** — Senior Data Scientist  
[LinkedIn](https://www.linkedin.com/in/ege-%C3%B6zdemir-2235091a7/)
