FAANG Stock Direction Prediction
A machine learning project that predicts the next-day price direction (up or down) of FAANG stocks using engineered technical features and three classification models: Logistic Regression, Random Forest, and Gradient Boosting.

Best model — Gradient Boosting: Accuracy 0.518 · Precision 0.520 · Recall 0.762 · F1 0.618


Project Overview
Daily stock returns are noisy and close to a random walk, so the goal is not to achieve high accuracy alone, but to build a model with strong recall and F1-score for "up" days — capturing as many true upward movements as possible while keeping false positives reasonable.
Target variable: Binary — 1 if tomorrow's adjusted closing price is higher than today's, 0 otherwise.

Repository Structure
faang-stock-direction-prediction/
├── data/                        # Raw daily OHLCV CSV files for each FAANG company
├── notebooks/
│   ├── 01_data_wrangling.ipynb          # Data loading, cleaning, EDA
│   ├── 02_feature_engineering.ipynb     # Feature construction and selection
│   └── 03_modeling_and_evaluation.ipynb # Model training, comparison, and final results
├── reports/
│   ├── Final_Project_Report.pdf         # Written project report
│   └── FAANG_Presentation.pdf          # Slide deck with motivation and results
├── model_metrics.csv            # Final model hyperparameters and evaluation metrics
└── README.md

Notebooks
#NotebookDescriptionLink1Data WranglingLoad and combine raw FAANG CSVs, parse dates, inspect missing values, explore distributions▶ View on nbviewer2Feature EngineeringConstruct returns, moving averages, volatility windows, intraday spreads, and lagged features; define binary target▶ View on nbviewer3Modeling & EvaluationTrain and compare Logistic Regression, Random Forest, and Gradient Boosting; evaluate on held-out test set; feature importance analysis▶ View on nbviewer

Features Engineered
CategoryFeaturesReturnsReturn1, Return3, Return5, Return10Moving AveragesMA7, MA14, MA30VolatilityVolatility7, Volatility14, Volatility30Intraday SpreadsHigh_Low_Spread, Open_Close_SpreadLagged ReturnsLag1, Lag2, Lag3

Model Results
ModelAccuracyPrecisionRecallF1Logistic Regression0.510.510.850.64Random Forest0.520.530.710.60Gradient Boosting ✅0.520.520.760.62
Gradient Boosting was selected as the final model. It achieved the highest recall and F1-score, meaning it captures the most true upward movements with the best precision-recall balance. Top predictors include Lag1, Return1, Open_Close_Spread, High_Low_Spread, and MA7.
Final model hyperparameters: n_estimators=150, learning_rate=0.05, max_depth=3, random_state=42

Key Findings & Recommendations

Use Gradient Boosting as a ranking tool — rank trading days by predicted upward probability and focus on top-scored opportunities rather than treating predictions as guaranteed signals.
Combine with risk management — pair model signals with stop-loss rules and minimum return thresholds to account for trading costs on noisy daily moves.
Retrain regularly — market regimes shift over time; retraining on a rolling 1–2 year window helps keep feature relationships current.


Tech Stack

Language: Python 3
Libraries: pandas, numpy, scikit-learn, matplotlib, seaborn
Models: LogisticRegression, RandomForestClassifier, GradientBoostingClassifier (scikit-learn)
Data split: 70% train / 30% test, shuffle=False to respect time ordering
