# RCF - Front-end / Media

> Images, video, 3D / animation, and the GenAI prompts used to produce them. Consult this file before generating new visual assets or wiring up media playback.

See [`SYSTEM_PROMPT.md`](../../SYSTEM_PROMPT.md) for how the agent picks an entry from this file.

---

## Context Relevancy: Hero image - GenAI prompt for product launch

**Project fit:** Marketing site launching a SaaS product. Needs a hero visual consistent with brand palette, no text in image, exportable at 2x for retina.

**Value:**

> _(Add your tested image-model prompt here - e.g. the Midjourney / Imagen / Flux prompt string with style tokens, aspect ratio, and seed if reproducibility matters. Also paste the negative prompt and final post-processing notes.)_

---

## Context Relevancy: Product walkthrough video - autoplay, muted, looped, lazy-loaded

**Project fit:** Above-the-fold product demo on a landing page. Must autoplay on desktop, fall back to a poster on mobile data savers, never block LCP.

**Value:**

> _(Add your tested `<video>` / `next/video` wrapper here, including the lazy-load intersection observer, mobile fallback logic, and the encoding settings you use for the source files.)_
