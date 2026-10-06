---
layout: page
title: Movie Genre Classification
permalink: /code/movie-genre/
mathjax: true
---

### Description
This started as a public data challenge to guess movie genres just by looking at their posters. I expanded the scope to benchmark traditional CNN architectures against pre-trained Vision-Language Models (VLMs) with frozen weights. The dataset spans 9, 826 postes and 19 distinct movie genres.

### Evaluation Metrics
Because this is a multi-label classification problem, the overwhelming number of true negatives (TN) can skew results. To account for this, we rely on two key metrics. 

The first is the *minority F1-score*, defined as:
<div>
\[ F1 = \frac{TP}{TP + FP + FN} \]
</div>
where $TP$, $FP$, and $FN$ represent global true positives, false positives, and false negatives, respectively. 

We also report *subset accuracy*, which evaluates the strict fraction of predictions where the exact set of genres is correctly identified.

### Dataset split
The dataset is partitioned into a $60\%$ training set, a $20\%$ validation set and a $20\%$ hold-out test set.

### Algorithms

We selected ResNet-18 as our baseline CNN model and Qwen3-VL as the VLM. For the VLM approach, we freeze the model's weights and utilize the activations from its final layer as an extracted latent feature space. These embeddings are then passed into either a Logistic Regression (LR) model or a Multi-Layer Perceptron (MLP) to generate the final predictions. A graphical illustration of this architecture can be found below.
**[View Architecture Diagram](/assets/movie-poster.jpg)**


### Results

| Model | Params | Minority F1 | Subset Acc. |
| :--- | :---: | :---: | :---: |
| Qwen3-VL (ZS Naive) | 4B | 66.11% | 8.91% |
| Qwen3-VL (ZS JSON) | 4B | 64.09% | 11.68% |
| Qwen3-VL + LR | 4B | 66.26% | 14.86% |
| Qwen3-VL + MLP | 4B | 64.13% | 16.80% |
| ResNet-18 | 12M | 49.01% | 9.22% |

### Interpretation
We note that Qwen3-VL significantly outperforms ResNet-18 on the minority F1 metric without any task-specific tuning or prompt engineering. Interestingly, the addition of a trainable classification head (the LR or MLP) primarily improves subset accuracy. 

Before pursuing full fine-tuning or developing better-optimized architectures, it is necessary to benchmark these findings against other models (such as Vision Transformers) and additional datasets. I plan to expand the project [here](/code/movie-genre-2).

**[View Source Code on GitHub](https://github.com/Lezane/Movie-Genre-Classification)**
