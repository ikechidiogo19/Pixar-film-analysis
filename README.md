
# 📊 Pixar-film-analysis

This project analyzes a dataset of animated films, focusing on financial performance, critical reception, and audience feedback. Key metrics include budget, box office earnings (domestic and international), return on investment (ROI), and review scores from platforms such as Rotten Tomatoes, Metacritic, and IMDb.

---

## 🧠 Project Overview
The goal of this analysis is to understand how different factors like budget, critical scores, and release strategy impact a film's financial success. The study looked into ROI, audience vs critic perception, domestic vs international revenue, and the influence of budget size.

---

## 📂 Dataset

- **Source:** <a href = "https://github.com/ikechidiogo19/Pixar-film-analysis/blob/main/pixar_films.csv"> dataset </a>
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
- Very high budget films performed exceptionally well with a sum total of ($124,833,591,462), followed by high budget films ($2,099,645,228) and Moderate budget films ($2,013,815,346) 
- International markets contributed more revenue ($10.1B) than domestic ($6.9B).
- Films like Soul and Luca earned over 97% of their box office revenue internationally.
- Very high budget films perform better followed by Moderate budget then high budget.
- Cars 2, Cars 3 are films where critics and audiences strongly disagree.
- Turning Red, Onward, and Soul had negative ROI despite large budgets, indicating underperformance possibly due to audience reception..
- Toy story (12.147) performed the most followed by finding nemo (8.266) and the incredible (5.863) where the low budget films that overperformed with High ROI 


---

## 🧾 Recomendations
- Allocate more funding toward well-written, lower-budget animations or family films, especially from established franchises. These films can yield impressive profits while minimizing risk
- Since international revenue often surpasses domestic, consider tailoring marketing and localization strategies for global audiences, especially in Europe and Asia.
-  Use ROI as a core success metric, not just worldwide gross. It’s more reflective of actual business performance and long-term strategy.

---
## Limitations
- it is also worth to note that very high budget films are 18 in number while high budget films and Moderate budget films are 5 and 3 respectively.

## ⚙️ Technologies Used

- Python (Pandas, NumPy)
- Jupyter Notebook
-  Power BI 

