# Prompt: Improve Slide Design and Add Images

## Task

You have an existing HTML slide deck at `paper_reading/slides.html`. Please do two things:

1. Redesign the visual style to be cleaner and more polished
2. Add images from the `paper_reading/Image/` folder to the appropriate slides

---

## Part 1: Visual Redesign

Redesign the slide deck with the following direction:

- **Overall feel**: Clean, modern, minimalist academic style with a touch of design sensibility. Not plain or generic, but not distracting either.
- **Background**: Deep dark background (e.g. #0f1117 or similar dark navy/charcoal)
- **Text**: Off-white body text (#e8e8e8), with a soft accent color for titles and highlights (e.g. a muted teal #4ecdc4 or soft blue #6eb5ff)
- **Typography**: Use a clean geometric sans-serif. Prefer something with character — e.g. `DM Sans`, `Outfit`, or `Sora` loaded from Google Fonts. Title font can be slightly heavier weight.
- **Layout**: Each slide should have clear visual hierarchy — a prominent title at the top, bullet points below with generous line spacing. Left-aligned text. Comfortable padding on all sides.
- **Bullet points**: Use a subtle accent-colored dot or dash instead of default browser bullets. Each bullet should feel spacious, not cramped.
- **Slide counter**: Styled subtly in the bottom right corner (e.g. small, muted color)
- **Navigation buttons**: Minimal, icon-style arrows at the bottom center or sides. Unobtrusive.
- **No animations or transitions**: Keep it static and distraction-free.
- **Slides with images**: When a slide contains an image, place the image on the right half of the slide and the text on the left half, in a two-column layout. The image should be displayed cleanly without borders or heavy shadows.

---

## Part 2: Adding Images

The images are located in `paper_reading/Image/`. Add them to the following slides according to this mapping:

| Slide                                       | Image file       | Notes                                     |
| ------------------------------------------- | ---------------- | ----------------------------------------- |
| Slide 16 (No Overlap: Example)              | `figure1(d).png` | No Overlap condition diagram              |
| Slide 18 (Low-similarity Overlap: Example)  | `Figure1(c).png` | Low-sim condition diagram                 |
| Slide 20 (High-similarity Overlap: Example) | `Figure1(b).png` | High-sim condition diagram                |
| Slide 22 (Four Conditions: Summary)         | `Figure1.png`    | Full Figure 1 showing all four conditions |
| Slide 30 (Embedding Result 1)               | `Figure2_full_highsim.png`    | Full Figure 2 embedding analysis          |
| Slide 31 (Embedding Result 2)               | `Figure2_lowsim.png`    | Same Figure 2, different slide context    |
| Slide 32 (Embedding Result 3)               | `Figure2_nooverlap.png`    | Same Figure 2, different slide context    |

Use relative paths to reference the images (e.g. `Image/Figure1.png`). Do not embed images as base64.

---

## Output

Overwrite `paper_reading/slides.html` with the updated version.
