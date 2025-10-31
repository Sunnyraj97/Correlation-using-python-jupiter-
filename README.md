

# Correlation Analysis: Budget, Gross Earnings, Production Company and Votes

## Objective  
Analyze relationships among movie budget, gross earnings, votes, runtime, and production company using Python. Focus on Pearson correlation to identify strength and direction of linear relationships, supported by visualizations.

## Hypotheses  
- Budget is strongly correlated with Gross Earnings.  
- Production Company is strongly correlated with Gross Earnings.

## Key Findings  
- **Budget vs. Gross Earnings:** Strong positive correlation (r = 0.74), confirming that higher budgets tend to align with higher gross earnings.  
- **Production Company vs. Gross Earnings:** Weak correlation (r = 0.15), indicating production company is not a strong linear predictor of gross earnings in this dataset.  
- **Votes vs. Gross Earnings:** Moderate to strong positive correlation (r = 0.614), suggesting more votes associate with higher earnings.

## Data Insights  
- Budget is the strongest numerical predictor of gross earnings.  
- Audience engagement (votes) positively relates to revenue, reflecting popularity impact.  
- Other factors beyond production company likely influence gross earnings more significantly.

## Methods  
- Calculated Pearson correlation coefficients using cleaned numeric data.  
- Visualized relationships using scatter plots with regression lines, box plots, and heatmaps of correlation matrices.

## Reproducibility  
Use Python libraries (pandas, seaborn, scipy) to compute correlations and generate visualizations. Below is an example snippet:

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
```

## Interpretation Scale  
- +1 = perfect positive linear relationship  
- 0 = no linear relationship  
- -1 = perfect negative linear relationship

## Data Notes
- The strong positive correlation between budget and gross earnings suggests budget planning may affect revenue expectations.
- The low correlation for production company indicates that other factors (marketing, genre, release timing) likely influence gross earnings more significantly.
- Votes reflect audience engagement and are meaningfully related to revenue.

## Limitations & Next Steps  
- Correlation does not imply causation; further modeling needed for causal insights.  
- Production company’s categorical nature limits its direct correlation insight; encoding and advanced models may reveal nonlinear effects.  
- Explore metrics like ROI and multivariate regression for deeper understanding.

