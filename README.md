# Toy GCG: Gradient-Guided Discrete Optimization on GPT-2

## Goal
Test whether gradient-guided token proposals find lower-target-loss
suffixes than random token search under the same candidate-evaluation budget.

## Method
- GPT-2
- benign one-token target
- editable token suffix
- gradients with respect to input embeddings
- project gradients against vocabulary embeddings
- sample discrete candidate substitutions
- evaluate true target cross-entropy
- greedily retain the best candidate

## Result
Across 3 seeds:

- GCG average final loss: 3.167
- Random search average final loss: 6.600

This is a small toy experiment, not evidence of statistical superiority.

## What this reproduces
The central intuition of GCG:
gradient information narrows a large discrete token-search space,
while actual forward-pass loss determines which candidate is retained.

## Differences from the paper
- embedding-gradient projection rather than one-hot token gradients
- one benign target token
- one prompt
- one model
- no universal multi-prompt / multi-model optimization

## What I learned
- Much of manipulating models seems to be from applying "pressures" to create gradients we can learn on.
- These loss functions can be used to pressure white-box models to effectively teach us what prompt suffixes might trigger the desired response.
- GCG is autonomous, able to adapt to different white-box models, and generalizable to other black-box models including much larger frontier models which suggests that there are common representations and gradients between models that are trained on similar functions even if their training process/dataset was very different. 

## Reference
Zou et al., "Universal and Transferable Adversarial Attacks on Aligned
Language Models"
