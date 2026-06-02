# T-VAU AI-generated 视频生成说明

## 目标

仿照模板里的 Adobe Firefly 视频 slide，生成一个 5--10 秒的 AI-generated motivation b-roll。它只用于开场动机，不用于实验结果、benchmark 可视化或训练数据展示。

## 推荐场景

优先生成非血腥、非激烈冲突、监控视角的轻量异常：

1. 校园步道中一辆自行车进入行人区域。
2. 广场中一辆车从画面边缘突然进入。
3. 多个行人正常行走，其中一个人突然加速跑动。

## 推荐流程

1. 在 Firefly / Runway 中选择 Text-to-video 或 Image-to-video。
2. 设置 16:9，5 秒或 10 秒，静态高角度监控视角。
3. 生成 4--8 个 variant，选择目标稳定、没有多余文字和水印、没有明显形变的一版。
4. 导出 MP4，尽量选择 720p 或 1080p。
5. 用 ffmpeg 压缩并放入 Slidev public 文件夹：

```bash
ffmpeg -i motivation_raw.mp4 -vf "scale=1280:-2,fps=24" -an -movflags +faststart public/ai_motivation_anomaly.mp4
```

## Prompt

```text
A realistic high-angle CCTV-style shot of a clean university campus walkway in daytime, static camera, wide shot, several pedestrians walking normally. A single cyclist slowly enters the pedestrian-only walkway from the right side and moves diagonally toward the upper-left area. The scene is calm and non-graphic, subtle anomaly, surveillance video aesthetic, muted colors, 24 fps, 5 seconds, 16:9, no text, no logos, no close-up faces.
```

## Negative prompt

```text
no blood, no injury, no dramatic violence, no weapons, no crash, no police, no readable text, no watermark, no extreme close-up faces, no cinematic camera shake
```

## Slide 中的标注

在视频右上角保留标注：

```text
Optional: AI-generated content for motivation only
```

或改成：

```text
Visual created using Adobe Firefly / Runway (AI-generated content)
```
