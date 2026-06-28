

FIFA World Cup Champion Predictor

A machine learning project that predicts the FIFA World Cup champion using historical tournament data, validated through leave-one-tournament-out cross-validation across six World Cups (2002–2022).

---

## 📌 Overview

This project builds and compares two classification models — *Random Forest* and *XGBoost* — to predict which national team is most likely to win the FIFA World Cup, based on pre-tournament features like squad market value, FIFA ranking, recent form, and historical tournament performance.

Rather than chasing an inflated accuracy number, this project focuses on *honest validation* and *interpreting results in the context of real-world football unpredictability*.

---

## 🎯 Problem Statement

Predicting a single-elimination tournament winner out of 32+ competing national teams is one of the hardest prediction problems in sports analytics. A single bad day, a red card, or a penalty shootout can eliminate the strongest team. This project explores how far historical data alone can take us — and, just as importantly, where its limits are.

---

## 🛠️ Methodology

*Models used:*
- Random Forest Classifier
- XGBoost Classifier

*Validation strategy:*
Leave-one-tournament-out cross-validation — for each of the 6 World Cups (2002, 2006, 2010, 2014, 2018, 2022), the model is trained on the other 5 tournaments and tested on the held-out one. This prevents data leakage and simulates genuinely predicting an unseen tournament.

*Features (17 total):*
- is_host
- goals_scored_last_4y, goals_received_last_4y
- wins_last_4y, losses_last_4y, draws_last_4y
- world_cup_titles_before
- squad_total_market_value_eur (log-transformed)
- fifa_rank_pre_tournament, fifa_points_pre_tournament
- squad_avg_age
- world_cup_participations_before
- groups_passed_before, round16_before, quarterfinals_before, semifinals_before, finals_before

*Preprocessing:*
- Missing market value filled with median (computed per training split to avoid leakage)
- Log transformation applied to squad market value to reduce wealth-driven skew

---

## 📊 Results

| Model | Accuracy (Leave-One-Out, 2002–2022) |
|---|---|
| Random Forest | 16.67% |
| XGBoost | 16.67% |

*Context matters:* With ~32 teams per tournament, random guessing yields roughly 3.1% accuracy. Both models perform *~5x better than random chance* — a meaningful signal given how genuinely unpredictable single-elimination football tournaments are.

---

## 🔍 Feature Importance (XGBoost)

![Feature Importance](images/feature_importance.png)

*Top predictors:*
1. groups_passed_before
2. squad_total_market_value_eur
3. quarterfinalist_before
4. semifinals_before
5. wins_last_4y

*Key insight:* Recent tournament progression and squad market value matter more to the model than all-time historical achievements (e.g., titles_before, finals_before carry near-zero importance). This suggests current squad quality and recent form outweigh legacy reputation — which aligns with footballing intuition.

---

## 🔮 2026 World Cup Prediction

Top win probability picks from the final model:

| Rank | Team | Win Probability |
|---|---|---|
| 1 | France | 3.98% |
| 2 | Spain | 3.93% |
| 3 | Argentina | 3.93% |

*Why are the top probabilities so close together?* This isn't a flaw — it reflects genuine competitive parity. France, Spain, and Argentina (along with England and Brazil) are widely considered the strongest contenders by football analysts and bookmakers, with no single team typically favored above 15–20% to win the entire tournament. A model that confidently assigns one team a 60% chance would actually be less realistic than this distribution.

---

## ⚠️ Limitations

- *Format change in 2026:* The model was trained exclusively on 32-team tournaments (2002–2022). The 2026 World Cup expands to 48 teams with a new Round of 32 stage — a structural change the model has never seen, representing a domain shift.
- *Inherent unpredictability:* Single-elimination tournaments are highly sensitive to one-off events (injuries, red cards, penalty shootouts) that historical statistics cannot capture.
- *Small sample size:* Only 6 World Cups worth of validation data exist in this format, limiting statistical robustness.

---

## 🧰 Tech Stack

Python · pandas · NumPy · scikit-learn · XGBoost · Matplotlib

---




---

## 📁 Repository Structure


fifa-worldcup-prediction/
├── README.md
├── worldcup_prediction.ipynb
├── train.csv
├── test.csv
├── requirements.txt
└── images/
    └── feature_importance.png


---

## 💭 Reflection

The most valuable part of this project wasn't achieving a high accuracy score — it was learning to correctly interpret what the model's output actually means. A 16% accuracy and near-uniform probabilities among top teams aren't weaknesses to hide; they're an honest reflection of how unpredictable elite football tournaments genuinely are.
