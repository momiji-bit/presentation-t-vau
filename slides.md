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
  background: #000000;
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
.badge-row {
  display: grid;
  grid-template-columns: repeat(2, max-content);
  gap: 12px;
  margin-top: 28px;
  align-items: center;
}
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
      <span class="badge">Video Anomaly Understanding (VAU)</span>
      <span class="badge">Subtle Visual Computing</span>
      <span class="badge">Large Vision-Language Models (LVLMs)</span>
      <span class="badge">Evidence-grounded QA</span>
    </div>
  </div>
<div class="absolute bottom-20 right-80">
    <img src="./assets/CVPR_Denver_2026.jpg" alt="lab logo" class="h-[200px] opacity-100">
  </div>
  <div class="absolute bottom-20 right-14">
    <img src="./assets/logo.png" alt="lab logo" class="h-[200px] opacity-100">
  </div>


</div>

<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

<!--
Today I present T-VAU, a framework for fine-grained video anomaly understanding. The goal is simple: connect pixel-level evidence with language reasoning.
-->

---

<style>
.slidev-layout {
  min-height: 100%;
  width: 100%;
  padding: 34px 48px 34px;
  background: #000000;
  color: #f8fafc;
}


.title-page {
  min-height: 610px;
  display: grid;
  grid-template-columns: 1fr;
  gap: 44px;
  align-items: center;
}

.title-main {
  font-size: 56px;
  line-height: 1.02;
  font-weight: 780;
  letter-spacing: -.04em;
  max-width: 1120px;
  color: #f8fafc;
}
</style>

<div class="title-page">
  <div>
    <div class="title-main">Motivation</div>
  </div>
</div>


<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>


<!--
I will start with the motivation. The key issue is that subtle anomalies need both precise evidence and clear explanations.
-->

---

<style>
.slidev-layout {
  min-height: 100%;
  width: 100%;
  padding: 34px 48px 34px;
  background: #000000;
  color: #f8fafc;
}


.title-main {
  font-size: 46px;
  line-height: 1.02;
  font-weight: 780;
  letter-spacing: -.04em;
  max-width: 1120px;
  color: #f8fafc;
}
</style>

<div class="title-main">Existing paradigms are fragmented</div>

<div class="grid grid-cols-2 gap-5 mt-6">
  <div v-click="1" class="bg-white/10 rounded-xl p-5 shadow-lg border border-white/10">
    <div class="text-2xl font-semibold text-orange-300">Traditional IAD / VAD</div>
    <div class="text-sm mt-1 text-orange-100">Image Anomaly Detection / Video Anomaly Detection</div>
    <div class="text-lg mt-3 text-gray-200 leading-relaxed">
      Produces anomaly scores or heatmaps, but usually lacks semantic explanation.
    </div>
    <div class="mt-4 bg-slate-900/80 rounded-lg p-3 text-gray-300">
      Output: score / heatmap only
    </div>
    <div class="mt-3 text-xs text-gray-400">Rep. works: Sultani et al. (UCF-Crime), CVPR 2018; Bergmann et al. (MVTec AD), CVPR 2019</div>
  </div>


  <div v-click="2" class="bg-white/10 rounded-xl p-5 shadow-lg border border-white/10">
    <div class="text-2xl font-semibold text-green-300">General LVLMs</div>
    <div class="text-sm mt-1 text-green-100">Large Vision-Language Models</div>
    <div class="text-lg mt-3 text-gray-200 leading-relaxed">
      Can answer in language, but often fails to ground subtle cues at pixel level.
    </div>
    <div class="mt-4 bg-slate-900/80 rounded-lg p-3 text-gray-300">
      Output: judgment without explicit evidence
    </div>
    <div class="mt-3 text-xs text-gray-400">Rep. works: Liu et al. (LLaVA), NeurIPS 2023; Bai et al. (Qwen-VL), arXiv 2023</div>
  </div>



  <div v-click="3" class="bg-white/10 rounded-xl p-5 shadow-lg border border-white/10">
    <div class="text-2xl font-semibold text-blue-300">LVLM + Diffusion hybrids</div>
    <div class="text-sm mt-1 text-blue-100">Language reasoning with generative visualization</div>
    <div class="text-lg mt-3 text-gray-200 leading-relaxed">
      Combine text and visualization, but generated explanations may be unstable or inconsistent.
    </div>
    <div class="mt-4 bg-slate-900/80 rounded-lg p-3 text-gray-300">
      Output: judgment + generated visualization
    </div>
    <div class="mt-3 text-xs text-gray-400">Rep. works: Wang et al. (LaVin-DiT), CVPR 2025; Li et al. (Dual Diffusion), CVPR 2025</div>
  </div>


  <div v-click="4" class="bg-pink-500/20 rounded-xl p-5 shadow-lg border border-pink-300/30">
    <div class="text-2xl font-semibold text-pink-300">T-VAU</div>
    <div class="text-sm mt-1 text-pink-100">Text-guided Fine-Grained Video Anomaly Understanding</div>
    <div class="text-lg mt-3 text-gray-100 leading-relaxed">
      Couples pixel-level anomaly evidence with language reasoning.
    </div>
    <div class="mt-4 bg-slate-900/80 rounded-lg p-3 text-gray-100">
      Output: detection + localization + identification + trajectory + explanation
    </div>
    <div class="mt-3 text-xs text-pink-100">This work: Gu et al., CVPRW SVC 2026</div>
  </div>

</div>

<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>


<!--
Existing paradigms solve only part of the problem. Traditional IAD and VAD give scores or heatmaps, while LVLMs give text but often miss pixel-level grounding. T-VAU connects these two sides.
-->

---

<style>
.slidev-layout {
  min-height: 100%;
  width: 100%;
  padding: 34px 48px 34px;
  background: #000000;
  color: #f8fafc;
}
.title-main {
  font-size: 46px;
  line-height: 1.02;
  font-weight: 780;
  letter-spacing: -.04em;
  max-width: 1120px;
  color: #f8fafc;
}
</style>


<div class="title-main">What does video anomaly detection need to achieve?</div>

<div class="absolute left-12 top-35 w-[520px]">
  <div class="text-3xl font-semibold leading-snug">
    A video anomaly should be<br />
    <span class="whitespace-nowrap">
      <span class="text-pink-300">detected</span>,
      <span class="text-blue-300">localized</span> and
      <span class="text-green-300">explained</span>.
    </span>
  </div>


  <div class="mt-8 text-xl text-gray-200 leading-relaxed">
    Fine-grained anomaly understanding asks the model to answer:
  </div>


  <div class="mt-6 space-y-4 text-lg">
    <div v-click="1" class="bg-white/10 rounded-lg p-4">Is there any anomaly?</div>
    <div v-click="2" class="bg-white/10 rounded-lg p-4">Where are the abnormal pixels?</div>
    <div v-click="3" class="bg-white/10 rounded-lg p-4">What is the target's appearance?</div>
    <div v-click="4" class="bg-white/10 rounded-lg p-4">How does the target move, and why is it abnormal?</div>
  </div>

</div>

