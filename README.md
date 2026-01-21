# OpenEXR Channel & Bit-Depth Inspector

A professional browser-based inspection tool for OpenEXR files. Analyze passes, channels, bit-depth, and metadata without external software — similar to After Effects EXtractoR.

**Built for [Blauw Films](https://www.blauwfilms.com)**

---

## Features

- **Layer/Pass Grouping** — Automatically groups channels (e.g., `diffuse.R`, `diffuse.G`, `diffuse.B`) into composite layers
- **RGB Composite Preview** — View passes with proper color, not individual R/G/B channels
- **Exposure Control** — Adjust exposure from -4 to +4 EV for HDR inspection
- **sRGB Gamma Toggle** — Switch between linear and sRGB display
- **Alpha Visualization** — Toggle alpha channel display
- **Per-Layer Statistics** — Min/max values, bit-depth, negative/invalid value detection
- **RGB Histograms** — Separate histograms for each color channel
- **Export Options** — Export layers as PNG (8-bit sRGB) or EXR (original bit-depth)
- **Drag & Drop** — Simple file upload interface
- **100% Client-Side** — No data uploaded to any server

---

## Supported Formats

| Compression | Status |
|-------------|--------|
| Uncompressed | ✅ Fully supported |
| RLE | ✅ Fully supported |
| ZIP | ✅ Fully supported |
| ZIPS | ✅ Fully supported |
| PIZ | ⚠️ Partial support |
| PXR24 | ❌ Not supported |
| B44 / B44A | ❌ Not supported |
| DWAA / DWAB | ❌ Not supported |

**Bit Depths:** 16-bit Half Float, 32-bit Float, 32-bit UINT

**Limitations:**
- Tiled EXR files not supported
- Deep data EXR files not supported
- Multi-part EXR: only first part processed
- Maximum file size: 500MB

---

## Installation

### Option 1: Webflow Integration

1. Upload `openexr-inspector-full.html` to this repository

2. Get the jsDelivr CDN URL:
   ```
   https://cdn.jsdelivr.net/gh/blauwfilms/openexr-channel-inspector@main/openexr-inspector-full.html
   ```

3. Edit `webflow-loader.html` and update the `GITHUB_URL` variable:
   ```javascript
   const GITHUB_URL = 'https://cdn.jsdelivr.net/gh/blauwfilms/openexr-channel-inspector@main/openexr-inspector-full.html';
   ```

4. Copy the contents of `webflow-loader.html` into a Webflow Embed/Code Block

### Option 2: Direct Hosting

Simply host `openexr-inspector-full.html` on any web server or open it directly in a browser.

### Option 3: GitHub Pages

1. Enable GitHub Pages in repository settings
2. Access at: `https://cdn.jsdelivr.net/gh/blauwfilms/openexr-channel-inspector@main/openexr-inspector-full.html`

---

## Usage

1. **Upload** — Drag & drop an EXR file or click to select
2. **Browse Layers** — Click any layer/pass in the grid to preview
3. **Adjust Display** — Use exposure and gamma controls for HDR content
4. **Inspect** — View statistics and histograms below the preview
5. **Export** — Download individual layers or all layers at once

---

## File Structure

```
├── openexr-inspector-full.html   # Main application (host on GitHub)
├── webflow-loader.html           # Loader code (paste into Webflow)
└── README.md                     # This file
```

---

## Technical Details

### EXR Parsing

The inspector implements a complete EXR parser in JavaScript:

- Magic number validation
- Header attribute parsing (channels, compression, data windows, etc.)
- Scanline offset table reading
- Decompression (RLE, ZIP/ZIPS with predictor reconstruction)
- 16-bit half-float to 32-bit float conversion using lookup tables
- Channel extraction and layer grouping

### Color Pipeline

1. Raw linear float data extracted from EXR
2. Exposure adjustment applied (2^EV multiplier)
3. Optional sRGB gamma curve (linear → sRGB transfer function)
4. 8-bit quantization for display

---

## Browser Compatibility

- Chrome 89+ (recommended)
- Firefox 102+
- Safari 15.4+
- Edge 89+

Requires `DecompressionStream` API for ZIP compression support.

---

## License

MIT License — Free for commercial and personal use.

---

## Credits

Developed for [Blauw Films](https://www.blauwfilms.com)

For issues or feature requests, please open a GitHub issue.