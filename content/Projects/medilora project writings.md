---
title: Project Medilora
tags:
- language-models
---

# Related Work: Meditron
## dataset
- **Medical Paper Abstracts**: 16.1M abstracts extracted from closed-access PubMed and PubMed Central papers.
- **Medical Papers**: full-text articles extracted from 5M publicly available PubMed and PubMed Central papers.
- **Clicnical Guidelines**: `epfl-llm/guidelines`
- 400M tokens sampled from `togethercomputer/RedPajama-Data-1T`


Constructing Preference Dataset from embedding dataframe
- [x] Take 500 rows of data, put inside a smaller dataframe


## Reminder to include:
Sure, the revised table with the standard error (stderr) terms next to the accuracy (acc) values and the omission of the normalized accuracy (acc_norm) row is as follows:
The table, reformatted to include only the accuracy (acc) values along with their standard errors (stderr), and excluding the normalized accuracy (acc_norm) rows, is presented as follows:

|                               | hendrycksTest-anatomy | hendrycksTest-clinical_knowledge | hendrycksTest-college_biology | hendrycksTest-college_medicine | hendrycksTest-high_school_biology | hendrycksTest-medical_genetics | hendrycksTest-nutrition | hendrycksTest-professional_medicine | hendrycksTest-virology |
| ----------------------------- | --------------------- | -------------------------------- | ----------------------------- | ------------------------------ | --------------------------------- | ------------------------------ | ----------------------- | ----------------------------------- | ---------------------- |
| **OpenHermes-2.5-Mistral-7B** | 0.5704 (± 0.0428)     | 0.6755 (± 0.0288)                | 0.7083 (± 0.0380)             | 0.5723 (± 0.0377)              | 0.7677 (± 0.0240)                 | 0.6900 (± 0.0465)              | 0.7353 (± 0.0253)       | 0.6581 (± 0.0288)                   | 0.5361 (± 0.0388)      |
| **Medilora**                  | 0.5556 (± 0.0429)     | 0.6453 (± 0.0294)                | 0.7014 (± 0.0383)             | 0.5896 (± 0.0375)              | 0.7355 (± 0.0251)                 | 0.6800 (± 0.0469)              | 0.6863 (± 0.0266)       | 0.6324 (± 0.0293)                   | 0.5181 (± 0.0389)      |

This format simplifies the table while maintaining the essential information about each test's accuracy and its variability.
# MMLU-Medical Results
hf-causal (pretrained=Medilora/medilora-mistral-7b), limit: None, provide_description: False, num_fewshot: 0, batch_size: None

## MMLU-Medical scores for Medilora-Mistral-7B

|               Task                |Version| Metric |Value |   |Stderr|

|-----------------------------------|------:|--------|-----:|---|-----:|

|hendrycksTest-anatomy              |      1|acc     |0.5556|±  |0.0429|

|                                   |       |acc_norm|0.5556|±  |0.0429|

|hendrycksTest-clinical_knowledge   |      1|acc     |0.6453|±  |0.0294|

|                                   |       |acc_norm|0.6453|±  |0.0294|

|hendrycksTest-college_biology      |      1|acc     |0.7014|±  |0.0383|

|                                   |       |acc_norm|0.7014|±  |0.0383|

|hendrycksTest-college_medicine     |      1|acc     |0.5896|±  |0.0375|

|                                   |       |acc_norm|0.5896|±  |0.0375|

|hendrycksTest-high_school_biology  |      1|acc     |0.7355|±  |0.0251|

|                                   |       |acc_norm|0.7355|±  |0.0251|

|hendrycksTest-medical_genetics     |      1|acc     |0.6800|±  |0.0469|

|                                   |       |acc_norm|0.6800|±  |0.0469|

|hendrycksTest-nutrition            |      1|acc     |0.6863|±  |0.0266|

|                                   |       |acc_norm|0.6863|±  |0.0266|

|hendrycksTest-professional_medicine|      1|acc     |0.6324|±  |0.0293|

|                                   |       |acc_norm|0.6324|±  |0.0293|

