# SAIA: Split Artificial Intelligence Architecture for Mobile Healhcare System

One Paragraph of project description goes here

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

### Prerequisites

Python >= 3.5, LightGBM 2.3.2

### Instruction
The example on Skin Lesion can be split into 2 mains parts:
#### Traininng Embbeded-AI model: 
The set of hyperparameters is derived from 5-fold cross validation, which yields the best performance in skin lesion data
```
classifier = LGBMClassifier(boosting_type = 'dart', learning_rate = 0.3, 
                            max_bin = 255, drop_rate = 0.015, objective = 'multiclassova',
                            num_class=8, metric='multi_error', num_leaves = 64, 
                            min_data=50, max_depth=-1, feature_fraction =1 , bagging_fraction=1,
                            n_estimators  = 1000, num_threads = 4, class_weight = 'balanced',silent = False
                           )
classifier.fit(X_train, y_train, verbose = True, 
               eval_set = [(X_train,y_train),(X_test,y_test)], eval_metric = 'multi_error')
# Saving embedded-AI model
classifier.booster_.save_model('embbeded-AI.txt', num_iteration = classifier.best_iteration_)
classifier.best_score_
```
#### Training SAIA decision unit:
By adjusting the parameter epsilon, we are able to control the amount of data sent to server.

## Built With

* [Python 3](https://www.python.org/download/releases/3.0/) 

## Authors

* **Di Zhuang** - *University of South Florida* - [PhD]

* **Nam Nguyen** - *University of South Florida* - [PhD]

* **Keyu Chen** - *University of South Florida* - [PhD]
* **J.Morris Chang** - *Senior Member, IEEE* - [PhD]

## Acknowledgments
Effort sponsored in whole or in part by United States Special Operations Command (USSOCOM), under Partnership Intermediary Agreement No. H92222-15-3-0001-01. The U.S. Government is authorized to reproduce and distribute reprints for Government purposes notwithstanding any copyright notation thereon. \footnote{The views and conclusions contained herein are those of the authors and should not be interpreted as necessarily representing the official policies or endorsements, either expressed or implied, of the United States Special Operations Command.
