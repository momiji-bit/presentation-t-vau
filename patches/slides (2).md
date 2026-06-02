---
theme: default
title: Text-guided Fine-Grained Video Anomaly Understanding
transition: fade
background: linear-gradient(135deg, #0f172a, #172554, #1e1b4b)
class: text-white
colorSchema: dark
canvasWidth: 1280
fonts:
  sans: Inter
  serif: Georgia
  mono: Fira Code
---

<style>
:root { --bg0:#0f172a; --bg1:#172554; --bg2:#1e1b4b; --pink:#f9a8d4; --green:#86efac; --blue:#93c5fd; --orange:#fdba74; --text:#f8fafc; --muted:#cbd5e1; --dim:#94a3b8; }
.slidev-layout { min-height:100%; width:100%; padding:34px 48px; background:linear-gradient(135deg,var(--bg0) 0%,var(--bg1) 48%,var(--bg2) 100%); color:var(--text); }
.slidev-layout h1,.title-main { font-size:46px; line-height:1.04; font-weight:780; letter-spacing:-.04em; margin:0; color:var(--text); }
.section-title { font-size:58px; line-height:1.02; font-weight:780; letter-spacing:-.045em; }
.kicker { color:var(--pink); font-weight:720; letter-spacing:.03em; text-transform:uppercase; font-size:14px; }
.subtitle { font-size:25px; color:var(--muted); margin-top:18px; font-style:italic; }
.body { font-size:20px; line-height:1.45; color:#e2e8f0; }
.small { font-size:13px; color:var(--dim); }
.card { background:rgba(255,255,255,.10); border:1px solid rgba(255,255,255,.12); border-radius:18px; padding:20px; box-shadow:0 14px 38px rgba(0,0,0,.22); }
.card-tight { background:rgba(255,255,255,.10); border:1px solid rgba(255,255,255,.12); border-radius:14px; padding:14px 16px; }
.figure { background:#fff; border-radius:16px; padding:8px; box-shadow:0 18px 46px rgba(0,0,0,.32); }
.figure img { width:100%; height:auto; border-radius:10px; display:block; }
.table-wrap { background:rgba(255,255,255,.08); border:1px solid rgba(255,255,255,.12); border-radius:14px; overflow:hidden; }
table.clean { width:100%; border-collapse:collapse; font-size:14px; }
table.clean th { background:rgba(255,255,255,.16); color:#f8fafc; font-weight:700; padding:9px 8px; text-align:center; }
table.clean td { padding:9px 8px; border-top:1px solid rgba(255,255,255,.10); color:#e2e8f0; text-align:center; }
table.clean td:first-child, table.clean th:first-child { text-align:left; }
table.clean tr.hl td { background:rgba(236,72,153,.18); color:#fff; font-weight:700; }
.metric { background:rgba(255,255,255,.10); border:1px solid rgba(255,255,255,.12); border-radius:18px; padding:17px; text-align:center; }
.metric .num { font-size:38px; line-height:1; font-weight:780; color:var(--green); }
.metric .label { margin-top:8px; color:#dbeafe; font-size:15px; }
.callout { border-left:5px solid #ec4899; background:rgba(236,72,153,.14); border-radius:14px; padding:16px 18px; }
.slide-no { position:absolute; right:24px; bottom:16px; font-size:13px; color:var(--dim); }
.loc-box { position:absolute; border:3px solid; border-radius:8px; background:transparent; pointer-events:none; z-index:20; }
.loc-pink { border-color:#f9a8d4; box-shadow:0 0 16px rgba(249,168,212,.55); }
.loc-green { border-color:#86efac; box-shadow:0 0 16px rgba(134,239,172,.55); }
</style>

<div class="absolute inset-0 opacity-15">
  <img src="/figs/teaser.png" class="w-full h-full object-cover" />
</div>
<div class="relative z-10 h-full flex flex-col justify-center">
  <div class="kicker">CVPR 2026 SVC Workshop</div>
  <div class="text-[58px] leading-[1.02] font-[780] tracking-[-0.045em] max-w-[1060px] mt-4">
    Text-guided Fine-Grained Video Anomaly Understanding
  </div>
  <div class="subtitle">Pixel Evidence to Language Reasoning</div>
  <div class="mt-9 body"><b>Jihao (Geo) Gu</b>, Kun Li, He Wang, Kaan Akşit</div>
  <div class="mt-2 small">University College London · CVLab, United Arab Emirates University</div>
  <div class="mt-8 flex gap-3 flex-wrap">
    <span class="card-tight">Video Anomaly Understanding</span>
    <span class="card-tight">Pixel-level Evidence</span>
    <span class="card-tight">LVLM Reasoning</span>
  </div>
</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="h-full flex flex-col justify-center">
  <div class="section-title">Talk roadmap</div>
  <div class="grid grid-cols-4 gap-5 mt-12">
    <div class="card"><div class="text-2xl font-semibold text-pink-300">1. Motivation</div><div class="body mt-4">Why anomaly understanding needs pixel evidence, not only labels or captions.</div></div>
    <div class="card"><div class="text-2xl font-semibold text-blue-300">2. Method</div><div class="body mt-4">AHD grounds anomaly evidence; RAE injects it into LVLM reasoning.</div></div>
    <div class="card"><div class="text-2xl font-semibold text-orange-300">3. Dataset</div><div class="body mt-4">Target-level appearance, localization, and trajectory supervision.</div></div>
    <div class="card"><div class="text-2xl font-semibold text-green-300">4. Results</div><div class="body mt-4">Localization, dialogue, ablations, and qualitative consistency.</div></div>
  </div>
</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="h-full flex items-center">
  <div>
    <div class="section-title">Motivation</div>
    <div class="subtitle">Fine-grained anomaly understanding should answer what, where, when, and why.</div>
  </div>
</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="title-main">Existing paradigms are fragmented</div>
<div class="grid grid-cols-2 gap-6 mt-8">
  <div v-click="1" class="card">
    <div class="text-2xl font-semibold text-orange-300">Traditional IAD / VAD</div>
    <div class="body mt-4">Produces anomaly scores or heatmaps, but usually lacks semantic explanation.</div>
    <div class="mt-5 card-tight text-gray-300">Output: score / heatmap</div>
  </div>
  <div v-click="2" class="card">
    <div class="text-2xl font-semibold text-green-300">General LVLMs</div>
    <div class="body mt-4">Can answer in language, but often fails to ground subtle cues at the pixel level.</div>
    <div class="mt-5 card-tight text-gray-300">Output: text judgment</div>
  </div>
  <div v-click="3" class="card">
    <div class="text-2xl font-semibold text-blue-300">LVLM + diffusion hybrids</div>
    <div class="body mt-4">Combine visualization and text, but generated explanations may be unstable or inconsistent.</div>
    <div class="mt-5 card-tight text-gray-300">Output: judgment + generated heatmap</div>
  </div>
  <div v-click="4" class="card bg-pink-500/20 border-pink-300/30">
    <div class="text-2xl font-semibold text-pink-300">T-VAU</div>
    <div class="body mt-4">Couples pixel-level anomaly evidence with language reasoning.</div>
    <div class="mt-5 card-tight text-gray-100">Output: detection + localization + identification + trajectory + explanation</div>
  </div>
</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="title-main">The gap: anomaly understanding requires evidence</div>
<div class="grid grid-cols-2 gap-9 mt-8 items-center">
  <div>
    <div class="text-3xl font-semibold leading-snug">
      An anomaly should be <span class="text-pink-300">detected</span>, <span class="text-blue-300">localized</span>, and <span class="text-green-300">explained</span>.
    </div>
    <div class="mt-8 body">Fine-grained anomaly understanding asks the model to answer:</div>
    <div class="mt-6 space-y-3 text-lg">
      <div v-click="1" class="card-tight">Is there any anomaly?</div>
      <div v-click="2" class="card-tight">Where is the abnormal evidence?</div>
      <div v-click="3" class="card-tight">Which target is responsible?</div>
      <div v-click="4" class="card-tight">How does the target evolve over time?</div>
    </div>
  </div>
  <div class="figure"><img src="/figs/teaser.png" /></div>
</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="title-main">Main contributions</div>
<div class="grid grid-cols-3 gap-6 mt-12">
  <div v-click="1" class="card min-h-[280px]"><div class="text-2xl font-semibold text-green-300">AHD</div><div class="body mt-5">Text-aligned Anomaly Heatmap Decoder for threshold-free, pixel-level spatio-temporal anomaly localization.</div></div>
  <div v-click="2" class="card min-h-[280px]"><div class="text-2xl font-semibold text-orange-300">RAE</div><div class="body mt-5">Region-aware Anomaly Encoder that turns heatmaps into motion- and region-aware prompts for LVLM reasoning.</div></div>
  <div v-click="3" class="card min-h-[280px]"><div class="text-2xl font-semibold text-pink-300">Dataset + evaluation</div><div class="body mt-5">Target-level video–text anomaly supervision on ShanghaiTech and UBnormal, covering appearance, localization, and trajectories.</div></div>
</div>
<div v-click="4" class="absolute bottom-20 left-20 right-20 text-center text-2xl italic text-gray-200">The core loop: pixel evidence → structured prompts → language reasoning.</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="h-full flex items-center">
  <div>
    <div class="section-title">Proposed Method</div>
    <div class="subtitle">AHD localizes subtle evidence; RAE makes that evidence usable by the LVLM.</div>
  </div>
</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="title-main">T-VAU: closed-loop anomaly understanding</div>
<div class="mt-4 body">Given a video clip, dialogue history, and normal/abnormal prompts, T-VAU predicts both heatmaps and language answers.</div>
<div class="relative mt-5 mx-auto w-[960px]">
  <div class="figure"><img src="/figs/framework.png" /></div>
  <div v-click="1" class="loc-box loc-pink" style="left: 779px; top: 12px; width: 178px; height: 157px;"></div>
  <div v-click="2" class="loc-box loc-green" style="left: 584px; top: 302px; width: 199px; height: 53px;"></div>
  <div v-click="2" class="loc-box loc-green" style="left: 11px; top: 13px; width: 165px; height: 350px;"></div>
</div>
<div class="grid grid-cols-2 gap-6 mt-4 max-w-[930px] mx-auto">
  <div v-click="1" class="card-tight"><span class="text-pink-300 font-semibold">Pixel-level heatmaps</span><br/>spatio-temporal anomaly evidence $\,\mathbf{H}$</div>
  <div v-click="2" class="card-tight"><span class="text-green-300 font-semibold">Language responses</span><br/>judgment, appearance, location, motion, trajectory</div>
</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="title-main">Anomaly Heatmap Decoder (AHD)</div>
<div class="grid grid-cols-[0.82fr_1.18fr] gap-8 mt-8 items-start">
  <div>
    <div class="text-2xl font-semibold text-green-300">Purpose</div>
    <div class="body mt-3">Generate pixel-level anomaly heatmaps by aligning multiscale visual tokens with normal / abnormal text prompts.</div>
    <div class="mt-7 space-y-3 text-[17px]">
      <div v-click="1" class="card-tight">1. Template prompts: <b>normal</b> vs. <b>abnormal</b></div>
      <div v-click="2" class="card-tight">2. Multiscale visual features: transformer blocks 1, 8, 16, 32</div>
      <div v-click="3" class="card-tight">3. MLP projection + cosine similarity</div>
      <div v-click="4" class="card-tight">4. Learnable layer fusion + softmax anomaly channel</div>
    </div>
  </div>
  <div>
    <div class="figure"><img src="/figs/framework.png" /></div>
    <div class="small text-center mt-2">Focus: Text Encoder + AHD + Similarity-Aware Fusion</div>
  </div>
</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="title-main">Region-aware Anomaly Encoder (RAE)</div>
<div class="grid grid-cols-[0.84fr_1.16fr] gap-8 mt-8 items-start">
  <div>
    <div class="text-2xl font-semibold text-orange-300">Purpose</div>
    <div class="body mt-3">Transform heatmap evidence into structured prompt embeddings for multi-turn anomaly reasoning.</div>
    <div class="mt-7 space-y-3 text-[17px]">
      <div v-click="1" class="card-tight">1. Temporal difference: $\Delta \mathbf{H}_c[t]=\mathbf{H}_c[t+1]-\mathbf{H}_c[t]$</div>
      <div v-click="2" class="card-tight">2. Lightweight convolutional backbone extracts motion-aware features</div>
      <div v-click="3" class="card-tight">3. 3×3 regional pooling + global pooling</div>
      <div v-click="4" class="card-tight">4. Base + region + global prompts are concatenated with video and dialogue prompts</div>
    </div>
  </div>
  <div>
    <div class="figure"><img src="/figs/framework.png" /></div>
    <div class="small text-center mt-2">Focus: heatmap evidence → region-aware prompt embedding → LVLM response</div>
  </div>
</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="title-main">Training and implementation protocol</div>
<div class="grid grid-cols-2 gap-6 mt-10">
  <div v-click="1" class="card">
    <div class="text-2xl font-semibold text-green-300">Stage 1: train AHD</div>
    <div class="body mt-4">Frozen Qwen2.5-VL 7B backbone; optimize only AHD with pixel-level cross-entropy.</div>
    <div class="small mt-4">AdamW, peak LR $1\times10^{-3}$, warmup 0.1, batch size 1, accumulation 8.</div>
  </div>
  <div v-click="2" class="card">
    <div class="text-2xl font-semibold text-orange-300">Stage 2: fine-tune RAE</div>
    <div class="body mt-4">Load the best AHD weights; train prompt learner and LoRA-enhanced language decoder via SFT.</div>
    <div class="small mt-4">LoRA rank 16, $\alpha=32$, dropout 0.05 on q_proj/v_proj; LR $2\times10^{-4}$, BF16, max seq 2048.</div>
  </div>
</div>
<div v-click="3" class="callout mt-8 body">Two SFT phases: first holistic appearance–motion narratives, then anomaly-focused refinement.</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="title-main">Multi-turn anomaly reasoning</div>
<div class="grid grid-cols-[0.62fr_1.38fr] gap-8 mt-8 items-start">
  <div>
    <div class="text-2xl font-semibold text-pink-300">Dialogue hierarchy</div>
    <div class="mt-6 space-y-3 text-lg">
      <div v-click="1" class="card-tight">Q0: Is there any anomaly?</div>
      <div v-click="2" class="card-tight">Q1: Which target and what appearance?</div>
      <div v-click="3" class="card-tight">Q2: What motion or trajectory?</div>
      <div v-click="4" class="card-tight">Q3: What temporal anchors or causal cues?</div>
    </div>
  </div>
  <div class="figure"><img src="/figs/vis1.png" /></div>
</div>
<div v-click="5" class="absolute bottom-14 left-14 right-14 text-center text-xl text-gray-200">The language output is constrained by spatial and temporal evidence, reducing target drift and hallucinated explanations.</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="h-full flex items-center">
  <div>
    <div class="section-title">Fine-grained Dataset Construction</div>
    <div class="subtitle">From pixel masks to target-level video–text supervision.</div>
  </div>
</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="title-main">Why construct a new supervision pipeline?</div>
<div class="grid grid-cols-[0.88fr_1.12fr] gap-8 mt-8 items-center">
  <div>
    <div class="text-3xl font-semibold leading-snug">Pixel masks alone do not teach the model to explain.</div>
    <div class="mt-8 space-y-4 text-lg">
      <div v-click="1" class="card-tight">Existing VAD labels: anomaly score / mask</div>
      <div v-click="2" class="card-tight">Needed by T-VAU: target identity, appearance, position, motion, trajectory</div>
      <div v-click="3" class="card-tight bg-pink-500/20 border-pink-300/20">Solution: target-level video–text annotations derived from ShanghaiTech and UBnormal</div>
    </div>
  </div>
  <div class="figure"><img src="/figs/dataset.png" /></div>
</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="title-main">Dataset construction pipeline</div>
<div class="figure mt-5"><img src="/figs/dataset.png" /></div>
<div class="grid grid-cols-3 gap-4 mt-4 text-base">
  <div v-click="1" class="card-tight"><span class="text-blue-300 font-semibold">Step 1</span><br/>Frame-level structured prompting and temporal aggregation.</div>
  <div v-click="2" class="card-tight"><span class="text-orange-300 font-semibold">Step 2</span><br/>Mask + Gaussian blur to focus on abnormal evidence.</div>
  <div v-click="3" class="card-tight"><span class="text-green-300 font-semibold">Step 3</span><br/>Bidirectional consistency verification between appearance and motion.</div>
</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="title-main">Resulting supervision</div>
<div class="grid grid-cols-3 gap-6 mt-10">
  <div v-click="1" class="card min-h-[220px]"><div class="text-2xl font-semibold text-blue-300">Appearance</div><div class="body mt-5">Target-level attributes such as clothing, object type, and visible distinguishing cues.</div></div>
  <div v-click="2" class="card min-h-[220px]"><div class="text-2xl font-semibold text-green-300">Spatio-temporal localization</div><div class="body mt-5">Frame-wise target location and abnormal period supervision.</div></div>
  <div v-click="3" class="card min-h-[220px]"><div class="text-2xl font-semibold text-orange-300">Motion trajectory</div><div class="body mt-5">Direction, state changes, and target path over time.</div></div>
</div>
<div v-click="4" class="callout mt-9 text-xl text-center">
  ShanghaiTech frame-wise annotations: <b>4,108 train / 1,028 validation</b><br/>
  Target-aligned descriptions: <b>5,136 ShanghaiTech samples + 7,912 UBnormal samples</b>
</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="h-full flex items-center">
  <div>
    <div class="section-title">Experiments</div>
    <div class="subtitle">Localization, language grounding, and module ablations.</div>
  </div>
</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="title-main">Evaluation setup</div>
<div class="grid grid-cols-2 gap-6 mt-10">
  <div class="card">
    <div class="text-2xl font-semibold text-green-300">AHD localization</div>
    <div class="body mt-4">Evaluated on UBnormal with frame-level micro-/macro-AUC, Region-Based Detection Criterion (RBDC), and Track-Based Detection Criterion (TBDC).</div>
  </div>
  <div class="card">
    <div class="text-2xl font-semibold text-orange-300">RAE reasoning</div>
    <div class="body mt-4">Evaluated with Target BLEU-4, Trajectory BLEU-4, and Yes/No accuracy under one-shot prompting.</div>
  </div>
</div>
<div class="callout mt-8 body">The paper also defines balanced accuracy and threshold-free ROC–AUC for discriminative ability; the main reported language table focuses on BLEU-4 and Yes/No accuracy.</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="title-main">Anomaly localization on UBnormal</div>
<div class="grid grid-cols-[0.82fr_1.18fr] gap-8 mt-7 items-start">
  <div>
    <div class="text-2xl font-semibold text-pink-300">AHD improves localization-oriented metrics</div>
    <div class="body mt-4">Fine-tuned AHD reaches the strongest Micro-AUC, RBDC, and TBDC among the compared methods.</div>
    <div class="grid grid-cols-2 gap-4 mt-7">
      <div class="metric"><div class="num">94.8</div><div class="label">Micro-AUC</div></div>
      <div class="metric"><div class="num">87.8</div><div class="label">Macro-AUC</div></div>
      <div class="metric"><div class="num">67.8</div><div class="label">RBDC</div></div>
      <div class="metric"><div class="num">76.7</div><div class="label">TBDC</div></div>
    </div>
  </div>
  <div class="table-wrap">
    <table class="clean">
      <thead><tr><th>Method</th><th>Micro</th><th>Macro</th><th>RBDC</th><th>TBDC</th></tr></thead>
      <tbody>
        <tr><td>Georgescu et al.</td><td>58.5</td><td>94.4</td><td>18.580</td><td>48.213</td></tr>
        <tr><td>Georgescu et al. (FT)</td><td>68.2</td><td><b>95.3</b></td><td>28.654</td><td>58.097</td></tr>
        <tr><td>Bertasius et al. (FT, SR=1/32)</td><td>86.1</td><td>89.2</td><td>0.008</td><td>0.021</td></tr>
        <tr><td>AHD (1S)</td><td>94.5</td><td>85.2</td><td>64.300</td><td>74.400</td></tr>
        <tr class="hl"><td>AHD (Ours, FT)</td><td>94.8</td><td>87.8</td><td>67.800</td><td>76.700</td></tr>
      </tbody>
    </table>
  </div>
</div>
<div class="small mt-3 text-right">Metrics are reported in percentage, matching the paper table.</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="title-main">Multi-turn dialogue evaluation</div>
<div class="mt-7 table-wrap">
  <table class="clean" style="font-size:12px">
    <thead>
      <tr><th rowspan="2">Method</th><th rowspan="2">Size</th><th colspan="3">ShanghaiTech</th><th colspan="3">UBnormal</th></tr>
      <tr><th>Target</th><th>Traj.</th><th>Acc.</th><th>Target</th><th>Traj.</th><th>Acc.</th></tr>
    </thead>
    <tbody>
      <tr><td>Qwen2.5-VL zero-shot</td><td>7B</td><td>18.74</td><td>27.33</td><td>61.03</td><td>16.20</td><td>24.18</td><td>65.62</td></tr>
      <tr><td>Qwen2.5-VL one-shot</td><td>7B</td><td>50.42</td><td>78.91</td><td>92.36</td><td>44.35</td><td>70.82</td><td>87.24</td></tr>
      <tr><td>LLaVA-1.6 one-shot</td><td>7B</td><td>47.68</td><td>75.42</td><td>91.07</td><td>42.11</td><td>68.07</td><td>85.91</td></tr>
      <tr><td>MiniCPM-V 2.6 one-shot</td><td>7B</td><td>52.34</td><td>80.41</td><td>93.11</td><td>46.70</td><td>72.88</td><td>86.94</td></tr>
      <tr><td>Idefics2 one-shot</td><td>8B</td><td>44.29</td><td>73.84</td><td>90.12</td><td>39.51</td><td>65.92</td><td>84.03</td></tr>
      <tr><td>InternVL one-shot</td><td>8B</td><td>55.73</td><td>82.65</td><td>94.28</td><td>49.84</td><td>71.63</td><td>88.65</td></tr>
      <tr class="hl"><td>RAE (Ours) one-shot</td><td>7B</td><td>62.67</td><td>88.84</td><td>97.67</td><td>50.32</td><td>78.10</td><td>89.73</td></tr>
    </tbody>
  </table>
</div>
<div class="grid grid-cols-3 gap-4 mt-5">
  <div class="metric"><div class="num">62.67</div><div class="label">S.T. Target BLEU-4</div></div>
  <div class="metric"><div class="num">88.84</div><div class="label">S.T. Trajectory BLEU-4</div></div>
  <div class="metric"><div class="num">97.67%</div><div class="label">S.T. Yes/No accuracy</div></div>
</div>
<div class="small mt-2">BLEU-4 and accuracy are reported in percentage.</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="title-main">Ablation: both modules are necessary</div>
<div class="grid grid-cols-[0.7fr_1.3fr] gap-8 mt-8 items-start">
  <div>
    <div class="text-2xl font-semibold text-pink-300">Complementary roles</div>
    <div class="mt-6 space-y-4 text-lg">
      <div v-click="1" class="card-tight"><span class="text-green-300 font-semibold">AHD</span> supplies pixel-level evidence.</div>
      <div v-click="2" class="card-tight"><span class="text-orange-300 font-semibold">RAE</span> makes this evidence usable by the LVLM.</div>
      <div v-click="3" class="card-tight">Removing both reduces the model to a backbone-only LVLM setting.</div>
    </div>
  </div>
  <div class="table-wrap">
    <table class="clean" style="font-size:12px">
      <thead><tr><th>Variant</th><th>Params</th><th>RBDC</th><th>TBDC</th><th>Target</th><th>Traj.</th><th>Acc.</th></tr></thead>
      <tbody>
        <tr><td>T-VAU w/o AHD</td><td>8299.71M</td><td>–</td><td>–</td><td>61.82</td><td>85.47</td><td>95.38%</td></tr>
        <tr><td>T-VAU w/o RAE</td><td>8317.13M</td><td>67.8</td><td>76.7</td><td>–</td><td>–</td><td>–</td></tr>
        <tr><td>T-VAU w/o AHD & RAE</td><td>8274.74M</td><td>–</td><td>–</td><td>61.82</td><td>85.47</td><td>95.38%</td></tr>
        <tr class="hl"><td>T-VAU</td><td>8324.67M</td><td>67.8</td><td>76.7</td><td>62.67</td><td>88.84</td><td>97.67%</td></tr>
      </tbody>
    </table>
  </div>
</div>
<div class="small mt-3 text-right">Std values are omitted on this slide for readability; central values match the paper source.</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="h-full flex items-center">
  <div>
    <div class="section-title">Qualitative Results</div>
    <div class="subtitle">Inspecting whether the text answers follow the same spatial-temporal evidence chain.</div>
  </div>
</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="title-main">Evidence-grounded multi-turn QA</div>
<div class="figure mt-5"><img src="/figs/vis1.png" /></div>
<div class="grid grid-cols-3 gap-4 mt-4 text-base">
  <div v-click="1" class="card-tight">AHD localizes the abnormal target rather than the whole scene.</div>
  <div v-click="2" class="card-tight">RAE guides target-specific appearance and motion descriptions.</div>
  <div v-click="3" class="card-tight">The dialogue remains consistent across judgment, features, and trajectory.</div>
</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="title-main">Trajectory consistency</div>
<div class="figure mt-5"><img src="/figs/vis2.png" /></div>
<div class="mt-6 text-center text-xl text-gray-200 leading-relaxed">Accumulated predictions follow ground-truth anomaly regions over time, supporting motion and trajectory reasoning.</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="title-main">Failure modes and practical caveats</div>
<div class="grid grid-cols-3 gap-6 mt-12">
  <div v-click="1" class="card min-h-[250px]"><div class="text-2xl font-semibold text-orange-300">Micro-actions</div><div class="body mt-5">Tiny actions with minimal displacement can yield weak or ambiguous temporal evidence.</div></div>
  <div v-click="2" class="card min-h-[250px]"><div class="text-2xl font-semibold text-blue-300">Nonrigid motion</div><div class="body mt-5">Highly nonrigid motion may scatter activation and reduce spatial compactness.</div></div>
  <div v-click="3" class="card min-h-[250px]"><div class="text-2xl font-semibold text-pink-300">Scene-dependent shifts</div><div class="body mt-5">Specularities, fog, occlusions, and target scale changes can weaken localization fidelity.</div></div>
</div>
<div class="callout mt-8 body">These cases are useful for error analysis because heatmaps remain a visible spatial witness for each language claim.</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="title-main">Takeaway</div>
<div class="grid grid-cols-[0.9fr_1.1fr] gap-8 mt-8 items-center">
  <div>
    <div class="text-4xl font-semibold leading-tight">T-VAU closes the loop from <span class="text-green-300">pixel evidence</span> to <span class="text-pink-300">language reasoning</span>.</div>
    <div class="mt-8 space-y-4 text-lg">
      <div v-click="1" class="card-tight">AHD: threshold-free spatio-temporal anomaly heatmaps</div>
      <div v-click="2" class="card-tight">RAE: region-aware and motion-aware prompt injection</div>
      <div v-click="3" class="card-tight">Dataset: target-level appearance, localization, and trajectory supervision</div>
    </div>
  </div>
  <div class="figure"><img src="/figs/teaser.png" /></div>
</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="h-full flex flex-col justify-center">
  <div class="section-title">Thank you</div>
  <div class="subtitle">Questions?</div>
  <div class="mt-8 body">Code release: <span class="text-blue-300">github.com/momiji-bit/T-VAU</span></div>
</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>
