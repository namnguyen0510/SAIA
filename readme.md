# SAIA: Split Artificial Intelligence Architecture for Mobile Healhcare System

This respository provides instruction for Split Artificial Intelligence Architecture (SAIA) framework. The case study on Skin Lesion data will be analysized in detail to illustrate step-by-step instruction.

## Getting Started

As the advancement of deep learning (DL), the Internet of Things and cloud computing techniques for the analysis anddiagnosis of biomedical and health care problems in the last decade, mobile healthcare applications have received unprecedentedattention. Since DL techniques usually require enormous amount of computation, most of them cannot be directly deployed on thecomputation-constrained and energy-limited mobile and IoT devices. Hence, most of the mobile healthcare applications leverage thecloud computing infrastructure, where the data collected on the mobile/IoT devices would be transmitted to the cloud computingplatforms for analysis. However, in contested environments, relying on the cloud server might not be practical at all times; forinstance,the satellite communication might be denied or disrupted. In this paper, we propose SAIA, a Split Artificial IntelligenceArchitecture for mobile healthcare systems. Unlike traditional approach for artificial intelligence (AI) which solely exploits thecomputational power of the cloud server, SAIA not only relies on the cloud computing infrastructure while the wireless communicationis available, but also utilizes the lightweight AI solutions that work locally at the client side (e.g., mobile and IoT devices), hence, it canwork even when the communication is impeded. In SAIA, we propose a meta-information based decision unit, that could tune whethera sample captured by the client should be operated by embedded AI or networked AI, under different conditions. In the experimentalevaluation, extensive experiments have been conducted on two popular healthcare datasets. Our results show that SAIA consistentlyoutperforms its baselines in terms of both effectiveness and efficiency.

### Prerequisites

Python >= 3.5, LightGBM 2.3.2

### Case study - Skin Lesion Data
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
#### Training SAIA Decision Unit:
By adjusting the parameter epsilon, we are able to control the amount of data sent to server. Further details will be provied in the Jupyter Notebook.

## Built With

* [Python 3](https://www.python.org/download/releases/3.0/) 

## Publication (Link later)

* [SAIA: Split Artificial Intelligence Architecture for Mobile Healthcare System](https://www.python.org/download/releases/3.0/) 

## Authors

* **Di Zhuang** - *zhuangdi1990@gmail.com* 

* **Nam Nguyen** - *namnguyen2@mail.usf.edu* 

* **Keyu Chen** - *keyu@mail.usf.edu* 
* **J.Morris Chang** - *morrisjchang@gmail.com* 


