# Google1D
BTT Google 1D project — YouTube Trending Data Analysis

This repo analyzes YouTube trending datasets from multiple countries. Each dataset is stored separately, and there are per-country notebooks for analysis.

## Repository structure
.<br/>
├── datasets/ # raw CSVs per country<br/>
│ ├── BR_youtube_trending_data.csv<br/>
│ ├── CA_youtube_trending_data.csv<br/>
│ ├── DE_youtube_trending_data.csv<br/>
│ ├── FR_youtube_trending_data.csv<br/>
│ ├── GB_youtube_trending_data.csv<br/>
│ ├── IN_youtube_trending_data.csv<br/>
│ ├── JP_youtube_trending_data.csv<br/>
│ ├── KR_youtube_trending_data.csv<br/>
│ ├── MX_youtube_trending_data.csv<br/>
│ ├── RU_youtube_trending_data.csv<br/>
│ └── US_youtube_trending_data.csv<br/>
├── notebooks/ # per-country Jupyter notebooks<br/>
│ ├── BR_dataset.ipynb<br/>
│ ├── CA_dataset.ipynb<br/>
│ ├── DE_dataset.ipynb<br/>
│ ├── FR_dataset.ipynb<br/>
│ ├── GB_dataset.ipynb<br/>
│ ├── IN_dataset.ipynb<br/>
│ ├── JP_dataset.ipynb<br/>
│ ├── KR_dataset.ipynb<br/>
│ ├── MX_dataset.ipynb<br/>
│ ├── RU_dataset.ipynb<br/>
│ └── US_dataset.ipynb<br/>
├── utils/ # shared helper code (your modules go here)<br/>
├── .venv/ # local virtual environment (optional)<br/>
├── .gitattributes<br/>
└── README.md<br/>

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
Each notebook is intended to analyze the dataset with the same country code (e.g., US_dataset.ipynb ↔ US_youtube_trending_data.csv).<br/>
Notes<br/>
Keep shared functions in utils/ to avoid repeating code across notebooks.<br/>
The .venv/ directory is local to your machine and is not required for others; they can create their own environment.<br/>
