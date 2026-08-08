# Are Tanks Really Overpowered?

A causal inference analysis investigating whether Tank-class champions in **League of Legends** have an inherent win-rate advantage after accounting for differences in champion base statistics.

## Overview

Tanks are frequently criticized by League of Legends players for being difficult to kill while still providing meaningful damage and utility. However, simply comparing the win rates of Tanks and non-Tanks does not tell us whether being classified as a Tank actually causes a higher win rate.

Tank champions naturally differ from other champions in characteristics such as health, armor, magic resistance, movement speed, and other base statistics. These differences create a confounding problem when comparing the two groups directly.

This project uses **Propensity Score Matching (PSM)** to create more comparable groups of Tank and non-Tank champions and estimate the effect of Tank-class status on win rate. The primary question is:

> **Does Tank-class champion status causally increase win rate after adjusting for baseline champion characteristics?**

## Methods

The analysis treats:

- **Treatment:** Tank-class status
- **Control:** Non-Tank status
- **Outcome:** Champion win rate
- **Target population:** League of Legends champions

Propensity scores were estimated from champion characteristics including:

- Base HP and HP growth
- Base armor and armor growth
- Base magic resistance and resistance growth
- HP regeneration
- Movement speed
- Attack speed
- Attack damage
- Resource type

Several matching approaches were explored, with **1:1 nearest-neighbor propensity score matching** used for the primary analysis.

Covariate balance was evaluated before and after matching using standardized mean differences and diagnostic plots.

The matched sample was then analyzed using regression to estimate the association between Tank status and win rate after adjustment for the selected champion characteristics.

All statistical analysis was performed in **R 4.4.1** with a significance level of **α = 0.05**.

## Results

After propensity score matching, the analysis contained **56 champions: 28 Tanks and 28 matched non-Tanks**.

The estimated Tank treatment effect from the final regression model was approximately:

**+0.0025**, or about a **+0.25 percentage-point difference in win rate**.

This effect was substantially smaller than the project's pre-specified minimum meaningful effect of **3 percentage points**.

Under the study's decision framework, the results therefore did **not provide evidence that Tank-class status meaningfully increases champion win rate after accounting for observed champion characteristics**.

In other words, the analysis does not support the idea that Tanks are inherently overpowered simply because they belong to the Tank class.

## Data

Champion information was assembled from two League of Legends datasets:

1. [League of Legends Champion Stats – Season 12](https://www.kaggle.com/datasets/vivovinco/league-of-legends-champion-stats)
2. [League of Legends Champions](https://www.kaggle.com/datasets/cutedango/league-of-legends-champions)

Missing champion information was supplemented using the
[League of Legends Wiki](https://wiki.leagueoflegends.com/en-us/List_of_champions).

The datasets were joined by champion name and cleaned prior to analysis.

## R Packages

The analysis uses several R packages, including:

- `tidyverse`
- `MatchIt`
- `cobalt`
- `dagitty`
- `GGally`
- `tinytable`
- `optmatch`
- `pwr`
- `readr`

## Limitations

This is an observational analysis, so the causal interpretation depends on assumptions about the measured covariates.

Several potentially important factors were not included, particularly:

- Champion item builds
- Player rank
- Player skill
- Team composition
- Champion role and matchup effects
- Patch-specific balance changes

Items may be especially important because changes to Tank-oriented items can disproportionately affect Tank champions. Because these factors are not fully observed, the assumption of conditional ignorability is difficult to guarantee.

The results should therefore be interpreted as evidence about Tank status **conditional on the observed champion characteristics**, rather than definitive proof that Tank status can never affect competitive performance.

## Key Takeaway

After matching Tank and non-Tank champions on their baseline characteristics, **Tank status itself was not associated with a practically meaningful increase in win rate**.

The results suggest that the perception of Tanks as "overpowered" cannot be explained simply by belonging to the Tank class.

## References

The methodology draws primarily on work on propensity scores and observational causal inference, including:

- Rosenbaum & Rubin (1983), *The Central Role of the Propensity Score in Observational Studies for Causal Effects*
- Rosenbaum, *Design of Observational Studies*
- King & Nielsen (2019), *Why Propensity Scores Should Not Be Used for Matching*
- Senn et al. (2007), *Stratification for the Propensity Score Compared with Linear Regression Techniques*
- Wan (2025), *Propensity Score Matching: Should We Use It in Designing Observational Studies?*

See the full project report for methodological details, diagnostics, and complete references.
