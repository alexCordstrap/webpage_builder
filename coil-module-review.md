# Coil Module Alignment Review

## Existing Overlaps With Core Stylesheet
- **Restrainer spacing.** The core stylesheet already sets `.restrainer` containers to center content at a max width, so the inline `max-width:1280px` and `margin:0 auto` on the hero and body sections can be removed once we rely on the base class and only keep any truly unique spacing rules.【F:webpage.css†L1-L1】【F:metal-coil-module.html†L102-L147】
- **Form controls.** Global rules style `label`, `input`, and `textarea` elements (block labels, full-width inputs, radius, focus states). The Mailchimp form redefines the same properties inline—border, padding, width—that can be dropped in favour of the site defaults for consistency and easier theme updates.【F:webpage.css†L1-L1】【F:metal-coil-module.html†L175-L214】
- **Buttons.** Primary buttons already exist as `.btn.btn-primary` with the correct brand colour; the module duplicates the styling with bespoke `.cta` rules and inline submit button styles. Switching to the shared button classes will sync hover/focus behaviour and colours automatically.【F:webpage.css†L1-L1】【F:metal-coil-module.html†L45-L129】【F:metal-coil-module.html†L211-L214】

## Recommendations for a Unified Experience
1. **Migrate reusable CSS into the global bundle.** Move layout helpers such as `.category-hero`, `.jumpbar`, `.product-grid`, `.card`, and `.divider` into `webpage.css` so that both the full page and module draw from the same declarations instead of duplicating inline `<style>` blocks.【F:metal-coil-module.html†L18-L100】【F:metal-coil-module.html†L244-L275】
2. **Swap inline styles for semantic utility classes.** Introduce shared spacing/typography utility classes (e.g., `.mt-16`, `.text-muted`) in the core stylesheet and replace inline `style` attributes on paragraphs, lists, and FAQ counters to tighten maintenance and respect global tokens.【F:metal-coil-module.html†L116-L314】
3. **Adopt shared button and form patterns.** Replace `.cta` with `.btn btn-primary` and convert the Mailchimp submit input into `<button type="submit" class="btn btn-primary btn--full">` (adding a `.btn--full` helper if needed) to keep accessibility, spacing, and transitions aligned with the main site.【F:webpage.css†L1-L1】【F:metal-coil-module.html†L121-L214】
4. **Leverage existing grid/flex helpers.** Where possible, reuse `.grid-container`, `.module`, or flex utilities from the global CSS for hero and product layouts rather than bespoke CSS Grid declarations, ensuring responsive breakpoints match the rest of the site.【F:webpage.css†L1-L1】【F:metal-coil-module.html†L18-L104】【F:metal-coil-module.html†L244-L275】

## Roadmap to a Best-in-Class Module (UX, UI, SEO/AI)
- **Visual design & UX**
  - Establish a single headline hierarchy (introduce an on-page `<h1>` and cascade `h2/h3`) and use shared typography classes for consistent sizing and line height.【F:metal-coil-module.html†L151-L296】
  - Add global spacing tokens for sections (`padding-block`, `gap`) to reduce reliance on ad-hoc pixel values and improve rhythm across devices.【F:metal-coil-module.html†L120-L314】
  - Provide reusable component classes for FAQ accordions or cards so micro-interactions (hover, focus, animation) match broader site patterns.【F:metal-coil-module.html†L293-L315】
- **Accessibility & performance**
  - Replace duplicated `style` rules with classes so critical CSS can be loaded once; ensure `loading="lazy"` is applied to below-the-fold imagery and audit contrast for compliance when brand tokens are used automatically.【F:metal-coil-module.html†L133-L142】【F:metal-coil-module.html†L244-L315】
  - Standardise form validation messaging via shared JS utilities; surface inline errors with aria-live regions sourced from a central helper to avoid repeated scripts.【F:metal-coil-module.html†L320-L397】
- **SEO & AI readiness**
  - Declare structured data (FAQPage, Product) via JSON-LD derived from existing FAQ/product content to boost SERP features and AI snippet comprehension.【F:metal-coil-module.html†L244-L315】
  - Ensure metadata (title, description, canonical) and Open Graph tags remain in the CMS template rather than module markup, limiting duplication and ensuring site-wide consistency.【F:full-coil-page.html†L1-L120】
  - Consolidate anchor text styles using global classes so internal linking signals remain consistent for crawlers and knowledge graphs.【F:metal-coil-module.html†L120-L315】

Implementing the cleanup above will let the module inherit brand styling automatically, minimise duplicate CSS, and create a smoother path to future enhancements without fragmenting the design system.
