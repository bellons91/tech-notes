---
title: "Cross-Entropy Loss"
tags:
  - artificial-intelligence
  - machine-learning
  - loss-functions
  - optimization
  - classification
  - language-models
aliases:
  - Cross Entropy
  - Log Loss
  - Categorical Cross-Entropy
---

**Cross-entropy loss** measures how far a model's predicted probability distribution is from the target distribution. It is one of the most common training objectives for classification problems and next-token prediction in language models.

## Summary

- Cross-entropy loss is low when the model assigns high probability to the correct outcome and high when it assigns low probability.
- In binary classification, it is often called **log loss** or **logistic loss**.
- In multiclass settings, it is commonly applied to logits through a softmax-based formulation.
- Many ML libraries accept either **integer class labels** or **one-hot / probability targets**, depending on the API.
- Cross-entropy is typically computed from **unnormalized logits** for numerical stability rather than from manually normalized probabilities.
- The loss is closely related to **negative log-likelihood** and is commonly used in logistic regression, neural-network classifiers, and language modeling.
- Extensions such as **class weighting**, **ignore indices**, and **label smoothing** adjust how examples contribute to the objective.

## Intuition

Cross-entropy answers a practical training question: **how surprised should the model be by the correct answer, given its predicted probabilities?**

- If the model gives the correct class a probability near **1**, the loss is small.
- If the model gives the correct class a probability near **0**, the loss becomes large.

This makes the objective sensitive not only to whether the top prediction is correct, but also to **how confident** the model is.

## Common Form

For a target distribution \(y\) and predicted class probabilities \(p\), cross-entropy is commonly written as:

\[
L = - \sum_c y_c \log p_c
\]

For one-hot labels, only the true class contributes, so the loss reduces to the negative log of the predicted probability assigned to the correct class.

Libraries often implement this from **logits** rather than probabilities:

- PyTorch's `CrossEntropyLoss` expects **unnormalized logits** and is equivalent to **LogSoftmax + NLLLoss**.
- Keras distinguishes categorical and sparse categorical variants depending on whether labels are one-hot or integer encoded.
- Optax exposes softmax cross-entropy helpers for both one-hot labels and integer labels.

## Binary vs Multiclass Use

| Setting                       | Typical output                               | Common interpretation      |
| ----------------------------- | -------------------------------------------- | -------------------------- |
| **Binary classification**     | One probability for the positive class       | Log loss / logistic loss   |
| **Multiclass classification** | Probability distribution across classes      | Categorical cross-entropy  |
| **Language modeling**         | Probability distribution over the vocabulary | Next-token prediction loss |

In language models, each training step asks the model to assign high probability to the next correct token. That makes cross-entropy a natural fit for objectives used in [[Masked vs Autoregressive Language Models]].

## Why It Is So Common

Cross-entropy is widely used because it aligns well with probabilistic prediction:

- it rewards calibrated probability assignments better than simple 0/1 accuracy
- it strongly penalizes confident wrong answers
- it works naturally with gradient-based training
- it generalizes from binary classification to multiclass and token-level prediction

Scikit-learn describes log loss as the negative log-likelihood used in logistic regression and extensions such as neural networks.

## Practical Notes

- Pass **logits** when the API expects logits; adding softmax twice can be incorrect.
- Integer-label variants are often more efficient than dense one-hot targets.
- **Label smoothing** can reduce overconfidence by softening target distributions.
- **Class weights** can help on imbalanced datasets.
- Cross-entropy is informative for optimization, but lower loss does not always guarantee better real-world behavior or calibration.

## Related

- [[Parameters]]
- [[Hyperparameters]]
- [[Supervised vs Self-Supervised Learning]]
- [[Masked vs Autoregressive Language Models]]

## Sources

- [PyTorch `torch.nn.CrossEntropyLoss` source and documentation comments](https://github.com/pytorch/pytorch/blob/main/torch/nn/modules/loss.py)
- [Keras categorical crossentropy loss implementation and docstring](https://github.com/keras-team/keras/blob/master/keras/src/losses/losses.py)
- [Optax softmax cross-entropy helpers](https://github.com/google-deepmind/optax/blob/main/optax/losses/_classification.py)
- [scikit-learn `log_loss` documentation in source](https://github.com/scikit-learn/scikit-learn/blob/main/sklearn/metrics/_classification.py)
