Slide 6 — Background: What is Token Overlap?

Multilingual tokenizers are trained on concatenated corpora from multiple languages
Words with identical forms naturally get the same token ID
This is called "token overlap"
Examples: named entities (Batman), punctuation, cognates, false friends


Slide 7 — Why Does It Matter?

Shared token IDs → shared embeddings
The model sees the same vector for the same form, regardless of language
This could create cross-lingual anchors… or introduce confusion


Slide 8 — Prior Work: Mixed Evidence

Some work: overlap helps zero-shot cross-lingual transfer
Other work: overlap hurts performance on certain tasks
Missing piece: does the type of overlap matter?


Slide 9 — The Key Question

Not all overlapping tokens are equal
Some share form AND meaning (cognates)
Some share form but NOT meaning (false friends)
How does semantic similarity of shared tokens affect transfer?


Slide 10 — Experimental Design Overview

Train bilingual autoregressive models (GPT-2 scale, 85M params)
6 language pairs, all English-centric
4 vocabulary overlap settings
Evaluate on downstream tasks: XNLI, XQuAD


Slide 11 — 6 Language Pairs

English–Spanish, English–German (closely related)
English–Turkish, English–Arabic (distant)
English–Chinese (different script)
English–Swahili (low-resource)


Slide 12 — How to Control Overlap?

Base tokenizer: XLM-R (vocabulary size N)
For L1: all token IDs unchanged
For L2: tokens NOT in the shared set → ID shifted by +N
Tokens IN the shared set → ID unchanged, embedding shared
No need to retrain the tokenizer


Slide 13 — Finding the Overlapping Tokens

Tokenize both language corpora with XLM-R
Find tokens with identical forms in both languages → native overlap set O
These are the candidates for sharing


Slide 14 — Ranking by Semantic Similarity

For each overlapping token, compute cross-lingual semantic similarity
Use contextual embeddings from XLM-R
Rank all overlapping tokens by similarity score
Top half → High-similarity set
Bottom half → Low-similarity set


Slide 15 — Condition 1: No Overlap

All L2 token IDs shifted by +N
No shared embeddings between languages
The two languages are completely isolated
Baseline: what happens with zero cross-lingual anchors?


Slide 16 — No Overlap: Example

手紙 (Japanese) → token ID: 1042
手纸 (Chinese) → token ID: 1042 + N
Model treats them as completely different words


Slide 17 — Condition 2: Low-similarity Overlap

Only tokens with the LOWEST cross-lingual semantic similarity are shared
False friends: same form, different meaning
手紙／手纸 → shared embedding
True cognates: NOT shared


Slide 18 — Low-similarity Overlap: Example

手紙 (Japanese, "letter") and 手纸 (Chinese, "toilet paper")
Same token ID → same embedding
The model is forced to represent two different meanings with one vector


Slide 19 — Condition 3: High-similarity Overlap

Only tokens with the HIGHEST cross-lingual semantic similarity are shared
Cognates: same form, same meaning
経済 (Japanese) / 经济 (Chinese) → shared embedding
False friends: NOT shared


Slide 20 — High-similarity Overlap: Example

経済 (Japanese, "economy") and 经济 (Chinese, "economy")
Same token ID → same embedding
The model correctly links two words that mean the same thing


Slide 21 — Condition 4: Full Overlap

All natively overlapping tokens are shared — regardless of meaning
This is what real multilingual models (e.g., XLM-R) do by default
Mix of cognates, false friends, named entities, punctuation

Slide 22 — Four Conditions: Summary

No Overlap → complete isolation
Low-sim. Overlap → only false friends shared
High-sim. Overlap → only cognates shared
Full Overlap → everything shared
Everything else held constant: data, model size, architecture

