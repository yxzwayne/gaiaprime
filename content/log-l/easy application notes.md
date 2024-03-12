# Prerequisite course work or knowledge for this project

Prerequisite course: N/A.
Prerequisite knowledge: 
- Bayesian machine learning,
- variational inference,
- energy-based modeling,
- deep learning programming

# Means of Evaluation

Report and Manuscript

# Proposed Plan

Our work is inspired by key findings in the field, including:
- The significance of epistatic interactions in dictating mutation patterns linked to drug resistance, as discussed in "Efficient generative modeling of protein sequences using simple autoregressive models" (Nature Communications).
- The challenges in capturing higher-order epistasis through Generative Probabilistic Sequence Models (GPSMs), highlighted in "The generative capacity of probabilistic protein sequence models" (Nature Communications).

In the previous phase (FA23), computational biology methods and deep generative models were adapted and applied, fostering a robust understanding of the problem space. Key findings from experiments include:
- Variational Autoencoders (VAEs), specifically a previously deemed "simple" architecture, demonstrate performance on par with physics-based models (Potts model) in learning epistatic interactions within HIV sequence alignments, as evaluated by the r20[1] benchmark.
- The MSA Transformer model from the esm package[2] underperformed in generalizing to unseen sequences, particularly when new sequence alphabets were introduced.

The next phase aims to:
- Delve deeper into the latent space of VAEs to interpret labeled sequences and their mutation patterns.
- Examine the interpretability and utility of transformer blocks in encoder-decoder models, extending the capabilities demonstrated by MSA Transformers.
- Conduct a focused comparative study of VAEs and MSA Transformers in their ability to learn mutation effects in novel protein families, considering the inherent differences in their generalist vs. task-specific training approaches.

Adjacently, the MSA Transformer was trained to be a generalist model, where as the VAE architectures we replicate in our experiments were developed to be trained as task-specific models. This difference motivates a more rigorous study on critically comparing the VAE and the MSA Transformer in learning mutation effects in unseen protein families.

The student will develop and test hypotheses regarding mutation classification, mutation discovery and learning algorithms, then verify using modern computing libraries (Numpy, Numba, Jax and MLX). The student will consider alternative model architectures and verify using small-scale experiments and the r20 metric.

Regular meetings with project supervisor Dr. Avik Biswas will focus on progress assessment, code review, and discussion of experimental designs. Collaborative sessions with PI Professor Lyumkis will provide broader insights into genetics and biology, enriching the research perspective.

[1]: https://www.nature.com/articles/s41467-021-26529-9
[2]: https://github.com/facebookresearch/esm

Citation:
- Biswas A, Haldane A, Levy RM. Limits to detecting epistasis in the fitness landscape of HIV. PLoS One. 2022 Jan 18;17(1):e0262314. doi: 10.1371/journal.pone.0262314. PMID: 35041711; PMCID: PMC8765623.
- McGee, F., Hauri, S., Novinger, Q. _et al._ The generative capacity of probabilistic protein sequence models. _Nat Commun_ **12**, 6302 (2021). https://doi.org/10.1038/s41467-021-26529-9.
- Rao, Roshan and Liu, Jason and Verkuil, Robert and Meier, Joshua and Canny, John F. and Abbeel, Pieter and Sercu, Tom and Rives, Alexander. MSA Transformer. bioRxiv. 2021. doi: 10.1101/2021.02.12.430858. https://www.biorxiv.org/content/10.1101/2021.02.12.430858v1.

---
## Previous proposal

The objective of this research is to engage in experiential AI-driven investigation into HIV drug resistance evolution. Utilizing physics-informed machine learning and variational autoencoder-based deep neural networks, the project aims to identify and quantify epistatic interactions contributing to antiretroviral resistance. Key metrics include MSA alignment accuracies.  
  
Training will encompass computational biology algorithms, bioinformatic data pipelines, and ML/DL methodologies, particularly variational inference and latent variable models for feature selection and dimensionality reduction. The project will also allow student to explore other model architectures as the student sees fit.  
  
The research is structured into sprints aligned with milestones, encompassing data curation, model architecture selection, hyperparameter tuning, evaluation metrics assessment, and manuscript preparation. Essential computational frameworks and GPU resources have been identified for immediate project deployment.
  
Weekly sync-ups with PI Professor Lyumkis and Supervisor Dr. Avik Biswas will focus on git-based code reviews, algorithmic adjustments, and critical appraisal of newly-published, domain-specific literature. Iterative progress and insights will be disseminated in lab meetings.  
  
The work aspires to fill extant literature gaps by employing avant-garde ML techniques for granular insights into HIV resistance mechanisms.  
  
Referential literature:  
- McGee, F., Hauri, S., Novinger, Q. et al. The generative capacity of probabilistic protein sequence models. Nat Commun 12, 6302 (2021). https://doi.org/10.1038/s41467-021-26529-9  
- Avik Biswas, Allan Haldane, Eddy Arnold, Ronald M Levy (2019) Epistasis and entrenchment of drug resistance in HIV-1 subtype B eLife 8:e50524. https://doi.org/10.7554/eLife.50524  
- Dario Oliveira Passos et al. ,Structural basis for strand-transfer inhibitor binding to HIV intasomes. Science367,810-814(2020). DOI: 10.1126/science.aay8015
