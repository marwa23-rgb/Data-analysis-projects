<h1 align="center">🎞️ TMDb Movies Analysis</h1>

<p align="center">
  Exploratory data analysis of about 10,000 movies from The Movie Database (TMDb) using Python
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/Pandas-Data%20Analysis-150458?logo=pandas&logoColor=white" alt="Pandas">
  <img src="https://img.shields.io/badge/Seaborn-Visualization-4C8CBF" alt="Seaborn">
  <a href="https://www.themoviedb.org/"><img src="https://img.shields.io/badge/Data-TMDb-01B4E4" alt="TMDb"></a>
</p>

## 📌 Overview

This project explores a TMDb movie dataset covering films released between **1960 and 2015**, including user ratings, budget and revenue. It cleans the data, answers five questions about popularity, runtime, profit, revenue and genres with Pandas, and visualizes the results with Matplotlib and Seaborn.

> The `cast` and `genres` columns hold several values separated by `|`. The final two columns, `budget_adj` and `revenue_adj`, show budget and revenue in 2010 dollars to account for inflation.

---

## ❓ Questions

1. Does a higher budget mean higher popularity?
2. Does runtime affect popularity?
3. Does higher popularity mean higher profit?
4. What features are associated with the top 10 revenue movies?
5. Which genres are most popular from year to year?

---

## ⚡ At a Glance

| 🎬 Movies | 📊 Columns (raw) | 📅 Years Covered | ⭐ Avg. Vote | ⏱️ Avg. Runtime |
|:---:|:---:|:---:|:---:|:---:|
| **10,866** | **21** | **1960 – 2015** | **≈ 5.97** | **≈ 102 min** |

---

## 🔄 Workflow

1. **Load & Inspect** – Checked shape, data types, unique values, missing values and summary statistics.
2. **Clean the Data** – Dropped unneeded columns, filled missing values and removed duplicates.
3. **Feature Engineering** – Added a `profit` column (`revenue − budget`) and a `genre` column holding each movie's first listed genre.
4. **Analyze** – Compared groups split by median budget, runtime and popularity, and counted genres and directors.
5. **Visualize** – Built histograms, scatter plots, bar charts, line plots and heatmaps.

> **Columns kept:** `popularity` · `budget` · `revenue` · `original_title` · `cast` · `director` · `tagline` · `keywords` · `runtime` · `genres` · `production_companies` · `release_date` · `vote_count` · `vote_average` · `release_year` · `budget_adj` · `revenue_adj`

---

## 🧹 Data Cleaning

| Step | Action |
|---|---|
| **Dropped columns** | `id`, `imdb_id`, `homepage`, `overview` |
| **Missing text values** | `cast`, `director`, `tagline`, `keywords`, `genres` and `production_companies` filled with the string `"missing"` |
| **Zero budgets** | Zeros in `budget` replaced with `NaN` (5,696 values), since they are not real budgets |
| **Duplicates** | 1 duplicate row found and dropped |

---

## 🔍 Key Findings

| Question | Result |
|---|---|
| Budget vs. popularity | The scatter plot shows no strong relationship, but movies with a **higher-than-median budget** have a clearly higher average popularity. Low-budget movies average about **55% less popularity** than high-budget ones |
| Runtime vs. popularity | Movies under about **200 minutes** can be popular. Beyond 200 minutes, high popularity is rare |
| Popularity vs. profit | Movies with **higher popularity earn a higher average profit** |
| Top 10 revenue movies | Runtimes between about **100 and 200 minutes**, mostly released from the mid-1990s to 2015 |
| Genres over time | Genre variety and the number of movies released per year both grew over the decades. Drama, Comedy, Action, Horror and Adventure appear most often in the genre counts |
| Directors with the most movies | **Woody Allen** (46) · **Clint Eastwood** (34) · **Martin Scorsese** (31) · **Steven Spielberg** (30) |

---

## 📊 Visualizations

| Plot | Shows |
|---|---|
| Histograms | Distribution of every numeric column |
| Scatter plot | Budget vs. popularity |
| Bar chart | Average popularity for low vs. high budget |
| Bar chart | Average popularity by runtime group |
| Scatter plot | Runtime vs. popularity |
| Bar chart | Average profit for low vs. high popularity |
| Histograms | Features of the top 10 revenue movies |
| Bar plot | Number of movies per genre |
| Line plot | Number of movies released each year |
| Heatmaps | Average budget and revenue by genre and release year |

---

## ⚠️ Limitations

- Many budget and revenue values are zero or missing, which can distort averages and profit.
- It is unclear how `popularity` and `vote_count` are measured.
- Budget and revenue for foreign movies have no stated currency, and inflation over the years should be considered (the `_adj` columns help with this).
- The runtime groups in the analysis overlap (the "medium" group also includes the "short" movies), and the exact best runtime is not shown clearly by the charts.


## 👩‍💻 Author

**Marwa Samy** · [GitHub](https://github.com/marwa23-rgb)
