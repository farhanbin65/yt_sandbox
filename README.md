# 🎬 YT SandBox

A browser-based multi-instance YouTube player built with vanilla JavaScript, Tailwind CSS, and DaisyUI.
This project was created as a frontend learning exercise exploring iframe embedding, DOM manipulation,
randomisation techniques, and UI component design.

---

## 📚 What This Project Teaches

This is a great beginner-to-intermediate project for understanding several core web concepts:

### 1. **Dynamic DOM Manipulation**
The core of this app is JavaScript creating HTML elements on the fly — no frameworks, no virtual DOM.
````js
let div = document.createElement('div');
const iframe = document.createElement('iframe');
div.appendChild(iframe);
playerContainer.appendChild(div);
````

You'll learn how to build and inject elements programmatically rather than hardcoding HTML.

---

### 2. **Regex for URL Parsing**
The `getID()` function uses a regular expression to extract YouTube video IDs from multiple URL formats:

````js
const regExp = /^.*(youtu.be\/|v\/|u\/\w\/|embed\/|watch\?v=|&v=|shorts\/)([^#&?]*).*/;
````

This handles all these formats:
- `https://www.youtube.com/watch?v=abc123`
- `https://youtu.be/abc123`
- `https://www.youtube.com/shorts/abc123`

**Concept:** Regex capture groups, URL structure, string matching.

---

### 3. **Iframe Embedding & Query Parameters**
Each player is an `<iframe>` pointed at YouTube's embed API with query strings controlling behaviour:

````
https://www.youtube.com/embed/{videoId}?autoplay=1&mute=1&start=7&rel=0&widget_referrer=https://...
````

| Parameter | Purpose |
|---|---|
| `autoplay` | Starts video on load |
| `mute` | Required for autoplay in most browsers |
| `start` | Random start time in seconds |
| `rel` | Disables related videos |
| `widget_referrer` | Simulates traffic source |

**Concept:** Third-party embed APIs, query strings, iframe sandbox behaviour.

---

### 4. **Staggered Async Loading with `setTimeout`**
Rather than spawning all iframes at once (which would hammer the browser), each player loads with a delay:

````js
setTimeout(() => {
    // create and append iframe
}, i * 1500);
````

This is a simple form of **rate limiting** / **throttling** — a real-world pattern used in APIs and UI rendering.

**Concept:** Event loop, non-blocking execution, performance-conscious rendering.

---

### 5. **Randomisation Techniques**
Two randomisation strategies are used:

````js
const randomRef = platforms[Math.floor(Math.random() * platforms.length)]; // random array item
const randomStart = Math.floor(Math.random() * 15);                        // random number in range
````

**Concept:** `Math.random()`, array indexing, seeding variation in repeated operations.

---

### 6. **UI Component Design with DaisyUI + Tailwind**
The UI uses DaisyUI's component library layered on top of Tailwind utility classes:

````html
<div class="card bg-base-100 shadow-xl">
    <div class="card-body text-center">
````

The `data-theme="halloween"` attribute on `<html>` switches the entire app's colour scheme — one of DaisyUI's built-in themes.

**Concept:** Utility-first CSS, theming systems, component libraries.

---

### 7. **Responsive Grid Layout**
The player grid uses Tailwind's responsive grid system:

````html
<div class="grid grid-cols-2 md:grid-cols-5 gap-4">
````

- Mobile: 2 columns
- Desktop (`md` breakpoint): 5 columns

**Concept:** CSS Grid, responsive breakpoints, mobile-first design.

---

## 🛠 Tech Stack

| Technology | Role |
|---|---|
| HTML5 | Structure |
| Vanilla JavaScript | Logic & DOM manipulation |
| Tailwind CSS (CDN) | Utility styling |
| DaisyUI | Pre-built UI components |
| YouTube Embed API | Video playback |
| Google Analytics | Usage tracking |
| Google AdSense | Monetisation layer |

---

## 📁 Project Structure

````
yt-sandbox/
├── index.html       # Entire app — single file architecture
└── logo.png         # Favicon / brand logo
````

This is a **single-file application** — a common pattern for simple tools where the overhead of a build system (React, Vite, etc.) isn't justified.

---

## 🚀 How to Run

No installation needed. Open `index.html` directly in a browser, or deploy to any static host:

- [Netlify](https://netlify.com) — drag and drop the folder
- [GitHub Pages](https://pages.github.com) — push to a `gh-pages` branch
- [Vercel](https://vercel.com) — connect your repo

---

## ⚠️ Browser Behaviour Notes

- **Autoplay with sound** is blocked by most modern browsers unless the user has interacted with the page first. This is a browser security policy — the `mute` option works around it.
- **Iframe sandboxing** — some websites block being loaded inside iframes via `X-Frame-Options` headers. YouTube explicitly allows embedding via their embed endpoint.
- Heavy use of iframes is **resource intensive** — CPU and memory usage scales with player count.

---

## 💡 Potential Extensions (Learning Ideas)

- Add a **progress tracker** showing which players have finished loading
- Implement a **stop all / reset** button that clears the player grid
- Store recent URLs in **localStorage**
- Add a **fullscreen toggle** per player
- Rewrite logic as a **React component** with `useState` and `useEffect` for practice
- Add a **playlist mode** that queues multiple video IDs

---

## 👨‍💻 Author

Built by **Team Keo** — a final-year Computing Systems student project exploring frontend JavaScript and browser-based media tooling.

Credit & inspiration: https://github.com/pooreyoutuber

---

*This project is intended for educational and experimental purposes.*
