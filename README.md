# Movie Financial Performance — Correlation & EDA (Python)

## Project Overview

Analysed a movie dataset in Python to identify which factors most
strongly correlate with gross earnings — testing hypotheses around
**budget, audience votes, and production company influence.**

Built a **full Pearson correlation matrix** across all numeric features
using `pandas corr()` and visualised relationships through scatterplots,
regression lines, and a correlation heatmap.

Primary goal: determine whether budget, audience engagement, or
studio brand is the **strongest predictor of financial performance.**

---

## Dataset

| Column | Description |
|---|---|
| name | Movie title |
| budget | Production budget in USD |
| gross | Worldwide gross earnings in USD |
| votes | Number of audience votes (IMDb) |
| runtime | Film runtime in minutes |
| score | IMDb rating |
| year | Release year |
| company | Production company |
| genre | Film genre |
| country | Country of production |

> Each row represents one movie with its financial and
> audience performance metrics.

Source: IMDb movie dataset — Kaggle

---

## Metrics Defined

| Metric | Definition |
|---|---|
| Pearson r — Budget vs Gross | Strength of linear relationship between budget and earnings |
| Pearson r — Votes vs Gross | Strength of relationship between audience engagement and earnings |
| Pearson r — Company vs Gross | Strength of relationship between studio brand and earnings |
| Full Correlation Matrix | Pearson r values across all numeric features simultaneously |

---

## Key Findings

| Relationship | Pearson r | Interpretation |
|---|---|---|
| **Budget vs Gross Earnings** | **0.74** | Strong positive — budget is the dominant financial lever |
| **Votes vs Gross Earnings** | **0.61** | Moderate to strong — audience engagement drives revenue |
| **Production Company vs Gross** | **0.15** | Weak — studio brand is not a reliable earnings predictor |

---

### The Brand Illusion

> The studio name on the poster matters far less than the money
> behind the film and the audience interest it builds before release.

Breaking it down:

- **Budget (r = 0.74):** Strongest predictor — more investment
  generally produces more return
- **Votes (r = 0.61):** Audience engagement is a stronger signal
  than most analysts assume — and stronger than studio reputation
- **Production Company (r = 0.15):** Explains very little variance
  in earnings — genre, cast, release timing, and marketing spend
  account for far more

> **The key insight:** A smaller studio with strong audience
> engagement can outperform a major studio with a weak one.
> Brand is not the lever — interest is.

---

## How to Read Correlation Values

| Pearson r | Meaning |
|---|---|
| **+0.7 to +1.0** | Strong positive relationship |
| **+0.3 to +0.7** | Moderate positive relationship |
| 0.0 to +0.3 | Weak or no relationship |
| -0.3 to 0.0 | Weak negative relationship |
| **-0.7 to -0.3** | Moderate negative relationship |
| **-1.0 to -0.7** | Strong negative relationship |

---

## Tech Stack

| Tool | Purpose |
|---|---|
| **Python** | Core language |
| **Pandas** | Data cleaning and correlation matrix |
| **Seaborn** | Heatmap and regression plot visualisation |
| **Matplotlib** | Plot rendering and display |
| **scipy.stats** | Individual column pair correlation with p-value |

---

## Approach

1. Data cleaning — cast columns to numeric, handle missing values,
   remove rows where budget or gross is zero
2. Numerise categorical columns (production company) using
   **label encoding** to include in the correlation matrix
3. Build **full Pearson correlation matrix** across all numeric
   features using `pandas corr(method='pearson')`
4. Visualise as a **heatmap** to read all relationships at once
5. Plot scatterplots with **regression lines** for the three
   relationships of interest

---

## Code

### Method 1 — Full correlation matrix (used in this project)

Calculates Pearson correlation across **all numeric features at once.**
Gives a complete picture of all relationships in a single heatmap.
```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

df = pd.read_csv('movies.csv')

numeric_cols = ['budget', 'gross', 'votes', 'runtime', 'score', 'year']
corr_matrix = df[numeric_cols].corr(method='pearson')

sns.heatmap(corr_matrix, annot=True, cmap='coolwarm', fmt='.2f')
plt.title('Correlation Matrix — Numeric Features')
plt.xlabel('Movie Features')
plt.ylabel('Movie Features')
plt.show()
```

### Method 2 — Individual column pairs (alternative approach)

Use this when you need the **exact r value and p-value** for a
specific relationship rather than the full matrix.
```python
from scipy.stats import pearsonr

r_budget_gross, p_budget_gross = pearsonr(df['budget'], df['gross'])
r_votes_gross,  p_votes_gross  = pearsonr(df['votes'],  df['gross'])

print(f'Budget vs Gross:  r = {r_budget_gross:.2f},  p = {p_budget_gross:.4f}')
print(f'Votes vs Gross:   r = {r_votes_gross:.2f},   p = {p_votes_gross:.4f}')
```

> The **p-value** tells you whether the correlation is statistically
> significant. A p-value **below 0.05** means the relationship is
> unlikely to be due to chance.

### Scatterplots with regression lines
```python
sns.regplot(x='budget', y='gross', data=df)
plt.title('Budget vs Gross Earnings')
plt.xlabel('Budget ($)')
plt.ylabel('Gross Earnings ($)')
plt.show()

sns.regplot(x='votes', y='gross', data=df)
plt.title('Votes vs Gross Earnings')
plt.xlabel('Votes')
plt.ylabel('Gross Earnings ($)')
plt.show()

sns.boxplot(x='gross', data=df)
plt.title('Gross Earnings Distribution')
plt.show()
```

---

## How to Run

1. Clone the repository
2. Install dependencies:
```
pip install pandas seaborn matplotlib scipy
```

3. Place the dataset CSV in the project root folder
4. Run the script:
```
python movie_correlation.py
```

---

## Key Takeaway

**Budget predicts earnings. Audience engagement predicts earnings.
Studio brand barely does.**

What a film builds before release — audience interest, marketing
reach, engagement — matters more than which company produced it.
