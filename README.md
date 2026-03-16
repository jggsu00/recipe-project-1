# 🍳 Golden Pantry
 
A pure HTML & CSS recipe website with no JavaScript. Built by Jason Lopez and John Gomez for CSC 4370/6370 at Georgia State University. Features a gold colour scheme, local food photography, and interactive UI powered entirely by CSS.
 
---
 
## Pages
 
| File | Description |
|------|-------------|
| `index.html` | Landing / welcome page with navigation to Recipes and About |
| `recipe.html` | Recipe list — 2-column grid of recipe cards with food photos |
| `details.html` | Recipe detail page — all 4 recipes shown/hidden via CSS `:target` |
| `about.html` | About page with team bios, mission statement, and contact info |
| `styles.css` | Shared stylesheet for recipe, details, and about pages |
| `welcome.css` | Standalone stylesheet for the index/landing page |
 
---
 
## Assets
 
```
assets/
├── fonts/
│   └── Rowdies-Bold.ttf      # Display font used site-wide
├── carb.png                  # Spaghetti Carbonara photo
├── salmon.png                # Honey Garlic Salmon photo
├── taco.png                  # Classic Beef Tacos photo
└── tikka.png                 # Chicken Tikka Masala photo
```
 
> All food photography is stored locally — no external image dependencies.
 
---
 
## Features
 
- **CSS-only recipe routing** — clicking a Details button navigates to `details.html#recipe-id`, and the correct recipe is shown using `:target` with `body:has()` fallback
- **Ingredient checklist** — hidden checkboxes + adjacent labels; checked items get a strikethrough and gold tick via CSS
- **Suggested next steps** — 4-card grid per recipe with confidence bar indicators
- **Cooking method comparison** — flip cards using CSS `perspective` + `rotateY(180deg)` triggered by hidden checkboxes
- **Light / Dark mode toggle** — CSS-only theme switcher in the navbar using a hidden checkbox and `body:has(#dark-toggle:checked)` to swap CSS custom properties
- **Back button** — each recipe detail page has a `← Back to Recipes` link
- **Custom font** — Rowdies Bold loaded via `@font-face` from a local `.ttf` file, no external font service needed
 
---
 
## How the CSS tricks work
 
### Recipe show/hide (no JS)
Each recipe is a `div` with a unique `id`. The default recipe (carbonara) is shown with `#carbonara { display: block }` and hidden when another recipe is targeted:
 
```css
.recipe-detail { display: none; }
.recipe-detail:target { display: block; }
 
#carbonara { display: block; }
body:has(#salmon:target) #carbonara,
body:has(#tacos:target) #carbonara,
body:has(#tikka:target) #carbonara { display: none; }
```
 
### Flip cards
Each card contains a hidden checkbox. A full-size `<label>` overlay acts as the click target. When checked, `rotateY(180deg)` is applied to the inner container:
 
```css
.flip-card input[type="checkbox"]:checked ~ .flip-inner {
    transform: rotateY(180deg);
}
```
 
`perspective` is applied per `.flip-card` (not on the grid container) to prevent cards drifting during the animation.
 
### Dark mode
A hidden `<input type="checkbox" id="dark-toggle">` lives just before the `<header>`. The label inside the navbar toggles it. When checked, CSS custom properties are overridden:
 
```css
body:has(#dark-toggle:checked) {
    --bg-page: #1a1610;
    --bg-card: #231e14;
    --text-primary: #c8b882;
    /* etc. */
}
```
 
> ⚠️ The dark mode toggle resets on page navigation — this is an inherent limitation of CSS-only state. JavaScript would be required to persist it across pages.
 
---
 
## File structure
 
```
golden-pantry/
├── index.html
├── recipe.html
├── details.html
├── about.html
├── styles.css
├── welcome.css
└── assets/
    ├── fonts/
    │   └── Rowdies-Bold.ttf
    ├── carb.png
    ├── salmon.png
    ├── taco.png
    └── tikka.png
```
 
---
 
## Browser support
 
Relies on `body:has()` which requires a modern browser (Chrome 105+, Safari 15.4+, Firefox 121+). Does not work in older browsers.
 
---
 
## Authors
 
**Jason Lopez** — jlopez74@student.gsu.edu - Chef / Undergraduate Student, Georgia State University  
**John Gomez** — jgomez45@student.gsu.edu - Chef / Graduate Student, Georgia State University

Course: CSC 4370/6370
