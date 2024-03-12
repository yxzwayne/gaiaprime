# 1. Paper Discussions
## Mining Quality Phrases from Massive Text Corpora - 2015
This paper identifies the weakness of using raw frequency-based phrase mining and reasons through the previous heuristics used to tackle those weaknesses.
- The context information is lost when we only collect the frequency counts.
The paper proposes **phrasal segmentation** to rectify the raw-frequency approach:
- This technique assigns every word occurrence to only one phrase as a "non-composible semantic unit". This allows phrases with large similarities (i.e. Jaccard similarity) to have different scores.
- The technique integrate the segmentation with the phrase quality assessment, which in turn helps improve the segmentation;
- The proposed method is scalable and easily parallelize;
- The effectiveness, accuracy and generality of the model is demonstrated through empirical experiment results.
One key point I really like is that the authors acknowledged that a sequence's segmentation may not be unique due to two reasons: the subjective nature of regarding a word sequence as a phrase or not, and the potential ambiguity and multiple interpretations of a sequence. However, even with imperfect segmentation, a reasonably high-quality segmentation can still retain support for popularly adopted phrases in a large document collection.
## Automated Phrase Mining from Massive Text Corpora - 2017
In the field of data-driven phrase mining techniques, none of the state-of-the-art models is fully automated because they require human experts for designing rules or labeling phrases, such as SegPhrase. Such approach suffers from scaling weaknesses, i.e. when dealing with large corpus in new knowledge domains. This paper argues that one can easily obtain many quality phrases from public knowledge bases on a scale larger than that produced by human experts. Hence, this paper 
1. proposes Robust Positive-Only Distant Training, a novel framework that effectively uses such quality phrase abundance;
	1. The framework is built on the argument that domain-specific quality phrases are also more likely to appear as high quality in generic corpus; this framework minimizes human expert dependency.
2. provides a part-of-speech (POS) guided phrasal segmentation model, which incorporate a _pre-trained_ part-of-speech (POS) tagger and leverages shallow syntactic information in the POS tags to guide the segmentation model;
	1. so basically, the POS tags and the phrase segmentation model complements and improves each other.
## (b) What is the major problem when someone is going to apply SegPhrase to a new corpus? Is there any human effort?
The major problem with applying SegPhrase to a new corpus is that it requires human expertise for it to function well. The paper started introducing human effort in 5.4 Evaluation in the Pooling paragraph. 
Most of the existing methods, SegPhrase included, require human experts to select and annotate phrases. Intuitively, this task couldn't possibly scale well when there are millions of new documents for a new corpus from a new domain. This reliance on manual efforts by domain and linguistic experts can be an impediment when trying to scale the analysis of a new massive, emerging text corpora.
## (c) What is the motivation of **AutoPhrase**? Compared with SegPhrase, which parts do you believe are novel?
The motivation for AutoPhrase is to address the challenge of needing human expertise in phrase mining, especially in new and emerging domains. AutoPhrase also proposes a more rigorous framework, having the pre-trained tagger and the segmentation model improve each other. In my opinion, both the distant training and the POST guided tagging are considered novel. 
First, it is intuitive that a high quality phrases in a domain-specific corpus will also have a strong presence in the general knowledge base, but it may have been empirically hard to conclude or even verify. Once this thesis is realized, the problem of phrase mining is now easier to scale up as we have more text data, a significant improvement over the human-relying SegPhrase.
Secondly, using a pre-trained POS tagger is a direct followup of the spirit that quality phrases exist in general knowledge base; its effect of co-improvement with the segmentation model is another novel aspect that I think paved the way for scalable phrase mining in larger corpuses. It also made it possible to have more accurate phrasal segmentation without relying on complex, trained linguistic analyzers.
## (d) Why do we want to evaluate the results following the pooling strategy?
In "Mining Quality Phrases," pooling is the act of selecting a subset of $k$ questions and provide them to human evaluators, forming a pool that is then evaluated by human reviewers. This significantly reduces the number of phrases that need to be manually evaluated. The paper used $k=500$. 
The phrases in the pool are Wiki-uncovered, probably indicating that Wikipedia is not a complete source of quality phrases? Having the AutoPhrase knowledge, this means that the pooling evaluation concerns with phrase that are not necessarily empirically quality, and that the human ev aluators need to identify quality phrases that are not already recognized in a well-established knowledge base like Wikipedia.
Further more, there were only 3 human evaluators, thus human resource was scarce. Pooling reduced the workload each evaluator needed to fulfill, quite possibly at the cost of review rigor.
## (e) What are the drawbacks of these two papers? Do you see any limitations?
There are a couple of limitations I could think of:
1. Reliance on Wikipedia and Pre-trained POS Taggers: The model uses Wikipedia as a major data source. What if a culture's language doesn't have a strong presence in Wikipedia? Those people would fall back to relying human experts.
2. The evaluation strategies used in the papers may not completely reflect the real-world performance of the methods. The use of Wikipedia phrases as ground truth in evaluations could introduce bias, as it assumes that all high-quality phrases are present in Wikipedia, which is not always the case. Similarly, the pooling strategy for evaluation, while efficient, may not fully capture the ability of the method to identify high-quality phrases in the entirety of a large corpus.
3. The methods aim to minimize the reliance on complex linguistic analyzers, which can be difficult to adapt to new domains or languages. Some level of linguistic analysis, such as POS tagging, is still required. This could be a limitation in scenarios where such tools are not readily available or accurate for the specific language or domain.