<div class="absolute right-12 top-46">
  <div class="bg-white p-2 rounded-lg shadow-lg">
    <img src="./assets/tvau_teaser.png" alt="sensor" class="w-[560px] h-auto rounded" />
  </div>
</div>
<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<!--
For video anomalies, a yes-or-no answer is not enough. We need to know where the abnormal pixels are, what target is involved, and how its motion becomes abnormal.
-->

---

<style>
.slidev-layout {
  min-height: 100%;
  width: 100%;
  padding: 34px 48px 34px;
  background: #000000;
  color: #f8fafc;
}


.title-main {
  font-size: 46px;
  line-height: 1.02;
  font-weight: 780;
  letter-spacing: -.04em;
  max-width: 1120px;
  color: #f8fafc;
}
</style>

<div class="title-main">What T-VAU adds</div>

<div class="grid grid-cols-3 gap-6 mt-18">
  <div v-click="1" class="bg-white/10 rounded-xl p-6 border border-white/10 min-h-[270px]">
    <div class="text-2xl font-semibold text-blue-300">1. Pixel evidence</div>
    <p class="text-lg mt-5 leading-relaxed text-gray-200">
      Produce threshold-free spatio-temporal heatmaps instead of only clip-level anomaly scores.
    </p>
    <div class="mt-6 text-sm text-gray-400">
      Anomaly Heatmap Decoder <br>
      (AHD for pixel-level evidence)
    </div>
  </div>


  <div v-click="2" class="bg-white/10 rounded-xl p-6 border border-white/10 min-h-[270px]">
    <div class="text-2xl font-semibold text-orange-300">2. Region-aware prompting</div>
    <p class="text-lg mt-5 leading-relaxed text-gray-200">
      Convert heatmap dynamics into local, global, and learnable prompt embeddings for the LVLM.
    </p>
    <div class="mt-6 text-sm text-gray-400">
      Region-aware Anomaly Encoder <br>
      (RAE + evidence-conditioned prompts)
    </div>
  </div>


  <div v-click="3" class="bg-white/10 rounded-xl p-6 border border-white/10 min-h-[270px]">
    <div class="text-2xl font-semibold text-pink-300">3. Target-level supervision</div>
    <p class="text-lg mt-5 leading-relaxed text-gray-200">
      Provide aligned annotations for abnormal appearance, spatial localization, and motion trajectories.
    </p>
    <div class="mt-6 text-sm text-gray-400">
      Fine-grained anomaly annotations <br>
      (Appearance + localization + trajectory)
    </div>
  </div>

</div>

<div v-click="4" class="absolute bottom-20 left-20 right-20 text-2xl text-center italic text-gray-200">
  The core contribution is a closed loop: visual-text alignment → anomaly heatmaps → evidence-conditioned language reasoning.
</div>


<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>


<!--
T-VAU adds three pieces: pixel evidence, region-aware prompting, and target-level supervision. Together, they form a closed loop from visual-text alignment to heatmaps and then to language reasoning.
-->

---

<style>
.slidev-layout {
  min-height: 100%;
  width: 100%;
  padding: 34px 48px 34px;
  background: #000000;
  color: #f8fafc;
}


.title-page {
  min-height: 610px;
  display: grid;
  grid-template-columns: 1fr;
  gap: 44px;
  align-items: center;
}

.title-main {
  font-size: 56px;
  line-height: 1.02;
  font-weight: 780;
  letter-spacing: -.04em;
  max-width: 1120px;
  color: #f8fafc;
}
</style>

<div class="title-page">
  <div>
    <div class="title-main">Proposed Method</div>
  </div>
</div>
<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>


<!--
Next, I will describe the proposed method. The focus is how T-VAU turns visual evidence into prompts that an LVLM can use.
-->

---

<style>
.slidev-layout {
  min-height: 100%;
  width: 100%;
  padding: 34px 48px 34px;
  background: #000000;
  color: #f8fafc;
}


.title-main {
  font-size: 46px;
  line-height: 1.02;
  font-weight: 780;
  letter-spacing: -.04em;
  max-width: 1120px;
  color: #f8fafc;
}
.loc-box {
  position: absolute;
  border: 3px solid;
  border-radius: 8px;
  background: transparent;
  pointer-events: none;
  z-index: 20;
}

.loc-box-pink {
  border-color: #f9a8d4;
  box-shadow: 0 0 16px rgba(249, 168, 212, 0.55);
}

.loc-box-green {
  border-color: #86efac;
  box-shadow: 0 0 16px rgba(134, 239, 172, 0.55);
}

.loc-box-blue {
  border-color: #93c5fd;
  box-shadow: 0 0 16px rgba(147, 197, 253, 0.55);
}
</style>

<div class="title-main">T-VAU: closed-loop anomaly understanding</div>

<div class="absolute left-15 top-24 w-[1150px] text-xl leading-relaxed">
  Given a video clip and multi-turn queries, T-VAU predicts:


  <div class="mt-100 mx-auto w-[1100px] grid grid-cols-3 gap-10">
    <div v-click="1" class="bg-white/10 rounded-xl p-4 border border-white/10">
      <span class="text-pink-300 font-semibold">Pixel-level spatio-temporal heatmaps</span><br>
      Explicit anomaly evidence, <br> Anomaly Heatmaps
    </div>
    <div v-click="2" class="bg-white/10 rounded-xl p-4 border border-white/10">
      <span class="text-green-300 font-semibold">Language responses</span><br>
      Judgment, Appearance, Location, Motion, <br>Trajectory
    </div>
    <div v-click="3" class="bg-white/10 rounded-xl p-4 border border-white/10">
      <span class="text-blue-300 font-semibold">Trainable lightweight modules</span><br>
      <span class="text-gray-200">Frozen Qwen2.5-VL 7B backbone + AHD + RAE <br>+ LoRA prompt tuning.</span>
    </div>
  </div>

</div>

<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>


<div class="absolute left-45 top-35">
  <div class="bg-white p-2 rounded-lg shadow-lg">
    <img src="./assets/tvau_framework.png" class="w-[900px] h-auto rounded" />
  </div>
    <div class="caption text-center mt-1">
    Framework overview: Text Encoder + AHD + RAE + LVLM decoder.
  </div>
  <div v-click="1" class="loc-box loc-box-pink" style="left: 735px; top: 10px; width: 170px; height: 160px;" ></div>
  <div v-click="1" class="loc-box loc-box-pink" style="left: 170px; top: 10px; width: 170px; height: 320px;" ></div>
  <div v-click="2" class="loc-box loc-box-green" style="left: 3px; top: 3px; width: 160px; height: 335px;" ></div>
  <div v-click="3" class="loc-box loc-box-blue" style="left: 340px; top: 10px; width: 395px; height: 320px; " ></div>


</div>

<!--
Given a video and multi-turn questions, T-VAU outputs heatmaps and language answers. The backbone is frozen Qwen2.5-VL 7B, while AHD, RAE, and LoRA prompt tuning provide the trainable adaptation.
-->

---

<style>
.slidev-layout {
  min-height: 100%;
  width: 100%;
  padding: 34px 48px 34px;
  background: #000000;
  color: #f8fafc;
}


.title-main {
  font-size: 46px;
  line-height: 1.02;
  font-weight: 780;
  letter-spacing: -.04em;
  max-width: 1120px;
  color: #f8fafc;
}
</style>

