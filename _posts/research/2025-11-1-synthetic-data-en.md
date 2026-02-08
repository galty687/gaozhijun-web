---
layout: post
title: "Building Large-Scale Synthetic Tibetan Datasets"
excerpt: "Synthesizing large-scale Tibetan datasets to enhance LLM capabilities in Tibetan"
tags: [NLP]
comments: true
category: research
lang: en
---




## Project Source

Commissioned by:

Principal Investigator: Zhijun Gao

Project Duration: November 1, 2026 - June 1, 2026

## Research Tasks

Due to the insufficiency of natural Tibetan data, this project explores large-scale generation of high-quality Tibetan datasets through synthetic data approaches.



### **Project Objectives**

1. **Synthetic data quality benchmarked against natural data**

   - Maintain consistency with natural data in key linguistic features such as vocabulary, syntax, semantics, and discourse, with no significant differences (statistical test *p* > 0.05; also providing effect size thresholds, such as `|d| < 0.2 / KL` divergence below a set threshold).
   - Validated through both manual spot-checking and automated quality assessment (including metrics for fluency, grammatical correctness, factual consistency, translation fidelity, etc.).

2. **Multi-domain data resource pool with balanced distribution**

   - Build a Tibetan dataset covering core domains including science and technology, geography, history and culture, education, public services, etc.
   - Ensure sample sizes in each domain reach preset scales while preventing excessive scarcity in long-tail domains

3. **Multi-task data types covering high-frequency use scenarios for Tibetan users**

   - Data task type coverage: Chinese-Tibetan/Tibetan-Chinese translation, summarization/key point extraction, dialogue response, concept explanation, QA retrieval-based generation, writing polishing/rewriting, etc.

4. **Usability objectives for training and evaluation**

   - Synthetic data can be directly used in mainstream training pipelines (cleaning, deduplication, annotation fields, complete metadata), forming a reusable data generation and quality control pipeline.
   - Deliver quantifiable gains on downstream benchmark tasks (e.g., translation BLEU/COMET, QA accuracy, summarization ROUGE improvements reaching preset targets), and provide comparative experiment reports for "natural data only / synthetic data only / mixed data."
