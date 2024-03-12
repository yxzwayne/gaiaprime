---
title: Implementing Unsupervised Image Clustering
tags:
  - project
  - computer-vision
---

I wanted to see how many clusters or classes an algorithm or system can discover from my iCloud photo album. I keep images throughout the year and there are many memes across it. 

Also, my images are typically large in size, and despite there are only 10k of them, the computing should still turn out to be a nice programming practice.

I also want to implement some sort of feature learning, given that it was a huge deal when I studied deep learning mathematics under Prof. Belkin. Feature learning is intuitive to reason in image learning tasks, because it is natural that an image contains many useful regions or features that can act as representations. This kind of open-endedness should be well-captured in the modern diffusion literatures.

Some of the open questions I stumbled upon include how I represent the images (I thought of convoluted matrices and just flattening), and the next step should be training a neural represnetation for the entire image dataset.

In this direction, I have looked into training VGG or ResNets; modifying them for unlabeled representation learning turned out to not be conceptually intuitive to me as I thought it would.

