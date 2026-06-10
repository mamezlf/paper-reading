Slide 17: Embedding Analysis — Condition 10 Results
(violin plot: Condition 10 — figure inserted here)

Condition 10: Ohi shared, Olo not shared
Analogous to High-similarity Overlap in the original paper


Slide 18: Embedding Analysis — Condition 10 Interpretation
Comparing Condition 00 → Condition 10:
Token groupCondition 00Condition 10ChangeOhi~0.78~0.75≈ no changeOlo~0.49~0.05↓ dramaticallyRandom~0.03~0.05≈ no change

Olo drop (0.49 → 0.05) is striking and expected: Olo is not shared in condition 10, so JA and ZH learn independent embeddings for these tokens → similarity collapses toward the random baseline
Ohi barely changes (0.78 → 0.75): sharing token IDs brings little additional alignment gain for already semantically similar kanji

Reason: parallel corpus context alone is sufficient to align semantically similar tokens — shared ID provides minimal extra signal


Key insight: token ID sharing matters most for semantically dissimilar tokens — it is the ID sharing that forces their embeddings together (or apart), not semantic content