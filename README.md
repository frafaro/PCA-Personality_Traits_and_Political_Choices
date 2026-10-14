# Political Parties and Personalities — Principal Components Analysis

> **Disclaimer**
> This study was carried out on my own initiative during my internship. For privacy reasons, I can share the PDF of the R Markdown file, but not the dataset or any other private information about the survey respondents.

This README summarizes **Section 3) PRINCIPAL COMPONENTS ANALYSIS** of the study *Political Parties and Personalities* (Francesco Farolfi, 03/11/2022).

## Goal

The study investigates the relationship between HEXACO personality traits and the Spanish political parties that respondents chose when answering the survey question:

> *"¿Cuál de los siguientes partidos políticos cree que apoya la lucha contra el cambio climático?"*
> ("Which of the following political parties do you think supports the fight against climate change?")

In this section, a Principal Components Analysis (PCA) is run to find out whether there are principal components able to explain the correlation between the 24 personality traits and the 11 political parties.

## Methodology

1. **Input data** — The PCA is run on the correlation table between personality traits and political parties (built in Section 1), so that all data share the same dimension. The table is arranged with the political parties as observations (rows) and the 24 personality traits as variables (columns).
2. **Model fitting** — The PCA is computed with R's `prcomp` command; the summary of the model is analyzed by studying the scores of the principal components in search of patterns.
3. **Visualization** — Results are plotted with a **biplot** (`fviz_pca_biplot`, with confidence ellipses). A new categorical variable called **`ideology`** is created to color the parties as *izquierda* (left) or *derecha* (right), making it easier to read the data and spot correlations with the principal components.
4. **Validation** — A correlation matrix between the original variables and the scores of the first two principal components is computed to statistically back up what the biplot suggests.

## Results

### Variance explained

| Component | Proportion of variance | Cumulative |
|-----------|------------------------|------------|
| PC1 | 42.75% | 42.75% |
| PC2 | 25.34% | 68.09% |
| PC3 | 9.82% | 77.91% |
| PC4 | 7.47% | 85.38% |

The first two components together explain **68.09%** of the variance, which is considered a good result to proceed with the analysis (four components are needed to reach at least 85%).

### Party scores on PC1: a left/right split

Looking at the PC scores of each political party, a clear pattern emerges on **PC1**:

- **Derecha (right-wing) parties** — VOX, PP, PNV, CIUDADANOS, UPN — have **negative** PC1 scores.
- **Izquierda (left-wing) parties** — PODEMOS, IZQUIERDA UNIDA, MÁS PAÍS, BILDU, COMPROMÍS — have **positive** PC1 scores.

The biplot (PC1 on the x-axis, PC2 on the y-axis) shows an evident split between derecha (red) and izquierda (blue) parties along PC1; the `ideology` variable and the confidence ellipses make this pattern visually clear.

### Trait correlations with PC1 and PC2

To statistically prove the relation between personality traits and parties suggested by the biplot, the PC1 and PC2 scores were extracted and correlated with the original data:

- **PC1** — positive correlation with **Modesty (0.74), Patience (0.76), Prudence (0.94), Aesthetic Appreciation (0.87), Unconventionality (0.96) and Inquisitiveness (0.67)**; negative correlation with **Perfectionism (−0.76) and Creativity (−0.62)**.
- **PC2** — positive correlation with **Social Self-Esteem (0.93), Flexibility (0.71), Diligence (0.81) and Organization (0.65)**; negative correlation with **Sociability (−0.86)**.

Since izquierda parties score positively on PC1, traits such as **prudence, unconventionality, aesthetic appreciation and modesty are more connected to left-wing parties** being perceived as fighting climate change.

### Validation test on Prudence

As a final check, the trait **Prudence** (the one most correlated with the left-wing parties, r = 0.94 with PC1) was tested against the raw data by counting votes in the first versus the last quantile of Prudence:

| Party | Votes (1st quantile, low Prudence) | Votes (4th quantile, high Prudence) |
|----------|-----------------------------------:|------------------------------------:|
| PODEMOS | 774 | 1079 |
| IZQUIERDA UNIDA | 594 | 972 |
| MÁS PAÍS | 468 | 683 |
| BILDU | 126 | 270 |

As expected, respondents with **higher Prudence scores chose izquierda parties more often** as parties they believe are fighting climate change, confirming the model.

## Conclusion

The PCA shows great results. The most interesting finding is the relation between the observations (political parties) and PC1, where a clear pattern appears: **derecha parties have negative scores and izquierda parties have positive scores**. Furthermore, the correlations between the personality traits and the PC1/PC2 scores prove that some personality traits are more connected than others to the choice of a political party perceived as fighting against climate change.
