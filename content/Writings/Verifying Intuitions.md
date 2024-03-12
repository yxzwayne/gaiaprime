---
title: Verifying Intuitions
date: 2024-02-20
---
This is a semi-serious rant.

Recent work by [Yao et al.](https://arxiv.org/pdf/2402.10171.pdf) on universally scaling language model context lengths built on the hypothesis that "the capability of utilizing information anywhere within the 128k context is already in the base model, and can be readily “unlocked” by lightweight continued pretraining."

Of course, the claim is intuitively sensible. Indeed, the entire project withstands initial scrutiny...

Anyway, their experiments also verified that:
- naively upsampling training data is suboptimal,
- balanced domain mixture is important.

Both of these claims have been persistent lessons in making a good machine learning model: class imbalance in a dataset causes subpar performance of a classifier (hell, I haven't verified this yet)Data quality is also crucial for deep learning models, particularly in vision and language. This likely underpins the intuition behind data pruning and deduplication efforts.

Additionally, early scaling law literature, such as Kaplan et al. and Hoffmann et al., overlooks data quality in general. Context length was not considered a relevant model parameter back then for their research scope, so long data quality also did not stand out. However, it has been a growing topic, as many have been discussing the necessity of extending context window, both for just plain and simple ease of mind, and for "replacing RAG". 

It is retrospectively natural to think about the problem "how can we improve a long-context model to better use or attend to later parts in the input," but I speculate the reason Yao et al. get to ship this amazing work is that they have played with the long-context models (perhaps specifically curious about the performance of open models on the Needle-in-a-Haystack test). The journey from experimenting with the model to forming their hypothesis can also be attributed to experience.

---

I am sure the bittersweet feeling of an intuition getting "worked out" by other people is somewhat a walk in the park for any serious researcher. For someone aspiring to be a quick shipper, however, this serves as good stimulation. 

Overall, I really like seeing classic intuitions being applied to novel directions *that matters*. Further, I simply don't think I cared about context window sufficiently to have thoughts as relevant as "I wonder if these models ever trained on long texts" or "man i sure wish these open models can catch up on the needle test." I do think that if I have them, I would be able to hypothesize the same.

So, if Sutton's Bitter Lesson is to leverage more compute than human knowledge, mine would be two parts:
- verify as many intuitions as possible.
- think deeply and more critically in general. I read [kaiokendev's context window extension post](https://kaiokendev.github.io/context) very early, and have kept up to date with every advancement in context window size. When I see 32k context window being realized the first time, I had the feeling of "this is gamechanging for assistant-oriented tasks," and never acted on it because I did not think about it long enough to start caring.

In similar spirit to the Bitter Lesson, instead of telling myself "personal devices are not going to provide enough compute for powerful local assistants," I should just hack on the software stacks under the assumption that they will provide enough compute one day.


# References

Fu et al. "Data Engineering for Scaling Language Models to 128K Context." arXiv, 2402.10171. (2024)

Sorscher et al. "Beyond neural scaling laws: beating power law scaling via data pruning." arXiv, 2206.14486. (2023)

Kaplan et al. "Scaling Laws for Neural Language Models." arXiv, 2001.08361. (2020)

Hoffmann et al. "Training Compute-Optimal Large Language Models." arXiv, 2203.15556. (2022)
