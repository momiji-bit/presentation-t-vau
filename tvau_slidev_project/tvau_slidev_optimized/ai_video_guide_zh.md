# AI-generated motivation video guide

建议只把生成视频作为 motivation b-roll；不要用于实验结果、定量比较或 qualitative benchmark。生成后的 mp4 放在：

```text
public/ai_motivation_anomaly.mp4
```

推荐 prompt：

```text
A realistic high-angle CCTV-style shot of a clean university campus walkway in daytime, static camera, wide shot, several pedestrians walking normally. A single cyclist slowly enters the pedestrian-only walkway from the right side and moves diagonally toward the upper-left area. The scene is calm and non-graphic, subtle anomaly, surveillance video aesthetic, muted colors, 24 fps, 5 seconds, 16:9, no text, no logos, no close-up faces.
```

Negative prompt：

```text
no injury, no dramatic violence, no weapons, no crash, no police, no readable text, no watermark, no extreme close-up faces, no cinematic camera shake
```

压缩命令：

```bash
ffmpeg -i motivation_raw.mp4 -vf "scale=1280:-2,fps=24" -an -movflags +faststart public/ai_motivation_anomaly.mp4
```
