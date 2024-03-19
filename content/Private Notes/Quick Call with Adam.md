- synthetic data is like 20% of my waking thoughts these days
- essentially building search engine as a service
- the idea is, given an arbitrary dataset of arbitrary modality, how do you process, understand, and restructure the data such that you can support really fast really good semantic search
	- This may need some joint or contrastive embedding breakthrough.
- QA synthesis has been super clutch for eval, but playing with using it for indexing and fine tuning on data upload
- focusing on just text data, keeping response time under 500 ms including network calls, Node.js and python SDKs, and custom metadata filtering
- Pure embedding search is pretty bad in most cases imho. Usually there needs to be a keyword ranking component too. e.g. when searching for a paper name the authors often gave their model or method a short name that normal vector sim search cant cope with.

Just got the azure credit, 25000
Adam worked for many projects and startups, and he kept making the same system.
With transcript, being able to attribute who said what is a lot harder. Try to chunk up the audio to meaningful way.
Clustering audio cuts and 
Scale of data? Some are small, some are all of the building codes,
Just the idea of very general evolutionary processes optimization processes. The approach they are taking here is that search is heuristic based, even the chunking thing, even things like html parsing. the approach to break the market is the leverage compute and generalized approaches.
dirty secrete: using computer vision to parse,
using off the shelf, trading speed and price for performance and convenience, once we validate market, then we gotta get cost down
- crazy idea: whenever a search index is created, can we take whatever amount of data and then try to generate enough synthetic data using that to then fine-tune our own LoRA, so we have our own embedding models,

for intelligent semantic search to be functional primitive that everyone has in the stack, it has to be performant and fast. with long context model, we can't even do multi-turn retrieval and style conversation. even with long context, it's taking us many seconds to take the response back. in software, the search time scales very poorly. We gotta provide stupid fast LLM level semantic search as core primitive that developers can use. Abstract as many garbage away. whether pdf, textbook, html, they can upload and query.

physics -> microsoft, in azure, automating call centers, two guys, one guy informatics, graduated a year before me. performance is his speciality, third guy, management consulting, A&M, pitching AI strategies to Fortune-500,
point is.

What I would like to work on:
- Synthetic data generation,
