# Slide Draft: Kanji Token Sharing and Cross-Lingual Embedding Alignment in Japanese–Chinese Bilingual LMs

---

## Slide 1: Title

**Title:** Does Kanji Sharing Help? Investigating Vocabulary Overlap in a Japanese–Chinese Bilingual Language Model

**Subtitle:** Research Meeting – Progress Report

**Author:** [Your Name]

**Date:** 2026/06/04

---

## Slide 2: Research Background (1) — Why Multilingual Models?

- Multilingual LLMs are trained on data from many languages simultaneously
- A key design question: **how should vocabularies be shared across languages?**
- Subword tokenizers trained on multilingual corpora naturally produce **overlapping tokens** across languages
- Token overlap has been shown to **facilitate cross-lingual transfer** — but the conditions under which this holds remain unclear

---

## Slide 3: Research Background (2) — The Original Paper

- **"False Friends Are Not Foes"** (Kallini et al., 2025, Stanford)
- Trained bilingual autoregressive models on 6 English-X language pairs
- Key insight: **not all overlap is equal** — semantic similarity of shared tokens matters
- Four controlled overlap conditions:
  - **Full Overlap** — all native overlapping tokens shared
  - **High-similarity Overlap** — only semantically similar tokens shared
  - **Low-similarity Overlap** — only semantically dissimilar tokens shared
  - **No Overlap** — completely disjoint vocabularies
- Main finding: any overlap helps, but **high-similarity overlap helps most**

*(この論文については前回の paper reading で紹介済み)*

---

## Slide 4: Research Motivation — Why Japanese–Chinese?

- The original paper focused exclusively on **English-centric pairs**
- Limitation acknowledged by the authors: *"Exploring overlap effects in non-English pairings would complement our findings"*
- **Japanese and Chinese share a writing system: kanji (漢字)**
  - Many characters are shared in form, but meanings may differ
  - e.g., 手紙 = "letter" (JA) vs. "toilet paper" (ZH)
- This makes Japanese–Chinese a **natural testbed** for the high-sim / low-sim distinction
- Research question: **Does kanji token sharing facilitate or hinder cross-lingual alignment?**

---

## Slide 5: Key Challenge — Scale of Overlap

- In the original paper, English-X overlap is **sparse**
  - e.g., English–Chinese: |O| ≈ 57,000 out of 141,000 effective vocab (~40%)
- In Japanese–Chinese, overlap via XLM-R tokenizer is **extremely dense**
  - Native overlap |O| ≈ **26,360 tokens**
  - This is largely driven by shared kanji characters
- This density means:
  - We **cannot** rely on word-level cognate annotations (as the original paper did for English–Dutch layer sweep)
  - We must use **token-level similarity scoring** to partition O into Ohi and Olo

---

## Slide 6: Token Similarity Partitioning (1) — Method

- For each token t in the native overlap set O:
  1. Sample 100 sentences containing t from the Japanese CCMatrix corpus → extract XLM-R contextual embeddings → mean-pool → static embedding **e_ja**
  2. Repeat for Chinese corpus → **e_zh**
  3. Compute **cosine similarity** between e_ja and e_zh
- Rank all tokens in O by similarity score
- Top 500 → **Ohi_500** (high-similarity kanji)
- Bottom 500 → **Olo_500** (low-similarity kanji)
- Additional: **Random_500** — randomly selected non-overlapping JA/ZH token pairs (anisotropy control baseline)

---

## Slide 7: Token Similarity Partitioning (2) — Layer Selection

- Which XLM-R layer gives the best signal for semantic similarity?
- Conducted a **layer sweep** on the JKVC dataset (Japanese–Chinese vocabulary cognate data)
- For each layer l ∈ {1, …, 12}:
  - Extract static embeddings for overlapping tokens in both languages
  - Rank by cosine similarity, sweep classification threshold
  - Record peak accuracy against gold labels
- **Result: Layer 9 achieved peak accuracy = 0.6936**
- → All similarity scores computed using **XLM-R Layer 9**

---

## Slide 8: Experimental Design — 2×2 Factorial

