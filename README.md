
# 📊 Pixar-film-analysis

This project explores the intersection between film budgets, box office performance, and critical/audience reception. It analyzes a dataset of major film releases using Python to uncover business-relevant insights, such as return on investment (ROI), box office trends, and the role of critic vs. audience ratings.

---

## 📌 Table of Contents

- [Project Overview](#project-overview)
- [Dataset](#dataset)
- [Business/Research Questions](#businessresearch-questions)
- [Methodology](#methodology)
- [Analysis and Visualizations](#analysis-and-visualizations)
- [Findings](#findings)
- [Recomendations](#recomendations)

---

## 🧠 Project Overview
- Identify which films yielded the highest ROI and what contributed to their success.
- Compare domestic (US/Canada) vs. international revenue performance.
- Investigate the relationship between critical/audience ratings and commercial success.
- Use data-driven methods to suggest strategic decisions for film production and marketing.

---

## 📂 Dataset

- **Source:** [Link to dataset]
- **Format:** CSV
---

## ❓ Business/Research Questions
-	Which films had the highest return on investment (ROI = (box_office_worldwide - budget) / budget)?
-	Is there a correlation between budget and worldwide box office performance?
-	Do films typically earn more domestically (US/Canada) or internationally?
-	Which films had the highest international share of revenue (box_office_other / box_office_worldwide)?
-	Do higher-budget films always perform better than lower-budget ones?
-	Are there films where critics and audiences strongly disagreed (e.g., high RT score but low Cinema Score)?
-	Which high-budget films had the worst ROI? What were their ratings?
-	Which low-budget films overperformed? What factors contributed?
---

## 🛠 Methodology

Outline your process:
- Data Cleaning
- Missing values in the 'cinema_score' column were filled with 'unknown'
- Missing values in the 'budget' column were filled with 0
- changed the 'release_date' column from object to datetime dtype
- **Exploratory Data Analysis (EDA)**
- I created a column for the budget category
 ``` python
def categorize_budget(budget):
    if budget <= 60000000:
        return 'Low Budget'
    elif budget <= 100000000:
        return 'Moderate Budget'
    elif budget <= 150000000:
        return 'High Budget'
    else:
        return 'Very High Budget'
```
``` python
df['budget_category'] = df['budget'].apply(categorize_budget)
```
- I created a new column and calculated the ROI

``` python
df['ROI'] = (df.box_office_worldwide - df.budget) / df.budget
```
- created a column to calculate the % of the international revenue share
``` python
df['intenational_share'] = (df.box_office_other / df.box_office_worldwide) * 100
```
---

## 📈 Analysis and Visualizations
``` python
# Which films had the highest return on investment?
df.groupby('film')['ROI'].sum().sort_values(ascending = False)
```
``` python
# Is there a correlation between budget and worldwide box office performance?
df.groupby('budget_category')['box_office_worldwide'].sum().sort_values(ascending= False)
```
``` python
# Do films typically earn more domestically (US/Canada) or internationally?
total_sum_us = df['box_office_us_canada'].sum()
total_sum_others = df['box_office_other'].sum()

```
``` python
#Which films had the highest international share of revenue (box_office_other / box_office_worldwide)?
df[['film','intenational_share']].sort_values(by = 'intenational_share', ascending = False)
```
``` python
# Do higher-budget films always perform better than lower-budget ones?
df.groupby('budget_category')['ROI'].sum().sort_values(ascending= False)
```
---

## 📌 Findings

- Tory story has a ROI of (12.147) followed by finding Nemo (8.266) and inside out 2 (7.490)
- Very high budget films performed exceptionally well with a sum total of ($124,833,591,462), followed by high budget films ($2,099,645,228) and Moderate budget films ($2,013,815,346) it is also worth to note that very high budget films are 18 in number while high budget films and Moderate budget films are 5 and 3 respectively.
- Films earn less domestically in the US/Canada box office at ($6,931,243,909) While internationally films earn ($10,111,357,027)
- Soul and Luca had the highest share of international revenue at 99.2% and 97.4% respectively.
- Very high budget films perform better followed by Moderate budget then high budget.
- Cars 2, Cars 3 are films where critics and audiences strongly disagree.
- Turning red (-0.875), Onward (-0.188), Soul (-0.187) are high budget films that had the worst ROI.
- Toy story (12.147) performed the most followed by finding nemo (8.266) and the incredible (5.863) where the low budget films that overperformed with High ROI 


---

## 🧾 Recomendations
- Allocate more funding toward well-written, lower-budget animations or family films, especially from established franchises. These films can yield impressive profits while minimizing risk
- Don’t assume high budget equals success. Prioritize strong scripts, branding, and marketing over sheer budget size.
-  Use ROI as a core success metric, not just worldwide gross. It’s more reflective of actual business performance and long-term strategy.



---

## ⚙️ Technologies Used

- Python (Pandas, NumPy)
- Jupyter Notebook
-  Power BI 

