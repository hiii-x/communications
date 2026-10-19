# X Communications: Website Documentation (v1.8, launch build)

## 1. Web content

**Page order (single page):** Intro → Hero → Services → FAQ → The Heart of X → Background → Testimonials → Get in touch → Footer.

| Section | Content |
|---|---|
| Hero | "Communicate. Connect. Create Impact." in three large lines sliding in one after another. Sub-heading centred directly under the headline, on a single line on desktop, at description size: "Strategic brand and digital advisory for leaders, built for people and for AI search." |
| Services | Six practices: Brand Communication & Thought Leadership, Messaging & Architecture, Executive Communications & Media Training, Reputation Management, Digital Content & GEO Strategy, Event Management, each with a description and keyword tags. |
| FAQ | Five dialog-style questions. Answers appear after typing dots. |
| The Heart of X | Connect, Partnership, Breakthroughs. The four strokes join as "Connect" appears; the solid, thick X fades in and starts to glow as "Partnership" appears, and the glow swells again for "Breakthroughs". The earlier drag-to-rotate and double-click spin (and their on-screen hint) are removed; only a gentle mouse-parallax tilt remains. |
| Background | "20+" years figure and three practice cards. The figure flicks upward from 10 to 20, then the "+" pops in. |
| Testimonials | Intro line: "Hover a glassball to read what people said." 30 remarks in 7 categories (below). Each logo ball shows its category name; on hover it flips to the X logo and a call-out shows the remark. Moving away flips it back to the category name. Under the bubbles: "References and client testimonials available upon request", in the same size as the Background stat caption. |
| Get in touch | "Ready to communicate with impact. Let's talk." set in the sub-heading typeface over two lines on the left ("Ready to communicate with impact." / "Let's talk."), over a field of drifting crystal particles. On the right, three glass buttons, the same size and font as the nav "Let's talk" button, keep the details hidden until clicked: **Send an Email** reveals the address as a mailto link; **WhatsApp now** reveals a "Chat on WhatsApp" link using WhatsApp's official click-to-chat format, `https://wa.me/<number>`, so visitors can start a chat without saving the number. On phones it opens the WhatsApp app if installed; otherwise (and on desktop) it shows WhatsApp's own page with a "Continue to chat" step. The link is kept Base64-encoded in the `D` object, never in the visible markup; **Post a mail** reveals the address on two lines (PO Box 71764 / Kowloon Central Post Office, Hong Kong). There is no "Reach us" panel, "Open mail app" or "Copy" button. |

**Testimonial categories:** Brand Comms (7), Messaging (4), Executive Comms (4), Crisis (5), Digital (3), Stakeholder (5), Event (2). Quotes are kept verbatim from the brief. The Pizza Hut messaging ball carries only "impactful messaging"; "exceptional judgement" and "trusted partner" live on their own Crisis and Executive Comms balls.

**GEO:** `ProfessionalService` and `FAQPage` JSON-LD in the head. All testimonials are also in a visually hidden list (`.sr`) for crawlers and screen readers.

## 2. Design direction

- **Mood:** Apple-grade minimalism meets dark glassmorphism. Void black `#000`, silver, luminous white. Testimonials add a black, blue and white palette.
- **Typefaces:** Fredoka for the hero headline (now much larger, as a full-impact banner), all sub-headings, and all sub-sub-headings: the service and background card titles, the Connect / Partnership / Breakthroughs captions, and the "Ready to communicate with impact" line. Only Frequently asked *questions*, The *Heart* of X and Get in *touch* keep a normal and italic mix. Services, Background, Testimonials and "Create Impact." are all upright. Unbounded and Instrument Sans are kept for numbers and body text.
- **FAQ questions:** set at body-text size (1.1rem), matching the card descriptions.
- **Sub-heading motion:** a plain slide up from below as the heading enters view. No character scrambling.
- **The X in "The Heart of X":** upright, bold and glowing, with no slit.
- **Logo:** vector SVG traced from the hi-res white logo. The grey 3D X is used in the intro.
- **Glass:** translucent fills, light edges, 14–26px backdrop blur, specular highlights. Nav buttons use liquid glass with a hover glow. The Get in touch block is a single glass panel; the three buttons sit directly on it at the right.
- **Particles:** crystal diamonds in pale cyan, blue and violet in the hero (a pointer-reactive grid), The Heart of X and Get in touch. No connecting lines.
- **Heart of X logo:** a vector X with real thickness: stacked side faces for depth, a bevelled rim and a bright top face, so it reads as solid even in white.
- **Layout:** the page keeps a 58px right margin (34px on mobile) so no content overlaps the scroll rail. Captions and headings in The Heart of X are sized from the remaining width, so no word is clipped at the right edge.
- **Type tiers (one size per tier, desktop / mobile):**

