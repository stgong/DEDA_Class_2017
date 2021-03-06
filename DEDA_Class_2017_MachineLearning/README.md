
[<img src="https://github.com/QuantLet/Styleguide-and-FAQ/blob/master/pictures/banner.png" width="888" alt="Visit QuantNet">](http://quantlet.de/)

## [<img src="https://github.com/QuantLet/Styleguide-and-FAQ/blob/master/pictures/qloqo.png" alt="Visit QuantNet">](http://quantlet.de/) **Digital Economy and Decision Analytics** [<img src="https://github.com/QuantLet/Styleguide-and-FAQ/blob/master/pictures/QN2.png" width="60" alt="Visit QuantNet 2.0">](http://quantlet.de/)

```yaml
Name of Quantlet : DEDA_Class_2017_MachineLearning
Published in : Digital Economy and Decision Analytics
Description :
- Demonstrate decision tree
- Demonstrate applied SVM on NLP sentiment classification

Keywords :
- Python
- Teaching
- Machine learning
- Sklearn
- Decision tree
- Support vector machine
- Sentiment classification

Author : Junjie Hu
```

### Python Code:
```python

"""
### Please note: This file is not for execution ###
"""

from sklearn.datasets import load_iris
# More toy data sets from sklearn please refer:
# http://scikit-learn.org/stable/datasets/
import numpy as np
from sklearn import tree
import graphviz
from sklearn.metrics import accuracy_score as acc_rate

iris = load_iris()

# Glance the data set
print(iris.feature_names)  # name of features
print(iris.data)  # data for the 4 features
print(iris.target_names)  # name of the targets
print(iris.target)  # data for the targets

# randomly choose 1/3 of samples as testing data
np.random.seed(123)
test_idx = np.random.randint(0, len(iris.target), len(iris.target) // 3)

# training data
train_data = np.delete(iris.data, test_idx, axis=0)
train_target = np.delete(iris.target, test_idx)

# testing data
test_data = iris.data[test_idx]
test_target = iris.target[test_idx]

# train the model
# initial an decision tree classifier object with given arguments
clf = tree.DecisionTreeClassifier(criterion='entropy',
                                  splitter='best')
# A lot of arguments can be placed into the object
# Refer docs: http://scikit-learn.org/stable/modules/generated/sklearn.tree.DecisionTreeClassifier.html#sklearn.tree.DecisionTreeClassifier
clf.fit(X=train_data, y=train_target)

# make prediction
print('\nThe target test data set is:\n', test_target)
print('\nThe predicted result is:\n', clf.predict(test_data))
print('\nAccuracy rate is:\n', acc_rate(test_target, clf.predict(test_data)))

# visualizing the tree

dot_data = tree.export_graphviz(clf,
                                out_file=None,
                                feature_names=iris.feature_names,
                                class_names=iris.target_names,
                                filled=True,
                                rounded=True,
                                impurity=False,
                                special_characters=True)
graph = graphviz.Source(dot_data)
graph.render("iris")



```