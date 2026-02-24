# Bias Analysis and Mitigation in Medical AI

This repository contains our work evaluating and mitigating biases in diagnostic prediction models using a radiological dataset. In medical AI, an unfair model can have severe clinical consequences, so we wanted to test how different fairness interventions perform in practice when faced with heavily imbalanced data—both in terms of the target variable (healthy vs. sick) and sensitive attributes (like radiographic view positions).

## What we did
The notebook breaks down the problem into three main stages:
1. **Measuring Initial Bias:** We quantified the biases already present in the dataset and tracked how they skewed our baseline model's predictions.
2. **Training Interventions (In-processing):** We experimented with class weighting and resampling techniques to see if we could correct the imbalances while the model was actually learning.
3. **Post-processing:** We applied post-prediction fairness algorithms using the AIF360 library—specifically Reject Option Classification (ROC) and Calibrated Equalized Odds (CEO)—to force the outputs to be more equitable.

## What we found
* **The accuracy vs. fairness trade-off is brutal.** When we applied aggressive post-processing to force strict mathematical fairness, our model's accuracy collapsed to around 35-50%. Lighter interventions barely made a dent in the initial bias.
* **CEO performed slightly better than ROC.** Calibrated Equalized Odds held up a bit better, preserving some fairness metrics without completely destroying predictive performance, but neither was a magic fix.
* **There is no quick fix.** The main takeaway is that you can't just slap a post-processing algorithm on biased medical data. Meaningful fairness requires a custom approach starting from the data collection phase, likely combining multiple lighter interventions rather than relying on heavy post-hoc corrections.

## Tech Stack
* Python (Jupyter Notebook)
* AIF360 (AI Fairness 360)
* Scikit-learn, Pandas, NumPy

## Authors
* Maxime Hayakawa Ivanovic
* Fatimata Kone
