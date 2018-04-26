# Assess Learners

Implement Random Tree Learner, Bag learner and Insane Learner. Evaluate all the learners implemented in this project as well as those in [Part 1](https://github.com/ntrang086/ml_trading_defeat_learners)

This is Part 2 in a four-part series of **Machine Learning Algorithms for Trading**:

* [**Part 1**](https://github.com/ntrang086/ml_trading_defeat_learners): Implement the Linear Regression Learner and Decision Tree Learner and generate data that works better for one learner than the other.
* [**Part 2**](https://github.com/ntrang086/ml_trading_assess_learners) (this repository): Implement Random Tree Learner, Bag learner and Insane Learner. Evaluate all the learners implemented in Parts 1 and 2.
* [**Part 3**](https://github.com/ntrang086/q_learning_robot): Implement the Q-Learning and Dyna-Q solutions to the reinforcement learning problem.
* [**Part 4**](https://github.com/ntrang086/q_learning_trading): Implement a learning trading agent using Q-learning.


## Code and project details

Code in this project can be grouped into two categories:

**1) Implement decision tree learner, random tree learner, bag learner and insane learner**

* **`DTLearner.py`** - The Decision Tree Learner is based on [J.R. Quinlan's paper](https://link.springer.com/content/pdf/10.1007/BF00116251.pdf). Other than `addEvidence` and `query`, this learner also has:
  * `__build_tree`: A private function called by `addEvidence`. It builds the decision tree recursively by choosing the best feature to split on and the splitting value. The best feature has the highest absolute correlation with dataY. If all features have the same absolute correlation, choose the first feature. The splitting value is the median of the data according to the best feature.
  * `__tree_search`(self, point, row): A private function called by query. It recursively searches the decision tree matrix and returns a predicted value for a given query.
  * `get_learner_info`: It print out a tree in the form of a pandas dataframe if verbose is set to True.

* **`RTLearner.py`** - The Random Tree Learner is based on [A. Cutler's algorithm](https://www.stat.berkeley.edu/~breiman/RandomForests/cc_home.htm). It has a similar API to DTLearner, but has a few key differences regarding `__build_tree`:
  * The choice of feature to split on is be made randomly.
  * For the chosen feature, calculate the mean of feature values from two randomly-chosen rows. This mean will be the splitting value for the feature.

* **`BagLearner.py`** - Code that implements Bootstrap Aggregating as a Python class named BagLearner. BagLearner can accept any learner (e.g., RTLearner, LinRegLearner, etc.) as input and use it to generate a learner ensemble. 

* **`InsaneLearner.py`** - An InsaneLearner should contain 20 BagLearner instances where each instance is composed of 20 instances of LinRegLearner or another learner.


**2) Evaluate learners**

* **`analyze_learners_util.py`** - Helper code to proccess, train, test and plot data.

* **`analyze_learners.ipynb`** - Uses helper functions from `analyze_learners_util.py` to evaluate different learners.


## Setup

You need Python 2.7.x or 3.x, and the following packages: pandas, numpy, and scipy.

## Data
All the data files are in `Data` subdirectory. However, we will only use `Istabul.csv` to analyze the learners in the notebook `analyze_learners.ipynb`. This data includes the returns of multiple worldwide indexes for a number of days in history. The overall objective is to predict what the return for the MSCI Emerging Markets (EM) index will be on the basis of the other index returns. Y in this case is the last column to the right, and the X values are the remaining columns to the left (except the first column which is the date).

## Run

To run any script file, use:

```bash
python <script.py>
```

To run any IPython Notebook, use:

```bash
jupyter notebook <notebook_name.ipynb>
```

Source: [Part 3](http://quantsoftware.gatech.edu/Machine_Learning_Algorithms_for_Trading) of [Machine Learning for Trading](http://quantsoftware.gatech.edu/Machine_Learning_for_Trading_Course) by Georgia Tech