|hendrycksTest-virology             |      1|acc     |0.5181|±  |0.0389|

|                                   |       |acc_norm|0.5181|±  |0.0389|


## MMLU-Medical scores for OpenHermes-2.5-Mistral-7B

|               Task                |Version| Metric |Value |   |Stderr|

|-----------------------------------|------:|--------|-----:|---|-----:|

|hendrycksTest-anatomy              |      1|acc     |0.5704|±  |0.0428|

|                                   |       |acc_norm|0.5704|±  |0.0428|

|hendrycksTest-clinical_knowledge   |      1|acc     |0.6755|±  |0.0288|

|                                   |       |acc_norm|0.6755|±  |0.0288|

|hendrycksTest-college_biology      |      1|acc     |0.7083|±  |0.0380|

|                                   |       |acc_norm|0.7083|±  |0.0380|

|hendrycksTest-college_medicine     |      1|acc     |0.5723|±  |0.0377|

|                                   |       |acc_norm|0.5723|±  |0.0377|

|hendrycksTest-high_school_biology  |      1|acc     |0.7677|±  |0.0240|

|                                   |       |acc_norm|0.7677|±  |0.0240|

|hendrycksTest-medical_genetics     |      1|acc     |0.6900|±  |0.0465|

|                                   |       |acc_norm|0.6900|±  |0.0465|

|hendrycksTest-nutrition            |      1|acc     |0.7353|±  |0.0253|

|                                   |       |acc_norm|0.7353|±  |0.0253|

|hendrycksTest-professional_medicine|      1|acc     |0.6581|±  |0.0288|

|                                   |       |acc_norm|0.6581|±  |0.0288|

|hendrycksTest-virology             |      1|acc     |0.5361|±  |0.0388|

|                                   |       |acc_norm|0.5361|±  |0.0388|


# Other Eval Results

# Misc
We renamed our half-base model `Medilora/medilora-mistral-7b` to `Medilora/mimic-iii-textbooks`
# Compare to Meditron
Main Meditron Benchmark
⁃ MMLU-Medical
⁃ PubMedQA
⁃ MedMCQA
⁃ MedQA
⁃ MedQA-4-4Option
⁃ Avg of the tests

We can directly compare on 
MMLU-Medical
PubMedQA 
MedQA
MedQA-4-4Option


# Our Eval Results

passing score for humans on MedQA is 60.0

Both PubMedQA and MedMCQA provide reasoning traces (long answers or explanations) for chain-of- thought. 