<div class="title-main">Key idea</div>

<div class="grid grid-cols-3 gap-6 mt-18">
  <div v-click="1" class="bg-white/10 rounded-xl p-6 border border-white/10 min-h-[270px]">
    <div class="text-2xl font-semibold text-blue-300">1. Align</div>
    <p class="text-lg mt-5 leading-relaxed text-gray-200">
      Use normal / abnormal text prompts to align intermediate visual tokens with semantic anomaly concepts.
    </p>
    <div class="mt-6 text-sm text-gray-400">Visual-text similarity <br>(Element-wise cosine similarity)</div>
  </div>


  <div v-click="2" class="bg-white/10 rounded-xl p-6 border border-white/10 min-h-[270px]">
    <div class="text-2xl font-semibold text-orange-300">2. Ground</div>
    <p class="text-lg mt-5 leading-relaxed text-gray-200">
      Fuse similarity maps from multiscale ViT features to decode threshold-free heatmaps.
    </p>
    <div class="mt-6 text-sm text-gray-400">Anomaly Heatmap Decoder <br>(Similarity-Aware Fusion + AHD)</div>
  </div>


  <div v-click="3" class="bg-white/10 rounded-xl p-6 border border-white/10 min-h-[270px]">
    <div class="text-2xl font-semibold text-pink-300">3. Reason</div>
    <p class="text-lg mt-5 leading-relaxed text-gray-200">
      Convert heatmap evidence into region-aware prompts and inject them into the LVLM.
    </p>
    <div class="mt-6 text-sm text-gray-400">Region-aware Anomaly Encoder <br>(RAE + dialogue context)</div>
  </div>

</div>

<div v-click="4" class="absolute bottom-20 left-20 right-20 text-2xl text-center italic text-gray-200">
  Low-level anomaly evidence becomes structured language reasoning.
</div>


<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>


<!--
The method has three steps. First, align visual tokens with normal and abnormal text prompts. Then ground the anomaly as heatmaps, and finally use those heatmaps for reasoning.
-->

---


<style>
.slidev-layout {
  min-height: 100%;
  width: 100%;
  padding: 34px 48px 34px;
  background: #000000;
  color: #f8fafc;
}


.title-main {
  font-size: 46px;
  line-height: 1.02;
  font-weight: 780;
  letter-spacing: -.04em;
  max-width: 1120px;
  color: #f8fafc;
}
</style>

<div class="title-main">Anomaly Heatmap Decoder (AHD)</div>

<div class="absolute left-10 top-24 w-[470px]">
  <div class="text-2xl font-semibold text-green-300">Purpose</div>
  <p class="text-lg mt-3 text-gray-200 leading-relaxed">
    Generate pixel-level anomaly heatmaps by aligning visual tokens with text prompts.
  </p>


  <div class="mt-8 space-y-3 text-lg">
    <div v-click="1" class="bg-white/10 rounded-lg p-3">Text prompts: normal vs. abnormal</div>
    <div v-click="2" class="bg-white/10 rounded-lg p-3">Multiscale visual tokens: blocks 1, 8, 16, 32</div>
    <div v-click="3" class="bg-white/10 rounded-lg p-3">Similarity-Aware Fusion: <br>cosine similarity + weighted sum</div>
    <div v-click="4" class="bg-white/10 rounded-lg p-3">


Softmax anomaly channel → heatmap $\mathbf{H}$

</div>
  </div>
</div>

<div class="absolute right-20 top-30 w-[550px]">
  <div class="bg-white p-2 rounded-lg shadow-lg">
    <img src="./assets/AHD.png" class="w-full rounded" />
  </div>
  <div class="text-center text-sm text-gray-400 mt-2">
    Focus: Text Encoder + AHD + Similarity-Aware Fusion
  </div>
</div>


<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>


<!--
AHD compares multiscale visual tokens from blocks 1, 8, 16, and 32 with normal and abnormal text embeddings. The fused similarity maps are passed through softmax, and the abnormal channel becomes the heatmap.
-->

---

<style>
.slidev-layout {
  min-height: 100%;
  width: 100%;
  padding: 34px 48px 34px;
  background: #000000;
  color: #f8fafc;
}


.title-main {
  font-size: 46px;
  line-height: 1.02;
  font-weight: 780;
  letter-spacing: -.04em;
  max-width: 1120px;
  color: #f8fafc;
}
</style>

<div class="title-main">Region-aware Anomaly Encoder (RAE)</div>

<div class="absolute left-10 top-24 w-[500px]">
  <div class="text-2xl font-semibold text-orange-300">Purpose</div>
  <p class="text-lg mt-3 text-gray-200 leading-relaxed">
    Transform heatmap evidence into prompts that the LVLM can use for multi-turn reasoning.
  </p>


  <div class="mt-8 space-y-3 text-lg">
  <div v-click="1" class="bg-white/10 rounded-lg p-3">


Temporal difference: $\Delta\mathbf{H}_c$ captures motion cues

  </div>

  <div v-click="2" class="bg-white/10 rounded-lg p-3">Lightweight convolutional backbone extracts region-aware features</div>
  <div v-click="3" class="bg-white/10 rounded-lg p-3">


$3\times3$ regional pooling captures local evidence

</div>

  <div v-click="4" class="bg-white/10 rounded-lg p-3">Global pooling + learnable base tokens capture clip-level anomaly context</div>

  </div>
  </div>

<div class="absolute right-20 top-30 w-[550px]">
  <div class="bg-white p-2 rounded-lg shadow-lg">
    <img src="./assets/RAE.png" class="w-full rounded" />
  </div>
  <div class="text-center text-sm text-gray-400 mt-2">
    Focus: heatmap evidence → region-aware prompt embedding → LVLM response
  </div>
</div>


<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>



<!--
RAE starts from the heatmap sequence and its temporal differences. It extracts local grid features, global context, and learnable base prompts, then maps them into the LVLM prompt space.
-->

---

<style>
.slidev-layout {
  min-height: 100%;
  width: 100%;
  padding: 34px 48px 34px;
  background: #000000;
  color: #f8fafc;
}


.title-main {
  font-size: 46px;
  line-height: 1.02;
  font-weight: 780;
  letter-spacing: -.04em;
  max-width: 1120px;
  color: #f8fafc;
}
</style>

<div class="title-main">Multi-turn anomaly reasoning</div>

<div class="absolute left-14 top-30 w-[450px]">
  <div class="text-2xl font-semibold text-pink-300">Dialogue flow</div>


  <div class="mt-6 space-y-5 text-lg">
  <div v-click="1" class="bg-white/10 rounded-lg p-4">


  $Q_0$: Is there any anomaly in the video?

  </div>

  <div v-click="2" class="bg-white/10 rounded-lg p-4">


  $Q_1$: Describe anomaly target features.

  </div>

  <div v-click="3" class="bg-white/10 rounded-lg p-4">


  $Q_2$: What is the motion state?

  </div>

  <div v-click="4" class="bg-white/10 rounded-lg p-4">


  $Q_3$: From where to where?

  </div>
  </div>
</div>

