# Reusable Animation Prompt for Case Studies

Use this prompt whenever you want to add the same subtle motion layer to a new static HTML case study.
Paste it into Cowork and attach or reference your HTML file.

---

## The Prompt

```
I have a static HTML case study at [FILE PATH or "the attached file"]. 

Please add a subtle motion layer to it — the same treatment used in my Sara AI case study. 
Do NOT change any content, copy, layout, colors, fonts, or structure. Only add motion on top.

Here's exactly what to add:

1. SCROLL PROGRESS BAR
   - A fixed 2px blue (#053BEE) bar at the very top of the viewport
   - Width grows from 0% to 100% as the user scrolls down the page
   - Smooth transition: width 0.1s linear

2. NAV SCROLL SHADOW
   - When the user scrolls past 20px, add a subtle box-shadow to the nav bar
   - Also add backdrop-filter: blur(10px) and background: rgba(255,255,255,0.97) to the nav
   - Use a class .is-scrolled toggled via JavaScript

3. ACTIVE NAV LINK UNDERLINE
   - Nav links should have a sliding blue underline (height 1.5px) that animates in when active
   - The active link is whichever section is currently in view (tracked by scrollY vs section.offsetTop)

4. SCROLL REVEAL
   - Add class="reveal" to: section headings (h2), section labels, all body paragraphs, stat cards, 
     pillar cards, feature cards, iteration blocks, callout blocks, and the footer
   - CSS: opacity 0 + translateY(18px) initially; transition to opacity 1 + translateY(0) on .is-visible
   - Easing: cubic-bezier(0.22, 1, 0.36, 1), duration 0.65s
   - Use IntersectionObserver with threshold: 0.1, rootMargin: '0px 0px -40px 0px'
   - Once visible, unobserve (no re-animation on scroll back up)

5. STAGGER FOR GRIDS
   - Add class="stagger" to any grid wrapper (stat grids, pillar grids, card grids, testimonial grids)
   - Children get transition-delay: 0ms, 80ms, 160ms, 240ms respectively

6. HORIZONTAL SLIDE-IN FOR LISTS
   - For bullet-point lists (like "5 jobs" lists), add class="stagger-list reveal"
   - List items start at opacity 0 + translateX(-8px) and slide in with 70ms stagger when visible

7. HOVER MICRO-INTERACTIONS
   - Cards (feature cards, stat cards, pillar cards): background changes to var(--primary-subtle) on hover
   - Surface/feature cards with images: translateY(-3px) + blue box-shadow + image scale(1.03) on hover
   - List items: translateX(3px) + blue border on hover
   - All transitions: 0.2–0.25s ease

8. COVER / HERO IMAGE SCALE-IN
   - If there's a full-width cover image, start it at scale(1.015) and transition to scale(1) once loaded
   - Use an .is-loaded class added via JavaScript after the image's load event fires
   - Transition: 1.2s cubic-bezier(0.22, 1, 0.36, 1)

9. ANIMATED COUNTERS (if applicable)
   - If any elements show key numbers/stats with data-count attributes, animate them counting up
   - Use requestAnimationFrame with a cubic easeOut function, duration 1200ms
   - Trigger via IntersectionObserver at threshold: 0.5

10. GENERAL RULES
    - All JavaScript goes in a single <script> block at the bottom of <body>
    - Each JS behavior is wrapped in its own IIFE (immediately invoked function expression)
    - Always provide a graceful fallback: if IntersectionObserver isn't supported, show everything immediately
    - Preserve all existing IDs, class names, and href targets — only add new classes/attributes
    - Keep the original file intact as a backup (copy it to index-original.html first)
    - Save the animated version as index.html (the live file)
```

---

## Tips for best results

- **Before running this prompt**, make sure your HTML file uses CSS custom properties (`--primary`, `--primary-subtle`, etc.) that match the rest of your portfolio's color system. If it uses different variable names, note them in your prompt.
- If your case study has a **video**, also say: *"Add a click-to-pause toggle on the video with a centered play icon overlay."*
- If you want to **skip any step** (e.g. no counter animation), just delete that numbered item from the prompt.
- After Claude applies the changes, always **open the file in your browser** to check everything looks right before deploying.

---

## Deployment reminder

Once your case study HTML is ready:
1. Drag the entire case study folder to **netlify.com/drop**
2. You'll get a live public URL in under 60 seconds
3. No account, no build step, no configuration needed
