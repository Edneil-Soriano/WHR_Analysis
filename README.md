#  World Happiness Report Analysis

This project analyzes the **World Happiness Report (WHR)** data from 2015 using Python. We explore how happiness scores relate to other factors like GDP per capita, family, life expectancy, freedom, government corruption, and generosity. Using a mix of regression models, dimensionality reduction (PCA), clustering (k-means), and correlation analysis, we extract insights about what matters most—and how countries compare.

---

##  Dataset

**Source**: https://www.kaggle.com/datasets/unsdsn/world-happiness <br/>
**Standardization**: All six features were scaled and mean-centered using [StandardScaler](https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.StandardScaler.html) to ensure fair comparisons in modeling and PCA.

---

##  Libraries Used

The following Python libraries are used:

- `pandas` — for data manipulation
- `numpy` — for numerical operations
- `matplotlib.pyplot` — for plotting
- `seaborn` — for statistical visualizations
- `scikit-learn` — for PCA and clustering
- `statsmodels` — for regression analysis

---

##  Project Walkthrough

### 1. **Loading and Inspecting the Data**

We load the CSV files for each year into a dictionary and inspect their contents:

***whr = {
    "2015.csv": pd.read_csv("data/2015.csv"), <br/>
    "2016.csv": pd.read_csv("data/2016.csv"), <br/>
    "2017.csv": pd.read_csv("data/2017.csv"), <br/>
    "2018.csv": pd.read_csv("data/2018.csv"), <br/>
    "2019.csv": pd.read_csv("data/2019.csv"), <br/>
}***  <br/>

Note that only the 2015 file was used for most analysis. 


### 3. **Visualizing Feature CDFs**
<img width="664" alt="2015-2019" src="https://github.com/user-attachments/assets/5b87a672-3225-4592-b6dd-587640123f38" />    <br/>
Visualizing each feature shows little variation to the overall trend based on year. Hence, modelling results will vary only slightly allowing us to just analyze a single year. 

### 4. **Linear Regression Modelling**
![Regression Plot](https://github.com/Edneil-Soriano/WHR_Analysis/raw/main/figures/Regression.png)
We applied:
- **Linear Regression**
- **Ridge Regression** (with fixed and CV-based regularization)
- **LASSO Regression** (for feature selection and sparsity)

***Implication***:  
Across all models, **Family**, **Economy**, and **Health** consistently stood out as the top contributors to happiness.  
- LASSO shrinks coefficients for **Generosity** and **Trust** close to zero, confirming their weaker predictive power.
- Cross-validation helped avoid overfitting while preserving feature importance rankings.

---


### 5. **Principal Component Analysis (PCA)**
![Correlation Matrix](https://github.com/Edneil-Soriano/WHR_Analysis/blob/main/figures/correlation-matrix.png) <br/>
We visualized the Pearson correlation matrix between all features.

**Implication**:  
- **Economy** strongly correlates with both **Health** and **Family**.
- Investing in the economy has **compound benefits**—it indirectly boosts other key happiness features.
  
This insight is valuable for **policy-making**: improving a single metric (Economy) can yield **multi-dimensional happiness gains**.

---

### 5. **PCA Scree Plot**
![Scree Plot](https://github.com/Edneil-Soriano/WHR_Analysis/blob/main/figures/scree-plot.png)
Principal Component Analysis (PCA) reduced the 6-dimensional feature space into 2 dimensions for easier visualization.

** Implication**:  
The first two principal components (PC1 and PC2) capture about **70% of the total variance**. This is a good trade-off between simplification and fidelity—perfect for clustering and visual pattern detection.

---


### 6. **Clustering with K-Means**
![Regression Plot](https://github.com/Edneil-Soriano/WHR_Analysis/blob/main/figures/clusterk2.png)
![Regression Plot](https://github.com/Edneil-Soriano/WHR_Analysis/blob/main/figures/clusterk5.png)
We applied **k-means clustering** on the 2D PCA-transformed data:
- `k = 2` → Divides countries into broad **“Happy”** and **“Unhappy”** groups.
- `k = 5` → Reveals more nuanced happiness levels.

** Implication**:
- **Switzerland** and the **U.S.** appear in the top clusters.
- **Syria** and **Burundi** are grouped in the lower clusters.
- Interestingly, **Togo**, the country with the lowest WHR score, is **not** the furthest in PCA space. This suggests that **a single score may not capture all dimensions of happiness**.
- The **Philippines** ranks relatively high, reinforcing cultural/contextual resilience despite economic limits.

---

## Summary of Key Findings
| **Which features matter most?** | Family, Economy, and Health |
| **What can we ignore?** | Generosity and Trust (minor impact) |
| **Can we visualize happiness effectively?** | Yes—PCA reduces dimensions while retaining 70% of variance |
| **Do clusters reveal structure?** | Yes—countries cluster logically into happy/unhappy tiers |
| **Where should we invest first?** | Economy: affects Health & Family due to strong correlation |

---

## Insights and Conclusions
Happiness scores are generally influenced most by Family, Economy, and Health, while Generosity and Trust in government had minimal impact. PCA reduced the dataset to two PCs that captured ~70% of the variance, making patterns easier to visualize. 

Some regional patterns were evident in PCA space, though clustering also revealed similarities between countries that are not geographically close. For instance, the Philippines ranked relatively high despite its lower GDP, suggesting the influence of cultural and social resilience. In contrast, Togo did not appear at the extreme end of the PC space despite having the lowest WHR score, which suggests that a single score may not capture all dimensions of national well-being.

Given the strong correlation between Economy with Health and Family, investments in economic development may yield compound benefits across other happiness indicators. These findings also suggest that while economic performance is important, broader social and cultural structures contribute significantly to how people percieve happiness.