| Tier | Used for | Size |
|---|---|---|
| Hero | "Communicate. Connect. Create Impact." | `clamp(2.8rem, 9.6vw, 10.8rem)` / `clamp(2.2rem, 10vw, 4.4rem)` |
| Sub-heading | All section titles (`h2.title`) | `clamp(1.75rem, 4vw, 3.4rem)` |
| Sub-sub-heading | Service and background card titles, Connect / Partnership / Breakthroughs, "Ready to communicate with impact." | `clamp(1.25rem, 1.9vw, 1.7rem)` / `1.2rem` |
| Description | Card descriptions, heart captions, FAQ questions and answers, hero line, Background caption, testimonial intro and small print, revealed contact details | `1rem` / `.95rem` |
| Keywords | Hashtag chips | `.85rem` |

  The vertical label on a collapsed desktop card is a fixed `1.05rem`. Every description is smaller than the sub-sub-heading above it.
- **Alignment:** a card's title, description and keywords share one left edge. The old pointer parallax that shifted descriptions sideways is removed.
- **Card spacing:** a script (`fit()`) measures each card's title and description. On mobile the card height and the description's top offset adapt to the content, so keywords are never covered. On desktop the cards' minimum height grows to fit the longest one.
- **Navigation bar:** hides as soon as the page scrolls, slides back down after 1.8 seconds without scrolling, and always shows near the top of the page or while the menu is open.
- **Scroll rail:** fine glass line, glowing marker, ticks per section and the active section name.
- **Testimonial bubbles:** a black X on a white glass ball, or a white X on a black-to-blue glass ball. Happy faces are in blues, white and navy. On hover a ball turns into a glossy candy ball showing its category name, and a light-grey rounded call-out shows the company and executive on line one and the remark on line two. Logo balls spin more slowly than before.

## 3. Code

Single file `index.html`. External: Google Fonts, GSAP 3.12.5 and ScrollTrigger (cdnjs), Lenis 1.1.20 (jsDelivr). The logo and glow assets are embedded as CSS variables.

| Block | Purpose |
|---|---|
| `<style>` | Original design system and layout |
| `<style id="rev">` | Revision layer: liquid-glass buttons, right margin, Fredoka headings, slide-up reveal, testimonials, contact panel, rail |
| `rise()` | Wraps each `[data-rise]` heading and slides it up when 50% visible |
| `dotGrid()` | Hero crystal field reacting to the pointer |
| Background stat | Count-up flick from 10 to 20, then the "+" pops in, triggered by ScrollTrigger |
| `heartCanvas()` / `heartScroll()` | Crystal galaxy and the scroll timeline, with a gentle mouse tilt. The stage is now CSS-sticky inside a 420svh section (no GSAP pin-spacer), which fixes the Heart of X overlapping Background on mobile browsers whose toolbar changes height. The X uses `--logo-3d` (vector with extruded depth); `--logo-glow` stays behind it for the glow |
| `fit()` | Measures card titles and descriptions and sets card heights so nothing is clipped |
| `rail()` | Scroll rail |
| `pit()` | Canvas physics: gravity, collisions, pointer push, hover hit-testing, category-name to logo flip, call-out balloon |
| `contact()` | Two-line typing headline, crystal particle field behind the panel, and the Base64-decoded reveals (mailto link, wa.me link, two-line address). The "Line open" status is removed |

**Editing testimonials:** change the `TT` array (`[category, speaker, [quotes]]`) in the script. Category names, candy colours and label colours are in `CATS`.

## 4. Change log

