# CLAUDE.md — Yoga With Claire

## Business Overview
Yoga With Claire is a yoga teaching business run by Claire. She teaches friendly, accessible yoga classes that focus on breath-led movement, sustainable strength, and finding a calm, steady mind. Classes are suitable for complete beginners through to those returning to the mat. Claire is a registered teacher with the British Wheel of Yoga (BWY) — the UK's national governing body for yoga.

## Tech Stack
- **Astro 5** — static site generator
- **Tailwind CSS 4** — via `@tailwindcss/vite` plugin (NOT the older `@astrojs/tailwind`)
- **TypeScript** — strict mode
- **Sharp** — image optimisation (dev dependency)
- **@astrojs/sitemap** — auto-generates XML sitemap

## Project Structure
```
src/
    assets/images/              # Source images (jpg, png → optimised via astro:assets)
    components/
        layout/
            Header.astro        # Site navigation
            Footer.astro        # Footer with social links, copyright
        sections/
            Hero.astro           # Homepage hero section
            ClassesOverview.astro # Class cards for homepage
            Testimonials.astro   # Student testimonials carousel/grid
            About.astro          # About section
        ui/
            Button.astro         # Reusable button component
            Card.astro           # Reusable card component
            SectionHeading.astro # Consistent section headings
        SEO.astro               # Meta tags, OG tags, canonical URL
    data/
        siteConfig.ts           # Centralised site config
    layouts/
        BaseLayout.astro        # HTML shell, font loading, global structure
    pages/                      # File-based routing (trailing slashes)
        index.astro             # Homepage
        about/index.astro       # About Claire
        classes/index.astro     # Class descriptions
        timetable/index.astro   # Weekly schedule
        prices/index.astro      # Pricing info
        contact/index.astro     # Contact details and social links
        privacy/index.astro     # Privacy policy
    styles/
        global.css              # Tailwind directives + CSS custom properties
public/
    robots.txt                  # Search engine rules
    favicon.svg                 # Site favicon (replace with Claire's logo)
```

## Design System

### Colours
- **Primary (deep sage green):** #5B7B6F — calm, natural, grounding
- **Secondary (warm sand):** #E8DDD3 — soft backgrounds
- **Accent (muted terracotta):** #C4856A — CTAs, highlights
- **Text (charcoal):** #2D2D2D
- **Background (off-white):** #FAFAF7
- **White:** #FFFFFF

### Typography
- **Headings:** Cormorant Garamond (Google Fonts) — elegant but approachable
- **Body:** Inter (Google Fonts) — clean, modern, readable
- **Base size:** 16px / 1rem
- **Line height:** 1.6 for body text

### Overall Feel
Warm, calm, welcoming, natural. Clean layouts with generous whitespace. Not overly spiritual — matches Claire's friendly, down-to-earth personality. Think: modern wellness, not incense-and-crystals.

## Accreditation
Claire is a registered teacher with the **British Wheel of Yoga (BWY)** — the UK's national governing body for yoga. Display the BWY Teacher badge on the About page and/or footer. The badge image is in `src/assets/images/bwy-teacher-badge.png`.

## Testimonials
Use 2–3 on the homepage as social proof. Show all on the About page.

1. **Amanda:** "Claire is an amazing teacher who inspires us all. She puts so much thought into every class. She encourages us and guides us safely through our poses, providing lots of adaptations & extensions throughout. I always feel uplifted, relaxed and empowered after each & every class. Thx so much Claire."
2. **Emma:** "I honestly cannot recommend Claire's yoga classes highly enough. The atmosphere is calm, friendly and relaxing and the environment is safe and welcoming. All levels are catered for and Claire is totally mindful of everyone's individual capabilities and requirements - adjusting the moves accordingly. I feel fabulous and refreshed after each session."
3. **Diana:** "Claire is a wonderful yoga teacher, her classes always flow beautifully, leaving you feeling relaxed yet energised and spiritually ready to face your day. She also has the most wonderful calm voice."
4. **Rue:** "Yoga with Claire envelopes you into a loving embrace which nourishes body and soul. It is the highlight of my week!"
5. **Lucy:** "Yoga with Claire is amazing. I love all the different breathing techniques I have learnt. I would highly recommend this class."