<div class="absolute right-20 top-30 w-[550px]">
  <div class="bg-white p-2 rounded-lg shadow-lg">
    <img src="./assets/tvau_vis1.png" class="w-full rounded" />
  </div>
</div>


<div v-click="5" class="absolute bottom-20 left-20 right-20 text-2xl text-center italic text-gray-200">
  The language output is constrained by spatial and temporal evidence, reducing target drift and hallucinated explanations.
</div>


<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>



<!--
The dialogue moves from simple judgment to detailed reasoning. The model first decides whether an anomaly exists, then describes the target, motion state, and trajectory using the same evidence chain.
-->

---

<style>
.slidev-layout {
  min-height: 100%;
  width: 100%;
  padding: 34px 48px 34px;
  background: #000000;
  color: #f8fafc;
}


.title-page {
  min-height: 610px;
  display: grid;
  grid-template-columns: 1fr;
  gap: 44px;
  align-items: center;
}

.title-main {
  font-size: 56px;
  line-height: 1.02;
  font-weight: 780;
  letter-spacing: -.04em;
  max-width: 1120px;
  color: #f8fafc;
}
</style>

<div class="title-page">
  <div>
    <div class="title-main">Fine-grained Dataset Construction</div>
  </div>
</div>
<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>


<!--
Now I will move to dataset construction. This part is needed because fine-grained reasoning requires supervision beyond masks or scores.
-->

---

<style>
.slidev-layout {
  min-height: 100%;
  width: 100%;
  padding: 34px 48px 34px;
  background: #000000;
  color: #f8fafc;
}


.title-main {
  font-size: 46px;
  line-height: 1.02;
  font-weight: 780;
  letter-spacing: -.04em;
  max-width: 1120px;
  color: #f8fafc;
}
</style>

<div class="title-main">Why construct a new supervision pipeline?</div>

<div class="absolute left-15 top-30 w-[500px]">
  <div class="text-2xl font-semibold text-pink-300">
    Pixel masks alone do not teach the model to explain.
  </div>


  <div class="mt-8 space-y-6 text-lg">
    <div v-click="1" class="bg-white/10 rounded-xl p-4 border border-white/10">
      VAD labels: anomaly score / mask
    </div>
    <div v-click="2" class="bg-white/10 rounded-xl p-4 border border-white/10">
      Needed by T-VAU: target identity, appearance, position, motion, trajectory
    </div>
    <div v-click="3" class="bg-pink-500/20 rounded-xl p-4 border border-pink-300/20">
      Solution: target-level video-text annotations derived from ShanghaiTech and UBnormal
    </div>
  </div>

</div>

<div class="absolute right-20 top-30 w-[550px]">
  <div class="bg-white p-2 rounded-lg shadow-lg">
    <img src="./assets/ubnormal_examples.png" class="w-full rounded" />
  </div>
  <div class="text-center text-sm text-gray-400 mt-2">
    UBnormal dataset examples (label mask only)
  </div>
</div>
<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>


<!--
Pixel masks tell the model where the anomaly is, but not how to describe it. T-VAU needs target identity, appearance, position, motion, and trajectory, so we build target-level video-text annotations from ShanghaiTech and UBnormal.
-->

---

<style>
.slidev-layout {
  min-height: 100%;
  width: 100%;
  padding: 34px 48px 34px;
  background: #000000;
  color: #f8fafc;
}


.title-main {
  font-size: 46px;
  line-height: 1.02;
  font-weight: 780;
  letter-spacing: -.04em;
  max-width: 1120px;
  color: #f8fafc;
}
</style>

<div class="title-main">Dataset construction pipeline</div>

<div class="absolute top-25 left-1/2 -translate-x-1/2 w-[900px]">
  <div class="bg-white p-2 rounded-lg shadow-lg">
    <img src="./assets/tvau_dataset.png" class="w-full h-auto rounded" />
  </div>
</div>


<div class="absolute bottom-14 left-12 right-12 grid grid-cols-3 gap-4 text-base">
  <div v-click="1" class="bg-white/10 rounded-xl p-4 border border-white/10">
  <span class="text-blue-300 font-semibold">Step 1</span><br>
  Frame-level structured prompting and temporal aggregation.
  </div>
  <div v-click="2" class="bg-white/10 rounded-xl p-4 border border-white/10">
    <span class="text-orange-300 font-semibold">Step 2</span><br>
    Mask-guided refinement with Gaussian-blurred background suppression.
  </div>
  <div v-click="3" class="bg-white/10 rounded-xl p-4 border border-white/10">
    <span class="text-green-300 font-semibold">Step 3</span><br>
    Cross-modal consistency verification between appearance and motion.
  </div>
</div>
<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>


<!--
The pipeline has three stages. We first extract frame-level structure, then refine it with anomaly masks and background suppression, and finally verify consistency between appearance and motion.
-->

---

<style>
.slidev-layout {
  min-height: 100%;
  width: 100%;
  padding: 34px 48px 34px;
  background: #000000;
  color: #f8fafc;
}


.title-main {
  font-size: 46px;
  line-height: 1.02;
  font-weight: 780;
  letter-spacing: -.04em;
  max-width: 1120px;
  color: #f8fafc;
}
</style>

<div class="title-main">Resulting supervision</div>

<div class="grid grid-cols-3 gap-6 mt-20">
  <div v-click="1" class="bg-white/10 rounded-xl p-6 border border-white/10 min-h-[230px]">
    <div class="text-2xl font-semibold text-blue-300">Appearance</div>
    <p class="text-lg mt-5 text-gray-200 leading-relaxed">
      Target-level attributes such as clothing, object type, and visible distinguishing cues.
    </p>
  </div>


  <div v-click="2" class="bg-white/10 rounded-xl p-6 border border-white/10 min-h-[230px]">
    <div class="text-2xl font-semibold text-green-300">Spatio-temporal localization</div>
    <p class="text-lg mt-5 text-gray-200 leading-relaxed">
      Frame-wise target location and abnormal period supervision.
    </p>
  </div>


  <div v-click="3" class="bg-white/10 rounded-xl p-6 border border-white/10 min-h-[230px]">
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


<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>


<!--
The resulting supervision covers appearance, localization, and trajectory. It includes 4,108 training and 1,028 validation frame-wise annotations for ShanghaiTech, plus 5,136 ShanghaiTech and 7,912 UBnormal target-aligned descriptions.
-->

---

<style>
.slidev-layout {
  min-height: 100%;
  width: 100%;
  padding: 34px 48px 34px;
  background: #000000;
  color: #f8fafc;
}


.title-page {
  min-height: 610px;
  display: grid;
  grid-template-columns: 1fr;
  gap: 44px;
  align-items: center;
}

.title-main {
  font-size: 56px;
  line-height: 1.02;
  font-weight: 780;
  letter-spacing: -.04em;
  max-width: 1120px;
  color: #f8fafc;
}
</style>

<div class="title-page">
  <div>
    <div class="title-main">Experiments</div>
  </div>
</div>
<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>


<!--
Next are the experiments. I will show localization, dialogue evaluation, ablation, and qualitative results.
-->

---

