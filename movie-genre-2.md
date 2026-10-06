---
layout: page
title: Movie Genre Classification - Follow Up (Testing Phase)
permalink: /code/movie-genre-2/
mathjax: true
---

### Objective

Building on our [previous work](/code/movie-genre), initial experiments using frozen weights achieved an F1 score of ~65% and a subset accuracy of 15%. Before committing to a more complex fine-tuning setup, we need to conduct three sanity checks to validate our current approach.

### Sanity Check I: Is the Feature Extraction a Coherent Metric?
The goal here is to verify whether the structural distances between movie posters are accurately preserved within the extracted feature space.

### Sanity Check II: Does Feature Extraction Improve with Larger VLMs?

### Sanity Check III: How Does This Approach Generalize to Other Data?

### Possible Follow-Up
If these checks yield positive results, the next step will be to apply standard fine-tuning methods and compare the performance against Vision Transformers and low-rank approximations.

**[View Source Code on GitHub](https://github.com/Lezane/Movie-Genre-Classification)**