| Version | Changes |
|---|---|
| 1.0 | Original single-file site: intro, hero, Services slider, FAQ dialogs, The Heart of X, Background, Contact. Logo replaced with a sharp vector white X traced from the hi-res file. |
| 1.1 | "X" removed before "Communications". Liquid-glass nav buttons. Scroll rail on the right. Testimonials section added (canvas physics, 30 remarks, 7 categories). Contact buttons hidden until clicked. "20+" shows a real plus. Heart of X: circle, side lines and fine lines removed, crystal particles added. |
| 1.2 | Fredoka for the hero and sub-headings. Character scrambling replaced by a slide-up reveal. Search removed. Page gets a right margin so content never overlaps the rail. Testimonials in black / blue / white. Get in touch becomes a glass panel; "Line open" removed. |
| 1.3 | Larger hero. Hero line on one line at under half size. Sub-sub-headings in the sub-heading typeface. FAQ questions at description size. Contact heading smaller, with crystal particles behind it. |
| 1.4 | Hero line centred and hero particles turned into crystals. "Executive Communications & Media Training". Drag-to-rotate removed from The Heart of X. The X now has real thickness. "20+" counts up from 10. Logo balls show the category name, flipping to the logo on hover. Pizza Hut messaging remark shortened. Contact: two-line headline, no "Reach us" panel, nav-sized buttons, mailto, WhatsApp and two-line address reveals. |
| 1.5 | One size per type tier. Shared left edge for titles and descriptions. Space around text and card heights fitted to content. Right-hand space fixed in The Heart of X. Logo glow starts at "Partnership". Heart of X made CSS-sticky to stop the mobile overlap with Background. Nav slides down after 1.8 s of no scrolling and hides while scrolling. WhatsApp opens WhatsApp Web once a numeric phone number is stored. |
| 1.6 | Launch build: hero line centred under the headline; "Hover a glassball"; "Jetstar Group executive"; WhatsApp number set; title, description, canonical, Open Graph and Twitter tags finalised; supplied ProfessionalService schema added with generated OfferCatalog and FAQPage schema; every card title and FAQ question is now a real `<h3>`; stray draft comments removed; robots.txt, sitemap.xml, logo and social preview image added. |
| 1.7 | WhatsApp link switched to the official wa.me click-to-chat format; final clean-up audit repeated and comments tidied. |
| 1.8 | Google Analytics (gtag.js, G-8R0VXDH2DZ) inserted in the head after the viewport tag; clean-up audit repeated. |

## 5. Open items before launch

- The site URL is set to `https://hiii-x.github.io/communications/` in `index.html`, `robots.txt` and `sitemap.xml`. If you later move to a custom domain, replace it in all three files and add a `CNAME` file.
- The Jardine crisis quote ("navigate complex communicate with challenges") is kept word for word; confirm the intended wording.
- Fredoka is the closest match to the supplied "friendly" sample; swap it if the exact font is known.
- Bubble sizes and colours approximate the Bubblepit reference.
- Test on real phones and desktops, especially The Heart of X scroll and the Services cards.

## 6. Launch settings and deployment

### 6.1 Metadata (in `<head>`)

| Item | Value |
|---|---|
| Title | X Communications \| Strategic Brand & Digital Advisory |
| Description | Premier strategic brand and digital advisory in Hong Kong. Expert PR consultancy, communications advisory, and digital transformation for brands across Asia-Pacific. |
| Canonical / `og:url` | `https://hiii-x.github.io/communications/`  |
| `og:image` / `twitter:image` | `https://hiii-x.github.io/communications/assets/og-preview.jpg` (1200 × 630) |
| Other | `og:type`, `og:title`, `og:description`, `og:site_name`, `og:locale` (en_HK), `twitter:card` = summary_large_image, `robots` = index,follow,max-image-preview:large, `theme-color` #000000, `color-scheme` dark |
| Viewport | `width=device-width, initial-scale=1, viewport-fit=cover` |
| Fonts | Google Fonts: Unbounded 300/500/700, Instrument Sans 400/500/600, Fredoka 400/500/600 |
| Analytics | Google tag (gtag.js), measurement ID `G-8R0VXDH2DZ`, placed in `<head>` straight after the viewport tag (line 5 onwards) so it loads early. The `async` script loads without blocking the page. |
| Fallback | `<noscript>` hides the intro overlay and shows the hero lines when JavaScript is off |

### 6.2 Structured data