<style>
.slidev-layout {
  min-height: 100%;
  width: 100%;
  padding: 34px 48px 34px;
  background: #000000;
  color: #f8fafc;
}


.title-main {
  font-size: 46px;
  line-height: 1.02;
  font-weight: 780;
  letter-spacing: -.04em;
  max-width: 1120px;
  color: #f8fafc;
}
</style>

<div class="title-main">Anomaly localization on UBnormal</div>

<div class="absolute left-12 top-35 w-[500px]">
  <div class="text-2xl font-semibold text-pink-300">AHD achieves strong localization</div>
  <p class="text-lg mt-4 text-gray-200 leading-relaxed">
    Fine-tuned AHD improves micro-AUC, RBDC, and TBDC over prior baselines. Macro-AUC remains lower than the strongest multi-stream baseline.
  </p>


  <div class="mt-8 grid grid-cols-2 gap-4">
    <div v-click="1" class="bg-white/10 rounded-xl p-5 text-center">
      <div class="text-4xl font-bold text-green-300">94.8</div>
      <div class="text-gray-300 mt-2">Micro-AUC</div>
    </div>
    <div v-click="2" class="bg-white/10 rounded-xl p-5 text-center">
      <div class="text-4xl font-bold text-green-300">87.8</div>
      <div class="text-gray-300 mt-2">Macro-AUC</div>
    </div>
    <div v-click="3" class="bg-white/10 rounded-xl p-5 text-center">
      <div class="text-4xl font-bold text-green-300">67.8</div>
      <div class="text-gray-300 mt-2">RBDC</div>
    </div>
    <div v-click="4" class="bg-white/10 rounded-xl p-5 text-center">
      <div class="text-4xl font-bold text-green-300">76.7</div>
      <div class="text-gray-300 mt-2">TBDC</div>
    </div>
  </div>

</div>

<div v-click="5" class="absolute right-20 top-40 w-[600px]">
  <table class="w-full text-xs bg-white/10 rounded-lg overflow-hidden border-collapse">
    <thead class="bg-white/20">
      <tr class="border-b border-white/20">
        <th rowspan="3" class="p-2 text-left align-middle">Method</th>
        <th colspan="4" class="p-2 text-center">Validation</th>
      </tr>
      <tr class="border-b border-white/20">
        <th colspan="2" class="p-2 text-center">AUC</th>
        <th rowspan="2" class="p-2 text-center align-middle">RBDC ↑</th>
        <th rowspan="2" class="p-2 text-center align-middle">TBDC ↑</th>
      </tr>
      <tr class="border-b border-white/20">
        <th class="p-2 text-center">Micro ↑</th>
        <th class="p-2 text-center">Macro ↑</th>
      </tr>
    </thead>
    <tbody>
      <tr class="border-t border-white/10">
        <td class="p-2">Georgescu et al.</td>
        <td class="p-2 text-center">58.5</td>
        <td class="p-2 text-center bg-green-400/20">94.4</td>
        <td class="p-2 text-center">18.580</td>
        <td class="p-2 text-center">48.213</td>
      </tr>
      <tr class="border-t border-white/10">
        <td class="p-2">Georgescu et al. (FT)</td>
        <td class="p-2 text-center">68.2</td>
        <td class="p-2 text-center bg-green-400/40 font-semibold">95.3</td>
        <td class="p-2 text-center">28.654</td>
        <td class="p-2 text-center">58.097</td>
      </tr>
      <tr class="border-t border-white/20">
        <td class="p-2">Sultani et al. (PT)</td>
        <td class="p-2 text-center">61.1</td>
        <td class="p-2 text-center">89.4</td>
        <td class="p-2 text-center">0.001</td>
        <td class="p-2 text-center">0.012</td>
      </tr>
      <tr class="border-t border-white/10">
        <td class="p-2">Sultani et al. (FT)</td>
        <td class="p-2 text-center">51.8</td>
        <td class="p-2 text-center">88.0</td>
        <td class="p-2 text-center">0.001</td>
        <td class="p-2 text-center">0.001</td>
      </tr>
      <tr class="border-t border-white/20">
        <td class="p-2">Bertasius et al. (FT, SR=1/32)</td>
        <td class="p-2 text-center">86.1</td>
        <td class="p-2 text-center">89.2</td>
        <td class="p-2 text-center">0.008</td>
        <td class="p-2 text-center">0.021</td>
      </tr>
      <tr class="border-t border-white/10">
        <td class="p-2">Bertasius et al. (FT, SR=1/8)</td>
        <td class="p-2 text-center">83.4</td>
        <td class="p-2 text-center">90.6</td>
        <td class="p-2 text-center">0.009</td>
        <td class="p-2 text-center">0.023</td>
      </tr>
      <tr class="border-t border-white/10">
        <td class="p-2">Bertasius et al. (FT, SR=1/4)</td>
        <td class="p-2 text-center">78.5</td>
        <td class="p-2 text-center">89.2</td>
        <td class="p-2 text-center">0.006</td>
        <td class="p-2 text-center">0.018</td>
      </tr>
      <tr class="border-t border-white/20">
        <td class="p-2 font-semibold">AHD (1S)</td>
        <td class="p-2 text-center bg-green-400/20 font-semibold">94.5</td>
        <td class="p-2 text-center">85.2</td>
        <td class="p-2 text-center bg-green-400/20 font-semibold">64.300</td>
        <td class="p-2 text-center bg-green-400/20 font-semibold">74.400</td>
      </tr>
      <tr class="border-t border-white/10 bg-pink-500/20">
        <td class="p-2 font-semibold">AHD (FT)</td>
        <td class="p-2 text-center bg-green-400/40 font-semibold">94.8</td>
        <td class="p-2 text-center font-semibold">87.8</td>
        <td class="p-2 text-center bg-green-400/40 font-semibold">67.800</td>
        <td class="p-2 text-center bg-green-400/40 font-semibold">76.700</td>
      </tr>
    </tbody>
  </table>


  <div class="text-xs text-gray-400 mt-3 leading-relaxed text-center px-1">
  <span class="font-semibold text-gray-300">Experimental results on UBnormal.</span>
  We report micro-/macro-averaged frame-level AUC, RBDC, and TBDC (%) for the baselines
  Georgescu et al., Sultani et al., and Bertasius et al.
  PT, FT, and 1S denote pre-trained, fine-tuned, and one-shot; SR denotes frame sampling rate.
  Although only Georgescu et al. supports anomaly localization, we report RBDC and TBDC for all baselines for completeness.
  Best results are highlighted in bold with a green background.
</div>

</div>

<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>


<!--
On UBnormal, fine-tuned AHD reaches 94.8 micro-AUC, 87.8 macro-AUC, 67.8 RBDC, and 76.7 TBDC. It improves localization-oriented metrics over prior baselines, while macro-AUC remains below the strongest multi-stream baseline.
-->

---

<style>
.slidev-layout {
  min-height: 100%;
  width: 100%;
  padding: 34px 48px 34px;
  background: #000000;
  color: #f8fafc;
}


.title-main {
  font-size: 46px;
  line-height: 1.02;
  font-weight: 780;
  letter-spacing: -.04em;
  max-width: 1120px;
  color: #f8fafc;
}
</style>

