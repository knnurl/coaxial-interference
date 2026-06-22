# Coaxial Interference Studio

A single-file browser tool for designing **counter-rotating coaxial disc sculptures** with live moire preview and laser/waterjet-ready export.

**[Open the studio](https://kaanaksit.github.io/coaxial-interference-studio/index.html)**

Built for designing laser-cut acrylic discs that mount on a shared axis and spin in opposite directions. The overlapping patterns produce a travelling moire interference figure that changes continuously as the discs rotate.

![Coaxial Interference Studio](https://raw.githubusercontent.com/kaanaksit/coaxial-interference-studio/main/preview.png)

---

## Features

**Pattern engine**
- Five base generators: Superformula rings, Harmonic grating, Spiral, Maurer rose, Phyllotaxis field
- Per-disc tuning with 10+ parameters each
- Linked mode mirrors Disc A into Disc B with a detune offset for travelling moire
- Independent mode lets each disc carry a different pattern
- Mirror Disc B across horizontal, vertical, or point axis for a kaleidoscope effect on counter-rotation
- Wedge repeat: clip to a segment and stamp it around the disc (e.g. 90 deg x 4 pieces)

**Live animation**
- Adjustable RPM (-15 to +15, so each disc can spin either direction)
- Configurable speed ratio B/A; golden ratio drift mode for never-repeating phase
- Trail blur and motion controls

**Fabrication mode**
- Converts centrelines to closed contours of real physical width
- Slot or rib mode, with optional invert
- Kerf compensation for acrylic (laser) and aluminium (waterjet)
- Connector tabs: straight, tapered, rounded, or curved arc; hub-to-ring and ring-to-ring
- Structural rims: outer, inner, and mid-disc solid rings
- One-piece connectivity validation: flood-fills the rasterised plate from the hub outward and drops any island not attached, so the exported file is always one connected part
- Drop preview overlay: shows in red exactly what would be excluded on export

**Export**
- Per-disc SVG and DXF (AC1015, mm, LWPOLYLINE)
- Composite SVG with both discs at current rotation angles
- PNG snapshot
- JSON setup save/load

---

## Usage

No build step, no dependencies, no server.

```
open coaxial_interference.html
```

Or serve locally if your browser restricts local file access:

```bash
python3 -m http.server 8080
# then open http://localhost:8080/coaxial_interference.html
```

---

## Workflow

1. Pick a preset from the header to orient yourself.
2. Open **Form & motion** and set your disc diameter, hub, and bore size.
3. Open **Disc A** and choose a pattern. Tune the sliders; use locks to pin values while randomising.
4. Open **Disc B** and decide: linked (symmetric moire with detune) or independent. Turn on Mirror B for the kaleidoscope effect.
5. Open **Fabrication**. Switch to **Manufactured part** preview, set feature width and material.
6. Open **Tabs** and add connector tabs until the drop preview shows no red islands.
7. Export per-disc DXF for CAM, or SVG/PNG for proofing.

---

## File structure

```
coaxial_interference.html        single self-contained file, no external dependencies at runtime
.github/
  workflows/
    pages.yml                    deploys to GitHub Pages on every push to main
README.md
LICENSE
```

The HTML file is intentionally monolithic. All geometry, UI, rendering, and export live in one file so it can be dropped anywhere and opened directly.

---

## Fabrication notes

- Default kerf: 0.15 mm (acrylic, 60W CO2 laser). Adjust in the Fabrication panel.
- Minimum web for acrylic: 1.5 mm. Below this, narrow ribs snap during cutting or handling.
- The DXF uses AC1015 format with all geometry on layer `CUT`. Import directly into LightBurn, RDWorks, or any waterjet CAM.
- The centre bore is sized for a standard shaft. The hub solid radius sets how much material is always kept around the bore regardless of pattern.
- Tabs connect concentric rings into one cuttable piece. At least 4 tabs, 2.5 mm wide, with hub-to-ring and ring-to-ring both enabled is a reliable starting point for acrylic.

---

## License

MIT. See [LICENSE](LICENSE).
