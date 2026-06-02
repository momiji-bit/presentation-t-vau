---
theme: default
title: Text-guided Fine-Grained Video Anomaly Understanding
transition: fade
background: linear-gradient(135deg, #0f172a, #1e293b)
class: text-white
colorSchema: dark
canvasWidth: 1280
fonts:
  sans: Inter
  serif: Georgia
  mono: Fira Code
---

<style>
.slidev-layout {
  min-height: 100%;
  width: 100%;
  padding: 34px 48px 34px;
  background: linear-gradient(135deg, #0f172a 0%, #172554 48%, #1e1b4b 100%);
  color: #f8fafc;
}
.slide-title {
  font-size: 46px;
  line-height: 1.02;
  font-weight: 780;
  letter-spacing: -.04em;
  max-width: 1120px;
  color: #f8fafc;
}
.section-title {
  font-size: 58px;
  line-height: 1.02;
  font-weight: 780;
  letter-spacing: -.045em;
  color: #f8fafc;
}
.kicker {
  color:#f9a8d4;
  font-weight:700;
  letter-spacing:.02em;
  text-transform:uppercase;
  font-size:14px;
}
.title-main {
  font-size:56px;
  line-height:1.02;
  font-weight:780;
  letter-spacing:-.04em;
  max-width: 1120px;
}
.title-sub { font-size:28px; color:#cbd5e1; margin-top:20px; font-style:italic; }
.author-line { margin-top:34px; font-size:20px; color:#e2e8f0; }
.affiliation-line { margin-top:10px; font-size:16px; color:#cbd5e1; }
.badge-row { display:flex; flex-wrap:wrap; gap:12px; margin-top:28px; }
.badge { display:inline-flex; align-items:center; border-radius:999px; padding:8px 14px; background:rgba(255,255,255,.10); border:1px solid rgba(255,255,255,.12); color:#e2e8f0; font-size:15px; }
.panel { background:rgba(15,23,42,.62); border:1px solid rgba(255,255,255,.12); border-radius:20px; box-shadow:0 16px 42px rgba(0,0,0,.28); }
.card { background:rgba(255,255,255,.10); border:1px solid rgba(255,255,255,.12); border-radius:18px; padding:20px; }
.card h3 { font-size:25px; font-weight:720; margin:0 0 10px 0; }
.card p { font-size:18px; line-height:1.38; color:#e2e8f0; margin:0; }
.figure-card { background:#ffffff; border-radius:18px; padding:12px; box-shadow:0 18px 46px rgba(0,0,0,.32); display:flex; align-items:center; justify-content:center; overflow:hidden; }
.figure-card img { max-width:100%; max-height:100%; object-fit:contain; border-radius:12px; }
.metric-grid { display:grid; grid-template-columns: repeat(4, 1fr); gap:18px; }
.metric { background:rgba(255,255,255,.10); border:1px solid rgba(255,255,255,.12); border-radius:18px; padding:20px; min-height:126px; text-align:center; }
.metric .num { font-size:42px; line-height:1; font-weight:780; color:#86efac; }
.metric .label { margin-top:10px; font-size:18px; color:#e2e8f0; }
.callout { border-left:5px solid #ec4899; padding:16px 18px; background:rgba(236,72,153,.14); border-radius:14px; color:#f8fafc; }
.clean-table { width:100%; border-collapse:collapse; font-size:15px; overflow:hidden; border-radius:16px; }
.clean-table th { background:rgba(255,255,255,.16); color:#f8fafc; font-weight:700; padding:10px 9px; text-align:left; }
.clean-table td { padding:9px 9px; border-top:1px solid rgba(255,255,255,.12); color:#e2e8f0; }
.clean-table .center { text-align:center; }
.clean-table tr.highlight td { background:rgba(236,72,153,.16); color:#ffffff; font-weight:700; }
.small { font-size:14px; color:#94a3b8; }
.body { font-size:22px; line-height:1.42; color:#e2e8f0; }
.body-sm { font-size:18px; line-height:1.42; color:#dbeafe; }
.slide-no { position:absolute; right:24px; bottom:16px; font-size:13px; color:#94a3b8; }
.caption { font-size:14px; color:#94a3b8; margin-top:8px; text-align:center; }
.mathbox { font-size:19px; line-height:1.35; color:#e2e8f0; background:rgba(15,23,42,.72); border:1px solid rgba(255,255,255,.14); border-radius:14px; padding:16px; }
.title-page { min-height:610px; display:grid; grid-template-columns:1fr; gap:44px; align-items:center; }
</style>

<div class="title-page">
  <div>
    <div class="kicker">The 2nd Workshop & Challenge on Subtle Visual Computing (SVC) @ CVPR 2026</div>
    <div class="title-main">Text-guided Fine-Grained Video Anomaly Understanding</div>
    <div class="title-sub">Pixel Evidence to Language Reasoning</div>
    <div class="author-line"><b>Jihao (Geo) Gu</b><sup>1</sup>, Kun Li<sup>2</sup>, He Wang<sup>1</sup>, Kaan Akşit<sup>1</sup></div>
    <div class="affiliation-line"><sup>1</sup>University College London · <sup>2</sup>CVLab, United Arab Emirates University</div>
    <div class="badge-row">
      <span class="badge">Video Anomaly Understanding</span>
      <span class="badge">Subtle Visual Computing</span>
      <span class="badge">LVLMs</span>
      <span class="badge">Evidence-grounded QA</span>
    </div>
  </div>
  <div class="absolute bottom-20 right-14">
    <img src="/logo.png" alt="lab logo" class="h-[200px] opacity-100">
  </div>
  <div class="absolute bottom-20 left-160">
    <img src="/CVPR_Denver_2026.jpg" alt="lab logo" class="h-[200px] opacity-100">
  </div>
</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="title-page">
  <div>
    <div class="section-title">Motivation</div>
  </div>
</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="slide-title">Existing paradigms are fragmented</div>

<div class="grid grid-cols-2 gap-6 mt-8">
  <div v-click="1" class="card">
    <div class="text-2xl font-semibold text-orange-300">Traditional IAD / VAD</div>
    <div class="text-lg mt-4 text-gray-200 leading-relaxed">
      Produces anomaly scores or heatmaps, but usually lacks semantic explanation.
    </div>
    <div class="mt-5 bg-slate-900/80 rounded-lg p-4 text-gray-300">
      Output: score / heatmap only
    </div>
  </div>

  <div v-click="2" class="card">
    <div class="text-2xl font-semibold text-green-300">General LVLMs</div>
    <div class="text-lg mt-4 text-gray-200 leading-relaxed">
      Can answer in language, but often fails to ground subtle cues at pixel level.
    </div>
    <div class="mt-5 bg-slate-900/80 rounded-lg p-4 text-gray-300">
      Output: judgment without explicit evidence
    </div>
  </div>

  <div v-click="3" class="card">
    <div class="text-2xl font-semibold text-blue-300">LVLM + diffusion hybrids</div>
    <div class="text-lg mt-4 text-gray-200 leading-relaxed">
      Combine text and visualization, but generated explanations may be unstable or inconsistent.
    </div>
    <div class="mt-5 bg-slate-900/80 rounded-lg p-4 text-gray-300">
      Output: judgment + generated visualization
    </div>
  </div>

  <div v-click="4" class="card bg-pink-500/20 border-pink-300/30">
    <div class="text-2xl font-semibold text-pink-300">T-VAU</div>
    <div class="text-lg mt-4 text-gray-100 leading-relaxed">
      Couples pixel-level anomaly evidence with language reasoning.
    </div>
    <div class="mt-5 bg-slate-900/80 rounded-lg p-4 text-gray-100">
      Output: detection + localization + identification + trajectory + explanation
    </div>
  </div>
</div>

<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="slide-title">The gap: anomaly understanding requires evidence</div>

<div class="grid grid-cols-[0.9fr_1.1fr] gap-8 mt-8 items-start">
  <div>
    <div class="text-3xl font-semibold leading-snug">
      An anomaly should be<br />
      <span class="text-pink-300">detected</span>,
      <span class="text-blue-300">localized</span>, and
      <span class="text-green-300">explained</span>.
    </div>

    <div class="mt-8 text-xl text-gray-200 leading-relaxed">
      Fine-grained anomaly understanding asks the model to answer:
    </div>
    
    <div class="mt-6 space-y-4 text-lg">
      <div v-click="1" class="bg-white/10 rounded-lg p-4">Is there any anomaly?</div>
      <div v-click="2" class="bg-white/10 rounded-lg p-4">Where is the abnormal evidence?</div>
      <div v-click="3" class="bg-white/10 rounded-lg p-4">Which target is responsible?</div>
      <div v-click="4" class="bg-white/10 rounded-lg p-4">How does the target move over time?</div>
    </div>
  </div>

  <div class="figure-card mt-2 h-[440px]">
    <img src="/figs/teaser.png" alt="T-VAU teaser" />
  </div>
</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="slide-title">What T-VAU adds</div>

<div class="grid grid-cols-3 gap-6 mt-12">
  <div v-click="1" class="card min-h-[260px]">
    <div class="text-2xl font-semibold text-green-300">1. Pixel evidence</div>
    <p class="mt-5 text-lg leading-relaxed text-gray-200">
      AHD produces threshold-free spatio-temporal heatmaps rather than only clip-level anomaly scores.
    </p>
  </div>

  <div v-click="2" class="card min-h-[260px]">
    <div class="text-2xl font-semibold text-orange-300">2. Region-aware prompting</div>
    <p class="mt-5 text-lg leading-relaxed text-gray-200">
      RAE converts heatmap dynamics into local, global, and learnable prompt embeddings for the LVLM.
    </p>
  </div>

  <div v-click="3" class="card min-h-[260px]">
    <div class="text-2xl font-semibold text-pink-300">3. Target-level supervision</div>
    <p class="mt-5 text-lg leading-relaxed text-gray-200">
      The dataset provides aligned annotations for appearance, localization, and motion trajectories.
    </p>
  </div>
</div>

<div v-click="4" class="absolute bottom-20 left-20 right-20 callout text-xl text-center">
  The core contribution is a closed loop: visual-text alignment → anomaly heatmaps → evidence-conditioned language reasoning.
</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="title-page">
  <div>
    <div class="section-title">Proposed Method</div>
  </div>
</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="slide-title">T-VAU: closed-loop anomaly understanding</div>

<div class="grid grid-cols-[0.82fr_1.18fr] gap-8 mt-8 items-start">
  <div>
    <div class="body-sm">
      Given a video clip, dialogue history, and normal / abnormal text prompts, T-VAU jointly predicts:
    </div>
    <div class="mt-6 space-y-4">
      <div v-click="1" class="card">
        <span class="text-pink-300 font-semibold text-xl">Pixel-level spatio-temporal heatmaps</span><br>
        <span class="text-gray-200">Explicit anomaly evidence $\mathbf{H}$ from category-wise heatmaps $\mathbf{H}_c$.</span>
      </div>
      <div v-click="2" class="card">
        <span class="text-green-300 font-semibold text-xl">Language responses</span><br>
        <span class="text-gray-200">Judgment, target identity, appearance, localization, motion, and trajectory.</span>
      </div>
      <div v-click="3" class="card">
        <span class="text-blue-300 font-semibold text-xl">Trainable lightweight modules</span><br>
        <span class="text-gray-200">Frozen Qwen2.5-VL 7B backbone + AHD + RAE / LoRA prompt tuning.</span>
      </div>
    </div>
  </div>

  <div>
    <div class="figure-card h-[455px]">
      <img src="/figs/framework.png" alt="T-VAU framework" />
    </div>
    <div class="caption">Framework overview: Text Encoder + AHD + RAE + LVLM decoder.</div>
  </div>
</div>

<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="slide-title">Key idea</div>

<div class="grid grid-cols-3 gap-6 mt-12">
  <div v-click="1" class="card min-h-[270px]">
    <div class="text-2xl font-semibold text-blue-300">1. Align</div>
    <p class="text-lg mt-5 leading-relaxed text-gray-200">
      Use normal / abnormal text prompts to align intermediate visual tokens with semantic anomaly concepts.
    </p>
    <div class="mt-6 small">Element-wise cosine similarity</div>
  </div>

  <div v-click="2" class="card min-h-[270px]">
    <div class="text-2xl font-semibold text-orange-300">2. Ground</div>
    <p class="text-lg mt-5 leading-relaxed text-gray-200">
      Fuse similarity maps from multiscale ViT features to decode threshold-free heatmaps.
    </p>
    <div class="mt-6 small">Similarity-Aware Fusion + AHD</div>
  </div>

  <div v-click="3" class="card min-h-[270px]">
    <div class="text-2xl font-semibold text-pink-300">3. Reason</div>
    <p class="text-lg mt-5 leading-relaxed text-gray-200">
      Convert heatmap evidence into region- and motion-aware prompts injected into the LVLM.
    </p>
    <div class="mt-6 small">RAE + dialogue context</div>
  </div>
</div>

<div v-click="4" class="absolute bottom-20 left-20 right-20 text-2xl text-center italic text-gray-200">
  Low-level anomaly evidence becomes structured language reasoning.
</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="slide-title">Anomaly Heatmap Decoder (AHD)</div>

<div class="grid grid-cols-[0.8fr_1.2fr] gap-8 mt-8 items-start">
  <div>
    <div class="text-2xl font-semibold text-green-300">Purpose</div>
    <p class="text-lg mt-3 text-gray-200 leading-relaxed">
      Generate pixel-level anomaly heatmaps by aligning visual tokens with normal / abnormal text prompts.
    </p>

    <div class="mt-8 space-y-3 text-lg">
      <div v-click="1" class="bg-white/10 rounded-lg p-3">Text prompts: normal vs. abnormal</div>
      <div v-click="2" class="bg-white/10 rounded-lg p-3">Multiscale visual tokens: ViT blocks 1, 8, 16, 32</div>
      <div v-click="3" class="bg-white/10 rounded-lg p-3">Similarity-Aware Fusion: cosine similarity + learnable weighted sum</div>
      <div v-click="4" class="bg-white/10 rounded-lg p-3">Softmax anomaly channel → heatmap $\mathbf{H}$</div>
    </div>
  </div>

  <div>
    <div class="figure-card h-[445px]">
      <img src="/figs/framework.png" alt="AHD in framework" />
    </div>
    <div class="caption">Focus: Text Encoder + SAF + AHD.</div>
  </div>
</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="slide-title">AHD computation</div>

<div class="grid grid-cols-2 gap-8 mt-10 items-start">
  <div class="space-y-5">
    <div v-click="1" class="mathbox">
      <div class="text-pink-300 font-semibold mb-2">Text feature</div>
      $\mathbf{T}_c = \frac{1}{N_cL}\sum_{n=1}^{N_c}\sum_{\ell=1}^{L}\mathbf{T}'_c[n,\ell,:]$
    </div>
    <div v-click="2" class="mathbox">
      <div class="text-blue-300 font-semibold mb-2">Visual features</div>
      $\mathbf{V}_{i}=\phi_i(\mathbf{V}_0),\quad i\in\{1,8,16,32\}$
    </div>
  </div>

  <div class="space-y-5">
    <div v-click="3" class="mathbox">
      <div class="text-orange-300 font-semibold mb-2">Similarity map</div>
      $\mathbf{h}_{c}^{i}[t,h,w]=\mathrm{CosSim}(\mathbf{V}'_i[t,:,h,w],\mathbf{T}_{c})$
    </div>
    <div v-click="4" class="mathbox">
      <div class="text-green-300 font-semibold mb-2">Heatmap</div>
      $\mathbf{H}_{c}=\sum_i w_i\mathbf{h}^{i}_{c}$, then $\mathbf{H}=\mathrm{Softmax}(\mathbf{H}_{c})[:,\mathrm{abnormal},:,:]$
    </div>
  </div>
</div>

<div v-click="5" class="absolute bottom-20 left-20 right-20 callout text-xl text-center">
  AHD is optimized for localization; no manual threshold is needed to form the anomaly evidence map.
</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="slide-title">Region-aware Anomaly Encoder (RAE)</div>

<div class="grid grid-cols-[0.84fr_1.16fr] gap-8 mt-8 items-start">
  <div>
    <div class="text-2xl font-semibold text-orange-300">Purpose</div>
    <p class="text-lg mt-3 text-gray-200 leading-relaxed">
      Transform heatmap evidence into prompts that the LVLM can use for multi-turn reasoning.
    </p>

    <div class="mt-8 space-y-3 text-lg">
      <div v-click="1" class="bg-white/10 rounded-lg p-3">Temporal difference: $\Delta\mathbf{H}_c$ captures motion cues</div>
      <div v-click="2" class="bg-white/10 rounded-lg p-3">Lightweight convolutional backbone extracts region-aware features</div>
      <div v-click="3" class="bg-white/10 rounded-lg p-3">$3\times3$ regional pooling captures local evidence</div>
      <div v-click="4" class="bg-white/10 rounded-lg p-3">Global pooling + learnable base tokens capture clip-level anomaly context</div>
    </div>
  </div>

  <div>
    <div class="figure-card h-[445px]">
      <img src="/figs/framework.png" alt="RAE in framework" />
    </div>
    <div class="caption">Focus: heatmap dynamics → region-aware prompt embedding → LVLM response.</div>
  </div>
</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="slide-title">RAE prompt construction</div>

<div class="grid grid-cols-2 gap-8 mt-10 items-start">
  <div class="space-y-5">
    <div v-click="1" class="mathbox">
      <div class="text-pink-300 font-semibold mb-2">Motion-aware heatmaps</div>
      $\mathbf{X}[t]=\mathbf{H}_{c}[t+1]-\mathbf{H}_{c}[t]$
    </div>
    <div v-click="2" class="mathbox">
      <div class="text-blue-300 font-semibold mb-2">Region prompts</div>
      $\mathbf{P}_{\mathrm{region}}=\mathrm{MLP}_{\mathrm{region}}(\mathbf{F}_{\mathrm{grid}})$, with $3\times3$ grid pooling
    </div>
  </div>

  <div class="space-y-5">
    <div v-click="3" class="mathbox">
      <div class="text-orange-300 font-semibold mb-2">Global + base prompts</div>
      $\mathbf{P}_{\mathrm{An}}=[\mathbf{P}_{\mathrm{base}},\mathbf{P}_{\mathrm{region}},\mathbf{p}_{\mathrm{global}}]$
    </div>
    <div v-click="4" class="mathbox">
      <div class="text-green-300 font-semibold mb-2">Final prompt sequence</div>
      $\mathbf{P}=[\mathbf{P}_{\mathbf{V}},\mathbf{P}_{\mathrm{An}},\mathbf{P}_{\mathbf{Q}_{\leq t}}] \rightarrow D_l \rightarrow \mathbf{A}_t$
    </div>
  </div>
</div>

<div v-click="5" class="absolute bottom-20 left-20 right-20 callout text-xl text-center">
  RAE makes heatmap evidence usable by the language decoder instead of asking the LVLM to infer anomalies from raw frames alone.
</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="slide-title">Multi-turn anomaly reasoning</div>

<div class="grid grid-cols-[0.75fr_1.25fr] gap-8 mt-8 items-start">
  <div>
    <div class="text-2xl font-semibold text-pink-300">Dialogue flow</div>
    <div class="mt-6 space-y-3 text-lg">
      <div v-click="1" class="bg-white/10 rounded-lg p-4">Q0: Is there any anomaly?</div>
      <div v-click="2" class="bg-white/10 rounded-lg p-4">Q1: Which target is abnormal?</div>
      <div v-click="3" class="bg-white/10 rounded-lg p-4">Q2: What are the target features?</div>
      <div v-click="4" class="bg-white/10 rounded-lg p-4">Q3: What is the motion state?</div>
      <div v-click="5" class="bg-white/10 rounded-lg p-4">Q4: From where to where?</div>
    </div>
  </div>

  <div>
    <div class="figure-card h-[385px]">
      <img src="/figs/vis1.png" alt="Multi-turn anomaly QA" />
    </div>
    <div v-click="6" class="mt-6 callout text-lg text-center">
      The language output is constrained by spatial and temporal evidence, reducing target drift and hallucinated explanations.
    </div>
  </div>
</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="title-page">
  <div>
    <div class="section-title">Fine-grained Dataset Construction</div>
  </div>
</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="slide-title">Why construct a new supervision pipeline?</div>

<div class="grid grid-cols-[0.88fr_1.12fr] gap-8 mt-8 items-start">
  <div>
    <div class="text-3xl font-semibold leading-snug">
      Pixel masks alone do not teach the model to explain.
    </div>

    <div class="mt-8 space-y-4 text-lg">
      <div v-click="1" class="card">Existing VAD labels: anomaly score / pixel mask</div>
      <div v-click="2" class="card">Needed by T-VAU: target identity, appearance, position, motion, trajectory</div>
      <div v-click="3" class="card bg-pink-500/20 border-pink-300/20">Solution: target-level video-text annotations derived from ShanghaiTech and UBnormal</div>
    </div>
  </div>

  <div class="figure-card h-[445px]">
    <img src="/figs/dataset.png" alt="Dataset construction" />
  </div>
</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="slide-title">Dataset construction pipeline</div>

<div class="figure-card mt-6 h-[410px]">
  <img src="/figs/dataset.png" alt="Dataset construction pipeline" />
</div>

<div class="grid grid-cols-3 gap-4 mt-5 text-base">
  <div v-click="1" class="card p-4">
    <span class="text-blue-300 font-semibold">Step 1</span><br>
    Frame-level structured prompting and temporal aggregation.
  </div>
  <div v-click="2" class="card p-4">
    <span class="text-orange-300 font-semibold">Step 2</span><br>
    Mask-guided refinement with Gaussian-blurred background suppression.
  </div>
  <div v-click="3" class="card p-4">
    <span class="text-green-300 font-semibold">Step 3</span><br>
    Cross-modal consistency verification between appearance and motion.
  </div>
</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="slide-title">Resulting supervision</div>

<div class="grid grid-cols-3 gap-6 mt-12">
  <div v-click="1" class="card min-h-[220px]">
    <div class="text-2xl font-semibold text-blue-300">Appearance</div>
    <p class="text-lg mt-5 text-gray-200 leading-relaxed">
      Target-level attributes such as clothing, object type, and visible distinguishing cues.
    </p>
  </div>

  <div v-click="2" class="card min-h-[220px]">
    <div class="text-2xl font-semibold text-green-300">Spatio-temporal localization</div>
    <p class="text-lg mt-5 text-gray-200 leading-relaxed">
      Frame-wise target location and abnormal period supervision.
    </p>
  </div>

  <div v-click="3" class="card min-h-[220px]">
    <div class="text-2xl font-semibold text-orange-300">Motion trajectory</div>
    <p class="text-lg mt-5 text-gray-200 leading-relaxed">
      Direction, state changes, and target path over time.
    </p>
  </div>
</div>

<div v-click="4" class="absolute bottom-22 left-20 right-20 bg-slate-900/80 rounded-xl p-6 text-xl text-center">
  ShanghaiTech: 4,108 train / 1,028 validation frame-wise annotations<br>
  Target-aligned descriptions: 5,136 ShanghaiTech samples + 7,912 UBnormal samples
</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="title-page">
  <div>
    <div class="section-title">Experiments</div>
  </div>
</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="slide-title">Experimental setup</div>

<div class="grid grid-cols-3 gap-6 mt-10">
  <div v-click="1" class="card min-h-[300px]">
    <div class="text-2xl font-semibold text-blue-300">Datasets</div>
    <div class="mt-5 text-lg leading-relaxed text-gray-200">
      <b>UBnormal</b>: 543 clips, 236,902 frames, 29 virtual scenes, 22 anomaly types, pixel-level target annotations.<br><br>
      <b>ShanghaiTech</b>: 330 normal training videos, 107 test videos, 13 scenes, 130 annotated anomalies.
    </div>
  </div>

  <div v-click="2" class="card min-h-[300px]">
    <div class="text-2xl font-semibold text-green-300">AHD metrics</div>
    <div class="mt-5 text-lg leading-relaxed text-gray-200">
      Frame-level micro-/macro-AUC for anomaly discrimination.<br><br>
      RBDC and TBDC for spatial and trajectory-oriented localization.
    </div>
  </div>

  <div v-click="3" class="card min-h-[300px]">
    <div class="text-2xl font-semibold text-pink-300">RAE metrics</div>
    <div class="mt-5 text-lg leading-relaxed text-gray-200">
      BLEU-4 for target and trajectory descriptions.<br><br>
      Yes/No accuracy for binary anomaly judgment.
    </div>
  </div>
</div>

<div v-click="4" class="absolute bottom-20 left-20 right-20 callout text-xl text-center">
  Evaluation separates localization quality from evidence-grounded language quality.
</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="slide-title">Anomaly localization on UBnormal</div>

<div class="grid grid-cols-[0.78fr_1.22fr] gap-8 mt-8 items-start">
  <div>
    <div class="text-2xl font-semibold text-pink-300">AHD achieves strong localization</div>
    <p class="text-lg mt-4 text-gray-200 leading-relaxed">
      Fine-tuned AHD improves micro-AUC, RBDC, and TBDC over prior baselines. Macro-AUC remains lower than the strongest multi-stream baseline.
    </p>

    <div class="metric-grid mt-8">
      <div v-click="1" class="metric"><div class="num">94.8</div><div class="label">Micro-AUC</div></div>
      <div v-click="2" class="metric"><div class="num">87.8</div><div class="label">Macro-AUC</div></div>
      <div v-click="3" class="metric"><div class="num">67.8</div><div class="label">RBDC</div></div>
      <div v-click="4" class="metric"><div class="num">76.7</div><div class="label">TBDC</div></div>
    </div>
  </div>

  <div>
    <table class="clean-table text-sm">
      <thead>
        <tr><th>Method</th><th class="center">Micro</th><th class="center">Macro</th><th class="center">RBDC</th><th class="center">TBDC</th></tr>
      </thead>
      <tbody>
        <tr><td>Georgescu et al.</td><td class="center">58.5</td><td class="center">94.4</td><td class="center">18.6</td><td class="center">48.2</td></tr>
        <tr><td>Georgescu et al. (FT)</td><td class="center">68.2</td><td class="center">95.3</td><td class="center">28.7</td><td class="center">58.1</td></tr>
        <tr><td>Sultani et al. (PT)</td><td class="center">61.1</td><td class="center">89.4</td><td class="center">0.001</td><td class="center">0.012</td></tr>
        <tr><td>Bertasius et al. (FT, SR=1/32)</td><td class="center">86.1</td><td class="center">89.2</td><td class="center">0.008</td><td class="center">0.021</td></tr>
        <tr><td>AHD (1S)</td><td class="center">94.5</td><td class="center">85.2</td><td class="center">64.3</td><td class="center">74.4</td></tr>
        <tr class="highlight"><td>AHD (Ours, FT)</td><td class="center">94.8</td><td class="center">87.8</td><td class="center">67.8</td><td class="center">76.7</td></tr>
      </tbody>
    </table>
    <div class="small mt-3">Metrics are reported in percentage. PT = pre-trained, FT = fine-tuned, 1S = one-shot, SR = frame sampling rate.</div>
  </div>
</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="slide-title">Multi-turn dialogue evaluation</div>

<div class="grid grid-cols-[0.82fr_1.18fr] gap-8 mt-8 items-start">
  <div>
    <div class="text-2xl font-semibold text-pink-300">RAE improves language grounding</div>
    <p class="text-lg mt-4 text-gray-200 leading-relaxed">
      One-shot evaluation compares representative LVLMs on target description, trajectory description, and Yes/No judgment.
    </p>

    <div class="mt-8 space-y-4 text-lg">
      <div v-click="1" class="bg-white/10 rounded-lg p-4">
        ShanghaiTech: <span class="text-green-300 font-semibold">62.67</span> Target BLEU-4,
        <span class="text-green-300 font-semibold">88.84</span> Trajectory BLEU-4
      </div>
      <div v-click="2" class="bg-white/10 rounded-lg p-4">
        ShanghaiTech Yes/No: <span class="text-green-300 font-semibold">97.67%</span>
      </div>
      <div v-click="3" class="bg-white/10 rounded-lg p-4">
        UBnormal: <span class="text-green-300 font-semibold">50.32 / 78.10</span> BLEU-4 and
        <span class="text-green-300 font-semibold">89.73%</span> Yes/No
      </div>
    </div>
  </div>

  <div>
    <table class="clean-table text-xs">
      <thead>
        <tr>
          <th>Method</th>
          <th class="center">S.T. Target</th><th class="center">S.T. Traj.</th><th class="center">S.T. Acc.</th>
          <th class="center">UB Target</th><th class="center">UB Traj.</th><th class="center">UB Acc.</th>
        </tr>
      </thead>
      <tbody>
        <tr><td>Qwen2.5-VL zero-shot</td><td class="center">18.74</td><td class="center">27.33</td><td class="center">61.03</td><td class="center">16.20</td><td class="center">24.18</td><td class="center">65.62</td></tr>
        <tr><td>Qwen2.5-VL one-shot</td><td class="center">50.42</td><td class="center">78.91</td><td class="center">92.36</td><td class="center">44.35</td><td class="center">70.82</td><td class="center">87.24</td></tr>
        <tr><td>MiniCPM-V 2.6 one-shot</td><td class="center">52.34</td><td class="center">80.41</td><td class="center">93.11</td><td class="center">46.70</td><td class="center">72.88</td><td class="center">86.94</td></tr>
        <tr><td>InternVL one-shot</td><td class="center">55.73</td><td class="center">82.65</td><td class="center">94.28</td><td class="center">49.84</td><td class="center">71.63</td><td class="center">88.65</td></tr>
        <tr class="highlight"><td>RAE (Ours) one-shot</td><td class="center">62.67</td><td class="center">88.84</td><td class="center">97.67</td><td class="center">50.32</td><td class="center">78.10</td><td class="center">89.73</td></tr>
      </tbody>
    </table>
    <div class="small mt-3">S.T. = ShanghaiTech. BLEU-4 and accuracy are reported in percentage.</div>
  </div>
</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="slide-title">Ablation: both modules are necessary</div>

<div class="grid grid-cols-[0.82fr_1.18fr] gap-8 mt-8 items-start">
  <div>
    <div class="text-2xl font-semibold text-pink-300">Complementary roles</div>
    <div class="mt-6 space-y-4 text-lg">
      <div v-click="1" class="card">
        <span class="text-green-300 font-semibold">AHD</span> supplies pixel-level evidence.
      </div>
      <div v-click="2" class="card">
        <span class="text-orange-300 font-semibold">RAE</span> makes this evidence usable by the LVLM.
      </div>
      <div v-click="3" class="card">
        Removing AHD makes heatmap metrics inapplicable; removing RAE leaves heatmaps but removes evidence-conditioned dialogue.
      </div>
    </div>
  </div>

  <div>
    <table class="clean-table text-sm">
      <thead>
        <tr><th>Variant</th><th class="center">RBDC</th><th class="center">TBDC</th><th class="center">Target BLEU</th><th class="center">Traj. BLEU</th><th class="center">Acc.</th></tr>
      </thead>
      <tbody>
        <tr><td>w/o AHD</td><td class="center">–</td><td class="center">–</td><td class="center">61.82</td><td class="center">85.47</td><td class="center">95.38</td></tr>
        <tr><td>w/o RAE</td><td class="center">67.8</td><td class="center">76.7</td><td class="center">–</td><td class="center">–</td><td class="center">–</td></tr>
        <tr><td>w/o AHD & RAE</td><td class="center">–</td><td class="center">–</td><td class="center">61.82</td><td class="center">85.47</td><td class="center">95.38</td></tr>
        <tr class="highlight"><td>T-VAU</td><td class="center">67.8</td><td class="center">76.7</td><td class="center">62.67</td><td class="center">88.84</td><td class="center">97.67</td></tr>
      </tbody>
    </table>
    <div class="small mt-3">Current source reports w/o AHD and w/o AHD & RAE with the same text-only baseline scores; keep this note unless updated ablation numbers are available.</div>
  </div>
</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="title-page">
  <div>
    <div class="section-title">Qualitative Results</div>
  </div>
</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="slide-title">Evidence-grounded multi-turn QA</div>

<div class="figure-card mt-6 h-[390px]">
  <img src="/figs/vis1.png" alt="Evidence grounded multi-turn QA" />
</div>

<div class="grid grid-cols-3 gap-4 mt-5 text-base">
  <div v-click="1" class="card p-4">AHD localizes the abnormal target rather than the whole scene.</div>
  <div v-click="2" class="card p-4">RAE guides target-specific appearance and motion descriptions.</div>
  <div v-click="3" class="card p-4">The dialogue remains consistent across judgment, features, and trajectory.</div>
</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="slide-title">Trajectory consistency</div>

<div class="figure-card mt-6 h-[420px]">
  <img src="/figs/vis2.png" alt="Trajectory consistency" />
</div>

<div class="mt-6 text-center text-xl text-gray-200 leading-relaxed">
  Accumulated predictions follow the ground-truth anomaly regions over time, supporting motion and trajectory reasoning.
</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="slide-title">Failure modes and discussion</div>

<div class="grid grid-cols-3 gap-6 mt-12">
  <div v-click="1" class="card min-h-[240px]">
    <div class="text-2xl font-semibold text-orange-300">Micro-actions</div>
    <p class="text-lg mt-5 text-gray-200 leading-relaxed">
      Very small displacements can produce weak temporal differences and ambiguous trajectory evidence.
    </p>
  </div>

  <div v-click="2" class="card min-h-[240px]">
    <div class="text-2xl font-semibold text-blue-300">Nonrigid motion</div>
    <p class="text-lg mt-5 text-gray-200 leading-relaxed">
      Highly nonrigid or scattered motion may diffuse heatmap activation across multiple body parts or regions.
    </p>
  </div>

  <div v-click="3" class="card min-h-[240px]">
    <div class="text-2xl font-semibold text-pink-300">Scene-dependent appearance</div>
    <p class="text-lg mt-5 text-gray-200 leading-relaxed">
      Specularities, fog, scale changes, and partial occlusion can degrade target appearance descriptions.
    </p>
  </div>
</div>

<div v-click="4" class="absolute bottom-20 left-20 right-20 callout text-xl text-center">
  Use this slide as Q&A backup: it prevents the presentation from sounding over-claimed.
</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="slide-title">Takeaway</div>

<div class="grid grid-cols-[0.9fr_1.1fr] gap-8 mt-8 items-start">
  <div>
    <div class="text-4xl font-semibold leading-tight">
      T-VAU closes the loop from
      <span class="text-green-300">pixel evidence</span>
      to
      <span class="text-pink-300">language reasoning</span>.
    </div>

    <div class="mt-8 space-y-4 text-lg">
      <div v-click="1" class="card">AHD: threshold-free spatio-temporal anomaly heatmaps</div>
      <div v-click="2" class="card">RAE: region-aware and motion-aware prompt injection</div>
      <div v-click="3" class="card">Dataset: target-level appearance, localization, and trajectory supervision</div>
    </div>
  </div>

  <div class="figure-card h-[445px]">
    <img src="/figs/teaser.png" alt="T-VAU teaser" />
  </div>
</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

---

<div class="title-page">
  <div>
    <div class="section-title">Thank you</div>
    <div class="mt-10 text-2xl text-gray-200">Questions?</div>
    <div class="mt-8 text-lg text-gray-300 leading-relaxed">
      Acknowledgments: Alex Chapiro; HPC system at the United Arab Emirates University.
    </div>
    <div class="badge-row">
      <span class="badge">T-VAU</span>
      <span class="badge">AHD</span>
      <span class="badge">RAE</span>
      <span class="badge">Fine-grained Video Anomaly Understanding</span>
    </div>
  </div>
</div>
<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>
