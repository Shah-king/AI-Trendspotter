# Google1D

BTT Google 1D project

YouTube Trending Data Analysis

This project analyzes YouTube trending datasets from multiple countries. Each dataset is stored separately, and there are per-country notebooks for analysis.

Repository Structure
.
├── datasets/                 # Raw CSV files for each country
│   ├── BR_youtube_trending_data.csv
│   ├── CA_youtube_trending_data.csv
│   └── ...
├── notebooks/                # Jupyter notebooks for analysis (per country)
│   ├── BR_dataset.ipynb
│   ├── CA_dataset.ipynb
│   └── ...
├── utils/                    # Shared helper code (e.g., loading, cleaning)
├── .venv/                    # Local virtual environment (optional)
├── .gitattributes
└── README.md

Usage

Set up environment
python -m venv .venv
source .venv/bin/activate   # Windows: .venv\Scripts\activate
pip install -r requirements.txt   # if you have one
Open a notebook
Each notebook in notebooks/ corresponds to one country’s dataset in datasets/.
Example:
US_dataset.ipynb → works with US_youtube_trending_data.csv
RU_dataset.ipynb → works with RU_youtube_trending_data.csv

Using utils/

Common functions for loading data, cleaning, or plotting can go inside utils/ and be imported into notebooks.
Example (if you add io.py or cleaning.py):
from utils import io, cleaning
df = io.load_csv("datasets/US_youtube_trending_data.csv")
df = cleaning.clean_titles(df)

Notes

Each dataset is named with the country code (ISO Alpha-2) for consistency.
Each notebook matches a dataset, making it easy to work country by country.
The utils/ folder is for shared functions so code doesn’t get repeated in every notebook.
