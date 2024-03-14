---
tags:
  - "#project-ideas"
---
The font is Soehne
Comment from S2
- The font is not fixed-width, consideration needs to be made about this.
- Can also assume that the majority of information which is redacted is about Google
Asked by Spike:
- can't we do top-k and then filter out things that 1. aren't real words, and 2. aren't a valid length [a..b]
- 2. is trivial and 1. is doable with a spellchecker
S2:
- per-redaction or per-line may be a better predictive method, calculating error based on observed vs. control word lengths and then using a top-k rank descending of the solutions with the lowest error rate. but maybe there's someone here more language specialized with a more intuitive method

provide likely solutions which are within a range +/- 1 unit of the predicted word length, and then compute a per-predicted-word error, and then composite that into a mean error rate that can be used to generate and rank solutions
