# Kaggle-TalkingData

This repository contains my solution for the Kaggle competition <a href='https://www.kaggle.com/c/talkingdata-adtracking-fraud-detection'>TalkingData AdTracking Fraud Detection</a>. It ranked 197 out of 3967 (Top 5%).

The goal of this competition was to predict if mobile users will install an app they have clicked (Click-Through prediction). The biggest challenge in this competition was to handle the huge amount of data (about 250 millions rows). 

This solution is based on 2 different models: 
 * Field-Aware Factorization Machine
 * Gradient Boosted Decision Tree

The Field-Aware Factorization Machine was combined with an unsupervised gradient boosted decision tree (with 30 trees) for feature engineering. The gradient boosted decision tree is regularly trained in a supervised way but instead of using its target predictions the leaf index predictions are used as features for the Field-Aware Factorization machine. This approach was proposed by Xinran He et al. <a href='http://quinonero.net/Publications/predicting-clicks-facebook.pdf'>Practical Lessons from Predicting Clicks on Ads at Facebook</a> and used in the winning solution of the previous Click-Trough prediction competition <a href='https://www.kaggle.com/c/criteo-display-ad-challenge'>Display Advertising Challenge</a>. Field-Aware Factorization machines proved to be a very strong powerful model in past Click-Trough prediction competitions. They work well when used with categorical features. The used library is <a href='http://xlearn-doc.readthedocs.io/en/latest/'>xLearn</a>.

The Gradient Boosted Decision Tree is trained using various Groupby and Aggregating features including aggregate functions `count`, `var`, `mean`, `nunique`and `cumcount` in addition to time-to-next-click features. Those features Those features were used in almost all top solutions and many kernels. The used library was <a href='http://lightgbm.readthedocs.io'>LightGBM</a> because its impressived speed given the huge amount of data.

These 2 models were ensembled using weighted blending.