<div class="title-main">Multi-turn dialogue evaluation</div>

<div class="absolute left-12 top-35 w-[500px]">
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

<div v-click="4" class="absolute right-6 top-48 w-[660px]">
  <table class="w-full text-[10px] bg-white/10 rounded-lg overflow-hidden border-collapse">
    <thead class="bg-white/20">
      <tr class="border-b border-white/20">
        <th rowspan="3" class="p-1.5 text-left align-middle">Method</th>
        <th rowspan="3" class="p-1.5 text-center align-middle">Size ↓</th>
        <th colspan="3" class="p-1.5 text-center">ShanghaiTech</th>
        <th colspan="3" class="p-1.5 text-center">UBnormal</th>
      </tr>
      <tr class="border-b border-white/20">
        <th colspan="2" class="p-1.5 text-center">BLEU-4 ± Std ↑</th>
        <th class="p-1.5 text-center">Acc. ± Std ↑</th>
        <th colspan="2" class="p-1.5 text-center">BLEU-4 ± Std ↑</th>
        <th class="p-1.5 text-center">Acc. ± Std ↑</th>
      </tr>
      <tr class="border-b border-white/20">
        <th class="p-1.5 text-center">Target</th>
        <th class="p-1.5 text-center">Trajectory</th>
        <th class="p-1.5 text-center">Yes/No</th>
        <th class="p-1.5 text-center">Target</th>
        <th class="p-1.5 text-center">Trajectory</th>
        <th class="p-1.5 text-center">Yes/No</th>
      </tr>
    </thead>
    <tbody>
      <tr class="border-t border-white/10">
        <td class="p-1.5">Qwen2.5-VL (zero-shot)</td>
        <td class="p-1.5 text-center">7B</td>
        <td class="p-1.5 text-center">18.74 ± 0.82</td>
        <td class="p-1.5 text-center">27.33 ± 1.05</td>
        <td class="p-1.5 text-center">61.03 ± 0.38%</td>
        <td class="p-1.5 text-center">16.20 ± 0.85</td>
        <td class="p-1.5 text-center">24.18 ± 1.08</td>
        <td class="p-1.5 text-center">65.62 ± 0.41%</td>
      </tr>
      <tr class="border-t border-white/10">
        <td class="p-1.5">Qwen2.5-VL (one-shot)</td>
        <td class="p-1.5 text-center">7B</td>
        <td class="p-1.5 text-center">50.42 ± 0.58</td>
        <td class="p-1.5 text-center">78.91 ± 0.72</td>
        <td class="p-1.5 text-center">92.36 ± 0.24%</td>
        <td class="p-1.5 text-center">44.35 ± 0.62</td>
        <td class="p-1.5 text-center">70.82 ± 0.75</td>
        <td class="p-1.5 text-center">87.24 ± 0.27%</td>
      </tr>
      <tr class="border-t border-white/10">
        <td class="p-1.5">LLaVA-1.6 (one-shot)</td>
        <td class="p-1.5 text-center">7B</td>
        <td class="p-1.5 text-center">47.68 ± 0.60</td>
        <td class="p-1.5 text-center">75.42 ± 0.74</td>
        <td class="p-1.5 text-center">91.07 ± 0.26%</td>
        <td class="p-1.5 text-center">42.11 ± 0.64</td>
        <td class="p-1.5 text-center">68.07 ± 0.78</td>
        <td class="p-1.5 text-center">85.91 ± 0.28%</td>
      </tr>
      <tr class="border-t border-white/10">
        <td class="p-1.5">MiniCPM-V 2.6 (one-shot)</td>
        <td class="p-1.5 text-center">7B</td>
        <td class="p-1.5 text-center">52.34 ± 0.54</td>
        <td class="p-1.5 text-center">80.41 ± 0.69</td>
        <td class="p-1.5 text-center">93.11 ± 0.23%</td>
        <td class="p-1.5 text-center">46.70 ± 0.59</td>
        <td class="p-1.5 text-center bg-green-400/20">72.88 ± 0.73</td>
        <td class="p-1.5 text-center">86.94 ± 0.26%</td>
      </tr>
      <tr class="border-t border-white/10">
        <td class="p-1.5">Idefics2 (one-shot)</td>
        <td class="p-1.5 text-center">8B</td>
        <td class="p-1.5 text-center">44.29 ± 0.62</td>
        <td class="p-1.5 text-center">73.84 ± 0.76</td>
        <td class="p-1.5 text-center">90.12 ± 0.27%</td>
        <td class="p-1.5 text-center">39.51 ± 0.66</td>
        <td class="p-1.5 text-center">65.92 ± 0.80</td>
        <td class="p-1.5 text-center">84.03 ± 0.29%</td>
      </tr>
      <tr class="border-t border-white/10">
        <td class="p-1.5">InternVL (one-shot)</td>
        <td class="p-1.5 text-center">8B</td>
        <td class="p-1.5 text-center bg-green-400/20">55.73 ± 0.50</td>
        <td class="p-1.5 text-center bg-green-400/20">82.65 ± 0.66</td>
        <td class="p-1.5 text-center bg-green-400/20">94.28 ± 0.22%</td>
        <td class="p-1.5 text-center bg-green-400/20">49.84 ± 0.55</td>
        <td class="p-1.5 text-center">71.63 ± 0.70</td>
        <td class="p-1.5 text-center bg-green-400/20">88.65 ± 0.24%</td>
      </tr>
      <tr class="border-t-2 border-white/30 bg-pink-500/20">
        <td class="p-1.5 font-semibold">RAE (Ours) (one-shot)</td>
        <td class="p-1.5 text-center font-semibold">7B</td>
        <td class="p-1.5 text-center bg-green-400/40 font-semibold">62.67 ± 0.45</td>
        <td class="p-1.5 text-center bg-green-400/40 font-semibold">88.84 ± 0.53</td>
        <td class="p-1.5 text-center bg-green-400/40 font-semibold">97.67 ± 0.12%</td>
        <td class="p-1.5 text-center bg-green-400/40 font-semibold">50.32 ± 0.49</td>
        <td class="p-1.5 text-center bg-green-400/40 font-semibold">78.10 ± 0.58</td>
        <td class="p-1.5 text-center bg-green-400/40 font-semibold">89.73 ± 0.18%</td>
      </tr>
    </tbody>
  </table>
  <div class="text-xs text-gray-400 mt-3 leading-relaxed text-center px-1">
  <span class="font-semibold text-gray-300">One-shot evaluation results of representative LVLMs on our constructed dataset.</span>
  “Size” denotes the number of model parameters in billions.
  BLEU-4 is reported for Target and Trajectory, and Accuracy for Yes/No.
  All metrics are in percentages.
  Our <span class="font-semibold text-pink-300">RAE</span> performs best across tasks.
</div>
</div>


<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>


<!--
For multi-turn dialogue, RAE gives the best one-shot results in this table. On ShanghaiTech it reaches 62.67 Target BLEU-4, 88.84 Trajectory BLEU-4, and 97.67 percent Yes/No accuracy. On UBnormal it reaches 50.32 and 78.10 BLEU-4, with 89.73 percent Yes/No accuracy.
-->

