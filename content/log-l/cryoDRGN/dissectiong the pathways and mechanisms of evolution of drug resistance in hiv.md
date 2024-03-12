Avik Talk, Jan 24, 2024
# Motivation
- emergence of pan-resistant HIV
- No vaccine yet, increasing drug resistance
- No more drug target for the HIV, so switching target isn't viable.

Fitness of drug-resistant variants of HIV
- Most of the mutant sequences with a single mutation (show in HIV protease) have a lower melting temperature, which means lower fitness, than the wild-type sequences
- 75% of sequences in the HIVDB have more than 3 inhibitor-associated mutations. If so detrimental,
# Intro to Methodology: Protein Sequence Covariation Analysis
Fitness landscape of HIV proteins
Covariation analysis, sequence -> function (fitness)
contacts in protein structure -> compensatory mutations -> correlations in MSA columns
![[Screenshot 2024-01-24 at 09.38.51.png]]

If we mutate one, we will likely mutate another.
- Observed correlations in an MSA can correspond to both direct and indirect statistical dependencies
Potts model filters indirect statistical dependency out from direct statistical dependencies.
Questions regarding Potts model:
- how many accessories mutations are needed in HIV proteins to entrench mutations?
- are there particular patterns or motifs of mutations that cause entrenchment?
- how strong is the entrenchment effect?
## Understanding the mechanism of evolution of INSTI resistance
Double mutant cycles indicate strength of interactions between pairs of mutations. This is essentially a pairwise interaction model;
- look at the combined effects of two mutatinos and each single mutation in the sum;
- We say there is epistasis when the sum minus two independent mutation energy is not zero; vice versa.
Dmitry question here:
- Potts model input is the patient received drug treatments
- if we are to look at natural evolution of HIV-1, would we see the same mutation arise? or are the data to the Potts specifically selected because they are drug-resistance?
- HIV resistence mutation is much to be a detriment and do not correlate with other mutations

mutations exist, but we don't know how strongly-coupled they are to each other and why. The coupling between S-H is exceptionally strong (either through the plot or through other experiments)
Tao: can we predict mutations happening in the future?
- Given a dataset, predicted where the mutation may occur, looked at data collected some time after the dataset was collected, and the
## Pathways
what are the distinct order of events (pathways) that lead to complex drug resistant variants?
- Explicitly follow the temporal ordering of mutations leading to highly resistant variants in vitro
- start from a sepcific sequence (NL4-3)
- then, only specifica mutations are allowed at some residue positions.
All the structures of proteins were obtained from patients, so the ordering of events occurring is natural.

The sequences are collected from mostly patients treated with RAL. Structures are with DTG bound.
We then had a Structure - Rationale table

Are the pathways we predicted drug-specific?
- potts models are based on patients treated with RAL. Can this generalize to DTG?
We can bin the sequence data based on the drug usage;

## Modify the ml model to obtain drug-specific pathways
self interactions, which is residue-residue pairs, plus external environment factors, such as binding pcoket shape, hydro phobic/philic, resistance mutations.
In the MSA, add extra column with environment informations
- can we add positional embeddings?

# Other pathway questions
- what are the mechanisms by which G118R and R263K lead to loss of DTG binding? why is 4d more potent than DTG against this set of resistant variants?

# Constraint pathways
what is the constraints and what's not having them? - having the same starting sequences, but you can have any possible mutations;
evaluating evolutionary trajectories in vivo:
- constraints are removed when looking at evolutionary trajectories in patients:
- mutations can happen anywhere and even abck mutations are allowed.
- How to look at the problem?
	- Initiate a seed sequence(s)
	- try to mutate it every time it's accepted or rejected with a probabilities
	- end up with sequences with all mutations,
	- Then what?
- In the temporal evolution of the drug resistant viral population
- drug-naive going through drug-pressure will spread out the mutation types,

Groups of mutations that follow similar orderings 

Relevance and questions to VAE:
maybe the features VAE are learning are no more different than that from an independent model, and potts model that kind of stuff better.
- Does this mean potts can 
