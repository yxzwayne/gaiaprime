---
tags:
  - "#project-ideas"
---
LLM papers are polluted with a wasteful abundance of new terminologies that does not lead anywhere. Most hard problems (hardware and inference optimization, quantization) are rare to come by but easy to remember because they're impressive, but an immediate parse of most technique papers can quickly give one a coarse clusters of in-context learning, retrieval augmentation, context window extension, training dynamics, quantization (Github PRs >>>> papers with the exception of QuiP... maybe), etc. 


For each chunk of the paper, repeat:
- Check if question bank has questions,
- if has, iteratively ask each.
- Ask "what is the most scientific, empirical, technical, or just important question that we can ask when reading this excerpt from a paper?"
- Add to list

Prompt candidates:
- "Contemporary ai papers conflate in size and add a lot of useless noise. On the contrary, many classical machine learning papers are adept at explaining the problem and their works elegantly and succinctly, despite their problem being similar in complexity if not more intricate. Given the following abstract of a scientific paper, assume it is unnecessarily excessive, redundant, obfuscating and indirect, and optimize the writing such that problem, proposed solution and results and/or conclusions are clearly and simplistically expressed."
