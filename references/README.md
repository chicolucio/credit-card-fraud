# Data Dictionary

Data source: [Kaggle](https://www.kaggle.com/mlg-ulb/creditcardfraud)

| Column Name    | Description                                                  | Data Type |
|----------------|--------------------------------------------------------------|-----------|
| `Time`         | Interval in seconds between each transaction and the first   | float     |
| `Vx`           | PCA result of the original variables                         | float     |
| `Amount`       | Value of each transaction                                    | float     |
| `Class`        | Transaction classification: genuine (0) or fraudulent (1)    | int       |

In the Kaggle dataset description, some explanations about the variables are provided:

- For confidentiality reasons, the identifiers of most of the original variables are not
disclosed;
- The variables represented as V1, V2, ... V28 are the result of a principal component
analysis (PCA) transformation, a technique used to condense the information contained in
several original variables into a smaller set of statistical variables (components) with
minimal loss of information. In this work, we will examine some consequences of this
transformation in our analysis.
