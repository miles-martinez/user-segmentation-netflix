# Netflix User Segmentation

Segments Netflix-style subscribers into behavioral groups by combining user
profile data with watch-history logs, then digs into what drives those
behaviors using unsupervised machine learning.

## What's inside

- Data cleaning and exploratory analysis of user demographics and subscription patterns
- User-level feature engineering from raw viewing sessions (session length, binge score, completion rate, device diversity, etc.)
- K-Means clustering to segment users into behavioral groups
- Factor Analysis to uncover the latent dimensions behind those behaviors

## Project structure

```
.
├── notebooks/
│   └── netflix_user_segmentation.ipynb   # main analysis notebook
├── data/                                  # place users.csv and watch_history.csv here (not tracked)
├── requirements.txt
└── README.md
```

## Data

The notebook expects two CSV files in `data/`:

| File | Description |
|---|---|
| `users.csv` | One row per subscriber: demographics, subscription plan, spend, device, etc. |
| `watch_history.csv` | One row per viewing session: user, movie, duration, progress, rating, action, timestamps, etc. |

These files are not included in this repository. Point `DATA_DIR` in the
notebook at wherever your copies live, or drop them into `data/`.

## Setup

```bash
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install -r requirements.txt
jupyter notebook notebooks/netflix_user_segmentation.ipynb
```

## Method summary

1. **Cleaning & EDA** — inspect missing values, distributions of age/spend/device/plan, and signup trends.
2. **Feature engineering** — aggregate session-level watch history into ~18 user-level behavioral features (session length, completion rate, binge score, content diversity, device diversity, HD/download preference, weekend viewing, etc.).
3. **K-Means clustering** — standardize features, pick k via the elbow method and silhouette score, and profile the resulting segments.
4. **Factor Analysis** — check suitability (Bartlett's test, KMO), drop zero-variance features, determine the number of latent factors (scree plot, Kaiser criterion, parallel analysis), then fit a Varimax-rotated model and interpret the factors.

## Notes

Outputs (plots, printed tables) are cleared in the committed notebook so the
repo stays lightweight and diffs stay readable — run the notebook end-to-end
to reproduce them.
