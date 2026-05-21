# Instructions: Add Formulas to Slides

Please modify `index.html` to add mathematical formulas to the following slides.
The presentation uses KaTeX or MathJax for rendering — please add the appropriate
CDN link in the `<head>` if not already present. Render all formulas inline in the HTML.

---

## Slide: "Finding the Overlapping Tokens"

In the `<ul>`, find the `<li>` that currently reads:

```
Find tokens with identical forms in both languages → native overlap set O
```

Replace it with:

```html
<li>
  Find tokens with identical forms in both languages → native overlap set
  <span class="math">\( O = V_1 \cap V_2 \)</span>
</li>
```

---

## Slide: "How to Control Overlap?"

After the closing `</ul>` tag, add the following block:

```html
<div class="formula">
  \[
    x'_i = \begin{cases}
      x_i + N, & \ell = L_2 \text{ and } x_i \notin O' \\
      x_i,     & \text{otherwise}
    \end{cases}
  \]
</div>
```

Also add the following CSS for `.formula`:

```css
.formula {
  margin-top: 2rem;
  font-size: 1.6rem;
  color: var(--text-color);
  text-align: center;
}
```

---

## Slide: "Ranking by Semantic Similarity"

In the `<ul>`, find the `<li>` that currently reads:

```
Use contextual embeddings from XLM-R
```

Replace it with:

```html
<li>
  Use contextual embeddings from XLM-R:
  <span class="math">\( \text{sim}(t) = \cos(e_1, e_2) \)</span>
</li>
```

---

## Slides: Four Condition slides

For each of the four condition slides below, find the **first `<li>`** inside the `<ul>`
(or inside `.two-column .text > ul` for slides with two-column layout),
and add a formula block **immediately after** that `<li>` closing tag.

### Slide: "Condition 1: No Overlap"

After the first `<li>` (currently: "All L2 token IDs shifted by +N"), add:

```html
<div class="formula">\( O' = \emptyset \)</div>
```

### Slide: "Condition 2: Low-similarity Overlap"

After the first `<li>` (currently: "Only tokens with the LOWEST cross-lingual semantic similarity are shared"), add:

```html
<div class="formula">\( O' = O_{lo} \)</div>
```

### Slide: "Condition 3: High-similarity Overlap"

After the first `<li>` (currently: "Only tokens with the HIGHEST cross-lingual semantic similarity are shared"), add:

```html
<div class="formula">\( O' = O_{hi} \)</div>
```

### Slide: "Condition 4: Full Overlap"

After the first `<li>` (currently: "All natively overlapping tokens are shared — regardless of meaning"), add:

```html
<div class="formula">\( O' = O \)</div>
```

---

## Notes

- All formulas use LaTeX syntax and should be rendered by MathJax or KaTeX.
- `.formula` blocks are centered and sized at `1.6rem` to match the slide's visual weight.
- Do not change any other content, layout, or styling outside of what is specified above.