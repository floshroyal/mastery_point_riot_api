# League of Legends: Champion Mastery’s Effect on Bronze ELO Win Rate

## Project Summary

This project analyzes the effect of champion mastery points on match victory for players in the Bronze IV league using the Riot Games API and Logistic Regression. The study was designed to test whether specialized champion knowledge meaningfully influences a player's ability to win low-ranking games. The analysis concluded that champion mastery points have no statistically significant effect on match outcomes, leading to the rejection of the initial hypothesis.

---

## Hypothesis & Goal

**Hypothesis:**  
Higher champion mastery points (a proxy for player experience on a specific champion) will lead to a higher probability of winning in low-ELO games.

**Goal:**  
To build a robust data pipeline and statistical model that quantifies the relationship between the team-wide difference in mastery points and the final match outcome (Win/Loss).

---

## Methodology & Data Engineering

This project involved data acquisition from the Riot Games API, error handling, data cleaning, and data enrichment.

**Data Acquisition:**  
Player PUUIDs were collected from the League-Exp-v4 endpoint for Bronze IV accounts.

**Match Data Collection:**  
A dataset of 1000 ranked solo queue matches was retrieved using the Match-V5 endpoint.

**Data Enrichment:**  
The Champion-Mastery-v4 endpoint provided the mastery score for the specific champion each player used in the match.

**Persistence:**  
All raw and processed data were saved to JSON and CSV files to maintain reproducibility and avoid re-fetching data under API rate limits.

---

## Data Cleaning

To ensure the Logistic Regression model was trained on valid and competitive data, the following filtering rules were implemented:

**Remake / Early Surrender Filter:**  
Matches with a duration of less than 8 minutes (480 seconds) were excluded.

**AFK Player Filter:**  
Matches were removed if any player demonstrated low-effort or AFK-like behavior, such as extremely low activity, near-zero combat participation, or unreliable performance metrics.

**Smurf Detection Filter:**  
Matches containing players with abnormally high performance for Bronze ELO (e.g., 9.0+ CS/min, or 20+ kills with only 2 or fewer deaths) were excluded.

These filtering steps ensured that only competitive and representative Bronze IV games remained in the dataset.

---

## Modeling & Conclusion

**Model Used:** Logistic Regression

The cleaned dataset was used to predict the match outcome (`Win`) using **Mastery_Diff**, defined as the difference in average team mastery points between the winning and losing teams.

- **Model Accuracy:** 54.10%  
- **Mastery Coefficient:** 1.7083291544221246e-07 (effectively zero)

**Interpretation:**  
The logistic regression coefficient is statistically indistinguishable from zero, meaning differences in champion mastery have no measurable impact on the probability of winning a Bronze IV match.

---

## Final Conclusion

The analysis demonstrates that champion mastery points do not meaningfully influence match outcomes in the Bronze IV tier.  
Instead, match results in this tier are more strongly affected by high-variance factors such as real-time execution errors, poor objective control, team coordination issues, and inconsistent mechanical performance, rather than accumulated champion experience.

Therefore, the initial hypothesis was rejected.