---

<style>
.slidev-layout {
  min-height: 100%;
  width: 100%;
  padding: 34px 48px 34px;
  background: #000000;
  color: #f8fafc;
}


.title-main {
  font-size: 46px;
  line-height: 1.02;
  font-weight: 780;
  letter-spacing: -.04em;
  max-width: 1120px;
  color: #f8fafc;
}
</style>

<div class="title-main">Ablation: both modules are necessary</div>

<div class="absolute left-12 top-35 w-[500px]">
  <div class="text-2xl font-semibold text-pink-300">Complementary roles</div>
  <div class="mt-6 space-y-4 text-lg">
    <div v-click="1" class="bg-white/10 rounded-xl p-4 border border-white/10">
      <span class="text-green-300 font-semibold">AHD</span> supplies pixel-level evidence.
    </div>
    <div v-click="2" class="bg-white/10 rounded-xl p-4 border border-white/10">
      <span class="text-orange-300 font-semibold">RAE</span> makes this evidence usable by the LVLM.
    </div>
    <div v-click="3" class="bg-white/10 rounded-xl p-4 border border-white/10">
      Removing <span class="text-green-300 font-semibold">AHD</span> makes heatmap metrics inapplicable. <br>Removing <span class="text-orange-300 font-semibold">RAE</span> leaves heatmaps but removes evidence-conditioned dialogue.
    </div>
  </div>
</div>


<div v-click="4" class="absolute right-8 top-50 w-[660px]">
  <table class="w-full text-[10px] bg-white/10 rounded-lg overflow-hidden border-collapse">
    <thead class="bg-white/20">
      <tr class="border-b border-white/20">
        <th rowspan="2" class="p-1.5 text-left align-middle">Method</th>
        <th class="p-1.5 text-center">Size ↓</th>
        <th colspan="2" class="p-1.5 text-center">Heatmap (UBnormal) ↑</th>
        <th colspan="2" class="p-1.5 text-center">BLEU-4 (ShanghaiTech) ↑</th>
        <th class="p-1.5 text-center">Acc. (S.T.) ↑</th>
      </tr>
      <tr class="border-b border-white/20">
        <th class="p-1.5 text-center">Parameters</th>
        <th class="p-1.5 text-center">RBDC ± Std</th>
        <th class="p-1.5 text-center">TBDC ± Std</th>
        <th class="p-1.5 text-center">Target ± Std</th>
        <th class="p-1.5 text-center">Trajectory ± Std</th>
        <th class="p-1.5 text-center">Yes/No ± Std</th>
      </tr>
    </thead>
    <tbody>
      <tr class="border-t border-white/10">
        <td class="p-1.5">T-VAU w/o AHD</td>
        <td class="p-1.5 text-center">8299.71M</td>
        <td class="p-1.5 text-center">--</td>
        <td class="p-1.5 text-center">--</td>
        <td class="p-1.5 text-center">61.82 ± 0.42</td>
        <td class="p-1.5 text-center">85.47 ± 0.51</td>
        <td class="p-1.5 text-center">95.38 ± 0.18%</td>
      </tr>
      <tr class="border-t border-white/10">
        <td class="p-1.5">T-VAU w/o RAE</td>
        <td class="p-1.5 text-center">8317.13M</td>
        <td class="p-1.5 text-center">67.8 ± 0.36</td>
        <td class="p-1.5 text-center">76.7 ± 0.41</td>
        <td class="p-1.5 text-center">--</td>
        <td class="p-1.5 text-center">--</td>
        <td class="p-1.5 text-center">--</td>
      </tr>
      <tr class="border-t border-white/10">
        <td class="p-1.5">T-VAU w/o AHD & RAE</td>
        <td class="p-1.5 text-center">8274.74M</td>
        <td class="p-1.5 text-center">--</td>
        <td class="p-1.5 text-center">--</td>
        <td class="p-1.5 text-center">61.82 ± 0.42</td>
        <td class="p-1.5 text-center">85.47 ± 0.51</td>
        <td class="p-1.5 text-center">95.38 ± 0.18%</td>
      </tr>
      <tr class="border-t-2 border-white/30 bg-pink-500/20">
        <td class="p-1.5 font-semibold">T-VAU</td>
        <td class="p-1.5 text-center font-semibold">8324.67M</td>
        <td class="p-1.5 text-center font-semibold">67.8 ± 0.36</td>
        <td class="p-1.5 text-center font-semibold">76.7 ± 0.41</td>
        <td class="p-1.5 text-center font-semibold">62.67 ± 0.45</td>
        <td class="p-1.5 text-center font-semibold">88.84 ± 0.53</td>
        <td class="p-1.5 text-center font-semibold">97.67 ± 0.12%</td>
      </tr>
    </tbody>
  </table>
  <div class="text-xs text-gray-400 mt-3 leading-relaxed text-center px-1">
    <span class="font-semibold text-gray-300">Table:</span>
    Results of different <span class="font-semibold text-pink-300">T-VAU</span> variants.
    “Parameters/Size” denotes the number of model parameters in millions.
    Heatmap metrics include RBDC and TBDC.
    BLEU-4 is reported for both Target and Trajectory.
    Accuracy is evaluated on Yes/No classification.
  </div>
</div>


<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>


<!--
The ablation shows that AHD and RAE play different roles. AHD supplies local heatmap evidence, and RAE converts that evidence into useful language prompts. The full model gives the best complete result.
-->

---

<style>
.slidev-layout {
  min-height: 100%;
  width: 100%;
  padding: 34px 48px 34px;
  background: #000000;
  color: #f8fafc;
}


.title-page {
  min-height: 610px;
  display: grid;
  grid-template-columns: 1fr;
  gap: 44px;
  align-items: center;
}

.title-main {
  font-size: 56px;
  line-height: 1.02;
  font-weight: 780;
  letter-spacing: -.04em;
  max-width: 1120px;
  color: #f8fafc;
}
</style>

<div class="title-page">
  <div>
    <div class="title-main">Qualitative Results</div>
  </div>
</div>
<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>


<!--
Finally, I show qualitative results. These examples check whether the model's text is supported by spatial and temporal evidence.
-->

---

<style>
.slidev-layout {
  min-height: 100%;
  width: 100%;
  padding: 34px 48px 34px;
  background: #000000;
  color: #f8fafc;
}


.title-main {
  font-size: 46px;
  line-height: 1.02;
  font-weight: 780;
  letter-spacing: -.04em;
  max-width: 1120px;
  color: #f8fafc;
}
</style>

<div class="title-main">Evidence-grounded multi-turn QA</div>

<div class="absolute top-30 left-1/2 -translate-x-1/2 w-[1100px]">
  <div class="bg-white p-2 rounded-lg shadow-lg">
    <img src="./assets/tvau_vis1_1.png" class="w-full h-auto rounded" />
  </div>
</div>


