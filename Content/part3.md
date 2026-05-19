Slide 23 — Downstream Tasks

Zero-shot cross-lingual transfer setup
Fine-tune on English, evaluate on L2
XNLI: natural language inference
XQuAD: question answering


Slide 24 — Results Overview

Main finding: any overlap is better than no overlap
No Overlap performs significantly worse across all language pairs and tasks
The type of overlap also matters


Slide 25 — Result 1: No Overlap is Always Worst

Across all 6 language pairs, all tasks
XNLI accuracy on L2: No Overlap often drops to ~33-42%
With any overlap: 49-75%
Shared vocabulary is always beneficial for transfer


Slide 26 — Result 2: High-sim. > Low-sim.

High-similarity Overlap consistently outperforms Low-similarity Overlap
Especially for typologically distant languages (Chinese, Arabic, Turkish)
Semantically aligned tokens contribute most to transfer


Slide 27 — Result 3: Full ≈ High-sim.

Full Overlap and High-similarity Overlap perform comparably
Differences often not statistically significant
Adding false friends on top of cognates doesn't hurt much


Slide 28 — But Low-sim. Still Beats No Overlap

Even sharing only false friends helps transfer
Counterintuitive: misleading anchors are still better than no anchors
Any shared embedding creates some cross-lingual structure


Slide 29 — Embedding Space Analysis

Before downstream tasks: what do the learned representations look like?
For each overlapping token: measure cosine similarity between L1 and L2 embeddings
Does the model represent the same form similarly across languages?


Slide 30 — Embedding Result 1: Full & High-sim. Overlap

High-similarity tokens → very similar embeddings across languages
Low-similarity tokens → more distinct embeddings
Model correctly distinguishes cognates from false friends


Slide 31 — Embedding Result 2: Low-sim. Overlap

False friends are forced to share an embedding
Result: model represents them as similar — even though meanings differ
Embedding space is "misled" by the shared token ID


Slide 32 — Embedding Result 3: No Overlap

Without any shared tokens, cross-lingual similarity is weak
Even cognates are represented differently across languages
No shared vocabulary → no cross-lingual structure


Slide 33 — Key Insight: Overlap Creates Anchors

Shared tokens act as cross-lingual anchors in the embedding space
These anchors propagate structure to neighboring tokens via attention
Even "wrong" anchors (false friends) are better than no anchors


Slide 34 — Language Distance Matters

For closely related languages (Spanish, German): Low-sim. and High-sim. perform similarly
For distant languages (Chinese, Arabic): High-sim. has a clear advantage
More distant → less contextual signal to compensate for misleading anchors


Slide 35 — Takeaway 1

Shared vocabulary is always beneficial for cross-lingual transfer
No Overlap is significantly worse in every setting tested


Slide 36 — Takeaway 2

The semantic similarity of shared tokens matters
High-similarity overlap (cognates) contributes most to transfer performance


Slide 37 — Takeaway 3

False friends are not foes
Even semantically misaligned overlap creates useful cross-lingual structure
Better to share than not to share


Slide 38 — Practical Implication

Multilingual tokenizer design: don't reduce overlap
Focus instead on other quality factors (e.g., per-language compression rates)
Substantial shared vocabulary remains a good design choice


Slide 39 — Limitations & Future Work

Only English-centric language pairs
Single tokenizer (XLM-R)
Future: non-English pairs, more low-resource languages, different tokenizer designs


Slide 40 — Thank You

False Friends Are Not Foes: Investigating Vocabulary Overlap in Multilingual Language Models
Kallini et al., EMNLP 2025
Questions?

