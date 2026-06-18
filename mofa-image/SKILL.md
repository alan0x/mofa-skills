---
name: mofa-image
version: 0.1.0
description: "Single free-form illustration generation. Triggers: illustration, picture of, draw a, 插图, 配图, 画一张, realistic image, diagram image, mofa image. Generates one clean borderless PNG from a prompt via Gemini, with optional reference images."
requires_bins: mofa
requires_env: GEMINI_API_KEY
---

# mofa-image

CLI plugin: `mofa_image` — generate a single free-form illustration as a PNG via Gemini (`gemini-3.1-flash-image-preview`).

Unlike `mofa_cards` (greeting-card chrome) or `mofa_infographic` (multi-section poster), this produces **one clean borderless image** from a prompt — the primitive for "show a picture of X", or for an illustration to embed inside other content (e.g. rich-output HTML).

## Output paths (LOAD-BEARING)

Use a RELATIVE `out` path. Never prefix `skill-output/` yourself — the Octos host rebinds plugin output paths to `<workspace>/skill-output/` automatically; a manual prefix double-prefixes and breaks delivery. Never use absolute paths like `/tmp/x.png`.

```
mofa-image-<YYYYMMDD-HHMMSS>/illustration.png
```

## Input

```json
{
  "prompt": "A clean labeled educational illustration of a human animal cell, textbook diagram style, white background",
  "out": "mofa-image-20260618-101500/illustration.png",
  "aspect": "4:3",
  "image_size": "1K"
}
```

| field | required | notes |
|-------|----------|-------|
| `prompt` | yes | what to draw |
| `out` | yes | relative PNG path (see above) |
| `ref_images` | no | array of image paths to ground the result on a reference |
| `aspect` | no | e.g. `16:9`, `1:1`, `4:3` |
| `image_size` | no | `1K`, `2K`, `4K` |
| `gen_model` | no | override the image model |

## Requirements

- `GEMINI_API_KEY` (or the host's configured Gemini credentials).
- Shared `mofa` binary (same one used by mofa-cards / mofa-infographic).

## Output

`{ "output": "Generated illustration: <path>", "success": true, "files_to_send": ["<abs path>"] }`
