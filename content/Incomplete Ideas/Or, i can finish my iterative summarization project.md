---
title: Or, I can finish my iterative summarization project
tags:
  - "#project-ideas"
---


it has been a while since the original paper was out, many achievements have been made in the field, and some techniques and the assumptions those techniques hinged on was no longer necessary or effective.
1. base models are capable and can be prompted to do summarization better than encoder decoder models,
2. chat-tuned LMs can act as judge, producing reward signals with quantizated models are fast.

Under these updates, there are still paradigm questions worth implementing as [verification of intuitions](/content/writings/intuitions.md).
1. so we don't need to go through behavior cloning because somebody else did it for us, how can we put the current models into an amplification cycle?
2. how does DPO play into the parts? what are some other implications of alignment methods?