<div class="absolute bottom-10 left-10 right-10 grid grid-cols-3 gap-4 text-base">
  <div v-click="1" class="bg-white/10 rounded-xl p-4 border border-white/10">
    <span class="text-green-300 font-semibold">AHD</span> localizes the abnormal target rather than the whole scene.
  </div>
  <div v-click="2" class="bg-white/10 rounded-xl p-4 border border-white/10">
    <span class="text-orange-300 font-semibold">RAE</span> guides target-specific appearance and motion descriptions.
  </div>
  <div v-click="3" class="bg-white/10 rounded-xl p-4 border border-white/10">
    The dialogue remains consistent across judgment, features, and trajectory.
  </div>
</div>


<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>


<!--
In these examples, AHD focuses on the anomalous target instead of the whole scene. RAE then keeps the answers consistent across anomaly judgment, appearance, motion, and trajectory.
-->

---

<style>
.slidev-layout {
  min-height: 100%;
  width: 100%;
  padding: 34px 48px 34px;
  background: #000000;
  color: #f8fafc;
}


.title-main {
  font-size: 46px;
  line-height: 1.02;
  font-weight: 780;
  letter-spacing: -.04em;
  max-width: 1120px;
  color: #f8fafc;
}
</style>

<div class="title-main">Trajectory consistency</div>

<div class="absolute top-35 left-6 right-6">
  <div class="bg-white p-2 rounded-lg shadow-lg">
    <img src="./assets/tvau_vis2.png" class="w-full h-auto rounded" />
  </div>
</div>


<div v-click="1" class="absolute bottom-20 left-20 right-20 text-2xl text-center italic text-gray-200">
  Accumulated predictions follow the ground-truth anomaly regions over time, supporting motion and trajectory reasoning.
</div>
<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<!--
The accumulated masks and boxes show how predictions move over time. The predicted trajectory follows the ground-truth anomaly regions, supporting the motion explanation.
-->

---

<style>
.slidev-layout {
  min-height: 100%;
  width: 100%;
  padding: 34px 48px 34px;
  background: #000000;
  color: #f8fafc;
}


.title-main {
  font-size: 46px;
  line-height: 1.02;
  font-weight: 780;
  letter-spacing: -.04em;
  max-width: 1120px;
  color: #f8fafc;
}
</style>

<div class="title-main">Takeaway</div>

<div class="absolute left-12 top-30 w-[530px]">
  <div class="text-4xl font-semibold leading-tight">
    T-VAU closes the loop from
    <span class="text-green-300">pixel evidence</span>
    to
    <span class="text-pink-300">language reasoning</span>.
  </div>


  <div class="mt-8 space-y-4 text-lg">
    <div v-click="1" class="bg-white/10 rounded-xl p-4 border border-white/10"><span class="text-green-300 font-semibold">AHD</span>: threshold-free spatio-temporal anomaly heatmaps</div>
    <div v-click="2" class="bg-white/10 rounded-xl p-4 border border-white/10"><span class="text-orange-300 font-semibold">RAE</span>: region-aware and motion-aware prompt injection</div>
    <div v-click="3" class="bg-white/10 rounded-xl p-4 border border-white/10"><span class="text-blue-300 font-semibold">Dataset</span>: target-level appearance, localization, and trajectory supervision</div>
  </div>

</div>

<div class="absolute right-12 top-35 w-[560px]">
  <div class="bg-white p-2 rounded-lg shadow-lg">
    <img src="./assets/tvau_teaser.png" class="w-full rounded" />
  </div>
</div>


<div v-click="4" class="absolute left-1/2 bottom-10 w-[900px] -translate-x-1/2 bg-white/10 rounded-xl px-4 py-3 border border-white/10">
  <div class="text-base font-semibold text-blue-300">Possible next directions</div>
  <div class="grid grid-cols-3 gap-3 mt-2 text-sm text-gray-200">
    <div class="bg-slate-900/70 rounded-lg px-3 py-2">Broader real-world scenes</div>
    <div class="bg-slate-900/70 rounded-lg px-3 py-2">Stronger long-term temporal reasoning</div>
    <div class="bg-slate-900/70 rounded-lg px-3 py-2">Efficient deployment for live video</div>
  </div>
</div>


<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>


<!--
The takeaway is that T-VAU closes the loop from pixel evidence to language reasoning. AHD localizes the anomaly, RAE injects the evidence into the LVLM, and the dataset supervises target-level appearance, localization, and trajectory.
-->

---

<style>
.slidev-layout {
  min-height: 100%;
  width: 100%;
  padding: 34px 48px 34px;
  background: #000000;
  color: #f8fafc;
}


.title-page {
  min-height: 610px;
  display: grid;
  grid-template-columns: 1fr;
  gap: 44px;
  align-items: center;
}

.title-main {
  font-size: 56px;
  line-height: 1.02;
  font-weight: 780;
  letter-spacing: -.04em;
  max-width: 1120px;
  color: #f8fafc;
}
</style>

<div class="absolute left-14 top-8 w-[800px]">


<div class="mt-8 flex items-center gap-4">
  <img
    src="./assets/profile.png"
    alt="profile photo"
    class="w-[160px] h-[160px] rounded-full object-cover border-2 border-white/20 shadow-lg"
  >
  <div>
    <div class="title-main">Thank you</div>
    <div class="mt-5 text-2xl text-gray-100"><b>Jihao (Geo) Gu</b></div>
    <div class="mt-5 text-2xl text-gray-100">momiji-bit.github.io</div>
  </div>
</div>




<div class="mt-8 bg-white/10 rounded-xl p-5 border border-white/10 text-gray-200">
  <div class="font-semibold text-pink-300 mb-3">BibTeX</div>


  <pre class="m-0 text-[13px] leading-relaxed font-mono whitespace-pre-wrap break-words text-gray-200"><code>@inproceedings{gu2026tvau,
  author    = {Gu, Jihao and Li, Kun and Wang, He and Ak{\c{s}}it, Kaan},
  title     = {Text-guided Fine-Grained Video Anomaly Understanding},
  booktitle = {Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition
               (CVPR) Workshops, 2nd Workshop on Subtle Visual Computing (SVC)},
  year      = {2026},
  address   = {Denver, CO, USA},
  url       = {https://openaccess.thecvf.com/content/CVPR2026W/SVC/html/Gu_Text-guided_Fine-Grained_Video_Anomaly_Understanding_CVPRW_2026_paper.html},
}</code></pre>

</div>

  <div class="mt-5 bg-blue-500/15 rounded-xl p-5 border border-blue-300/20 text-lg leading-relaxed text-blue-50">
    Acknowledgments: Alex Chapiro; HPC system at the United Arab Emirates University.
  </div>

</div>

<div class="absolute bottom-10 right-32">
    <img src="./assets/qr-code.png" alt="lab logo" class="h-[160px] opacity-100">
<a href="#" class="text-2xl text-gray-100 hover:text-blue-400 transition-colors font-semibold">Project Page</a>
  </div>
<div class="absolute bottom-65 right-23">
    <img src="./assets/logo.png" alt="lab logo" class="h-[200px] opacity-100">
  </div>
<div class="absolute right--3 up-20">
  <img src="./assets/CVPR_Logo1_Denver_2026_Color.png" alt="CVPR Denver" class="h-[210px] rounded-lg opacity-100">
</div>
<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<!--
Thank you. The main message is that subtle video anomalies need evidence-grounded reasoning, not only anomaly scores. I am happy to discuss questions.
-->
