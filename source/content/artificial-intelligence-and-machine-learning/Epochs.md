---
title: "Epochs"
tags:
  - ai
  - machine-learning
  - deep-learning
  - model-training
  - optimization
aliases:
  - Training Epochs
  - Epoch in Machine Learning
---

In machine learning, an **epoch** is one full pass of the training process over the training dataset (or over the configured training steps when steps are capped).  
This note is a quick reference for how epochs relate to batches, iterations, convergence, and overfitting risk.

## Summary

- An epoch represents a full training cycle over the training data.
- In mini-batch training, one epoch is composed of multiple parameter-update steps.
- A common relationship is: `steps per epoch ≈ number of training samples / batch size`.
- The number of epochs is a training hyperparameter that controls how long optimization runs.
- Too few epochs can underfit; too many can overfit, especially without regularization or early stopping.
- Frameworks may allow limiting `steps_per_epoch`, so an epoch can be defined operationally by a fixed step count.
- Progress is often monitored per epoch using training and validation metrics.
- Epoch count should be chosen with validation behavior, not only final training loss.

## Epochs, batches, and iterations

Training loops typically process data in mini-batches:

- **Batch**: a subset of examples processed together in one forward/backward pass.
- **Iteration / step**: one optimizer update after processing a batch.
- **Epoch**: a complete pass over the training data (or configured epoch steps).

For finite datasets in standard mini-batch training:

- `steps per epoch = ceil(number of training samples / batch size)` (framework behavior can vary with `drop_last`/partial batches).

## Why epoch count matters

Epoch count is one of the most important training-duration controls:

- Increasing epochs usually lowers training loss early on.
- Past a point, additional epochs may improve little or degrade validation metrics.
- Early stopping, learning-rate schedules, and regularization are often used alongside epoch tuning.

## Practical interpretation in frameworks

- Keras documents epochs as full iterations over provided training data and clarifies interaction with `steps_per_epoch`.
- PyTorch tutorials describe number of epochs as the number of times to iterate over the dataset.
- scikit-learn documentation often maps `max_iter` in stochastic solvers to maximum passes over training data (epochs).

## Related

- [[Hyperparameters]]
- [[Parameters]]
- [[Model Weights]]
- [[Supervised vs Self-Supervised Learning]]

## Sources

- [Keras trainer API docs in source (`epochs` definition)](https://github.com/keras-team/keras/blob/master/keras/src/trainers/trainer.py)
- [PyTorch basics optimization tutorial (`Number of Epochs`)](https://github.com/pytorch/tutorials/blob/main/beginner_source/basics/optimization_tutorial.py)
- [scikit-learn Perceptron docs (`max_iter` as passes over data / epochs)](https://github.com/scikit-learn/scikit-learn/blob/main/sklearn/linear_model/_perceptron.py)
