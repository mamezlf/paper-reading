Slide 14: Embedding Analysis — Method

Goal: test whether kanji token sharing causes the model to learn more or less aligned representations for JA and ZH
From a middle layer (l = 6) of each trained model:

For each token in Ohi_500 / Olo_500 / Random_500, sample up to 100 sentences per language from the training data
Extract contextual embeddings → mean-pool → one static embedding per token per language: e_ja, e_zh
Compute cosine similarity between e_ja and e_zh


Three token groups compared:

Ohi_500 (purple) — high-similarity kanji; should be semantically aligned across JA/ZH
Olo_500 (blue) — low-similarity kanji; should be semantically distinct
Random_500 (gray) — non-overlapping JA-only / ZH-only single-char tokens; anisotropy baseline


Results visualized as violin plots (replicating original paper Figure 2)


Slide 15: Embedding Analysis — Condition 00 Results
(violin plot: Condition 00 — figure inserted here)

Condition 00: no kanji tokens shared (Ohi and Olo both disjoint)
X-axis: token group; Y-axis: cosine similarity between e_ja and e_zh


Slide 16: Embedding Analysis — Condition 00 Interpretation

Even without any kanji sharing, High-sim tokens show higher embedding similarity (median ~0.78) than Low-sim tokens (median ~0.49)

Suggests some degree of semantic alignment emerges from shared context structure alone

Low-sim tokens show a broad distribution (range ~0.12–1.0), reflecting genuine semantic divergence across languages
