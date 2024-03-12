---
title: Implementing FunSearch (DeepMind)
tags:
  - "literature-review"
---
Mathematical discoveries from program search with large language models
https://www.nature.com/articles/s41586-023-06924-6

# Goal
Generate a ‘solve’ program, such that its outputs receive high scores from the ‘evaluate’ function (when executed on inputs of interest), and ultimately improve on the best-known solutions.
# Approach
Searching in the function space:
- Pairing an LLM with a systematic evaluator,

# Procedure
1. Sample best performing programs and feed them back into prompts (best shot prompting)
2. start a program skeleton and only evolve the part governing critical logic.
3. Maintain a pool of programs by using island-based evolutionary methods

Input: specification of the problem === evaluator function
Iteration:
- builds a prompt by combining programs sampled from the database,
- feed prompt to LLM 

Where do we get specification?
