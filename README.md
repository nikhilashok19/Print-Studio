# 🎞 Polaroid Batch Printer

A zero-dependency, browser-based tool that converts 100+ building/architecture photos into print-ready polaroid PDFs — black & white, 300 DPI, portrait A4, two landscape polaroids per page.

No installs. No server. No upload. Just open the HTML file and go.

---

## Preview

```
Portrait A4 page
┌─────────────────────────┐
│                         │
│  ┌───────────────────┐  │
│  │                   │  │
│  │  [landscape photo]│  │  ← 7" × 5" polaroid
│  │                   │  │
│  └───────────────────┘  │
│                         │
│  ┌───────────────────┐  │
│  │                   │  │
│  │  [landscape photo]│  │  ← 7" × 5" polaroid
│  │                   │  │
│  └───────────────────┘  │
│                         │
└─────────────────────────┘
```

---

## Features

- **Batch processing** — load 100+ photos at once via drag & drop or file picker
- **Landscape polaroid format** — each card is 7" wide × 5" tall, fitting landscape building shots perfectly
- **2 polaroids per A4 portrait page** — stacked vertically with balanced margins and drop shadows
- **300 DPI output** — A4 pages render internally at 2480 × 3508 px before PDF encoding
- **Black & white conversion** — luminance-weighted (0.299R + 0.587G + 0.114B), the standard photographic formula
- **Film grain** — optional subtle noise layer for an analogue feel
- **Smart cropping** — four aspect ratio options with top/center/bottom anchor control
- **Caption support** — add a project name or label to the bottom tab of every polaroid
- **Live page preview** — flip through all generated pages with a thumbnail strip before downloading
- **Configurable quality** — JPEG quality slider from 70% to 100%
- **Custom PDF filename**
- **Fully client-side** — nothing leaves your machine; no data is uploaded anywhere

---

## Getting Started

### Requirements

- A modern browser — **Chrome** or **Edge** recommended for best Canvas API performance
- An internet connection on first load (fetches Google Fonts for the UI — optional, tool works without them)
- No Node.js, Python, or any other runtime needed

### Usage

1. Download `polaroid_printer.html`
2. Double-click it to open in your browser
3. Drag & drop your photos (or click to browse)
4. Adjust settings as needed
5. Click **Generate PDF**
6. Preview the result, then click **Download**

---

## Settings Reference

### Crop & Aspect

| Option | Ratio | Best for |
|---|---|---|
| Standard landscape | 3:2 | Most building shots |
| Cinematic widescreen | 2.35:1 | Dramatic wide facades |
| Golden ratio | 1.618:1 | Balanced architectural composition |
| HD widescreen | 16:9 | Very wide panoramic shots |

**Crop anchor** — controls which part of the photo is kept when cropping:
- `Center` — keeps the middle of the frame (default)
- `Top` — preserves rooflines and upper details
- `Bottom` — preserves ground-level and foreground details

### Polaroid Style

| Setting | Default | Description |
|---|---|---|
| Caption text | *(empty)* | Label printed in the bottom white tab |
| Side border | 6 mm | White border on left, right, and top of photo |
| Bottom tab | 22 mm | Height of the white caption area below the photo |
| Black & white | On | Luminance-weighted greyscale conversion |
| Film grain | On | Subtle random noise for analogue texture |

### Output

| Setting | Default | Range |
|---|---|---|
| JPEG quality | 92% | 70–100% |
| PDF filename | `polaroids` | Any string |

**Quality guide:**
- `92%` — recommended default; sharp at print size, reasonable file size
- `98–100%` — use for professional print shop submission
- `75–80%` — use if emailing or sharing digitally and file size matters

---

## Technical Details

| Property | Value |
|---|---|
| Output DPI | 300 |
| A4 canvas size | 2480 × 3508 px |
| Polaroid card size | 2100 × 1500 px (7" × 5") |
| PDF format | A4 portrait, JPEG-compressed pages |
| B&W formula | `gray = 0.299R + 0.587G + 0.114B` |
| PDF library | [jsPDF 2.5.1](https://github.com/parallax/jsPDF) via CDN |
| Fonts | DM Sans + DM Mono via Google Fonts |

Processing is done entirely in the browser using the HTML5 Canvas API. Images are loaded one pair at a time to avoid memory issues with large batches, with a `setTimeout` yield between pairs to keep the UI responsive.

---

## File Structure

```
polaroid_printer.html    ← the entire tool, self-contained
README.md
```

---

## Limitations

- **Browser memory** — very large images (e.g. 50 MP RAW-converted TIFFs) may cause slowdowns. JPEGs exported from Lightroom or Photoshop at full resolution work fine.
- **Google Fonts** — the UI uses DM Sans / DM Mono loaded from Google Fonts. If you are offline, the browser falls back to system sans-serif fonts. The tool still works fully.
- **PDF file size** — 100 photos at 92% quality typically produces a 60–120 MB PDF depending on image complexity. Reduce quality to 80% if you need a smaller file.
- **Safari** — works, but Chrome/Edge have faster Canvas rendering for large batches.

---

## Customisation

All layout constants are defined at the top of the `<script>` block and are easy to change:

```js
const DPI      = 300;         // output resolution
const A4_W_MM  = 210;         // page width in mm
const A4_H_MM  = 297;         // page height in mm
const POL_W_MM = 7 * 25.4;    // polaroid width  (7 inches)
const POL_H_MM = 5 * 25.4;    // polaroid height (5 inches)
```

To change polaroid size, edit `POL_W_MM` and `POL_H_MM`. The layout engine will automatically recentre everything on the A4 page.

---

## License

MIT — free to use, modify, and distribute.

---

## Credits

Built with [jsPDF](https://github.com/parallax/jsPDF) for PDF generation and the browser's native Canvas 2D API for image processing.
