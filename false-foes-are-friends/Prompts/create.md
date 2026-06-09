# Prompt: Generate HTML Slide Deck for Paper Reading

## Task
Create a single HTML file that functions as a presentation slide deck for a paper reading session.

## Input Files
The slide content is split into three Markdown files located in `paper_reading/Content/`:
- `part1.md` — Opening section
- `part2.md` — Experimental setup section
- `part3.md` — Core results section

Read all three files carefully. Each file contains the slide titles and bullet points for that section. Use them as the exact content for the slides — do not paraphrase or reorder.

## Output
- A single self-contained HTML file
- Save it to `paper_reading/slides.html`

## Slide Structure
- Total slides: approximately 40
- Each slide has a clear title and 2–4 bullet points (keywords or short phrases)
- Do not make slides too sparse — every slide should have substantive content
- The final slide is a "Thank You / Questions" slide

## Navigation
- Arrow key navigation (left/right) between slides
- On-screen Previous / Next buttons
- Slide counter showing current slide and total (e.g., "3 / 40")
- Keyboard shortcut: press `F` to toggle fullscreen

## Visual Style
- Clean academic style
- Dark background (e.g., deep navy or dark gray)
- Light text (white or off-white)
- Accent color for titles and highlights (e.g., soft blue or teal)
- Simple sans-serif font (e.g., Inter, Helvetica, or system-ui)
- No animations or transitions — keep it minimal and distraction-free
- Generous whitespace; do not crowd the slide

## Language
- All slide content in English
- No Japanese or Chinese text in the slides themselves (examples from those languages may appear as illustrative text within bullet points if present in the content files)

## Technical Requirements
- Fully self-contained: no external dependencies or CDN links
- All CSS and JavaScript embedded in the single HTML file
- Must render correctly when opened locally in a browser (file:// protocol)
- Responsive to different screen sizes