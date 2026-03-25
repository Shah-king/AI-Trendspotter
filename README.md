# YouTube Trending & Viral Video Prediction (Global Analysis)  
*Break Through Tech AI Studio — Google Challenge (YouTube Trending & Virality)*

---

## Project Overview

**Business Context:** YouTube's recommendation algorithm is central to video discovery and creator success. This project aligns with Google's mission to "organize the world's information and make it universally accessible and useful" by providing data-driven insights into video virality. By understanding the key factors that contribute to a video's trending potential, we can support:
*   **YouTube's Goals:** Improving the accuracy and fairness of the recommendation algorithm to surface high-quality, engaging content.
*   **Creators' Strategy:** Empowering creators with actionable insights to optimize their content and reach a wider audience.

**Objective:** To build, train, and validate a machine learning model that can successfully predict a YouTube video's likelihood of becoming trending based on its metadata and early engagement metrics.

---

## Team Members

| Name | GitHub Handle | Contributions |
| :--- | :--- | :--- |
| Brenda | [BrendaG04](https://github.com/BrendaG04) | ... |
| Shyla | [shylabud](https://github.com/shylabud) | ... |
| Shahriar | [Shahking](https://github.com/Shah-king) | ... |
| Kristel | [kristel777](https://github.com/kristel777) | ... |
| Miles | [Miles1744](https://github.com/miles1744) | ... |
| Nancy Nakyung | [@nancy1404](https://github.com/nancy1404) | ... |
| Rishika Vats | [Irishsss](https://github.com/Irishsss) | ... |

| **Challenge Advisor:** Woon Ket Wong |  | Haziel Andrade |

---

## 🎯 Project Highlights

- Analyzed **2.9M+ YouTube Trending records** across **11 countries** using the Kaggle *YouTube Trending Video* dataset.  
- Framed virality as a **binary classification task** (top decile by views) and built models to predict whether a video will be **viral vs. non-viral**.  
- Engineered **time-to-trending** and **engagement-velocity** features (likes/hour, comments/hour, engagement/hour) to capture *how fast* videos gain traction.  
- Trained and compared multiple models (Logistic Regression, Random Forest, XGBoost, Naive Bayes) with **strong ROC-AUC and recall** on the viral class.  
- Built **per-country notebooks** plus a **Global notebook** to study **regional differences** in virality and trending speed.  
- Performed targeted **error analysis** (false positives/negatives) to uncover slow-burn virality and country-specific behaviors that raw metrics miss.

---

## 👩🏽‍💻 Setup and Installation

### 1. Clone the repository

```bash
git clone https://github.com/BrendaG04/Google1D.git
cd Google1D
```

### 2. (Optional) Create and activate a virtual environment

```bash
python3 -m venv venv
source venv/bin/activate         # on macOS / Linux
# .\venv\Scripts\activate        # on Windows (PowerShell)
```

### 3. Install dependencies

If you have a `requirements.txt`:

```bash
pip install -r requirements.txt
```

Typical packages used:

- `pandas`
- `numpy`
- `scikit-learn`
- `matplotlib`
- `seaborn`
- `xgboost`
- `jupyter`

---

### 4. Download the dataset(s)

1. Go to the Kaggle dataset: **“YouTube Trending Video Dataset”**.
2. Download all country files (e.g., `US_youtube_trending_data.csv`, `KR_youtube_trending_data.csv`, etc.).
3. Place them in the `datasets/` folder (this folder is **not** tracked in git due to file size):

```plaintext
youtube-trending-analysis/
├── datasets/
│   ├── US_youtube_trending_data.csv
│   ├── CA_youtube_trending_data.csv
│   ├── ...
│   └── KR_youtube_trending_data.csv
```

If you also use YouTube API–based files (e.g., category ID → category name mappings), place them in the same `datasets/` folder.

---

### 5. Launch Jupyter and open the notebooks

```bash
jupyter notebook
```

Open:

- `notebooks/Global_Notebook.ipynb` for the global pipeline.  
- `notebooks/XX_Notebook.ipynb` for each country (`US`, `CA`, `GB`, `DE`, `FR`, `BR`, `MX`, `IN`, `RU`, `JP`, `KR`).

---

## 🏗️ Project Overview

This project was completed as part of the **Break Through Tech AI Studio** program, in partnership with **Google**.  
The challenge focused on understanding **YouTube virality** and **Trending behavior** across countries.

### Problem Framing

**Core questions:**

1. **Virality**  
   Can we predict which videos will become **“viral”** (top 10% by views) using only early **engagement** and **metadata**?

2. **Trending Speed**  
   Given a video that reaches Trending, can we estimate **how long it takes** to get there (e.g., days from publish to first Trending appearance)?

### Real-World Significance

YouTube hosts **millions of uploads per day** — it’s impossible for humans to manually screen or prioritize them.

Understanding signals of **virality** and **trending speed** can help:

- Content teams design better **posting strategies**.  
- Platforms monitor **algorithmic amplification** and potential bias.  
- Creators interpret whether **early signals** are promising or not.

---

## 📊 Data Exploration

### Dataset Summary

- **Source:** Kaggle — *YouTube Trending Video Dataset*  
- **Countries:** 11 (e.g., `US`, `CA`, `GB`, `DE`, `FR`, `BR`, `MX`, `IN`, `RU`, `JP`, `KR`)  
- **Rows:** ~2.9 million total  

**Raw fields:**

- **Engagement:** `view_count`, `likes`, `dislikes` (legacy), `comment_count`  
- **Metadata:** `title`, `tags`, `channel_title`, `category_id`, `description`  
- **Time:** `publish_time`, `trending_date`  
- **Other:** `thumbnail_link`, `comments_disabled`, `ratings_disabled`  

### Key Preprocessing Steps

Across notebooks, we typically:

- Parsed and aligned **date/time** columns (`publish_time`, `trending_date`).  
- Removed or imputed rows with missing core fields (**views**, **likes**, **comments**).  
- Dropped fields not usable for modeling (e.g., raw thumbnail links).  
- Filtered out **extreme outliers** where needed when training regression models.  

### Feature Engineering

Some of the main engineered features included:

**Time-based:**

- `publish_hour`  
- `publish_dayofweek`  
- `days_to_trending` and/or `hours_to_trending`  
  - (difference between `publish_time` and first `trending_date`)  

**Metadata richness:**

- `title_length` (characters)  
- `tag_count` (number of tags)  

**Engagement-velocity** (core to virality):

- `likes_per_hour`  
- `comments_per_hour`  
- `engagement_per_hour` (e.g., `(likes + comments) / hours_since_publish`)  

**Virality label:**

- For each country, defined a **“viral”** flag as being in the **top 10%** of `view_count` (or views per day) at the time of observation.

### EDA Highlights

- Viral videos typically have **much higher engagement velocity early on**, not just more total views.  
- Some markets (e.g., **KR, IN, RU**) show **faster days-to-trending** compared with others (e.g., **US, CA, JP**).  
- Category effects exist but are often weaker than **engagement** and **timing** features.  

---

## 🧠 Model Development

We framed the work as two related tasks:

- **Classification:** Predict whether a video is **viral** (top decile) vs. **non-viral**.  
- **Regression:** Estimate **time-to-trending** for videos that hit Trending.  

### Models Used

**Classification:**

- Logistic Regression  
- Random Forest Classifier  
- XGBoost Classifier  
- Naive Bayes (as a simpler baseline)  

**Regression:**

- Linear Regression on **log-transformed** targets  
- Random Forest Regressor  
- XGBoost Regressor  

### Typical Training Setup

- Train/validation split (e.g., **70/30**) within each country or region.  
- Scaling numeric features (e.g., `StandardScaler`) and one-hot encoding categorical fields using `ColumnTransformer`.  
- **Main classification metric:** `ROC-AUC`, with **recall on the viral class** as a secondary focus.  
- **Main regression metrics:** `MAE`, `RMSE`, and `R²`.  

### Handling Imbalance

Because only ~10% of samples are labeled **viral**, we experimented with:

- Class weights (e.g., `class_weight="balanced"`).  
- **Threshold tuning** (moving away from 0.5) to recover better viral recall.  

---

## 📈 Results & Key Findings

> Note: Exact metrics may vary by country notebook; this section summarizes the overall behavior observed across runs.

### Classification Performance

- Tree-based models (**Random Forest**, **XGBoost**) consistently outperformed baselines.  
- **ROC-AUC** for the best models was typically **high** (≈ 0.96+ in many regions), with strong separation between **viral** and **non-viral** classes.  
- **Engagement-velocity** features (`likes_per_hour`, `comments_per_hour`, `engagement_per_hour`) were almost always among the **top feature importances**.  

### Regression (Time-to-Trending)

- Best regression models achieved **MAE ~1.5–2 days** and **moderate R²** (the platform has inherent randomness and unobserved factors).  
- Some markets trend faster on average; others have more **latency** between publish and Trending, even for videos that eventually go viral.  

### Behavioral Insights

**Velocity > raw counts**  
A video with modest total views but **high early engagement rate** is more likely to be predicted viral than a slow-growing video with bigger absolute numbers.

**Country differences:**

- Certain countries show more **“flash” virality** (quick spikes, fast Trending).  
- Others exhibit **slow-burn** trajectories where videos accumulate views over time before finally hitting Trending.  

**Error analysis:**

- **False positives:** High early engagement that never quite crosses the Trending threshold (e.g., niche but very loyal audiences).  
- **False negatives:** Videos that start slow but later surge due to external events, news cycles, or creator promotion — behavior that isn’t fully captured by simple early-time features.  

---

## 🚀 Next Steps

If we had more time or production constraints, we would explore:

### Richer text understanding

- Use multilingual models (e.g., **BERT variants**) to embed **titles, descriptions, and tags**.

### Temporal modeling

- Replace single “snapshot” features with **time-series curves** (engagement over 12–48 hours) and model them via **RNN**, **TCN**, or **temporal transformers**.

### Fairness & bias analysis

- Examine model performance across **categories**, **countries**, and **channel sizes** to see where predictions might systematically favor or penalize certain creators.

### Peak performance prediction

- Instead of only viral vs. non-viral, predict **future peak views** or **watch time** as a continuous outcome.

### Deployment-oriented work

- Wrap the best model in a simple **API** and create a lightweight **dashboard** for “what-if” analyses (e.g., *“What if we shift publish hour?”*).

---

## 📁 Repository Structure

```plaintext
youtube-trending-analysis/
├── notebooks/
│   ├── Global_Notebook.ipynb
│   ├── US_Notebook.ipynb
│   ├── CA_Notebook.ipynb
│   ├── GB_Notebook.ipynb
│   ├── DE_Notebook.ipynb
│   ├── FR_Notebook.ipynb
│   ├── BR_Notebook.ipynb
│   ├── MX_Notebook.ipynb
│   ├── IN_Notebook.ipynb
│   ├── RU_Notebook.ipynb
│   ├── JP_Notebook.ipynb
│   └── KR_Notebook.ipynb
├── datasets/           # (not tracked in git; add CSVs here locally)
├── slides/             # final AI Studio presentation (to be added)
├── README.md
├── requirements.txt    # (if used)
├── .gitignore
└── .DS_Store
```

## 📝 License

This project is licensed under the **MIT License**.

---

## 📄 References

- Kaggle: *YouTube Trending Video Dataset*
- Break Through Tech AI Studio curriculum materials (ML, MLOps, fairness modules)
- scikit-learn documentation
- XGBoost documentation
- (Add any additional papers, blogs, or resources you used.)

---

## 🙏 Acknowledgements

Huge thanks to:

- **Google / YouTube** for sponsoring the challenge.
- **Break Through Tech AI** for the curriculum, mentorship, and infrastructure.
- **Team Google 1D** members and coaches for feedback on modeling, EDA, and communication.


