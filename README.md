<h1 align="center">🎌 Anime Data Analysis</h1>

> Exploratory Data Analysis on 12,000+ anime titles — uncovering trends in genres, ratings, popularity, and the relationship between episode count and viewer engagement.

---

# 📌 Problem

With thousands of anime titles across multiple formats, understanding what drives ratings and popularity is non-trivial. This project explores the MyAnimeList dataset to answer:
- Which genres and types dominate the anime landscape?
- Does higher rating always mean higher popularity?
- Is there a correlation between episode count, rating, and member count?

---

# 📂 Dataset

| Property | Details |
|----------|---------|
| File | `anime.csv` |
| Records | 12,294 anime titles |
| Features | 7 columns |
| Source | MyAnimeList (MAL) |

**Columns:**

| Column | Type | Description |
|--------|------|-------------|
| `anime_id` | int | Unique identifier |
| `name` | str | Anime title |
| `genre` | str | Comma-separated genres |
| `type` | str | Format (TV, Movie, OVA, etc.) |
| `episodes` | str | Episode count (340 "Unknown" values) |
| `rating` | float | Average MAL rating (230 nulls) |
| `members` | int | Number of users who added it to their list |

**Missing Values Handled:**

| Column | Nulls | Treatment |
|--------|-------|-----------|
| `genre` | 62 | Filled with `"Unknown"` |
| `type` | 25 | Filled with `"Unknown"` |
| `rating` | 230 | Left as `NaN` (meaningful absence) |
| `episodes` | 340 "Unknown" strings | Replaced with `NaN`, converted to `float` |

---

# 🔍 Approach

1. **Load & Inspect** — Checked dtypes, shape, null counts
2. **Data Cleaning** — Handled mixed-type columns (`episodes`, `rating` stored as `object`); converted to numeric
3. **Missing Value Strategy** — Categorical nulls → `"Unknown"` string; numeric nulls → kept as `NaN` for statistical integrity
4. **Feature Engineering** — Created normalized `popularity` score from `members` using min-max scaling
5. **EDA** — 5 visualizations: type distribution, rating histogram, top genres, popularity vs rating scatter, correlation heatmap
6. **Insight Extraction** — Identified key patterns in ratings, genres, and popularity thresholds

---

# 📊 Results

**Anime Type Distribution:**

| Type | Count |
|------|-------|
| TV | 3,787 |
| OVA | 3,311 |
| Movie | 2,348 |
| Special | 1,676 |
| ONA | 659 |
| Music | 488 |

**Top 5 Genres:** Comedy (4,645) · Action (2,845) · Adventure (2,348) · Fantasy (2,309) · Sci-Fi (2,070)

**Key Insights:**

- 📈 **Rating vs Popularity** — Positive but non-linear relationship. Anime rated below ~7 rarely gain mainstream popularity. The real tipping point is **rating ≥ 8**, where member counts spike significantly
- 🔗 **Correlation** — `rating` ↔ `members`: **0.39** (moderate positive). `episodes` ↔ `rating` and `episodes` ↔ `members`: near **zero** — episode count doesn't predict quality or popularity
- ⭐ **Highest rated** titles (≥ 9.25): *Kimi no Na wa* (Movie), *Fullmetal Alchemist: Brotherhood* (TV), *Gintama°* (TV)
- 🚨 **Surprise finding** — The absolute highest-rated titles (10.0, 9.6) have fewer than 100 members — niche titles inflating ratings with tiny vote bases

---

# ▶️ How to Run

```bash
# 1. Clone the repo
git clone https://github.com/Chaithanya449/Anime-data-analysis.git
cd Anime-data-analysis

# 2. Install dependencies
pip install -r requirements.txt

# 3. Open the notebook
jupyter notebook "anime (1).ipynb"
```

> Ensure `anime.csv` is in the same directory as the notebook.

---

# 🛠️ Tech Stack

![Python](https://img.shields.io/badge/Python-3.11-blue?logo=python)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Wrangling-lightgrey?logo=pandas)
![NumPy](https://img.shields.io/badge/NumPy-Numerical-blue?logo=numpy)
![Seaborn](https://img.shields.io/badge/Seaborn-Visualization-9cf)
![Matplotlib](https://img.shields.io/badge/Matplotlib-Plots-yellow)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?logo=jupyter)

---

# 📁 Project Structure

```
Anime-data-analysis/
├── anime (1).ipynb     # Main EDA notebook
├── anime.csv           # Dataset (12,294 anime titles)
├── requirements.txt    # Python dependencies
├── .gitignore
└── README.md
```

---

# 🔮 Next Steps

- [ ] Build a **content-based recommender** using genre + rating features
- [ ] Analyze rating reliability — filter titles with < 100 votes to remove rating inflation
- [ ] Time-series analysis if release year data is available (anime trends over decades)
- [ ] Genre co-occurrence heatmap — which genres are most commonly paired together
- [ ] NLP on anime titles/descriptions to cluster by theme

---

# 👤 Author

**Chaithanya Krishna** · [LinkedIn](https://www.linkedin.com/in/chaitanyakrishna-profile)  [GitHub](https://github.com/Chaithanya449)
