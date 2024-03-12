---
title: Open-ended document classification via recursive summarization
---
# Abstract
Open-ended document classification with summarization is a novel approach to weakly-supervised document classification, a task that aims to categorize documents with minimal human supervision. Current methods in this domain rely heavily on user-provided seed information, which may not always be available, especially for domain newcomers. In this work, we make three main contributions: applying iterative amplification and recursive summarization to weakly-supervised document classification tasks, training a language model to generate document labels using said recursive summarization, and emphasizing the need to minimize human supervision by proposing a move away from human-generated seed words. With these advancements, we strive for a more accessible and user-friendly approach to document classification.
# Introduction
The rapid growth of the language model research landscape has resulted in a vast corpus of documents, demanding an efficient and automated categorization system. Previous weakly-supervised methods leverage metadata or expert-generated seed words, which are strong assumptions that may not always align with individual user's situations. What if a researcher in domain A starts to look This paper proposes an open-ended document classification system aimed at mitigating these assumptions and adapting to individual users' categorization preferences.

Inspired by recent advances in weakly-supervised text classification and Iterative Amplification and Recursive Summarization, we introduce a pipeline that combines supervised and unsupervised learning to generate concise document labels from summaries of the early parts of the paper. Our approach diverges from existing frameworks (e.g., Meng et al.) by incorporating human judgment in selecting model outputs as supervision, instead of relying on expert-generated labels. This adaptability facilitates a more personalized document categorization.

The proposed system contains two components: a strong agent pre-trained with various datasets and tasks, and a weak summarization agent for condensing document content into brief, relevant labels. The pipeline would operates iteratively, continuously refining the model according to user feedback while progressively shortening the generated labels.

While the experiments were limited by resources, we nevertheless demonstrated its ability to produce meaningful and accurate summaries and labels. We also documented the limitation of current experiment design. For future directions, the iterative and recursive nature of the approach may allow for continuous performance improvement based on user feedback, generating results tailored to individual needs.
# Related Work
## Weakly-supervised Classification
Weakly-supervised text classification methods have been previously investigated using human-generated seed words to guide the learning process. WeSTClass (Meng et al. 2018) leverages various weak supervision sources, including class labels, class-related keywords, or labeled documents, and applies either a Convolutional Neural Network (CNN) or Recurrent Neural Network (RNN) for classification. Its bootstrapped training process enables generalization across new domains. However, the use of human-generated seed words introduces ambiguity due to multiple interpretations of the same word.

To address this issue, ConWea (Contextualized Weak Supervision for Text Classification) utilizes a contextualized iterative framework that disambiguates the senses of seed words and word occurrences based on their contexts. Through this process, ConWea generates a contextualized corpus, which is employed to train the classifier and expand seed words iteratively. This method enables the addition of new contextualized keywords and refines the initial ambiguous seed words. 

A key limitation of both WesSTClass and ConWea is their assumption that users providing seed words are domain experts who can accurately specify the classes, which may not always be the case.

## Summarizing Books from Human Feedback
Our work builds upon key insights from two significant studies: "Learning to Summarize from Human Feedback" and "Recursively Summarizing Books with Human Feedback".

The former highlights the role of human feedback in training language models for high-quality summary generation. We adopt a similar feedback-oriented approach in our study, underscoring the significance of human evaluation in enhancing automatic summarization.

The latter employs a recursive summarization method for book-length documents, iteratively producing shorter summaries with human feedback. Our study also explores recursive summarization, albeit focusing on shorter text documents.

Both studies demonstrate the value of human feedback in improving the performance of machine learning algorithms in text summarization, a concept central to our research.


# Dataset
arxiv-metadata-oai-snapshot.json: https://www.kaggle.com/datasets/Cornell-University/arxiv 3GB
smaller arxiv data on Kaggle: https://www.kaggle.com/datasets/neelshah18/arxivdataset 24000+ papers, 72MB
## macrocosm/arxiv_abstracts
An ambitious project to index and embed all arxiv papers
(Nah, too large and only have abstracts)
https://huggingface.co/datasets/macrocosm/arxiv_abstracts
```Python
# from datasets import load_dataset  
# dataset = load_dataset("macrocosm/arxiv_abstracts", split='train[:10%]')  
## Instead, the parquet file can be straight up downloaded from the dataset hub.
```

## Final dataset selection for experiment:
[acl-publication-info.74k.parquet](https://paperswithcode.com/dataset/acl-anthology-corpus-with-full-text)


# Collect and Pre-process the Data
Collect a dataset of documents that are labeled according to our classification task. Pre-processing the data by cleaning the text and tokenizing it.
- I should also apply the fixed chunking algorithms here and create a new format of dataset as sequences of chunks that needs to be classified.
- In my experiment, I should iteratively train on each chunk and obtain a better version of the models.

# Experiment
In the original paper, the authors demonstrated their empirical finding that training just on the first subtree made the model capable of generalizing to all book texts.
In the beginning, they relied on supervised learning, repeatedly trained the BC model on the first leaf until the results look reasonable.

## From Learning to Summarize from Human Feedback: 
"existing automatic metrics for evaluating summary quality, such as ROUGE, have received criticism for poor correlation with human judgments"
- first collect a dataset of human preferences between pairs of summaries, 
- then train a reward model (RM) via supervised learning to predict the human-preferred summary. 
- finally, train a policy via reinforcement learning (RL) to maximize the score given by the RM; 
- the policy generates a token of text at each ‘time step’, and is updated using the PPO algorithm based on the RM ‘reward’ given to the entire generated summary.
# Steps
1. Preparing data
2. Choose a pretrained language model, we call it the Model, that we wish to train: GPT-2 on HuggingFace;
3. Decompose the paper into leaf chunks of 600 tokens;
4. Obtain training data:
	1. Demonstration: 500 samples, use human written summary AND labeling (replaced with gpt-3.5-turbo)
		1. OpenAI said it was trained with RLHF, and I essentially treat it as a human-level summarizer (which it is)
		2. The dataset contains only the first leaf node, which contains the abstract. This is where it was made possible to compare the ROUGE score.
		3. The demonstration dataset only has 500 samples in my experiment.
	2. Comparison (RL): run the Model to produce 2 outputs at temperature 1.
		1. Human rank whether which output between the two is better. This data is being used to train the reward model.


$$
egin{table} 
