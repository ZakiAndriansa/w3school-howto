# CLAUDE.md: W3Schools "How To" Clone

Context for Claude Code. Human-readable plan: `PLAN.md`. Reply to the user in Bahasa Indonesia.

## Project
University web programming assignment (2-person team). Clone the UI/UX of https://www.w3schools.com/howto/default.asp as closely as possible.
Required: top nav, left sidebar, ads (image AND video), every demo box rendered inside an `<iframe>`, a "Learn in Adventure Mode" section with self-made animation, footer.

Team:
1. **Anggota A (partner)**: page layout (`index.html` skeleton, `css/style.css`, nav, sidebar, ads, share bar, pagination, footer, responsive, deploy).
2. **Anggota B (Zaki)**: `demos/*.html` (22 iframe demo cards), Adventure Mode (`css/adventure.css`), filling `.howtocontainer` and `section.advb`.

Ask the user which member they are if it is unclear, and stay inside that member's files.

## Hard rules
1. **HTML + CSS only.** No `<script>`, no `on*=` attributes, no JS frameworks, no build tools.
2. **Links never navigate.** Every `<a>` in nav, sidebar, footer, share bar, pagination uses `href="#!"`. Only exceptions: `href="#id"` used for `:target` interactions, and `src` of iframes.
3. Interactions must still work through CSS (checkbox hack, radio `:checked`, `:target`, `:hover`, `:focus-within`, `<details>`).
4. **Self-made assets only.** Never hotlink or copy images, logos, or video from w3schools.com. Use own SVG, CSS shapes, or placeholder images the team created. Only exception, requested by Zaki: `assets/img/demos/slideshow-1.png` to `slideshow-4.png` are screenshots of the original Slideshow demo (credited in README). Do not add more.
5. Keep the code beginner-readable (it is graded): semantic tags, clear class names, short comments per section.
6. Do not edit files owned by the other member (see Ownership). If a change is needed there, tell the user instead.

## Ownership
| Path | Owner |
|---|---|
| `index.html` (everything except inside `.howtocontainer` and `section.advb`) | A |
| `css/style.css` | A |
| `assets/ads/`, `assets/img/` (logo, icons) | A |
| `demos/*.html` | B |
| `css/adventure.css`, `assets/img/adventure/` | B |
| content inside `.howtocontainer` and `section.advb` in `index.html` | B |
| `README.md`, `PLAN.md`, `CLAUDE.md` | both, via PR |

## Folder structure
```
index.html
css/style.css          layout, nav, sidebar, ads, cards, footer (A)
css/adventure.css      Adventure Mode (B)
demos/                 one self-contained HTML file per demo, CSS in its own <style> (B)
assets/ads/            banner.jpg, sky.png, iklan.mp4 (A)
assets/img/            logo.svg, social icons (A)
assets/img/adventure/  pixel-art sprites (B)
```

## Design tokens (define once in `css/style.css` `:root`)
```css
:root {
  --green: #04AA6D;       /* logo, Sign In, active item, active page number */
  --green-hover: #059862;
  --dark: #282A35;        /* subtopnav, footer */
  --sidebar: #E7E9EB;
  --content-bg: #F1F1F1;  /* .howtocontainer background */
  --purple: #9763F6;      /* Paid Courses button */
  --footer-link: #FFF4A3;
  --text: #000;
  --topnav-h: 46px;
  --subnav-h: 28px;
  --sidenav-w: 240px;
  --font: "Source Sans Pro", Verdana, sans-serif;
  --mono: Consolas, Menlo, "Courier New", monospace;
}
```
Breakpoints (same as W3.CSS): small `< 601px`, medium `601px to 992px`, large `>= 993px`. Sidebar collapses below 993px; right ad column moves under main below 993px.

## Required DOM contract (keep these ids/classes so A and B fit together)
```
header#top-nav-bar                     sticky top:0, white, height var(--topnav-h)
  a.tnb-logo
  nav.tnb-menu
    input#m-tut|#m-ref|#m-exe|#m-cert (type=checkbox, hidden) + label.tnb-menu-btn
    div.tnb-panel                      big modal-like panel, opens on :checked, label "×" closes it
  form.tnb-search  (input + icon button, no action needed)
  label.tnb-more "⋮"
  div.tnb-right   a "Spaces", a "Upgrade", a "App" + span.badge-new, a.btn-paid, a.btn-signin
nav#subtopnav                          dark bar, horizontal scroll, a.active = "HOW TO"
input#sidenav-toggle (checkbox, hidden) + label.sidenav-btn (hamburger, mobile only)
div.layout                             CSS grid: var(--sidenav-w) 1fr 2fr-ish right column
  aside#sidenav                        position sticky, height calc(100vh - topnav - subnav), overflow-y auto
    input.sidenav-search
    h2.sidenav-heading  + a.sidenav-link (a.sidenav-link.active for "HowTo Home")
  main#main
    div#mainLeaderboard                image ad, area height 250px
    div.ws-share                       "SHARE" + icon links
    h1 "W3Schools How To"
    div.howtopag                       ‹ 1 2 3 4 5 6 7 8 ›, .active = green
    p.intro "Code snippets for HTML, CSS and JavaScript."
    div.howtocontainer                 grey bg; B inserts .w3-card-4 cards here
    div.howtopag
  aside#right
    a.ad-sky > img                     image ad
    video.ad-video autoplay muted loop playsinline
    div.right-social + a.remove-ads "REMOVE ADS"
section.advb#adventure                 B
footer#footer                          dark
  div.footer-top    logo + PLUS SPACES GET CERTIFIED FOR TEACHERS PRACTICE CONTACT US
  div.footer-cols   4 columns: Top Tutorials, Top References, Top Examples, Get Certified
  div.footer-social + FORUM ABOUT ACADEMY
  p.footer-legal    disclaimer + "Copyright 1999-2026 ..."
```

