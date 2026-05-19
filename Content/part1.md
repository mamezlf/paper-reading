Slide 1 — Title

False Friends Are Not Foes: Investigating Vocabulary Overlap in Multilingual Language Models
Kallini et al., EMNLP 2025
Paper Reading — [你的名字] — [日期]


Slide 2 — A Familiar Situation

When you learn a foreign language, some words feel instantly familiar
Same form, same meaning → easy to learn
Same form, different meaning → dangerous


Slide 3 — Example: Japanese & Chinese

手紙 (tegami) in Japanese → letter
手纸 (shǒuzhǐ) in Chinese → toilet paper
Same characters, completely different meanings


Slide 4 — Example: English & German

"gift" in English → present
"Gift" in German → poison
Identical form, opposite meanings


Slide 5 — The Same Problem in NLP

Multilingual tokenizers assign the same token ID to words with identical forms across languages
They share the same embedding — regardless of meaning
Does this help or hurt cross-lingual transfer?