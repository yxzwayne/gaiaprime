# Readings

Watch Lecture or Read Blog Carefully:
    - Data Management: https://fullstackdeeplearning.com/course/2022/lecture-4-data-management/

Optional:
    - More Background on Data Operations: https://docs.google.com/document/d/10K3pYTNvreVy5hl2EqWf_LX3mMW4CQw1TdMrHplMu00/edit#heading=h.ygqitxw2cpfv
    - How ML Breaks A Decade of Outages for One Large ML Pipeline: https://www.usenix.org/conference/opml20/presentation/papasian
    - High Level Landscapes (good for shared vocab)
        - https://foundationcapital.com/foundation-model-ops-powering-the-next-wave-of-generative-ai-apps/
        - https://www.madrona.com/foundation-models/
    - All my machine learning problems are actually data management problems - Shreya Shankar: https://www.youtube.com/watch?v=sr3_DQ-RhTc
    - CleanLab: https://www.youtube.com/watch?v=aAUBK8gueHM

Tools/ Open Source Libraries:
    - Airflow (https://airflow.apache.org/) is a standard scheduler for Python, where it's possible to specify the DAG (directed acyclic graph) of tasks using Python code. The operator in that graph can be SQL operations or Python functions.
    - Apache Arrow: https://huggingface.co/docs/datasets/v1.16.0/about_arrow.html and https://arrow.apache.org/
    - Apache Beam: https://huggingface.co/docs/datasets/v1.16.0/beam.html and https://beam.apache.org/
    - Model Versioning: https://github.com/r-three/git-theta
    - Feature Stores (https://www.uber.com/blog/michelangelo-machine-learning-platform/)
    - Data Versioning (DVC, GitLFs, etc)
    - LabelStudio (https://labelstud.io/) is an open-source solution for performing annotation yourself, with a companion enterprise version. It has a great set of features that allow you to design your interface and even plug-in models for active learning!
    - Snorkel (https://github.com/snorkel-team/snorkel) is a dataset management and labeling platform that uses weak supervision, which is a similar concept. You can leverage composable rules (e.g., all sentences that have the term "amazing" are positive sentiments) that allow you to quickly label data faster than if you were to treat every data point the same.

# May 2

## Building ML Models Like OpenSource Software

Why we want fine-tuning efficient strategies;
- Flan and the two papers there
There is a need for efficient parameter tuning approaches to get better models
- Relationship to retrieval augmentations?

### FISH Masks 
merging:
- isotropic merging
- fisher merging -: augmented an $F_i$ into the equation;
- averaging weights get better performance: 
- // TODO: look into where else 
	- Average perceptrons

### ColD Fusion

### SMEAR:
soft merging of experts with adaptive routing - 
learning the lambdas


## FLAN
Minimum bayes risk decoding - different from beam search; - MBR is classical technique, pre 2015;

# Self-reflect is a relevant technique for recursive improvements

# May 9. 
## Few-shot PEFT
For every different task T, they introduce different set of parameters to train and learn;
Questions:
- why not evaluate on T5 for fair comparison with complete fine-tuning? T0 was already ft'ed on multi-task datasets!
- Does the RAFT benchmark consist of different tasks than what T0 already saw?
- why have three loss terms when L_LN when behaviro subsumes the nature of L_LM and L_UL ?
- Scaling vectors are learned for each task, how does this mean generalization to new unseen tasks, etc.

## Jobs and Markets
- AMD, Samsung, Twitter, 
- applied research feels similar;
- combine the paper/publications with KPIs, business goals;
- **Startups**: smaller and earlier stage: building demos, put in slides for next round of investment, etc;.
GPU / TPU utilization is a benchmark for training jobs;
Utilizing open source spaces, i.e. CohereAI, other startups, etc.
