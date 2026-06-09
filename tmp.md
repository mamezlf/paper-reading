# Edit Instructions for slide_draft.md

Please make the following two changes to `slide_draft.md`:

---

## Change 1: Slide 5 — Add overlap composition table

In **Slide 5: Key Challenge — Scale of Overlap**, after the existing bullet points, add the following table and a short sentence introducing it:

---

The native overlap O breaks down as follows:

| Category | Count | % of O |
|---|---|---|
| Total overlap (O) | 26,360 | 100% |
| Kanji-related (cognates, non-cognates, other kanji) | 3,459 | 17.3% |
| Latin characters | 18,929 | 71.8% |
| Digits | 1,255 | 4.8% |
| Symbols / special tokens | 1,581 | 6.0% |
| Other | 300 | 1.1% |

- The majority of overlap (~72%) comes from Latin characters, digits, and symbols — not kanji
- Transfer via Latin/digit tokens is not the focus of this study; we isolate the effect of **kanji token sharing** specifically

---

## Change 2: Slide 8 — Add 予想 column to condition table

In **Slide 8: Experimental Design — 2×2 Factorial**, replace the existing condition table with the following updated version that includes a "Hypothesis" column:

| Condition | Ohi shared | Olo shared | Hypothesis |
|---|---|---|---|
| **00** | ✗ | ✗ | Baseline |
| **01** | ✗ | ✓ | Embedding alignment degrades |
| **10** | ✓ | ✗ | Embedding alignment improves |
| **11** | ✓ | ✓ | Embedding alignment improves |

Also update the bullet point below the table to clarify that **Latin characters, digits, and punctuation are fixed as shared across all conditions**; only kanji tokens are manipulated.

Replace:
> - Background tokens (overlap O minus Ohi_500 minus Olo_500, ~25,518 tokens) are **shared across all conditions**
> - Non-kanji overlap tokens (digits, Latin, punctuation) also shared across all conditions

With:
> - **Latin characters, digits, and symbols** (~82.6% of O) are **fixed as shared across all conditions** — only kanji tokens are manipulated
> - Background kanji tokens (O minus Ohi_500 minus Olo_500, ~25,018 tokens) are also shared across all conditions