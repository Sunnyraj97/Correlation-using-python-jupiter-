# Movie Financial Performance — Correlation & EDA (Python)

## Project Overview

Analysed a movie dataset in Python to identify which factors most
strongly correlate with gross earnings — testing hypotheses around
budget, audience votes, and production company influence.

Built a full Pearson correlation matrix across all numeric features
using pandas corr() and visualised relationships through scatterplots,
regression lines, and a correlation heatmap.

---

## Hypotheses Tested

| Hypothesis | Expected Outcome |
|---|---|
| Higher budget → higher gross earnings | Likely strong correlation |
| Production company influences gross earnings | Needed validation |

---

## Key Findings

| Relationship | Pearson r | Interpretation |
|---|---|---|
| Budget vs Gross Earnings | 0.74 | Strong positive — budget is the dominant financial lever |
| Votes vs Gross Earnings | 0.61 | Moderate to strong — audience engagement drives revenue |
| Production Company vs Gross | 0.15 | Weak — studio brand is not a reliable earnings predictor |

### What this showed

Budget is the strongest predictor of gross earnings — but the more
interesting finding is that audience engagement (votes) outperforms
production company brand as a revenue signal.

This suggests that engagement-driven marketing may matter more than
studio reputation — a finding that holds implications for how smaller
studios compete against major production companies.

Production company alone explains very little of the variance in
earnings. Other factors — genre, cast, release timing, and marketing
spend — likely account for the gap.

---

## How to Read Correlation Values

| Pearson r | Meaning |
|---|---|
| +0.7 to +1.0 | Strong positive relationship |
| +0.3 to +0.7 | Moderate positive relationship |
| 0.0 to +0.3 | Weak or no relationship |
| -0.3 to 0.0 | Weak negative relationship |
| -0.7 to -0.3 | Moderate negative relationship |
| -1.0 to -0.7 | Strong negative relationship |

---

## Tech Stack

| Tool | Purpose |
|---|---|
| Python | Core language |
| Pandas | Data cleaning and correlation matrix |
| Seaborn | Heatmap and regression plot visualisation |
| Matplotlib | Plot rendering and display |
| scipy.stats | Individual column pair correlation with p-value |

---

## Approach

1. Data cleaning — cast columns to numeric, handle missing values,
   remove rows where budget or gross is zero
2. Numerise categorical columns (production company) using
   label encoding to include in the correlation matrix
3. Build full Pearson correlation matrix across all numeric features
   using pandas corr(method='pearson')
4. Visualise as a heatmap to read all relationships at once
5. Plot scatterplots with regression lines for the three
   relationships of interest

---

## Code

### Method 1 — Full correlation matrix (used in this project)

Calculates Pearson correlation across all numeric features at once.
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

Use this when you need the exact r value and p-value for a specific
relationship rather than the full matrix.
```python
from scipy.stats import pearsonr

r_budget_gross, p_budget_gross = pearsonr(df['budget'], df['gross'])
r_votes_gross,  p_votes_gross  = pearsonr(df['votes'],  df['gross'])

print(f'Budget vs Gross:  r = {r_budget_gross:.2f},  p = {p_budget_gross:.4f}')
print(f'Votes vs Gross:   r = {r_votes_gross:.2f},   p = {p_votes_gross:.4f}')
```

The p-value tells you whether the correlation is statistically
significant. A p-value below 0.05 means the relationship is
unlikely to be due to chance.

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

Source: IMDb movie dataset (available on Kaggle)

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

Budget predicts earnings. Audience engagement predicts earnings.
Studio brand barely does.

The data suggests that what a film builds before release — audience
interest, marketing reach, engagement — matters more than which
company produced it.
