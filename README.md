# Reveal Animated Hero Slider

A lightweight, CSS-animated hero image slider with smooth reveal effects, built with vanilla HTML, CSS (SCSS), and JavaScript. Features a Japan travel theme with four destinations — Tokyo, Kyoto, Osaka, and Hokkaido.

---

## Demo

![Slider Preview](https://assets.codepen.io/1159990/tokyo.jpg)

> The slider displays a full-width hero image with an animated title card that slides in from the left, paired with a fade-in description below.

---

## Features

- **Reveal animation** — A white overlay wipes off the image on each slide transition using a CSS `scaleX` keyframe animation
- **Fade-in title card** — The intro box animates in with `fadeInReveal` on desktop and `fadeInUp` on mobile
- **Fade-in description** — The description text fades in with a staggered delay after the title
- **Keyboard navigation** — Use the ← and → arrow keys to move between slides
- **Button controls** — Previous and next arrow buttons styled with pure CSS arrows (no icon fonts)
- **Responsive layout** — Mobile-first grid collapses cleanly; title card repositions and resizes for smaller screens
- **Accessible** — Navigation buttons include visually-hidden labels for screen readers
- **No dependencies** — Pure vanilla JS, no frameworks or libraries required

---

## File Structure

```
Reveal-Animated-Hero-Slider/
├── INDEX.HTML       # Markup: nav, slider list, controls
├── INDEX.JS         # Slider logic (next/prev, keyboard events)
├── INDEX.SCSS       # Source styles with variables and animations
├── INDEX.CSS        # Compiled CSS (ready to use in browser)
├── INDEX.CSS.map    # Source map for debugging
└── README.md
```

---

## Getting Started

### Option 1 — Open directly in browser

No build step needed. Just open `INDEX.HTML` in any modern browser:

```bash
git clone https://github.com/switchd2/Reveal-Animated-Hero-Slider.git
cd Reveal-Animated-Hero-Slider
open INDEX.HTML   # macOS
# or double-click INDEX.HTML in your file explorer
```

The compiled `INDEX.CSS` is already included, so everything works out of the box.

### Option 2 — Edit the SCSS source

If you want to modify styles, compile `INDEX.SCSS` to `INDEX.CSS` using any SCSS compiler:

```bash
# Using the Sass CLI
npm install -g sass
sass INDEX.SCSS INDEX.CSS --watch

# Or with Node.js sass package
npx sass INDEX.SCSS INDEX.CSS
```

---

## How It Works

### HTML Structure

The slider is an unordered list (`.slider`) where each `<li>` is a `.slider-item`. Only the item with the `.active` class is shown at a time:

```html
<ul class="slider">
  <li class="slider-item active">
    <!-- image, title card, description -->
  </li>
  <li class="slider-item">
    <!-- ... -->
  </li>
</ul>
```

### JavaScript

`INDEX.JS` manages the active state. It tracks the current index (`count`) and toggles the `.active` class between items:

- `showNextItem()` — increments the counter and wraps to 0 at the end
- `showPreviousItem()` — decrements the counter and wraps to the last slide
- `keyPress(e)` — listens for `keyCode 37` (←) and `keyCode 39` (→) on the document

### Animations

All animations are defined in `INDEX.SCSS` using `@keyframes` and triggered on the `.active` class:

| Animation | Element | Effect |
|---|---|---|
| `slideOut` | `.active .image-holder::after` | White overlay wipes off the image from right to left |
| `fadeInReveal` | `.intro` (desktop) | Title card slides in from the left and fades in |
| `fadeInUp` | `.intro` (mobile) | Title card rises up from below |
| `fadeIn` | `.description` | Description fades in with a 0.6s delay |

All transitions use a `cubic-bezier(0.19, 1, 0.22, 1)` easing for a snappy, elastic feel.

---

## Responsive Behaviour

| Breakpoint | Layout |
|---|---|
| **Mobile** (`< 768px`) | Single column, title card overlaps image from below, centered controls |
| **Desktop** (`≥ 768px`) | Image takes 85% width, title card floats absolutely on the left with a horizontal reveal animation |

---

## Customisation

### Changing slides

Add or remove `<li class="slider-item">` elements inside the `.slider` list. The JavaScript reads the count dynamically, so no JS changes are needed.

### Changing images

Replace the `src` attributes on the `<img>` tags inside each `.slider-item`:

```html
<img src="your-image.jpg">
```

Images are displayed at `70vh` height with `object-fit: cover` to maintain aspect ratio.

### Changing colours

Edit the SCSS variables at the top of `INDEX.SCSS`:

```scss
$white:     #fff;
$black:     #1a1a1a;
$gray:      #666;
$red:       #e83f43;   // accent colour — underline, logo dot
$off-white: #f9f9f9;   // page background
```

### Changing the font

The project uses [Outfit](https://fonts.google.com/specimen/Outfit) from Google Fonts. To switch fonts, update the `@import` at the top of `INDEX.SCSS` and change the `font-family` on `body`.

---

## Browser Support

Works in all modern browsers (Chrome, Firefox, Safari, Edge). Requires support for CSS animations, `object-fit`, and ES6.

---

## License

This project is open source. Feel free to use and adapt it for personal or commercial projects.
