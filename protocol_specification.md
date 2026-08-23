# Experimental Protocol Specification

## 1. Corpus harmonisation

Four public corpora are mapped to a binary stress-related label:

- Dreaddit
- SAD
- IRF
- MultiWD

Records with missing text/labels or fewer than three tokens are removed. No additional content filtering is applied.

## 2. Structural leakage audit

For Dreaddit, the parent-post identifier is used to determine:

- number of annotated segments;
- number of unique parent posts;
- number of parent posts contributing multiple segments;
- maximum segments per parent post;
- proportion of segments belonging to multi-segment posts;
- overlap of parent posts between the official train and test partitions.

## 3. Protocol comparison

Dreaddit is evaluated using:

- random segment-level stratified cross-validation;
- post-grouped stratified cross-validation.

Lexical and LIWC feature families are compared using paired seed-level differences.

## 4. In-domain transformer validation

The official Dreaddit train/test split is retained. The following encoders are evaluated over three seeds:

- BERT-base;
- MentalBERT;
- RoBERTa-base;
- MentalRoBERTa.

The primary comparison is positive-class F1.

## 5. Cross-corpus transfer

Each corpus is used as a source domain and evaluated on the remaining corpora. Three random seeds are used.

The honest in-domain reference is obtained from grouped/stratified cross-validation and is not replaced by optimistic train-on-all/test-on-all diagonal values.

## 6. Cross-domain control

Within Dreaddit, the five topical domains are used in a leave-one-domain-out design. Annotation scheme, annotator pool, platform, sampling procedure and genre remain fixed.

The primary decomposition is Dreaddit-anchored:

```text
Topic cost = Dreaddit grouped in-domain − leave-one-domain-out mean

Between-corpus cost =
    leave-one-domain-out mean − Dreaddit → other-corpora mean
```

## 7. Construct-validity probe

Community identity is evaluated as a partial-input signal using:

- majority-class prediction;
- oracle community prior;
- predicted-community prior;
- full transformer model.

## 8. Masking intervention

Community-identifying content words are selected using chi-square statistics. A frequency-matched random masking control is applied to a comparable amount of text.

The reported community-specific effect is:

```text
treatment drop − control drop
```

## 9. Label-noise ceiling

Dreaddit training is repeated using only instances with annotator agreement/confidence ≥ 0.8.

External transfer is compared with training on all available segments.

## 10. Statistical reporting

The notebook reports means and standard deviations across seeds/folds where applicable. Paired tests are used for the protocol comparison. Bootstrap confidence intervals are generated for the decomposition quantities.
