# Google1D
BTT Google 1D project — YouTube Trending Data Analysis

This repo analyzes YouTube trending datasets from multiple countries. Each dataset is stored separately, and there are per-country notebooks for analysis.

## Repository structure
.
├── datasets/ # raw CSVs per country
│ ├── BR_youtube_trending_data.csv
│ ├── CA_youtube_trending_data.csv
│ ├── DE_youtube_trending_data.csv
│ ├── FR_youtube_trending_data.csv
│ ├── GB_youtube_trending_data.csv
│ ├── IN_youtube_trending_data.csv
│ ├── JP_youtube_trending_data.csv
│ ├── KR_youtube_trending_data.csv
│ ├── MX_youtube_trending_data.csv
│ ├── RU_youtube_trending_data.csv
│ └── US_youtube_trending_data.csv
├── notebooks/ # per-country Jupyter notebooks
│ ├── BR_dataset.ipynb
│ ├── CA_dataset.ipynb
│ ├── DE_dataset.ipynb
│ ├── FR_dataset.ipynb
│ ├── GB_dataset.ipynb
│ ├── IN_dataset.ipynb
│ ├── JP_dataset.ipynb
│ ├── KR_dataset.ipynb
│ ├── MX_dataset.ipynb
│ ├── RU_dataset.ipynb
│ └── US_dataset.ipynb
├── utils/ # shared helper code (your modules go here)
├── .venv/ # local virtual environment (optional)
├── .gitattributes
└── README.md

## Usage

### 1) (Optional) Create/activate a virtual environment
```bash
python -m venv .venv
# macOS/Linux
source .venv/bin/activate
# Windows
# .venv\Scripts\activate
2) Open a notebook and load the matching CSV
Each notebook in notebooks/ corresponds to a dataset in datasets/ with the same country code.
Example (from notebooks/US_dataset.ipynb):

import pandas as pd

df = pd.read_csv("../datasets/US_youtube_trending_data.csv")
df.head()
3) Use code from utils/ in notebooks (if you add modules there)
import sys, os
sys.path.append(os.path.abspath(".."))   # allow importing ../utils

# Example:
# from utils import cleaning
# df = cleaning.basic_clean(df)
Naming convention
Datasets: <COUNTRY>_youtube_trending_data.csv (ISO Alpha-2 code)
Notebooks: <COUNTRY>_dataset.ipynb
Each notebook is intended to analyze the dataset with the same country code (e.g., US_dataset.ipynb ↔ US_youtube_trending_data.csv).
Notes
Keep shared functions in utils/ to avoid repeating code across notebooks.
The .venv/ directory is local to your machine and is not required for others; they can create their own environment.
