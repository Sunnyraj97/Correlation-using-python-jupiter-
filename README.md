# 🎬 Movie Correlation Analysis  
### Budget • Gross Earnings • Production Company • Votes

## 🎯 Objective  
Analyze relationships between **movie budget, gross earnings, votes, runtime**, and **production company** using Python.  
Primary goal: Determine how strongly each factor correlates with financial success (**Gross Earnings**) using Pearson correlation.

---

## ✅ Hypotheses  
| Hypothesis | Expected Outcome |
|------------|------------------|
| Higher Budget → Higher Gross Earnings | ✅ Likely strong correlation |
| Production Company influences Gross Earnings | ❓ Needs validation |

---

## 🔍 Key Findings  

| Relationship | Correlation (Pearson r) | Interpretation |
|--------------|-------------------------|----------------|
| **Budget → Gross Earnings** | **0.74** | Strong positive — more budget → more earnings |
| **Votes → Gross Earnings** | **0.61** | Moderate to strong — audience engagement drives revenue |
| **Production Company → Gross Earnings** | **0.15** | Weak — company itself is not a predictor |

💡 **Insight**  
- Budget is the strongest predictor of earnings  
- Votes reflect audience interest and popularity  
- Production Company shows weak predictive power

---

## 📊 Data Insights  

- Movies with higher budgets generally generate higher gross revenue.
- Higher vote counts suggest audience approval—which correlates to earnings.
- Production company does **not** directly influence earnings — other variables like:
  - Genre
  - Cast star power
  - Release timing (holiday vs. off-season)
  - Marketing spend  
  have a bigger impact.

---

## 🧠 Interpretation Scale (How to read correlation values)

| Pearson r Value | Meaning |
|-----------------|----------|
| **+1.0 to +0.7** | Strong positive relationship |
| **+0.7 to +0.3** | Moderate positive relationship |
| **+0.3 to 0.0** | Weak or no relationship |
| **0.0 to -0.3** | Weak negative relationship |
| **-0.3 to -0.7** | Moderate negative relationship |
| **-0.7 to -1.0** | Strong negative relationship |

> **Example**: r = 0.74 (Budget vs Gross) means earnings and budget move strongly in the same direction.

---

## 🧪 Methods & Tech Stack  

**Tech Used:**  
✅ Python  
✅ Pandas  
✅ Seaborn / Matplotlib  
✅ scipy.stats (Pearson correlation)

**Approach:**  
1. Data cleaning — ensure numeric consistency  
2. Correlation calculations using `pearsonr()`  
3. Scatterplots & regression lines  
4. Heatmap visualization for overview of all correlations

---

## 🧪 Reproducible Code Example

```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
from scipy.stats import pearsonr

df = pd.read_csv('your_dataset.csv')
numeric_cols = ['year', 'score', 'votes', 'budget', 'gross', 'runtime']
corr_matrix = df[numeric_cols].corr()

r_budget_gross, _ = pearsonr(df['budget'], df['gross'])
r_votes_gross, _ = pearsonr(df['votes'], df['gross'])

sns.regplot(x='budget', y='gross', data=df)
plt.title('Budget vs Gross Earnings')
plt.show()

sns.boxplot(x='gross', data=df)
plt.title('Gross Earnings Distribution')
plt.show()

sns.heatmap(corr_matrix, annot=True, cmap='coolwarm', fmt=".2f")
plt.title('Correlation Matrix')
plt.show()