- [https://arxiv.org/abs/2303.13375](https://t.co/eoFOoCDkDd): GPT-4 with good prompts (dynamic k-shot + self-generated CoT + choice-shuffled ensembles) beats Med-PaLM 2 on all nine of the MultiMedQA benchmarks it was fine-tuned for, without fine-tuning. They found with more sophisticated prompting that GPT-4 jumps past prior leading results for medical benchmarks, including a recent report on perf. of Med-PaLM 2, a model fine-tuned w. specialist data & studied using curated prompts. They make an order of magnitude fewer calls.

https://x.com/goodside/status/1730410630673244654?s=46

## MMLU-Medical subtasks
- Anatomy, 
- College Biology (C-Bio), 
- College Medicine (C-Med), 
- Professional Medicine (Pro-Med), 
- Genetics, 
- Virology, 
- Clinical Knowledge (Clinical-KG), 
- High-school Biology (H-Bio), 
- Nutrition 

### lm-eval task list format

Base MMLU

```
mmlu_anatomy,mmlu_college_biology,mmlu_college_medicine,mmlu_professional_medicine,mmlu_medical_genetics,mmlu_virology,mmlu_clinical_knowledge,mmlu_high_school_biology,mmlu_nutrition
```

flan_cot_fewshot 

```
mmlu_flan_cot_fewshot_anatomy,mmlu_flan_cot_fewshot_clinical_knowledge,mmlu_flan_cot_fewshot_college_biology,mmlu_flan_cot_fewshot_college_medicine,mmlu_flan_cot_fewshot_high_school_biology,mmlu_flan_cot_fewshot_medical_genetics,mmlu_flan_cot_fewshot_nutrition,mmlu_flan_cot_fewshot_professional_medicine,mmlu_flan_cot_fewshot_virology
```

flan_cot_zeroshot

```
mmlu_flan_cot_zeroshot_anatomy,mmlu_flan_cot_zeroshot_clinical_knowledge,mmlu_flan_cot_zeroshot_college_biology,mmlu_flan_cot_zeroshot_college_medicine,mmlu_flan_cot_zeroshot_high_school_biology,mmlu_flan_cot_zeroshot_medical_genetics,mmlu_flan_cot_zeroshot_nutrition,mmlu_flan_cot_zeroshot_professional_medicine,mmlu_flan_cot_zeroshot_virology
``` 

flan_n_shot_generative 

```
mmlu_flan_n_shot_generative_anatomy,mmlu_flan_n_shot_generative_clinical_knowledge,mmlu_flan_n_shot_generative_college_biology,mmlu_flan_n_shot_generative_college_medicine,mmlu_flan_n_shot_generative_high_school_biology,mmlu_flan_n_shot_generative_medical_genetics,mmlu_flan_n_shot_generative_nutrition,mmlu_flan_n_shot_generative_professional_medicine,mmlu_flan_n_shot_generative_virology
```


flan_n_shot_loglikelihood 

```
mmlu_flan_n_shot_loglikelihood_anatomy,mmlu_flan_n_shot_loglikelihood_clinical_knowledge,mmlu_flan_n_shot_loglikelihood_college_biology,mmlu_flan_n_shot_loglikelihood_college_medicine,mmlu_flan_n_shot_loglikelihood_high_school_biology,mmlu_flan_n_shot_loglikelihood_medical_genetics,mmlu_flan_n_shot_loglikelihood_nutrition,mmlu_flan_n_shot_loglikelihood_professional_medicine,mmlu_flan_n_shot_loglikelihood_virology
```

BigBench (from OpenHermes Mistral)
teknium/OpenHermes-2.5-Mistral-7B

```
lm_eval --model hf --model_args pretrained=teknium/OpenHermes-2.5-Mistral-7B --tasks bigbench_causal_judgment_multiple_choice,bigbench_date_understanding_multiple_choice,bigbench_disambiguation_qa_multiple_choice,bigbench_geometric_shapes_multiple_choice,bigbench_logical_deduction_multiple_choice,bigbench_movie_recommendation_multiple_choice,bigbench_navigate_multiple_choice,bigbench_reasoning_about_colored_objects_multiple_choice,bigbench_ruin_names_multiple_choice,bigbench_salient_translation_error_detection_multiple_choice,bigbench_snarks_multiple_choice,bigbench_sports_understanding_multiple_choice,bigbench_temporal_sequences_multiple_choice,bigbench_tracking_shuffled_objects_multiple_choice --device cuda:0 --batch_size 32
```

TruthfulQA

```
lm_eval --model hf --model_args pretrained=teknium/OpenHermes-2.5-Mistral-7B --tasks truthfulqa,truthfulqa_gen,truthfulqa_mc1,truthfulqa_mc2 --device cuda:0 --batch_size 32
```

GPT4All

```
lm_eval --model hf --model_args pretrained=teknium/OpenHermes-2.5-Mistral-7B --tasks arc_challenge,arc_easy,boolq,hellaswag,openbookqa,piqa,winogrande --device cuda:0 --batch_size 32
```


## OpenHermes Base Model Eval

### TruthfulQA

| - truthfulqa_mc1|Yaml   |none  |     0|acc        | 0.3611|±  |0.0168|

| - truthfulqa_mc2|Yaml   |none  |     0|acc        | 0.5300|±  |0.0153|



## Medilora Eval Results

---

### Base Model (Guideline)

hf (pretrained=Medilora/medilora-mistral-7b,peft=Medilora/guideline-medilora-adapter), gen_kwargs: (), limit: None, num_fewshot: None, batch_size: auto (32)

|        Tasks        |Version|Filter|n-shot|Metric|Value |   |Stderr|

|---------------------|-------|------|-----:|------|-----:|---|-----:|

|anatomy              |Yaml   |none  |     0|acc   |0.5926|±  |0.0424|

|clinical_knowledge   |Yaml   |none  |     0|acc   |0.6717|±  |0.0289|

|college_biology      |Yaml   |none  |     0|acc   |0.7083|±  |0.0380|

|college_medicine     |Yaml   |none  |     0|acc   |0.6358|±  |0.0367|

|high_school_biology  |Yaml   |none  |     0|acc   |0.7419|±  |0.0249|

|medical_genetics     |Yaml   |none  |     0|acc   |0.6900|±  |0.0465|

|nutrition            |Yaml   |none  |     0|acc   |0.7026|±  |0.0262|

|professional_medicine|Yaml   |none  |     0|acc   |0.6471|±  |0.0290|

|virology             |Yaml   |none  |     0|acc   |0.4940|±  |0.0389|

---

### PubMedQA Finetuned Adapter (avg 0.643)

hf (pretrained=Medilora/Medilora-Mistral-PubMedQAA), gen_kwargs: (), limit: None, num_fewshot: None, batch_size: auto (32)

|        Tasks        |Version|Filter|n-shot|Metric|Value |   |Stderr|

|---------------------|-------|------|-----:|------|-----:|---|-----:|

|anatomy              |Yaml   |none  |     0|acc   |0.5630|±  |0.0428|

|clinical_knowledge   |Yaml   |none  |     0|acc   |0.6755|±  |0.0288|

|college_biology      |Yaml   |none  |     0|acc   |0.6597|±  |0.0396|

|college_medicine     |Yaml   |none  |     0|acc   |0.6243|±  |0.0369|

|high_school_biology  |Yaml   |none  |     0|acc   |0.7387|±  |0.0250|

|medical_genetics     |Yaml   |none  |     0|acc   |0.6700|±  |0.0473|

|nutrition            |Yaml   |none  |     0|acc   |0.7157|±  |0.0258|

|professional_medicine|Yaml   |none  |     0|acc   |0.6581|±  |0.0288|

|virology             |Yaml   |none  |     0|acc   |0.4819|±  |0.0389|

---

### MedQA Finetuned Adapter (avg 0.624)

hf (pretrained=Medilora/medilora-mistral-7b,peft=Medilora/guideline-medqa-adapter), gen_kwargs: (), limit: None, num_fewshot: None, batch_size: auto (32)

|        Tasks        |Version|Filter|n-shot|Metric|Value |   |Stderr|

|---------------------|-------|------|-----:|------|-----:|---|-----:|

|anatomy              |Yaml   |none  |     0|acc   |0.5630|±  |0.0428|

|clinical_knowledge   |Yaml   |none  |     0|acc   |0.6377|±  |0.0296|

|college_biology      |Yaml   |none  |     0|acc   |0.6736|±  |0.0392|

|college_medicine     |Yaml   |none  |     0|acc   |0.5665|±  |0.0378|

|high_school_biology  |Yaml   |none  |     0|acc   |0.7194|±  |0.0256|

|medical_genetics     |Yaml   |none  |     0|acc   |0.6600|±  |0.0476|

|nutrition            |Yaml   |none  |     0|acc   |0.6634|±  |0.0271|

|professional_medicine|Yaml   |none  |     0|acc   |0.6287|±  |0.0293|

|virology             |Yaml   |none  |     0|acc   |0.5060|±  |0.0389|

---

### OpenHermes-2.5-Mistral-7B on base MMLU-Medical (0.659)

hf (pretrained=teknium/OpenHermes-2.5-Mistral-7B), gen_kwargs: (), limit: None, num_fewshot: None, batch_size: auto (32)

|        Tasks        |Version|Filter|n-shot|Metric|Value |   |Stderr|

|---------------------|-------|------|-----:|------|-----:|---|-----:|

|anatomy              |Yaml   |none  |     0|acc   |0.5630|±  |0.0428|

|clinical_knowledge   |Yaml   |none  |     0|acc   |0.6830|±  |0.0286|

|college_biology      |Yaml   |none  |     0|acc   |0.7014|±  |0.0383|

|college_medicine     |Yaml   |none  |     0|acc   |0.5723|±  |0.0377|

|high_school_biology  |Yaml   |none  |     0|acc   |0.7677|±  |0.0240|

|medical_genetics     |Yaml   |none  |     0|acc   |0.7000|±  |0.0461|

|nutrition            |Yaml   |none  |     0|acc   |0.7353|±  |0.0253|

|professional_medicine|Yaml   |none  |     0|acc   |0.6691|±  |0.0286|

|virology             |Yaml   |none  |     0|acc   |0.5361|±  |0.0388|

### Meditron-7B on base MMLU-Medical (avg 0.346)

```
lm_eval --model hf --model_args pretrained=epfl-llm/meditron-7b --tasks mmlu_anatomy,mmlu_college_biology,mmlu_college_medicine,mmlu_professional_medicine,mmlu_medical_genetics,mmlu_virology,mmlu_clinical_knowledge,mmlu_high_school_biology,mmlu_nutrition --device cuda:0 --batch_size auto
```

hf (pretrained=epfl-llm/meditron-7b), gen_kwargs: (), limit: None, num_fewshot: None, batch_size: auto (16)

|        Tasks        |Version|Filter|n-shot|Metric|Value |   |Stderr|

|---------------------|-------|------|-----:|------|-----:|---|-----:|

|anatomy                       |Yaml   |none  |     0|acc   |0.4148|±  |0.0426|

|clinical_knowledge     |Yaml   |none  |     0|acc   |0.3623|±  |0.0296|

|college_biology           |Yaml   |none  |     0|acc   |0.3958|±  |0.0409|

|college_medicine        |Yaml   |none  |     0|acc   |0.2890|±  |0.0346|

|high_school_biology  |Yaml   |none  |     0|acc   |0.3323|±  |0.0268|

|medical_genetics       |Yaml   |none  |     0|acc   |0.4300|±  |0.0498|

|nutrition                       |Yaml   |none  |     0|acc   |0.3693|±  |0.0276|

|professional_medicine|Yaml   |none  |     0|acc   |0.2463|±  |0.0262|

|virology                       |Yaml   |none  |     0|acc   |0.2771|±  |0.0348|



## TODO: Evaluation Tasks

### MedQA Results
- Medilora - 5 options: 37.9%
- Medilora - 4 options: 46.5%
### Aggregate TruthfulQA, GPT4All and BigBench results (average)

### Evaluate Medilora on OpenHermes Mistral Tasks

- [x] TruthfulQA
- [x] GPT4All
- [x] Bigbench

#### GPT4All

hf (pretrained=Medilora/mimic-iii-textbooks,peft=Medilora/medilora-pubmed-medqa-adapter), gen_kwargs: (), limit: None, num_fewshot: None, batch_size: 32

|    Tasks    |Version|Filter|n-shot| Metric |Value |   |Stderr|

|-------------|-------|------|-----:|--------|-----:|---|-----:|

|arc_challenge|Yaml   |none  |     0|acc     |0.5077|±  |0.0146|

|             |       |none  |     0|acc_norm|0.5580|±  |0.0145|

|arc_easy     |Yaml   |none  |     0|acc     |0.8089|±  |0.0081|

|             |       |none  |     0|acc_norm|0.8098|±  |0.0081|

|boolq        |Yaml   |none  |     0|acc     |0.8661|±  |0.0060|

|hellaswag    |Yaml   |none  |     0|acc     |0.6163|±  |0.0049|

|             |       |none  |     0|acc_norm|0.8049|±  |0.0040|

|openbookqa   |Yaml   |none  |     0|acc     |0.3160|±  |0.0208|

|             |       |none  |     0|acc_norm|0.4280|±  |0.0221|

|piqa         |Yaml   |none  |     0|acc     |0.7894|±  |0.0095|

|             |       |none  |     0|acc_norm|0.8079|±  |0.0092|

|winogrande   |Yaml   |none  |     0|acc     |0.7269|±  |0.0125|

#### TruthfulQA

| - truthfulqa_mc1|Yaml   |none  |     0|acc        | 0.3452|±  |0.0166|
| - truthfulqa_mc2|Yaml   |none  |     0|acc        | 0.4985|±  |0.0150|0.

#### TruthfulQA All Results

hf (pretrained=Medilora/mimic-iii-textbooks,peft=Medilora/medilora-pubmed-medqa-adapter), gen_kwargs: (), limit: None, num_fewshot: None, batch_size: 32

|      Tasks      |Version|Filter|n-shot|  Metric   | Value |   |Stderr|

|-----------------|-------|------|-----:|-----------|------:|---|-----:|

|truthfulqa       |N/A    |none  |     0|bleu_max   |38.6214|±  |0.7557|

|                 |       |none  |     0|bleu_acc   | 0.5459|±  |0.0003|

|                 |       |none  |     0|bleu_diff  |12.3859|±  |1.3656|

|                 |       |none  |     0|rouge1_max |65.1024|±  |0.8137|

|                 |       |none  |     0|rouge1_acc | 0.5704|±  |0.0003|

|                 |       |none  |     0|rouge1_diff|18.6584|±  |2.3539|

|                 |       |none  |     0|rouge2_max |53.8272|±  |1.2067|

|                 |       |none  |     0|rouge2_acc | 0.5288|±  |0.0003|

|                 |       |none  |     0|rouge2_diff|18.7040|±  |2.8482|

|                 |       |none  |     0|rougeL_max |62.6683|±  |0.8893|

|                 |       |none  |     0|rougeL_acc | 0.5618|±  |0.0003|

|                 |       |none  |     0|rougeL_diff|18.5156|±  |2.4271|

|                 |       |none  |     0|acc        | 0.3963|±  |0.0508|

| - truthfulqa_gen|Yaml   |none  |     0|bleu_max   |38.6214|±  |0.8693|

|                 |       |none  |     0|bleu_acc   | 0.5459|±  |0.0174|

|                 |       |none  |     0|bleu_diff  |12.3859|±  |1.1686|

|                 |       |none  |     0|rouge1_max |65.1024|±  |0.9021|

|                 |       |none  |     0|rouge1_acc | 0.5704|±  |0.0173|

|                 |       |none  |     0|rouge1_diff|18.6584|±  |1.5342|

|                 |       |none  |     0|rouge2_max |53.8272|±  |1.0985|

|                 |       |none  |     0|rouge2_acc | 0.5288|±  |0.0175|

|                 |       |none  |     0|rouge2_diff|18.7040|±  |1.6877|

|                 |       |none  |     0|rougeL_max |62.6683|±  |0.9430|

|                 |       |none  |     0|rougeL_acc | 0.5618|±  |0.0174|

|                 |       |none  |     0|rougeL_diff|18.5156|±  |1.5579|

| - truthfulqa_mc1|Yaml   |none  |     0|acc        | 0.3452|±  |0.0166|

| - truthfulqa_mc2|Yaml   |none  |     0|acc        | 0.4985|±  |0.0150|

  

|  Groups  |Version|Filter|n-shot|  Metric   | Value |   |Stderr|

|----------|-------|------|-----:|-----------|------:|---|-----:|

|truthfulqa|N/A    |none  |     0|bleu_max   |38.6214|±  |0.7557|

|          |       |none  |     0|bleu_acc   | 0.5459|±  |0.0003|

|          |       |none  |     0|bleu_diff  |12.3859|±  |1.3656|

|          |       |none  |     0|rouge1_max |65.1024|±  |0.8137|

|          |       |none  |     0|rouge1_acc | 0.5704|±  |0.0003|

|          |       |none  |     0|rouge1_diff|18.6584|±  |2.3539|

|          |       |none  |     0|rouge2_max |53.8272|±  |1.2067|

|          |       |none  |     0|rouge2_acc | 0.5288|±  |0.0003|

|          |       |none  |     0|rouge2_diff|18.7040|±  |2.8482|

|          |       |none  |     0|rougeL_max |62.6683|±  |0.8893|

|          |       |none  |     0|rougeL_acc | 0.5618|±  |0.0003|

|          |       |none  |     0|rougeL_diff|18.5156|±  |2.4271|

|          |       |none  |     0|acc        | 0.3963|±  |0.0508|

#### Bigbench

hf (pretrained=Medilora/mimic-iii-textbooks,peft=Medilora/medilora-pubmed-medqa-adapter), gen_kwargs: (), limit: None, num_fewshot: None, batch_size: 32

|                           Tasks                            |Version|Filter|n-shot|Metric|Value |   |Stderr|

|------------------------------------------------------------|-------|------|-----:|------|-----:|---|-----:|

|bigbench_causal_judgment_multiple_choice                    |Yaml   |none  |     0|acc   |0.5579|±  |0.0361|

|bigbench_date_understanding_multiple_choice                 |Yaml   |none  |     0|acc   |0.6396|±  |0.0250|

|bigbench_disambiguation_qa_multiple_choice                  |Yaml   |none  |     0|acc   |0.3721|±  |0.0302|

|bigbench_geometric_shapes_multiple_choice                   |Yaml   |none  |     0|acc   |0.1504|±  |0.0189|

|bigbench_logical_deduction_multiple_choice                  |Yaml   |none  |     0|acc   |0.2607|±  |0.0113|

|bigbench_movie_recommendation_multiple_choice               |Yaml   |none  |     0|acc   |0.2200|±  |0.0185|

|bigbench_navigate_multiple_choice                           |Yaml   |none  |     0|acc   |0.4980|±  |0.0158|

|bigbench_reasoning_about_colored_objects_multiple_choice    |Yaml   |none  |     0|acc   |0.5915|±  |0.0110|

|bigbench_ruin_names_multiple_choice                         |Yaml   |none  |     0|acc   |0.3326|±  |0.0223|

|bigbench_salient_translation_error_detection_multiple_choice|Yaml   |none  |     0|acc   |0.1503|±  |0.0113|

|bigbench_snarks_multiple_choice                             |Yaml   |none  |     0|acc   |0.5525|±  |0.0371|

|bigbench_sports_understanding_multiple_choice               |Yaml   |none  |     0|acc   |0.4980|±  |0.0159|

|bigbench_temporal_sequences_multiple_choice                 |Yaml   |none  |     0|acc   |0.2760|±  |0.0141|

|bigbench_tracking_shuffled_objects_multiple_choice          |Yaml   |none  |     0|acc   |0.2000|±  |0.0065|
```
lm_eval --model hf --model_args pretrained=Medilora/mimic-iii-textbooks,peft=Medilora/medilora-pubmed-medqa-adapter --tasks bigbench_causal_judgment_multiple_choice,bigbench_date_understanding_multiple_choice,bigbench_disambiguation_qa_multiple_choice,bigbench_geometric_shapes_multiple_choice,bigbench_logical_deduction_multiple_choice,bigbench_movie_recommendation_multiple_choice,bigbench_navigate_multiple_choice,bigbench_reasoning_about_colored_objects_multiple_choice,bigbench_ruin_names_multiple_choice,bigbench_salient_translation_error_detection_multiple_choice,bigbench_snarks_multiple_choice,bigbench_sports_understanding_multiple_choice,bigbench_temporal_sequences_multiple_choice,bigbench_tracking_shuffled_objects_multiple_choice --device cuda:0 --batch_size 32
```



# Opening Models

## State of the model repos

Medilora/guideline-medilora-adapter
- adapter only.
- Task required:
- [ ] merge
- [ ] quantize using Q3_K_L

Medilora/guideline-medqa-adapter
- adapter only. Remain this way.

Medilora/medilora-pubmed-medqa-adapter
- adapter only. Remain this way.

Medilora/Medilora-Mistral-PubMedQAA
* adapter, full f32 model, quantized model
* Task required:
* [ ] separate quantized model and create new repo;
* [ ] rename current repo
