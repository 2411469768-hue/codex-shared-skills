---
name: douyin-title-optimizer
description: Optimize Douyin/TikTok Shop product titles for Chinese e-commerce listings, especially apparel titles from Douyin share links, copied product titles, product detail pages, screenshots, or user-provided product facts. Use when the user asks to optimize, rewrite, score, test, or generate product titles for search traffic, click-through rate, Qianchuan/Douyin ads, style positioning, material accuracy, or conversion.
---

# Douyin Title Optimizer

Use this skill to turn a Douyin product link or rough product title into practical title variants for search, clicks, and conversion. The goal is not clever wording; it is a title that matches what buyers search, what the product actually is, and what the page can prove.

## Workflow

1. **Collect product facts**
   - If the user provides a Douyin short link, try to resolve it and extract visible fields such as title, price, sales, main image, and `goods_detail`.
   - If the link cannot be accessed, work from the pasted title and ask for only the smallest missing input if needed.
   - Use user-provided facts as authoritative when they clarify the product.

2. **Separate title terms by role**
   - Category terms: the product noun buyers search, such as `针织衫`, `短袖`, `T恤`, `连衣裙`.
   - Audience terms: `女`, age/style group, body concern, use scene.
   - Season terms: `夏季`, `春夏`, `薄款`, `防晒`, `通勤`.
   - Material or touch terms: cotton, Lyocell, polyester, ice-silk feel, chiffon, knit, etc.
   - Fit and benefit terms: `正肩`, `显瘦`, `遮肉`, `不透`, `透气`.
   - Style terms: `法式`, `老钱风`, `复古`, `通勤`, `小香风`.

3. **Respect material accuracy**
   - Do not invent material words.
   - Do not hardcode any material across products. Material is a per-product variable from the link, listing specs, image text, or user clarification.
   - If a popular search term describes a feel rather than the actual fiber, make it softer, for example `冰丝感`, `凉感`, or keep it as a secondary term only when the page can support it.
   - If the user says not to include a material term, exclude it from the final title variants.

4. **Build the recommended title**
   - Put high-intent search terms first: material or touch, category, audience, season.
   - Put fit and benefit terms in the middle.
   - Put style terms near the end unless style is the main purchase driver.
   - Avoid duplicate meanings and vague filler such as `新款`, `高级感`, or excessive trend words unless the user explicitly wants them.
   - Keep titles readable; do not produce keyword soup.

5. **Generate variants by goal**
   - Search traffic version: strongest searchable nouns and attributes.
   - Click-through version: more direct benefit or summer pain point.
   - Style positioning version: emphasizes aesthetic identity.
   - Pain-point version: focuses on slimming, cooling, non-see-through, coverage, or comfort.
   - Qianchuan/ad version: shorter, punchier, and easier to read in feed context.

6. **Explain the choice**
   - Pick one best title to use first.
   - Briefly explain which words were kept, removed, upgraded, or demoted.
   - Mention any claim or material term that needs page support.

## Output Format

Use this format unless the user asks for a different one:

```markdown
最推荐：
`...`

为什么这样改：
- ...

可测试版本：
1. 搜索流量版：`...`
2. 点击率版：`...`
3. 风格人群版：`...`
4. 痛点卖点版：`...`
5. 千川投放版：`...`

注意：
- ...
```

## Quality Rules

- Prefer concrete buyer language over decorative brand language.
- Never copy a competitor title wholesale.
- Do not overpromise unsupported claims.
- If title and product facts conflict, flag the conflict instead of hiding it.
- For apparel, prioritize: category clarity, season fit, material/touch accuracy, fit benefit, style positioning.
