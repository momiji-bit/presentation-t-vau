# T-VAU Slidev Draft

This folder contains a Slidev draft for **Text-guided Fine-Grained Video Anomaly Understanding (T-VAU)**.

## Structure

```text
slides.md
public/
  tvau_teaser.png
  tvau_framework.png
  tvau_dataset.png
  tvau_vis1.png
  tvau_vis2.png
```

The deck follows the style of the provided Slidev template: dark gradient background, white image cards, click-based reveal animations, and speaker notes in HTML comments.

## Run

```bash
npm install -g @slidev/cli
cd tvau_slidev_project
slidev slides.md
```

Export PDF if needed:

```bash
slidev export slides.md --format pdf
```

## Optional AI-generated motivation video

The Motivation slide references:

```text
public/ai_motivation_anomaly.mp4
```

Generate a 5--10 second 16:9 surveillance-style b-roll clip with Firefly, Runway, or another video generation model, then place it at that path. The slide uses `tvau_teaser.png` as a poster fallback when the MP4 is absent.

Recommended text-to-video prompt:

```text
A realistic high-angle CCTV-style shot of a clean university campus walkway in daytime, static camera, wide shot, several pedestrians walking normally. A single cyclist slowly enters the pedestrian-only walkway from the right side and moves diagonally toward the upper-left area. The scene is calm and non-graphic, subtle anomaly, surveillance video aesthetic, muted colors, 24 fps, 5 seconds, 16:9, no text, no logos, no close-up faces.
```

Negative prompt / avoid:

```text
no blood, no injury, no dramatic violence, no weapons, no crash, no police, no readable text, no watermark, no extreme close-up faces, no cinematic camera shake
```

Post-process for Slidev:

```bash
ffmpeg -i motivation_raw.mp4 -vf "scale=1280:-2,fps=24" -an -movflags +faststart public/ai_motivation_anomaly.mp4
```

Use generated video only as motivation or visual b-roll. Do not mix it with benchmark qualitative results unless clearly disclosed.