- **Block 1 (supplied):** `ProfessionalService` for X Communications with Hong Kong, Asia and Asia-Pacific `areaServed`, PR agency and communications consultancy keywords in `alternateName` and `serviceType`, and `priceRange` "$$$$".
- **Block 2 (generated from the visible copy):** an `OfferCatalog` of the six services and a `FAQPage` of the five questions. Names, descriptions, questions and answers were extracted from the page text, so the schema and the visible FAQ match word for word. If you edit FAQ or service text, update this block too.

### 6.3 Heading structure

One `<h1>` (the three-line hero headline). Each main section is an `<h2>` (Services, Frequently asked questions, The Heart of X, Background, Testimonials, Get in touch). Sub-items are `<h3>`: the six service cards, the five FAQ questions, Connect / Partnership / Breakthroughs, the three Background cards and "Ready to communicate with impact." Buttons sit inside their `<h3>`, the standard accordion pattern. No levels are skipped.

### 6.4 Tunable settings (all inside `index.html`)

| Setting | Where | Value |
|---|---|---|
| Right margin for the scroll rail | `--rail` | 58px desktop, 34px under 820px |
| Mobile breakpoint | CSS media queries and `fit()` | 820px |
| Nav reappears after no scrolling | `navT` timeout | 1800 ms |
| Nav always visible | scroll position | under 80px, or while the menu is open |
| Heart of X scroll length | `.heart` height | 420svh, with `end: 'bottom bottom'` |
| Heart of X timeline | `heartScroll()` | links 0 to .8; bars join .12 to .87; X and glow from 1.0 / 1.1; Breakthroughs burst at 2.0 |
| "20+" counter | background stat | steps every 85 ms from 10 to 20, then the plus |
| Heading reveal | `rise()` | IntersectionObserver at 50% visible; 1 s slide up |
| Bubble pit | `pit()` | gravity .5, bounce .52 (floor) / .45 (collisions), pointer push radius r + 70, spawn gap 85 ms, 30 logo balls + 16 faces, radius scale min(1, width / 1000) with a floor of .55 |
| Logo ball spin | `pit()` | angular speed capped at .035, logo balls damped to .94 |
| Type tiers | `--t-body`, `--t-h3`, `--t-sm` | see section 2 |
| Contact details | `D` object | Base64-encoded email address, wa.me WhatsApp link and two-line postal address |

### 6.5 Files to deploy (GitHub root)

```
index.html
robots.txt
sitemap.xml
assets/logo.png          (512 x 512, referenced by the schema)
assets/og-preview.jpg    (1200 x 630, social preview)
```

Optional: `CNAME` (one line with your custom domain) for GitHub Pages, and an empty `.nojekyll` file.

### 6.6 Pre-launch checklist

- Replace every `https://hiii-x.github.io/communications/` with the real domain in `index.html`, `robots.txt` and `sitemap.xml`.
- Update `<lastmod>` in `sitemap.xml` when content changes.
- Test social previews with the LinkedIn Post Inspector and the Facebook Sharing Debugger after deployment.
- Test on a real phone and a desktop: hero, Heart of X scroll, Services cards, testimonial bubbles and the three contact buttons.

### 6.7 Release notes: 1.7

- WhatsApp: replaced the unofficial `web.whatsapp.com/send` form (which did not open reliably) with the documented `https://wa.me/<number>` click-to-chat link.
- Re-ran the clean-up audit: the file starts with `<!DOCTYPE html>` and ends with `</html>`, with no text outside them, no markdown code markers, no tabs, no draft or conversational text, and descriptive comments only. Both JSON-LD blocks parse and both scripts pass a syntax check.

### 6.8 Release notes: 1.8

- Google Analytics added after line 5 of `index.html` (after `<meta charset>` and the viewport tag, before the title). The snippet is unchanged apart from indentation, with Google's standard comment above it.
- Audit repeated on the final file: starts with `<!DOCTYPE html>`, ends with `</html>`, nothing outside them; no markdown code markers, tabs, draft or conversational text; one `<h1>`; both JSON-LD blocks parse; all three inline scripts pass a syntax check.
- Privacy reminder: Google Analytics sets cookies and records visitor data. Depending on where visitors are (for example the EU or UK), a cookie notice or consent step may be required. Check the legal position for your audience, and consider adding a privacy notice.
- To confirm tracking after deployment, open the live site, then check Google Analytics > Reports > Realtime for your visit (it can take a minute to appear).
