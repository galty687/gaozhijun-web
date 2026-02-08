---
layout: post
title: 大规模藏文合成数据集的构建
excerpt: 合成大规模藏文数据集用于提升大模型藏文能力
modified:
tags: [NLP]
comments: true
category: research
title_en: "Building Large-Scale Synthetic Tibetan Datasets"
excerpt_en: "Synthesizing large-scale Tibetan datasets to enhance LLM capabilities in Tibetan"
---

<div class="lang-zh" markdown="1">




## 项目来源

委托方：

负责人：高志军

项目周期：2026年11月1日-2026年6月1日

## 研究任务

天然藏文数据不足，探索通过合成数据的方式，大规模生成制造高质量藏文数据集。



### **项目目标**

1. **合成数据质量对标天然数据**

   - 在词汇、句法、语义与篇章等关键语言特征上，与天然数据保持一致性，差异不显著（统计检验 *p* > 0.05；同时给出效应量阈值，如 `|d| < 0.2 / KL` 散度低于设定阈值）。
   - 通过人工抽检与自动化质量评估双重验证（含流畅性、语法正确性、事实一致性、译文忠实度等指标）。

2. **覆盖多领域、且分布均衡的数据资源池**

   - 构建覆盖科技、地理、历史文化、教育、公共服务等核心领域的藏文数据集
   - 各领域样本数量达到预设规模，并控制长尾领域不过度稀缺

3. **覆盖藏族用户高频使用场景的多任务数据类型**

   - 数据任务类型覆盖：汉藏/藏汉翻译、摘要/要点提取、对话回复、概念解释、问答检索式生成、写作润色/改写等。

4. **面向训练与评测的可用性目标**

   - 合成数据可直接用于主流训练流程（清洗、去重、标注字段、元数据齐全），形成可复用的数据生成与质检流水线。
   - 在下游基准任务上带来可量化增益（例如：翻译 BLEU/COMET、问答正确率、摘要 ROUGE 等提升达到预设目标），并提供与"仅天然数据/仅合成数据/混合数据"的对比实验报告。


</div>

<div class="lang-en" markdown="1">




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


</div>
