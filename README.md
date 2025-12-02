League of Legends: Champion Mastery's Effect on Bronze ELO Win Rate

Project Summary

Analysis of the effect of **Champion Mastery Points** on **match victory** for players in the **Bronze IV league** using the Riot Games API and **Logistic Regression**. The study was designed to test if specialized champion knowledge directly impacts a player's ability to carry a low-ranking game.
The analysis concluded that champion mastery points had **no statistically significant effect** on the match outcome, leading to the **rejection of the initial hypothesis**.

Hypothesis & Goal

**Hypothesis:** Higher champion mastery points (a proxy for player experience on a specific champion) will lead to a higher win probability in low-elo tier.
**Goal:** Build a robust data pipeline and a statistical model to quantify the relationship between the in-game difference in team mastery points and the final match outcome (Win/Loss).

Methodology & Data Engineering

This project involved data acquisition from the Riot Games API, error handling, and data enrichment. 
1.  **Data Acquisition:** Player PUUIDs were collected from the **League-Exp-v4** endpoint for Bronze IV.
2.  **Match Data Collection:** **1000 sample solo-queue ranked matches** were retrieved using the **Match-V5** endpoint.
3.  **Data Enrichment:** The **Champion-Mastery-v4** endpoint was used to pull the specific mastery score for the champion each player used in the match.
4.  **Persistence:** All raw and final data were saved to JSON/CSV files (e.g., `bronze4_matches_all.json`, `mastery_verisi.csv`) to prevent API rate limit issues and ensure reproducibility. 

Data Cleaning

To ensure the model only trained on valid and competitive data, the following custom filtering rules were implemented:
* **Remake/Early Surrender Filter:** Matches with a duration of **less than 8 minutes (480 seconds)** were excluded.
* **AFK Player Filter:** Matches containing any player who met low-effort criteria (e.g., played less than 60% of game duration, or ultra-low combined K/D/A, Gold, and Damage in long games) were removed.
* **Smurf Detection Filter:** Matches containing players who showed abnormally high performance metrics for the Bronze ELO were removed (e.g., **9.0+ CS/min or 20+ kills with 2 or less deaths**).

Modeling & Conclusion

Model Used: Logistic Regression
The clean dataset was used to predict the `Win` outcome based on the feature `Mastery_Diff` (the difference in average mastery points between the winning and losing teams).
Model Accuracy: 58.10% 
Mastery Coefficient 0.00000007580637253577291

Final Conclusion

The Logistic Regression Coefficient was found to be $7.58 \times 10^{-8}, which is statistically zero. This led to the rejection of the hypothesis.
The analysis definitively demonstrates that in the Bronze IV tier, the outcome of a match is likely determined by factors with greater variance, such as **real-time execution errors, poor objective control, or team coordination**, rather than a player's accumulated champion experience.
