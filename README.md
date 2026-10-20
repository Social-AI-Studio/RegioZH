# RegioZH: Unveiling Comprehension Disparities across Regional Chinese Varieties in LLMs

RegioZH is a multiple-choice benchmark for evaluating how well language models
understand regional varieties of Chinese. The dataset covers Mainland China,
Taiwan, Hong Kong, Singapore, and Malaysia. Its questions contain region-specific
vocabulary, local usages, code-switching, and sociocultural knowledge that may
not be recoverable from Standard Chinese alone.

Each item presents a question or conversational situation followed by several
candidate responses. Depending on the question, one or more options may be
required. A prediction is considered exactly correct only when the complete
predicted option set matches the reference option set.

## Dataset Statistics

| Region | File | Items |
|---|---|---:|
| Mainland China | `Chinese_Mainland_Update.json` | 520 |
| Taiwan | `Chinese_Taiwan_Update.json` | 536 |
| Hong Kong | `HongKong_QA_samples.json` | 520 |
| Singapore | `Chinese_Singapore_Update.json` | 515 |
| Malaysia | `Malay_Dataset_with_100_other.json` | 516 |
| **Total** |  | **2,607** |


## Data Format

Each regional file is a UTF-8 JSON array. Every item contains two fields:

```json
{
  "question_and_answer": "Question text followed by labeled answer options...",
  "reference_correct_answer": "a,c"
}
```

- `question_and_answer`: the complete question and its candidate options.
- `reference_correct_answer`: the gold option set requested by the question
  stem, represented by lowercase option labels separated by commas.

The wording of the question stem must be considered during evaluation. Some
items ask for correctly understood responses, while others ask for incorrect
interpretations. Therefore, `reference_correct_answer` should be treated as the
authoritative gold set rather than assuming that every item asks for the same
type of judgment.

## Recommended Evaluation

The primary metric is exact-set-match accuracy:

```text
correct = set(predicted_options) == set(reference_correct_answer)
```

Because the benchmark contains multi-select questions with different gold-set
sizes, partial-credit metrics such as example-level F1 or Jaccard similarity can
also be reported as robustness measures. Predictions should be normalized to
lowercase option labels before scoring, and option order should not affect the
result.

## Scope

RegioZH is designed to test regional Chinese comprehension rather than general
Chinese fluency alone. Performance may depend on recognizing local lexical
meanings, interpreting region-specific expressions, resolving code-switched
language, and applying relevant sociocultural background knowledge.

## Release Notes

- The five files listed in the statistics table constitute the current release.
- The dataset contains naturally varying numbers of answer options and correct
  options across items and regions.
- No train/dev/test split is imposed in this directory. Users should document
  any split or cross-validation procedure used in downstream experiments.