Demo card (styled by A, filled by B):
```html
<div class="w3-card-4">
  <h2>Slideshow</h2>
  <iframe class="howto-iframe" src="demos/slideshow.html" title="Slideshow" loading="lazy"></iframe>
  <p class="howto-container"><a href="#!" class="howto-link">Learn how to create a Slideshow »</a></p>
</div>
```
`.w3-card-4`: white bg, `box-shadow: 0 4px 10px 0 rgba(0,0,0,.2), 0 4px 20px 0 rgba(0,0,0,.19)`, padding 16px, margin 0 auto 24px, max-width ~820px. `.howto-iframe`: width 100%, no border, height set per demo by B.

## The 22 demo cards (page 1 of the original, in order)
Slideshow, Login Form, Accordion, Hover Dropdowns, Click Dropdowns, Side Navigation, Fixed Sidebar, Modal Box (its popup header reads "Modal Header"; not a separate card), Modal Image, Lightbox, Slideshow Gallery, Image Hover Overlay, Tabs, Vertical Tabs, Tab Image Gallery, Alert Buttons, Outline Buttons, Top Navigation, Responsive Top Navigation, Fullscreen Navigation, Login Form in Navbar, Change Background on Scroll.
File names: kebab-case, e.g. `demos/slideshow.html`, `demos/login-form.html`, `demos/change-bg-scroll.html`.

## CSS replacements for JS
| Need | Technique |
|---|---|
| Click-open panel / dropdown / hamburger | checkbox hack: hidden `<input type="checkbox" id>` + `<label for>` + `#id:checked ~ .target` |
| Hover dropdown | `:hover`, `:focus-within` |
| Slideshow prev/next/dots, tabs, gallery | hidden radios + `:checked ~` selectors (or `@keyframes` auto-play) |
| Accordion | `<details><summary>` |
| Modal, lightbox, login popup | `:target` (open `href="#modal1"`, close `href="#!"`) |
| Change background on scroll | stacked `background-size: cover` blocks + `position: fixed` text box (same as original, no JS needed) |
| Video ad | `<video autoplay muted loop playsinline>` |
| Adventure Mode | `@keyframes` + `steps()` sprite walk, swaying trees, blinking chest, bubble pop-in |

## Adventure Mode reference (B)
Left: white card "FREE ACCOUNT / Track your progress" with rows XP earned 0, Day streak 0, Spaces 0, League –, green button "Sign in to track progress".
Right: label "NEW", h2 "Learn in Adventure Mode", text "Coding fundamentals as bite-sized lessons and challenges.", three black buttons (App Store, Google Play, Browser).
Stage: light-blue sky, green grass, grey dirt path, wooden "ADVENTURE" signpost, walking pixel character, speech bubble "Learn more about Adventure Mode ›", pixel trees, stumps, rocks, treasure chest. All drawn by the team.

## Git workflow
Remote: https://github.com/ZakiAndriansa/w3school-howto.git. All branches below already exist; use them, do not invent new feature branches.

| Branch | Owner | Scope |
|---|---|---|
| `feat/topnav` | A | top nav, menu panels, subtopnav |
| `feat/sidebar` | A | sidebar 13 groups + mobile hamburger |
| `feat/ads` | A | leaderboard, right image ad, video ad + assets |
| `feat/footer` | A | footer |
| `feat/page-extras` | A | share bar, pagination, intro, final responsive |
| `feat/demos-basic` | B | Slideshow, Login Form, Accordion |
| `feat/demos-nav` | B | Hover Dropdowns, Click Dropdowns, Side Navigation, Fixed Sidebar, Top Navigation, Responsive Top Navigation, Fullscreen Navigation, Login Form in Navbar |
| `feat/demos-modal-image` | B | Modal Box, Modal Image, Lightbox, Slideshow Gallery, Image Hover Overlay |
| `feat/demos-tabs-buttons` | B | Tabs, Vertical Tabs, Tab Image Gallery, Alert Buttons, Outline Buttons, Change Background on Scroll |
| `feat/adventure` | B | Adventure Mode |
| `feat/slideshow-images` | B | Slideshow demo images (screenshots of the original) |

1. Never commit directly to `main` (exception: docs agreed by both). Each demo branch also adds its cards to `.howtocontainer`.
2. Before working on a branch: `git checkout main && git pull origin main && git checkout <branch> && git merge main`.
3. Fixes after a merge go on a new `fix/<what>` branch from `main`.
4. Small commits, conventional prefix: `feat:`, `fix:`, `style:`, `docs:`, `chore:`.
5. Open a Pull Request; the other member reviews and merges.
6. Deploy: GitHub Pages from `main`, root.
7. Only commit or push when the user asks.

## Verification before saying something is done
1. No JS: search the repo for `<script` and `\son[a-z]+=`; both must return nothing.
2. Open `index.html` with VS Code Live Server; check DevTools Console for 404s.
3. Test widths 375, 768, 1280 px (DevTools device mode).
4. Click every interactive element changed and confirm it opens and closes without JS and without changing page.
5. Compare side by side with the original page and fix visible differences in spacing, color, font size.
