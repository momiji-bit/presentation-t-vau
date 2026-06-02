# T-VAU Slidev Deck — Optimized Layout

This project is a cleaned Slidev version of the T-VAU presentation.

## Run

```bash
npm install -g @slidev/cli
cd tvau_slidev_optimized
slidev slides.md
```

## Export

```bash
slidev export slides.md --format pdf
```

## Layout notes

- Canvas: 1280 × 720, 16:9.
- Main slide content uses grid/flex layout instead of absolute positioning.
- Click animations were removed to avoid excessive click-through.
- Large figures were split into focus crops under `public/` for readability.