- Two independent variables:
  - **Ohi sharing**: are high-similarity kanji tokens shared? (0 = separate, 1 = shared)
  - **Olo sharing**: are low-similarity kanji tokens shared? (0 = separate, 1 = shared)

| Condition | Ohi shared | Olo shared | Analogy to original paper |
|---|---|---|---|
| **00** | ✗ | ✗ | No Overlap |
| **01** | ✗ | ✓ | Low-similarity Overlap |
| **10** | ✓ | ✗ | High-similarity Overlap |
| **11** | ✓ | ✓ | Full Overlap |

- Background tokens (overlap O minus Ohi_500 minus Olo_500, ~25,518 tokens) are **shared across all conditions**
- Non-kanji overlap tokens (digits, Latin, punctuation) also shared across all conditions

---

## Slide 9: Experimental Design — Vocabulary Sizes

- Token remapping ensures that only the designated tokens are shared per condition
- Re-indexing compresses the embedding matrix while preserving sharing relationships

| Condition | Vocab Size |
|---|---|
| 00 | 41,118 |
| 01 | 40,769 |
| 10 | 40,625 |
| 11 | 40,276 |

- Smaller vocab in conditions with more sharing → fewer embedding parameters

---

## Slide 10: Data — CCMatrix Japanese–Chinese

- **Dataset:** CCMatrix (Schwenk et al., 2021) — large-scale web-mined parallel texts
- **Source:** `larryvrh/CCMatrix-v1-Ja_Zh-filtered` (HuggingFace)
- **Size:** 5,686,275 Japanese–Chinese sentence pairs
- **Preprocessing:**
  - Tokenized with XLM-R SentencePiece tokenizer
  - Token remapping applied per condition
  - Sentences from both languages shuffled and interleaved
- **Training data format:** HuggingFace Dataset `.arrow` files

---

## Slide 11: Training Setup — Hyperparameters

- Hyperparameters copied directly from the original paper to maintain comparability

| Parameter | Value |
|---|---|
| Total steps | 20,000 |
| Warmup steps | 5,000 (linear) |
| Learning rate | 2.5e-4 |
| LR schedule | Cosine decay |
| Optimizer | AdamW |
| Effective batch size | 64 sequences |
| Device batch size | 8 + gradient accumulation ×8 |
| Sequence length | 512 tokens |

---

## Slide 12: Architecture — LlamaForCausalLM at GPT-2 Small Scale

- Model: **LlamaForCausalLM** (HuggingFace Transformers)
- Replaces GPT-2 architecture from the original paper to gain **native RoPE positional encoding**
- RoPE is the positional encoding method most commonly used in modern LLMs

| Parameter | Value |
|---|---|
| Hidden size | 768 |
| Intermediate size | 3,072 |
| Number of layers | 12 |
| Attention heads | 12 |
| Non-embedding parameters | ~85M |

- Trained **from scratch** — no pretrained weights used
- Four separate models trained (one per condition: 00, 01, 10, 11)

---

## Slide 13: Current Status & Next Steps

- **Training:** All 4 conditions launched on GPU server (University RTX A5000)
  - Running as background job via `nohup`, monitoring via log file
  - TOTAL_STEPS = 20,000

- **Next: Step 3 — Embedding Similarity Analysis**
  - Extract token embeddings from trained models (middle layer, l=6)
  - Compute cosine similarity between JA and ZH embeddings for Ohi_500 / Olo_500 / Random_500
  - Produce **violin plots** replicating original paper Figure 2
  - Key question: does kanji sharing align or misalign embedding spaces?

---

## [BACKUP] Token Remapping Mechanism

*(備用スライド — スライドに起こさない)*

- Base tokenizer T (XLM-R, vocab size N = 250,000)
- For Japanese tokens: indices unchanged
- For Chinese tokens **not in the shared set O'**: index offset by +N (= +250,000)
- This guarantees only tokens in O' are shared between JA and ZH
- Re-indexing then compresses the full index space back to the actual vocab size used
- Sharing is determined by **which tokens receive the same index** after re-indexing
- Re-indexing is applied consistently across conditions → does not corrupt sharing relationships

**Effective vocab size:** N'_eff = |V_ja| + |V_zh| − |O'|