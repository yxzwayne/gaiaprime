Main interest:
- latent space mapping
- learning higher order epistasis
	- know whether it exists

# Todo
- [x] Write a script to split any incozAming sequence data with the ratios specified in the parameter
Given: 6M.exper.seq
- [x] Generate test sequences from sVAE and DeepVAE
- [x] generate transformer sequences
- [x] redo deepVAE training and generation
- [x] generate plots that contain all the model performances. 
- [x] Upload sequences to server
	- [x] indep
	- [x] potts
	- [x] svae
	- [x] dvae
	- [x] modify plot code to generate plot instead of showing
	- [x] generate the plots for both svae and dvae generated codes
- [ ] repeat these for integrase and reverse transcriptase sequences
- [ ] after finishing all 1-3, start mining the latent spaces.

# Experiments
Number of sequences to generate: 1048576

Dmitry question:
can we mine latent space to provide insights into epistatic coupling in response to treatments with different drugs with respect to treatments with different drugs?
- if the VAE works, then yes, but experiemnt result seems negative.
The 6M is protease, can check othe three more kinds of proteins;
next, integrase -> then, reverse transcriptase

# Alphabet Reduction
Why do I see the sequences I'm working with in ABCD? Aren't nature of life encoded in ACTG?
* The technique is called alphabet reduction! 
* Avik Biswas elife 2019, William Flynn Allan Haldane HIV Molecular Biology & Evolution, 2017

## How can we make up for the lack of the constraint of joint frequency in the VAEs?
Some thoughts:
1. Introduce an additional regularization term in the loss function that encourages the model to fit the joint frequencies of amino acid pairs from the target MSA. This could be done by incorporating a term that measures the difference between the predicted and target joint frequencies, which would guide the model towards learning the desired statistics.

2. Modify the VAE architecture to explicitly include a component that models pairwise dependencies, similar to how Mi3 is designed. This can be achieved by incorporating a GPMM-like module within the VAE or by training an additional GPMM alongside the VAE and jointly optimizing their parameters.


# Project Roadmap
1. [https://www.nature.com/articles/s41467-021-26529-9](https://urldefense.com/v3/__https://www.nature.com/articles/s41467-021-26529-9__;!!Mih3wA!Fn8Cim9HLE-aI6F-W_8iYCin2MzqFhgqYc9dLiHYA8Yn1cG5cEXKuseeaFLzCbrO1ikTskHPqyStr1n6gjU$): 
	1. Compares deep neural network models such as VAEs with a more established physics-based model called the Potts model (a subclass of Boltzmann machine learning models) based on sequence covariation.
2. [https://elifesciences.org/articles/50524](https://urldefense.com/v3/__https://elifesciences.org/articles/50524__;!!Mih3wA!Fn8Cim9HLE-aI6F-W_8iYCin2MzqFhgqYc9dLiHYA8Yn1cG5cEXKuseeaFLzCbrO1ikTskHPqySthnBzJkA$) : 
	1. Setting up the research direction that we are building up on, using the Potts model to study the evolution of drug resistance in HIV.

3. [https://www.science.org/doi/abs/10.1126/science.aay8015](https://urldefense.com/v3/__https://www.science.org/doi/abs/10.1126/science.aay8015__;!!Mih3wA!Fn8Cim9HLE-aI6F-W_8iYCin2MzqFhgqYc9dLiHYA8Yn1cG5cEXKuseeaFLzCbrO1ikTskHPqySt1DRlLGk$): 
	1. The structure of the HIV intasome, which is the target of the latest generation of drugs against HIV, and a major component in our proposed research direction.

HIV Biology [https://en.wikipedia.org/wiki/Structure_and_genome_of_HIV](https://urldefense.com/v3/__https://en.wikipedia.org/wiki/Structure_and_genome_of_HIV__;!!Mih3wA!Fn8Cim9HLE-aI6F-W_8iYCin2MzqFhgqYc9dLiHYA8Yn1cG5cEXKuseeaFLzCbrO1ikTskHPqyStAduArt4$)

---

Project Milestone 1: build VAEs on HIV protein sequences from drug-experienced patients, run them through the different metric developed in paper 1 as a control to compare with established models of sequence covariation such as the Potts model, that captures 'epistasis', i.e., the evolutionary interaction network between different residue positions in the protein (see papers 1 and 2). 
	The project can be led into multiple directions to answer varied biological questions related to drug resistance, that are all highly relevant. But this depends on your interest and more importantly, the time and effort that you are able to put in.


Given 5000 natural sequences, trained a Potts model (Boltzmann Machine) to generate 10M sequences.