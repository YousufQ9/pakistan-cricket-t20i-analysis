# pakistan-cricket-t20i-analysis
Analysis of Pakistan Men's Cricket Team T20i performance (2021–2024) using K-Means clustering for player role classification and a custom impact scoring model to identify the Most Valuable Player.

# Pakistan Cricket T20i Performance Analysis (2021–2024)

A data analysis project exploring the performance of the Pakistan Men's Cricket team in T20 International (T20i) matches from 2021 to 2024.
---

## Project Overview

This project investigates three key questions about Pakistan's T20i performance:

1. **Does Pakistan have a home ground advantage?** — Comparing win/loss ratios in home vs. away games.
2. **What player roles exist in the squad, and are players fulfilling them?** — Using K-Means clustering to classify batsmen and bowlers by role.
3. **Who is Pakistan's Most Valuable Player?** — Calculating a per-game impact score for the top 10 players and comparing average impact in wins.

All data was sourced from [ESPNcricinfo](https://www.espncricinfo.com/) and captured as of **November 28, 2024**.

---

## Repository Structure

```
pakistan-cricket-t20i-analysis/
│
├── README.md                        # Project overview and instructions
│
├── Pakistan_Cricket_T20i_Analysis.ipynb   # Main Jupyter Notebook
│
└── Data Sets/                       # All CSV data files used in the analysis
    ├── Match_Results_2021-24.csv    # All T20i match results (2021–2024)
    ├── Batting_Stats.csv            # Aggregate batting stats for Pakistan players
    ├── Bowling_Stats.csv            # Aggregate bowling stats for Pakistan players
    ├── Babar.csv                    # Match-by-match batting data – Babar Azam
    ├── Rizwan.csv                   # Match-by-match batting data – Mohammad Rizwan
    ├── Iftikhar.csv                 # Match-by-match batting data – Iftikhar Ahmed
    ├── Fakhar.csv                   # Match-by-match batting data – Fakhar Zaman
    ├── Shadab(Batting).csv          # Match-by-match batting data – Shadab Khan
    ├── Shaheen.csv                  # Match-by-match bowling data – Shaheen Shah Afridi
    ├── Rauf.csv                     # Match-by-match bowling data – Haris Rauf
    ├── Shadab(Bowling).csv          # Match-by-match bowling data – Shadab Khan
    ├── Nawaz.csv                    # Match-by-match bowling data – Mohammad Nawaz
    └── Wasim.csv                    # Match-by-match bowling data – Mohammad Wasim
```

---

##  Analysis Breakdown

### Part 1 - Team Performance
- Filtered match results to Pakistan games only and removed rain-affected no-result matches
- Calculated overall, home, and away win/loss ratios, visualized as pie charts
- Extracted year-wise win percentages (2021–2024) and plotted a trend line
- **Key Finding:** Pakistan showed no significant home advantage (similar win % at home vs. away), but performance declined sharply from 76.9% in 2021 to 33.3% in 2024

### Part 2 - Player Roles via K-Means Clustering
- **Batting:** Clustered players (min. 10 innings) by Batting Average and Strike Rate into 5 clusters - identifying anchors, aggressors, tail-enders, and underperforming players
- **Bowling:** Clustered players (min. 10 innings) by Bowling Economy and Bowling Strike Rate into 3 clusters - identifying containment bowlers, strike bowlers, and underperformers
- **Key Finding:** A notable cluster of both batsmen and bowlers were not fulfilling their designated roles, potentially contributing to the team's declining win rate

### Part 3 - Most Valuable Player
- Selected the top 5 batsmen (by runs) and top 5 bowlers (by wickets) for analysis
- Calculated a per-game **impact score** for each player using a weighted formula based on benchmarks (50 runs / 140 SR for batsmen; 7 economy / 4 wickets for bowlers)
- Merged individual game data with match results and filtered to Pakistan wins only
- Computed average impact per player across all wins
- **Key Finding:** Shaheen Shah Afridi had the highest average impact (91.69), not Babar Azam as popularly believed. Bowlers consistently outperformed batsmen in contribution to wins

---

## Key Results Summary

| Category | Finding |
|---|---|
| Overall Win % (2021–2024) | 54.22% |
| Home Win % | 54.55% |
| Away Win % | 54.10% |
| Best year | 2021 (76.92%) |
| Worst year | 2024 (33.33%) |
| Most Valuable Player | Shaheen Shah Afridi (avg. impact: 91.69 in wins) |

---

## Libraries Used

```python
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np
from sklearn.cluster import KMeans
from collections import defaultdict
```

---

## How to Run

1. Clone the repository:
   ```bash
   git clone https://github.com/YousufQ9/pakistan-cricket-t20i-analysis.git
   cd pakistan-cricket-t20i-analysis
   ```

2. Install dependencies (all standard libraries):
   ```bash
   pip install pandas matplotlib numpy scikit-learn
   ```

3. Open the notebook:
   ```bash
   jupyter notebook Pakistan_Cricket_T20i_Analysis.ipynb
   ```

4. Run all cells from top to bottom. Estimated runtime: **< 1 minute**

> Ensure the `Data Sets/` folder is in the same directory as the notebook, as all CSV files are read from relative paths.

---

## Data Source

All data was manually collected from [ESPNcricinfo](https://www.espncricinfo.com/) on **November 28, 2024**. Any matches played after this date are not included.

---

## Notes

- Only T20i matches involving Pakistan are included in the analysis
- Players with fewer than 10 innings/appearances were excluded from role clustering to avoid bias from small sample sizes
- Impact scores are capped at 100 per game