## Image Handling
- Store source images in `src/assets/images/`
- Import using `import heroImg from '../assets/images/hero.jpg'`
- Use Astro's `<Image>` component: `import { Image } from 'astro:assets'`
- Astro auto-converts to WebP and generates responsive sizes
- Always include descriptive `alt` text
- Use `loading="lazy"` except for hero/above-fold images

## Configuration

### astro.config.mjs
The sitemap integration has already been added by `npx astro add sitemap`. You need to manually update astro.config.mjs to add the site URL and the Tailwind v4 vite plugin. The final file should look like this:

```javascript
import { defineConfig } from 'astro/config';
import tailwindcss from '@tailwindcss/vite';
import sitemap from '@astrojs/sitemap';

export default defineConfig({
  site: 'https://yogawithclaire.yoga',
  vite: {
    plugins: [tailwindcss()],
  },
  integrations: [sitemap()],
  trailingSlash: 'always',
});
```

### global.css
Create this file at `src/styles/global.css`:

```css
@import 'tailwindcss';

@theme {
  --color-primary: #5B7B6F;
  --color-primary-light: #7A9B8F;
  --color-primary-dark: #4A6A5E;
  --color-secondary: #E8DDD3;
  --color-secondary-dark: #D4C9BF;
  --color-accent: #C4856A;
  --color-accent-dark: #B07458;
  --color-text: #2D2D2D;
  --color-text-light: #6B6B6B;
  --color-bg: #FAFAF7;
  --color-white: #FFFFFF;
  --font-heading: 'Cormorant Garamond', serif;
  --font-body: 'Inter', sans-serif;
}
```

### siteConfig.ts
Create this file at `src/data/siteConfig.ts`:

```typescript
export const siteConfig = {
  name: 'Yoga With Claire',
  tagline: 'Friendly, accessible yoga classes',
  description: 'Yoga With Claire offers friendly, accessible yoga classes including Gentle Flow, Vinyasa, and Beginners. Build strength, mobility, and calm — whether you\'re a complete beginner or returning to the mat.',
  url: 'https://yogawithclaire.yoga',
  email: 'hello@yogawithclaire.yoga',
  social: {
    instagram: 'https://www.instagram.com/yo.gawithclaire/',
    facebook: 'https://www.facebook.com/people/Yoga-With-Claire/100089760002450/',
  },
  nav: [
    { label: 'Home', href: '/' },
    { label: 'About', href: '/about/' },
    { label: 'Classes', href: '/classes/' },
    { label: 'Timetable', href: '/timetable/' },
    { label: 'Prices', href: '/prices/' },
    { label: 'Contact', href: '/contact/' },
  ],
};
```

## Content

### Classes
1. **Gentle Flow** — Slow, spacious, and soothing. Great for beginners or those returning to practice.
2. **Vinyasa** — Steady, strength-building sequences with options for all levels.
3. **Beginners** — Foundations-focused, with simple cues and friendly pace.

### Timetable (confirmed)
- Monday — Gentle Flow — 6:00–7:00 pm
- Wednesday — Vinyasa — 6:30–7:30 pm
- Friday — Beginners — 9:30–10:30 am

### Prices
- Drop-in: £10
- 6-Class Block: £45
- Concessions available — just ask

## Key Patterns
- Use Astro components for reusable UI (Button, Card, SectionHeading)
- Use `siteConfig.ts` for all site-wide data (name, URLs, nav links)
- Keep pages thin — import section components rather than writing long pages
- Use semantic HTML (main, section, nav, footer, article)
- Mobile-first responsive design
- Accessible: proper heading hierarchy, alt text, focus states, sufficient contrast

## Common Tasks

### Adding a new page
1. Create `src/pages/pagename/index.astro`
2. Import `BaseLayout` and wrap content
3. Add to `nav` array in `siteConfig.ts`

### Adding images
1. Save image to `src/assets/images/`
2. Import in component: `import img from '../../assets/images/filename.jpg'`
3. Use: `<Image src={img} alt="Description" />`

## Build & Deploy
- **Dev:** `npm run dev` → http://localhost:4321
- **Build:** `npm run build` → outputs to `dist/`
- **Deploy:** Push to GitHub → Cloudflare Pages auto-deploys
- **Repo:** github.com/davidgelisa-spec/yoga-with-claire
- **Hosting:** Cloudflare Pages (free tier)
