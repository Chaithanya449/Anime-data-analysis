<h1 align="center">🎌 Anime Data Analysis</h1>

> Always wondered whether a highly-rated anime actually ends up popular, or if episode count even matters. This project digs into 12,000+ anime titles from MyAnimeList to find out.

---

# 📌 Problem

Three questions drove this analysis:
- What types and genres dominate the anime world?
- Does a high rating guarantee popularity?
- Does episode count affect ratings or viewer engagement?

---

# 📂 Dataset

| Property | Details |
|----------|---------|
| File | `anime.csv` |
| Records | 12,294 anime titles |
| Source | MyAnimeList (MAL) |

| Column | Description |
|--------|-------------|
| `name` | Anime title |
| `genre` | Comma-separated genres (multi-label) |
| `type` | Format: TV, Movie, OVA, Special, ONA, Music |
| `episodes` | Episode count — 340 entries had `"Unknown"` strings |
| `rating` | Average MAL user rating |
| `members` | Users who added it to their list (popularity proxy) |

The data wasn't clean out of the box — `rating` and `episodes` were stored as `object` dtype instead of numeric. Handled each null deliberately rather than blanket-dropping rows:

| Column | Nulls | Treatment | Reason |
|--------|-------|-----------|--------|
| `genre` | 62 | `"Unknown"` | Categorical — NaN label preserves the row |
| `type` | 25 | `"Unknown"` | Same reason |
| `rating` | 230 | Kept as `NaN` | Absence of rating is information, not noise |
| `episodes` | 340 `"Unknown"` strings | → `NaN`, cast to `float` | Required for numeric operations |

---

# 🔍 Approach

1. **Type conversion** — `episodes` and `rating` coerced to numeric via `pd.to_numeric()`
2. **Feature engineering** — Min-max scaled `members` into a `popularity` score (0–1) for scatter plotting
3. **Genre parsing** — Split multi-value `genre` column, counted individual genres using `Counter`
4. **EDA** — 5 visualizations: type distribution, rating histogram, top genres bar chart, popularity vs rating scatter, correlation heatmap

---

# 📊 Results

**Type Distribution:**

| Type | Count |
|------|-------|
| TV | 3,787 |
| OVA | 3,311 |
| Movie | 2,348 |
| Special | 1,676 |
| ONA | 659 |

**Top 5 Genres:** Comedy (4,645) · Action (2,845) · Adventure (2,348) · Fantasy (2,309) · Sci-Fi (2,070)

**Correlation (heatmap):**
- `rating` ↔ `members`: **0.39** — quality helps but doesn't guarantee reach
- `episodes` ↔ rating/members: ~**0** — episode count is irrelevant to both

**Key findings:**

- Rating and popularity are positively related but not linear — between ratings 2–6 almost everything stays niche. The real jump happens at **rating ≥ 8**, that's where mainstream popularity kicks in
- Highest-rated titles in the dataset (10.0, 9.6) had fewer than 100 members — small vote bases inflating scores. A minimum vote threshold filter would clean this up
- Episode count surprised me the most — long-running shows have zero statistical edge over short ones

---

# ▶️ How to Run

```bash
git clone https://github.com/Chaithanya449/Anime-data-analysis.git
cd Anime-data-analysis
pip install -r requirements.txt
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
├── anime.csv           # Dataset (12,294 titles)
├── requirements.txt
├── .gitignore
└── README.md
```

---

# 🔮 Next Steps

- [ ] Filter minimum vote threshold before ranking by rating — a 10.0 with 13 votes shouldn't top the charts
- [ ] Build a content-based recommender using genre + rating
- [ ] Genre co-occurrence heatmap — which genres are always paired together?
- [ ] Add release year data to track how anime trends shifted over decades

---

# 👤 Author

**Chaithanya Krishna** · [LinkedIn](https://www.linkedin.com/in/chaitanyakrishna-profile) · [GitHub](https://github.com/Chaithanya449)
