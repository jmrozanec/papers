# [The class imbalance problem in pattern classification and learning](http://marmota.dlsi.uji.es/WebBIB/papers/2007/1_GarciaTamida2007.pdf)

## Abstract
It has been observed that class imbalance may produce an important deterioration of the performance achieved by existing learning and classification problems.
Introduction
Traditionally research has focused on solutions at data and algorithmic levels:
- resample methods for balancing the dataset
- modification of existing learning algorithms
- measuring the classifier performance in imbalanced domains
- relationship between class imbalance and other data complexity characteristics

## Resampling techniques
Oversampling: increase the size of the minority class corresponds to random oversampling; a non-heuristic method that balances the class distribution through the random replication of positive examples. Increases likelyhood of overfitting. Alternative: creation of synthetic positive examples (SMOTE: combining near positive examples; or interpolating values of positive examples)
Undersampling: 
- randomly remove negative examples. 
- restricted decontamination technique: discard negative instance and relabel others as positive
- generic algorithms to reduce data set until obtaining a balance between classes

## Solutions at the algorithmic level
Addresses the imbalance problem by adapting existing algorithms and techniques to the special characteristics of imbalanced data sets.
Examples: weighted distance for k-mean classifier
- cost sensitive learning: different costs are assigned to errors regarding positive and negative examples
- one class classifier: tries to describe one class of objects and distinguish it from all other possible objects. 
- classifier ensembles: ensembles are defined as a set of individually trained classifiers whose decisions are combined when classifying new objects.

## Other complexity characteristics
The class imbalance may not a problem by itself, but the degradation of performance is also related to other factors.
