# Understanding dropout
[Source](http://papers.nips.cc/paper/4878-understanding-dropout.pdf)

## Introduction
Dropout is a relatively new algorithm for training neural networks which relies on stochastically “dropping out” neurons during training in order to avoid the co-adaptation of feature detectors. In its simple form, during training, at each example presentation, feature detectors are deleted with probability q = 1 − p = 0.5 and the remaining weights are trained by backpropagation. All weights are shared across all example presentations. During prediction, the weights are divided by two. The main motivation behind the algorithm is to prevent the co-adaptation of feature detectors, or overfitting, by forcing neurons to be robust and rely on population behavior, rather than on the activity of other specific units.

## Dropout in Linear Networks
The ensemble average can easily be computed by feedforward propagation in the original network, simply replacing the weights Wij by WijPj

## Dropout in Neural Networks
Dropout performs gradient descent on-line with respect to both the training examples and the ensemble of all possible subnetworks. As such, and with the appropriately decreasing learning rates, it is almost surely convergent like other forms of stochastic gradient descent.

