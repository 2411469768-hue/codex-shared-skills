---
name: product-page-remake
description: Analyze competitor product detail pages and turn them into original, conversion-focused product pages. Use when the user asks to remake, reverse-engineer, clone the structure of, improve, rewrite, or create a 商品详情页/product page from a competitor URL, screenshot, HTML export, marketplace listing, Shopify product page, Taobao/Tmall/JD/Douyin/TikTok Shop page, or reference page while avoiding direct copying of protected images, wording, brand assets, or code.
---

# Product Page Remake

Use this skill to deconstruct a reference product detail page and create an original page for the user's product. Preserve useful conversion logic, not protected expression.

## Core Rules

- Do not copy competitor copy, images, branding, layout code, reviews, testimonials, claims, or exact visual composition.
- Extract reusable strategy: page order, objection handling, proof types, comparison angles, benefit hierarchy, and conversion triggers.
- Rewrite from the user's product facts. If facts are missing, mark assumptions and ask for the smallest missing input needed.
- Keep claims supportable. Flag medical, safety, performance, legal, or platform-sensitive claims that need proof.
- When a page cannot be accessed, ask for screenshots, saved HTML, copied text, or a product URL that can be opened.

## Workflow

1. **Collect inputs**
   - Reference source: URL, screenshots, HTML, or pasted content.
   - User product: title, price, specs, audience, photos, platform, brand tone, constraints.
   - Output format: outline, rewritten copy, wireframe, HTML/CSS, Shopify section, image-generation shot list, or spreadsheet.

2. **Capture the reference**
   - If browsing or Chrome is available, inspect the page and take screenshots at desktop and mobile widths when visual fidelity matters.
   - If only screenshots are provided, analyze each visible section and note missing scroll depth.
   - Separate page structure from asset ownership.

3. **Deconstruct conversion logic**
   - Identify first-screen promise, target customer, product category cues, visual proof, benefit sequence, trust signals, objections, price framing, guarantees, FAQ, and CTA placement.
   - Note what is worth adapting and what should be avoided.

4. **Map to the user's product**
   - Convert competitor angles into original angles supported by the user's product facts.
   - Reorder sections for the user's strongest buying argument.
   - Replace competitor proof with user-owned proof placeholders when assets are unavailable.

5. **Produce the requested artifact**
   - For strategy: output a section-by-section teardown plus recommendations.
   - For copy: output original page copy with section labels and asset notes.
   - For build: output implementation files that use original content and user-owned or placeholder assets.
   - For design/image planning: output visual direction, shot list, and prompts without asking to recreate competitor assets exactly.

6. **Validate**
   - Check that every borrowed idea has been transformed into an original expression.
   - Check mobile-first readability, CTA repetition, claim support, and missing assets.
   - For coded pages, run or render locally and inspect screenshots before final delivery when feasible.

## Output Pattern

Prefer this structure unless the user asks for a specific artifact:

```markdown
## Reference Teardown
- Page sequence:
- Strongest conversion mechanisms:
- Weaknesses or risks:

## Original Page Plan
- Audience:
- Core promise:
- Section order:
- Asset requirements:

## Draft Page Copy
[Section-by-section original copy]

## Build Notes
- Layout:
- Mobile behavior:
- Claims/proof needed:
```

## Detailed Checklist

For deeper audits, compliance checks, or coded-page handoff, read `references/checklist.md`.