## (f) Can we do better in order to address these limitations? Propose a few ideas and explain how these would address the limitations.
1. Advancing the general knowledge base: recent breakthroughs in smaller LLMs, such as Vicuna, empirically demonstrates that it we can make small models very effective in producing the output we want. What if we can specifically train a generalist mining model? 
2. Retrieval-augmented knowledge base as an expansion direction: AutoPhrase relies on Wikipedia and pre-trained POS taggers. What if we encounter a new domain and we want to incorporate a large amount of raw text corpus from that discipline? One way to improve the approach could be to leverage recent retrieval research, such as Retro (Borgeaud et al. 2022) and Forward-Looking Active Retrieval Augmentation (Jiang et al. 2023) to further amplify the capability and efficiency of the general knowledge base and higher quality of the phrase mined from the knowledge base. 
	1. For instance, integrating specialized encyclopedias or databases for specific domains (like PubMed for medical texts) could enrich the pool of high-quality phrases for those domains instead of going through another training phase.
3. What if we can stop relying on POS tagging? I think the use of linguistic features is nice, but I really want to do some empirical experiments myself before verifying this claim.
# 2. Phrase Mining experiments
## (b) 
- Did you find any phrases with abnormal scores (e.g. non-phrase with a high score or good phrase with a low score)?
	- I believe there are plenty of such abnormal scores. However, I didn't find any non-phrase with high scores by looking with my eyes.
	- For what I have looked into, Microsoft Excel was one of the higher scores, which I don't know why it would be given the significance it has.02
	- Some of the phrase with high scores are abbreviations that is hard to read, such as: eb n0, fft ifft, etc.
- Do they show a systematic pattern? What can be the possible reason behind it and how to improve the algorithm to avoid such mistakes?
	- The abbreviations caught my eyes because it is likely (actually also very reasonable) to assume that they mean something in their respective fields and hold much significance. However, just by the abbreviation, I couldn't tell what they are. One way to remedy this is to have a word-bank of popular abbreviations and map it to what they actually mean. This could also achieved by a pre-trained tagger or some other architectures.
## (d) For output, please see cluster_phrases.txt in my submission files.
After comparing the outputs, I find that GMM has more occurrences of repeated phrases across clusters. 
- For example, the phrase "residuated lattices" and "simplical complexes" appeared in 5 out of 6 clusters! This is a near 66% unideal rate!
- From this perspective, the K-means clustering yielded a marginally better performance on my end.
However, both methods yield pretty much similar results for most of the phrases, and the differences are relatively minute. 
