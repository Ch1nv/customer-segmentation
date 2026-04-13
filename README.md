# Customer Segmentation
## Description
This project is based on a [Kaggle notebook](https://www.kaggle.com/code/weddou/cluster-analysis-identify-customers-behaviors/notebook) and a [Kaggle dataset](https://www.kaggle.com/datasets/vetrirah/customer/data).
This project is based on a Kaggle notebook and dataset. The goal is to segment customers into four distinct groups and analyze the characteristics and behaviors of each segment.

## Dataset
- Dataset: [Customer Segmentation](https://www.kaggle.com/datasets/vetrirah/customer/data)
- Column description: We drop `Var_1` and `Segmentation` since they have no help of our analysis. We construct a additional column `AgeCap` to group age into `0-18`, `19-25`, `26-35`, `36-46`,`47+`.

| Column            | data type | Description                                                        |
|-------------------|----------|--------------------------------------------------------------------|
| ID                | int64    |
| Gender            | str      |
| Ever_Married      | str      | Marital status of the customer.                                    |
| Age               | int64    |
| Graduated         | str      |
| Profession        | str      |
| Work_Experience   | float64  | Work Experience in years.                                          |
| Spending_Score    | str      |
| Family_Size       | float64  | Number of family members for the customer (including the customer). |

- Missing values:

| Column          | count  |
|-----------------|--------|
| ID              | 0      |
| Gender          | 0      |
| Ever_Married    | 140    |
| Age             | 0      |
| Graduated       | 78     |
| Profession      | 124    |
| Work_Experience | 829    |
| Spending_Score  | 0      |
| Family_Size     | 335    |
| AgeCat          | 0      |


## Missing Values
We try to find ways to insert appropriate values of each missing values of `Ever_Married`, `Graduated`, `Profession`, `Work_Experience`, and `Family_Size`.

### `Ever_Married`
- All average / high `Spending_Score` are married.
- People with Healthcare profession are mostly not married.
- 47+ People are mostly married / 19-25 People are mostly not married / 26-35 People are mostly not married.
- For people in 36-46, they're mostly married, apart for those in the Marketing field.

### `Graduated`
- 0-18 People are mostly not graduated / 19-25 People are mostly not graduated / 47+ People are mostly graduated
- Most Artist are graduated.
- There is more chance that married people are Graduated.

### `Profession`
- People that are 60+ years old are mostly Artist if they have an average `Spending_Score` and are mostly Lawyers if they have a High/Low `Spending_Score`.
- Most graduates are Artist.
- 0-18 and 19-25 People are mostly with Healthcare profession
- 47-60 People are mostly Artist.
- Not Married People have a Healthcare profession / Married People are Artists.

### `Work_Experience`
- There weren't too many statistical changes after using the `ffill()` filling method, so we use it.

### `Family_Size`
- There weren't too many statistical changes after using the `ffill()` filling method, so we use it.

## Processing
We will encode our discrete fields for our machine learning model so things like (Yes/No) (Male / Female) will become (1/0).

| Profession    | Number |
|---------------|--------|
| Healthcare    | 1      |
| Engineer      | 2      |
| Lawyer        | 3      |
| Entertainment | 4      |
| Artist        | 5      |
| Executive     | 6      |
| Doctor        | 7      |
| Homemaker     | 8      |
| Marketing     | 9      |

| Spending Score | Number |
|----------------|--------|
| Low            | 1      |
| Average        | 2      |
| High           | 3      |


## Clustering

Since the dataset contains both numerical and categorical features, we apply the K-Prototypes clustering algorithm, which combines the strengths of K-Means (for numerical data) and K-Modes (for categorical data).
- Categorical variables: `Gender`, `Ever_Married`, `Graduated`, `Profession`, `Work_Experience`, `Spending_Score`
- Numerical variables: `Age`, `Family_Size`


## Analysis
We have 4 groups of our customers, we analyze each of them.

### Balanced Family Professionals (Group 1)
This cluster represents stable, career-focused individuals who successfully balance professional responsibilities with family life. Their consumption patterns reflect practicality, moderate purchasing power, and a preference for cost-effective yet high-quality products.

**Business Insight:**
This segment is ideal for mid-range products, family-oriented services, and value-driven marketing strategies. Promotions emphasizing quality, practicality, and long-term value are likely to resonate well with this group.

| Feature        | Description                                      |
|----------------|--------------------------------------------------|
| Family Size    | Mostly 2 / Sometimes 1 / Sometimes 3             |
| Average Age    | 40                                               |
| Jobs           | Mostly Artist / Entertainment / Engineer         |

| Categorical variables | Yes | No |
|-----------------------|--|--|
| Ever Married          | 66.1% | 33.9%|
| Graduated             | 76.3% | 23.7% |

|                   | Low    | Avg     | High  |
|-------------------|--------|---------|-------|
| Spending Score    | 54.8%  | 33.7%   | 11.5% |



<p align="center">
  <img src="images/Ever_Married_Cluster_1.png" width="30%">
  <img src="images/Graduated_Cluster_1.png" width="30%">
  <img src="images/Spending_Score_Cluster_1.png" width="30%">
</p>

<p align="center">
  <em>Ever Married (left) vs Graduated (mid) vs Spending Score (right)</em>
</p>

<p align="center">
  <img src="images/Family_Size_Cluster_1.png">
</p>

<p align="center">
  <em>Family Size </em>
</p>

<p align="center">
  <img src="images/Profession_Cluster_1.png">
</p>

<p align="center">
  <em>Profession </em>
</p>

### Established Affluent Professionals (Group 2)
This segment represents financially secure and experienced individuals who are likely to be in advanced stages of their careers. Their consumption patterns reflect a balance between value consciousness and the ability to afford higher-quality products, making them a relatively affluent and stable consumer group.

**Business Insight:**
This segment is well-suited for premium and high-quality products, financial services, healthcare, and lifestyle upgrades. Marketing strategies that emphasize reliability, brand reputation, and long-term value are likely to resonate strongly with this group.

| Feature        | Description                               |
|----------------|-------------------------------------------|
| Family Size    | Mostly 2 / Sometimes 3 / Sometimes 4      |
| Average Age    | 54                                        |
| Jobs           | Mostly Artist / Entertainment / Executive |

| Categorical variables | Yes   | No    |
|-----------------------|-------|-------|
| Ever Married          | 87.5% | 12.5% |
| Graduated             | 79.4% | 20.6% |

|                   | Low   | Avg   | High  |
|-------------------|-------|-------|-------|
| Spending Score    | 38.2% | 43.9% | 17.9% |

<p align="center">
  <img src="images/Ever_Married_Cluster_2.png" width="30%">
  <img src="images/Graduated_Cluster_2.png" width="30%">
  <img src="images/Spending_Score_Cluster_2.png" width="30%">
</p>

<p align="center">
  <em>Ever Married (left) vs Graduated (mid) vs Spending Score (right)</em>
</p>

<p align="center">
  <img src="images/Family_Size_Cluster_2.png">
</p>

<p align="center">
  <em>Family Size </em>
</p>

<p align="center">
  <img src="images/Profession_Cluster_2.png">
</p>

<p align="center">
  <em>Profession </em>
</p>


### Senior Wealth-Diverse Elites (Group 3)
This cluster represents a mature and experienced population with diverse financial behaviors, ranging from highly frugal individuals to relatively affluent consumers. The clear polarization in spending patterns suggests significant variation in financial capacity and lifestyle preferences within this group.

**Business Insight:**
This segment requires differentiated strategies. High-spending individuals may respond well to premium healthcare, luxury services, and personalized experiences, while low-spending individuals may prioritize essential services, affordability, and reliability. Segmentation within this group is crucial to effectively address their diverse financial behaviors.

| Feature        | Description                          |
|----------------|--------------------------------------|
| Family Size    | Mostly 2 / Sometimes 1 / Sometimes 3 |
| Average Age    | 74                                   |
| Jobs           | Mostly Lawyer / Artist / Executive   |

| Categorical variables | Yes   | No    |
|-----------------------|-------|-------|
| Ever Married          | 95.2% | 4.8%  |
| Graduated             | 63.1% | 36.9% |

|                   | Low   | Avg   | High  |
|-------------------|-------|-------|-------|
| Spending Score    | 46.0% | 13.2% | 40.9% |

<p align="center">
  <img src="images/Ever_Married_Cluster_3.png" width="30%">
  <img src="images/Graduated_Cluster_3.png" width="30%">
  <img src="images/Spending_Score_Cluster_3.png" width="30%">
</p>

<p align="center">
  <em>Ever Married (left) vs Graduated (mid) vs Spending Score (right)</em>
</p>

<p align="center">
  <img src="images/Family_Size_Cluster_3.png">
</p>

<p align="center">
  <em>Family Size </em>
</p>

<p align="center">
  <img src="images/Profession_Cluster_3.png">
</p>

<p align="center">
  <em>Profession </em>
</p>

### Young Family Starters (Group 4)
This cluster represents individuals at an early life stage, facing relatively high financial pressure due to growing family responsibilities and limited income. Their overall behavior reflects a need to carefully manage expenses while supporting household needs.

**Business Insight:**
This segment is highly price-sensitive and responds well to affordable, essential, and family-oriented products. Promotions such as discounts, bundled offers, and value deals are likely to be effective. Services related to childcare, basic healthcare, and entry-level financial planning may also resonate strongly with this group.

| Feature        | Description                          |
|----------------|--------------------------------------|
| Family Size    | Mostly 4 / Sometimes 3 / Sometimes 2 |
| Average Age    | 26                                   |
| Jobs           | Mostly Healthcare / Doctor / Artist  |

| Categorical variables | Yes   | No    |
|-----------------------|-------|-------|
| Ever Married          | 82.0% | 18.0% |
| Graduated             | 37.4% | 62.6% |

|                   | Low   | Avg  | High |
|-------------------|-------|------|------|
| Spending Score    | 88.5% | 7.4% | 4.1% |

<p align="center">
  <img src="images/Ever_Married_Cluster_4.png" width="30%">
  <img src="images/Graduated_Cluster_4.png" width="30%">
  <img src="images/Spending_Score_Cluster_4.png" width="30%">
</p>

<p align="center">
  <em>Ever Married (left) vs Graduated (mid) vs Spending Score (right)</em>
</p>

<p align="center">
  <img src="images/Family_Size_Cluster_4.png">
</p>

<p align="center">
  <em>Family Size </em>
</p>

<p align="center">
  <img src="images/Profession_Cluster_4.png">
</p>

<p align="center">
  <em>Profession </em>
</p>


## Final Conclusion

This analysis identifies four distinct customer segments with clear differences in demographics, family structure, and spending behavior.

Among them, the **Balanced Family Professionals** and **Established Affluent Professionals** represent the most stable and commercially valuable segments. They demonstrate moderate to strong purchasing power, stable family structures, and consistent consumption patterns, making them ideal targets for mid-range to premium products and long-term customer engagement strategies.

The **Senior Wealth-Diverse Elites** segment exhibits a unique polarization in spending behavior, indicating the presence of both highly conservative and high-value customers. This suggests that a more refined, sub-segmentation strategy may be necessary to effectively capture value from this group.

In contrast, the **Young Family Starters** segment is characterized by limited financial capacity and high price sensitivity. While their immediate commercial value may be lower, they represent a potential long-term growth segment as their income and purchasing power increase over time.

Overall, this segmentation highlights the importance of differentiated marketing strategies. Rather than applying a one-size-fits-all approach, businesses can leverage these insights to tailor products, pricing, and communication strategies to better align with the needs and behaviors of each customer group.