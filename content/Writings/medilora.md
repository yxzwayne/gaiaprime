---
title: Lessons from training Medilora
tags:
  - language-models
date: 2024-02-22
---

I have read countless papers ranging from optimizing the attention mechanism, extending context windows to training convergence dynamics. This is in part thanks to going on Twitter right before ChatGPT drops. So, I thought I know most aspects of large language models and AI on the conceptual level. Medilora is the first serious fine-tuning effort I have found myself to dedicate to, in part because this was a course project, in part because I thought "well I already think I know most stuffs, might as well try to apply as many of them here as possible." Naturally, this came with an abundance of trial and error, and I learned a lot of lessons that I would otherwise never have learned just from reading papers.

I think the forefront of them is that retraining an instruction-tuned language models may not work as effective as it would be.

The rest of this draft is WIP, will be updated later. In the meantime, our write up is available on the project's [GitHub](https://github.com/yxzwayne/Medilora/blob/09dbf914e47ef218ea7422161991867fd6c3fd99/report/Medilora_Final_Report.pdf).

## The Problem

Open medical texts are mostly in the form of academic papers studying novel medicine, biology and operation breakthroughs. Medilora started as two of my project-mates wanted to build a diagnosis model. I quickly told them it's gonna be hard, but then again what problem isn't? We started with a simple idea: fine-tune a language model on a large medical corpus, and then further fine-tune on public diagnosis conversations given a patient's symptoms. The public diagnosis dataset we found was from ChatDoctor; but the conversation qualities are so subpar we did not follow through with rigorous preference cleaning. This remained my regret.

## The work

WIP
