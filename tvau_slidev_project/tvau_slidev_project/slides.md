---
theme: default
title: Text-guided Fine-Grained Video Anomaly Understanding
transition: slide-left
background: linear-gradient(135deg, #0f172a, #1e293b)
class: text-white
colorSchema: dark
fonts:
  sans: Inter
  serif: Georgia
  mono: Fira Code
---

<!-- Title -->
<h1 class="font-semibold tracking-tight leading-tight">
  Text-guided Fine-Grained Video Anomaly Understanding
</h1>

<p class="italic text-xl text-gray-300">
  From Pixel Evidence to Language Reasoning
</p>

<div class="text-lg text-gray-200 mt-4">
  <a href="https://momiji-bit.github.io"><span class="text-white font-bold">Jihao (Geo) Gu</span></a>,
  <a href="https://scholar.google.com/citations?user=UQ_bInoAAAAJ">Kun Li</a>,
  <a href="https://drhewang.com">He Wang</a>, and
  <a href="https://www.kaanaksit.com/">Kaan Akşit</a>
</div>

<div class="absolute bottom-12 left-14 text-sm text-gray-400">
  CVPR 2026 SVC Workshop
</div>

<div class="absolute bottom-12 right-14 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>
<!--
开场：今天介绍 T-VAU，一个面向 fine-grained video anomaly understanding 的框架。
核心信息不要讲成普通 VAD，而是强调 pixel-level evidence 和 language reasoning 的闭环。
-->

---

# Motivation

<br>

<div class="absolute left-20 top-28">
  <div class="bg-white p-2 rounded-lg shadow-lg relative inline-block">
    <video controls autoplay muted loop playsinline poster="/tvau_teaser.png" style="width: 700px; border-radius: 0.5rem;">
      <source src="/ai_motivation_anomaly.mp4" type="video/mp4">
    </video>
    <div class="absolute top-2 right-2 bg-black bg-opacity-60 text-white text-xs px-2 py-1 rounded-md">
      Optional: AI-generated content for motivation only
    </div>
  </div>
</div>

<div class="absolute right-16 top-36 w-78">
  <p class="text-2xl font-semibold text-pink-300">A practical question</p>
  <p class="text-xl mt-4 text-gray-200 leading-relaxed">
    When an anomaly happens, users need more than a score.
  </p>
  <div class="mt-6 space-y-3 text-lg">
    <div class="bg-white/10 rounded-lg p-3">Where is it?</div>
    <div class="bg-white/10 rounded-lg p-3">Which target causes it?</div>
    <div class="bg-white/10 rounded-lg p-3">How does it evolve over time?</div>
  </div>
</div>

<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<!--
这个 slide 可以放一个 AI-generated surveillance b-roll，和原模板中 Adobe Firefly 的用法一致。
注意只用于 motivation，不要把生成视频说成 benchmark 数据或真实实验结果。
-->

---
layout: cover
---

# Motivation

<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>
<!--
进入动机部分：现有方法各自只解决了一半问题。
-->

---

# Existing paradigms are fragmented

<div class="grid grid-cols-2 gap-6 mt-8">
  <div v-click="1" class="bg-white/10 rounded-xl p-6 shadow-lg border border-white/10">
    <div class="text-2xl font-semibold text-orange-300">Traditional IAD / VAD</div>
    <div class="text-lg mt-4 text-gray-200 leading-relaxed">
      Produces anomaly scores or heatmaps, but usually lacks semantic explanation.
    </div>
    <div class="mt-5 bg-slate-900/80 rounded-lg p-4 text-gray-300">
      Output: heatmap only
    </div>
  </div>

  <div v-click="2" class="bg-white/10 rounded-xl p-6 shadow-lg border border-white/10">
    <div class="text-2xl font-semibold text-green-300">General LVLMs</div>
    <div class="text-lg mt-4 text-gray-200 leading-relaxed">
      Can answer in language, but often fails to ground subtle cues at pixel level.
    </div>
    <div class="mt-5 bg-slate-900/80 rounded-lg p-4 text-gray-300">
      Output: judgment only
    </div>
  </div>

  <div v-click="3" class="bg-white/10 rounded-xl p-6 shadow-lg border border-white/10">
    <div class="text-2xl font-semibold text-blue-300">LVLM + Diffusion hybrids</div>
    <div class="text-lg mt-4 text-gray-200 leading-relaxed">
      Combine text and visualization, but generated explanations may be unstable or inconsistent.
    </div>
    <div class="mt-5 bg-slate-900/80 rounded-lg p-4 text-gray-300">
      Output: judgment + generated heatmap
    </div>
  </div>

  <div v-click="4" class="bg-pink-500/20 rounded-xl p-6 shadow-lg border border-pink-300/30">
    <div class="text-2xl font-semibold text-pink-300">T-VAU</div>
    <div class="text-lg mt-4 text-gray-100 leading-relaxed">
      Couples pixel-level anomaly evidence with language reasoning.
    </div>
    <div class="mt-5 bg-slate-900/80 rounded-lg p-4 text-gray-100">
      Output: detection + localization + identification + trajectory + explanation
    </div>
  </div>
</div>

<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>
---

# The gap: anomaly understanding requires evidence

<div class="absolute left-12 top-24 w-[520px]">
  <div class="text-3xl font-semibold leading-snug">
    An anomaly should be
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
    <div v-click="4" class="bg-white/10 rounded-lg p-4">What is the target's appearance and motion trajectory?</div>
  </div>
</div>

<div class="absolute right-12 top-22">
  <div class="bg-white p-2 rounded-lg shadow-lg">
    <img src="/tvau_teaser.png" class="w-[560px] h-auto rounded" />
  </div>
</div>

<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>
<!--
这页用 teaser 图直接说明文章定位。右图的底部五个 check mark 可以口头点出：Detection、Localization、Identification、Trajectory、Explanation。
-->

---
layout: cover
---

# Proposed Method

<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>
<!--
开始方法部分。方法讲法建议按输入输出、AHD、RAE、训练数据四步讲。
-->

---

# T-VAU: closed-loop anomaly understanding

<div class="absolute left-12 top-24 w-[460px] text-xl leading-relaxed">
  Given a video clip and multi-turn queries, T-VAU predicts:

  <div class="mt-6 space-y-4">
    <div v-click="1" class="bg-white/10 rounded-xl p-4 border border-white/10">
      <span class="text-pink-300 font-semibold">Pixel-level spatio-temporal heatmaps</span><br>
      explicit anomaly evidence
    </div>

    <div v-click="2" class="bg-white/10 rounded-xl p-4 border border-white/10">
      <span class="text-green-300 font-semibold">Language responses</span><br>
      judgment, appearance, location, motion, trajectory
    </div>
  </div>

  <div v-click="3" class="mt-8 bg-slate-900/80 rounded-lg p-4 text-[0.92em]">
    $\mathbf{H}, \mathbf{A}_t = \mathcal{M}(\mathcal{V}, \mathbf{Q}_{\leq t}, \mathbf{A}_{\leq t-1}, \mathcal{T}_c; \Theta)$
  </div>
</div>

<div class="absolute right-8 top-20">
  <div class="bg-white p-2 rounded-lg shadow-lg">
    <img src="/tvau_framework.png" class="w-[660px] h-auto rounded" />
  </div>
</div>

<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<!--
公式不是重点，重点是输入包括 video、multi-turn question、normal/abnormal prompts，输出同时包括 heatmap H 和 response A_t。
-->

---

# Key idea

<div class="grid grid-cols-3 gap-6 mt-12">
  <div v-click="1" class="bg-white/10 rounded-xl p-6 border border-white/10 min-h-[270px]">
    <div class="text-2xl font-semibold text-blue-300">1. Align</div>
    <p class="text-lg mt-5 leading-relaxed text-gray-200">
      Use normal / abnormal text prompts to align intermediate visual tokens with semantic anomaly concepts.
    </p>
    <div class="mt-6 text-sm text-gray-400">Visual-text similarity</div>
  </div>

  <div v-click="2" class="bg-white/10 rounded-xl p-6 border border-white/10 min-h-[270px]">
    <div class="text-2xl font-semibold text-orange-300">2. Ground</div>
    <p class="text-lg mt-5 leading-relaxed text-gray-200">
      Decode threshold-free spatio-temporal heatmaps from multiscale visual features.
    </p>
    <div class="mt-6 text-sm text-gray-400">Anomaly Heatmap Decoder</div>
  </div>

  <div v-click="3" class="bg-white/10 rounded-xl p-6 border border-white/10 min-h-[270px]">
    <div class="text-2xl font-semibold text-pink-300">3. Reason</div>
    <p class="text-lg mt-5 leading-relaxed text-gray-200">
      Convert heatmap evidence into region-aware prompts and inject them into the LVLM.
    </p>
    <div class="mt-6 text-sm text-gray-400">Region-aware Anomaly Encoder</div>
  </div>
</div>

<div v-click="4" class="absolute bottom-20 left-20 right-20 text-2xl text-center italic text-gray-200">
  Low-level anomaly evidence becomes structured language reasoning.
</div>

<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<!--
这页作为总览：align -> ground -> reason。后面两页分别展开 AHD 和 RAE。
-->

---

# Anomaly Heatmap Decoder (AHD)

<div class="absolute left-10 top-24 w-[470px]">
  <div class="text-2xl font-semibold text-green-300">Purpose</div>
  <p class="text-lg mt-3 text-gray-200 leading-relaxed">
    Generate pixel-level anomaly heatmaps by aligning visual tokens with text prompts.
  </p>

  <div class="mt-8 space-y-3 text-lg">
    <div v-click="1" class="bg-white/10 rounded-lg p-3">Text prompts: normal vs. abnormal</div>
    <div v-click="2" class="bg-white/10 rounded-lg p-3">Multiscale visual tokens: blocks 1, 8, 16, 32</div>
    <div v-click="3" class="bg-white/10 rounded-lg p-3">Similarity-Aware Fusion: cosine similarity + weighted sum</div>
    <div v-click="4" class="bg-white/10 rounded-lg p-3">Softmax anomaly channel → heatmap $\mathbf{H}$</div>
  </div>
</div>

<div class="absolute right-10 top-18 w-[650px]">
  <div class="bg-white p-2 rounded-lg shadow-lg">
    <img src="/tvau_framework.png" class="w-full rounded" />
  </div>
  <div class="text-center text-sm text-gray-400 mt-2">
    Focus: Text Encoder + AHD + Similarity-Aware Fusion
  </div>
</div>

<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<!--
讲 AHD 时不要整页推公式。用一句话概括：文本提供 anomaly/normal semantic anchor，视觉 token 提供空间位置，二者通过 cosine similarity 生成可解释 heatmap。
-->

---

# Region-aware Anomaly Encoder (RAE)

<div class="absolute left-10 top-24 w-[500px]">
  <div class="text-2xl font-semibold text-orange-300">Purpose</div>
  <p class="text-lg mt-3 text-gray-200 leading-relaxed">
    Transform heatmap evidence into prompts that the LVLM can use for multi-turn reasoning.
  </p>

  <div class="mt-8 space-y-3 text-lg">
    <div v-click="1" class="bg-white/10 rounded-lg p-3">Temporal difference: $\Delta \mathbf{H}$ captures motion cues</div>
    <div v-click="2" class="bg-white/10 rounded-lg p-3">3×3 regional pooling captures local evidence</div>
    <div v-click="3" class="bg-white/10 rounded-lg p-3">Global pooling captures clip-level anomaly context</div>
    <div v-click="4" class="bg-white/10 rounded-lg p-3">Base + region + global prompts are concatenated with video and dialogue prompts</div>
  </div>
</div>

<div class="absolute right-10 top-18 w-[650px]">
  <div class="bg-white p-2 rounded-lg shadow-lg">
    <img src="/tvau_framework.png" class="w-full rounded" />
  </div>
  <div class="text-center text-sm text-gray-400 mt-2">
    Focus: heatmap evidence → region-aware prompt embedding → LVLM response
  </div>
</div>

<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<!--
RAE 的关键卖点：不是把 heatmap 当成可视化结果，而是作为 prompt embedding 进入 LVLM semantic space。
-->

---

# Multi-turn anomaly reasoning

<div class="absolute left-14 top-24 w-[410px]">
  <div class="text-2xl font-semibold text-pink-300">Dialogue flow</div>

  <div class="mt-6 space-y-3 text-lg">
    <div v-click="1" class="bg-white/10 rounded-lg p-4">Q0: Is there any anomaly?</div>
    <div v-click="2" class="bg-white/10 rounded-lg p-4">Q1: Describe target features.</div>
    <div v-click="3" class="bg-white/10 rounded-lg p-4">Q2: What is the motion state?</div>
    <div v-click="4" class="bg-white/10 rounded-lg p-4">Q3: From where to where?</div>
  </div>
</div>

<div class="absolute right-12 top-20 w-[680px]">
  <div class="bg-white p-2 rounded-lg shadow-lg">
    <img src="/tvau_vis1.png" class="w-full rounded" />
  </div>
</div>

<div v-click="5" class="absolute bottom-14 left-14 right-14 text-center text-xl text-gray-200">
  The language output is constrained by spatial and temporal evidence, reducing target drift and hallucinated explanations.
</div>

<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<!--
这里用 vis1 展示：左边骑车者，右边 SUV。强调 multi-turn 输出的文字都被 heatmap 支持。
-->

---
layout: cover
---

# Fine-grained Dataset Construction

<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<!--
进入数据集部分。要强调数据集是方法成功的支撑，不只是补充材料。
-->

---

# Why construct a new supervision pipeline?

<div class="absolute left-12 top-24 w-[500px]">
  <div class="text-3xl font-semibold leading-snug">
    Pixel masks alone do not teach the model to explain.
  </div>

  <div class="mt-8 space-y-4 text-lg">
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

<div class="absolute right-12 top-20 w-[610px]">
  <div class="bg-white p-2 rounded-lg shadow-lg">
    <img src="/tvau_dataset.png" class="w-full rounded" />
  </div>
</div>

<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<!--
这页说明为什么论文里面数据集 pipeline 重要。目标：让听众接受 training supervision 的合理性。
-->

---

# Dataset construction pipeline

<div class="absolute top-20 left-8 right-8">
  <div class="bg-white p-2 rounded-lg shadow-lg">
    <img src="/tvau_dataset.png" class="w-full h-auto rounded" />
  </div>
</div>

<div class="absolute bottom-14 left-12 right-12 grid grid-cols-3 gap-4 text-base">
  <div v-click="1" class="bg-white/10 rounded-xl p-4 border border-white/10">
    <span class="text-blue-300 font-semibold">Step 1</span><br>
    Frame-level structured prompting and temporal aggregation.
  </div>
  <div v-click="2" class="bg-white/10 rounded-xl p-4 border border-white/10">
    <span class="text-orange-300 font-semibold">Step 2</span><br>
    Mask + Gaussian blur to focus on the abnormal target.
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
按图从左到右讲：已有数据集只有 pixel-level label；我们通过三步转成 fine-grained anomaly understanding dataset。
-->

---

# Resulting supervision

<div class="grid grid-cols-3 gap-6 mt-14">
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
这里给数字，突出数据集规模和监督粒度。
-->

---
layout: cover
---

# Experiments

<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<!--
实验部分只讲几个关键数字。Workshop talk 中不要完整复述所有表。
-->

---

# Anomaly localization on UBnormal

<div class="absolute left-12 top-24 w-[500px]">
  <div class="text-2xl font-semibold text-pink-300">AHD achieves strong localization</div>
  <p class="text-lg mt-4 text-gray-200 leading-relaxed">
    Compared with prior baselines, AHD produces high micro-AUC and localization-oriented scores.
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

<div class="absolute right-12 top-20 w-[600px]">
  <table class="w-full text-base bg-white/10 rounded-lg overflow-hidden">
    <thead class="bg-white/20">
      <tr><th class="p-3 text-left">Method</th><th>Micro</th><th>RBDC</th><th>TBDC</th></tr>
    </thead>
    <tbody>
      <tr class="border-t border-white/10"><td class="p-3">Georgescu et al. (FT)</td><td class="text-center">68.2</td><td class="text-center">28.7</td><td class="text-center">58.1</td></tr>
      <tr class="border-t border-white/10"><td class="p-3">Bertasius et al. (FT)</td><td class="text-center">86.1</td><td class="text-center">0.008</td><td class="text-center">0.021</td></tr>
      <tr class="border-t border-white/10 bg-pink-500/20"><td class="p-3 font-semibold">AHD (Ours, FT)</td><td class="text-center font-semibold">94.8</td><td class="text-center font-semibold">67.8</td><td class="text-center font-semibold">76.7</td></tr>
    </tbody>
  </table>
  <div class="text-sm text-gray-400 mt-3">Metrics are reported in percentage.</div>
</div>

<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<!--
这里强调 RBDC/TBDC，而不是只讲 AUC。因为文章主张是 localization + understanding。
-->

---

# Multi-turn dialogue evaluation

<div class="absolute left-12 top-24 w-[510px]">
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

<div class="absolute right-10 top-24 w-[610px]">
  <table class="w-full text-sm bg-white/10 rounded-lg overflow-hidden">
    <thead class="bg-white/20">
      <tr>
        <th class="p-3 text-left">Method</th>
        <th>S.T. Target</th><th>S.T. Traj.</th><th>S.T. Acc.</th>
        <th>UB Target</th><th>UB Traj.</th><th>UB Acc.</th>
      </tr>
    </thead>
    <tbody>
      <tr class="border-t border-white/10"><td class="p-3">Qwen2.5-VL one-shot</td><td class="text-center">50.42</td><td class="text-center">78.91</td><td class="text-center">92.36</td><td class="text-center">44.35</td><td class="text-center">70.82</td><td class="text-center">87.24</td></tr>
      <tr class="border-t border-white/10"><td class="p-3">InternVL one-shot</td><td class="text-center">55.73</td><td class="text-center">82.65</td><td class="text-center">94.28</td><td class="text-center">49.84</td><td class="text-center">71.63</td><td class="text-center">88.65</td></tr>
      <tr class="border-t border-white/10 bg-pink-500/20"><td class="p-3 font-semibold">RAE (Ours)</td><td class="text-center font-semibold">62.67</td><td class="text-center font-semibold">88.84</td><td class="text-center font-semibold">97.67</td><td class="text-center font-semibold">50.32</td><td class="text-center font-semibold">78.10</td><td class="text-center font-semibold">89.73</td></tr>
    </tbody>
  </table>
  <div class="text-sm text-gray-400 mt-3">S.T. = ShanghaiTech. BLEU-4 and accuracy are reported in percentage.</div>
</div>

<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<!--
不要逐行解释表。讲最强 baseline InternVL，再讲 ours 的提升。
-->

---

# Ablation: both modules are necessary

<div class="absolute left-12 top-24 w-[500px]">
  <div class="text-2xl font-semibold text-pink-300">Complementary roles</div>
  <div class="mt-6 space-y-4 text-lg">
    <div v-click="1" class="bg-white/10 rounded-xl p-4 border border-white/10">
      <span class="text-green-300 font-semibold">AHD</span> supplies pixel-level evidence.
    </div>
    <div v-click="2" class="bg-white/10 rounded-xl p-4 border border-white/10">
      <span class="text-orange-300 font-semibold">RAE</span> makes this evidence usable by the LVLM.
    </div>
    <div v-click="3" class="bg-white/10 rounded-xl p-4 border border-white/10">
      Removing either module breaks one side of the evidence-to-language loop.
    </div>
  </div>
</div>

<div class="absolute right-10 top-28 w-[620px]">
  <table class="w-full text-sm bg-white/10 rounded-lg overflow-hidden">
    <thead class="bg-white/20">
      <tr><th class="p-3 text-left">Variant</th><th>RBDC</th><th>TBDC</th><th>Target BLEU</th><th>Traj. BLEU</th><th>Acc.</th></tr>
    </thead>
    <tbody>
      <tr class="border-t border-white/10"><td class="p-3">w/o AHD</td><td class="text-center">–</td><td class="text-center">–</td><td class="text-center">61.82</td><td class="text-center">85.47</td><td class="text-center">95.38</td></tr>
      <tr class="border-t border-white/10"><td class="p-3">w/o RAE</td><td class="text-center">67.8</td><td class="text-center">76.7</td><td class="text-center">–</td><td class="text-center">–</td><td class="text-center">–</td></tr>
      <tr class="border-t border-white/10"><td class="p-3">w/o AHD & RAE</td><td class="text-center">–</td><td class="text-center">–</td><td class="text-center">61.82</td><td class="text-center">85.47</td><td class="text-center">95.38</td></tr>
      <tr class="border-t border-white/10 bg-pink-500/20"><td class="p-3 font-semibold">T-VAU</td><td class="text-center font-semibold">67.8</td><td class="text-center font-semibold">76.7</td><td class="text-center font-semibold">62.67</td><td class="text-center font-semibold">88.84</td><td class="text-center font-semibold">97.67</td></tr>
    </tbody>
  </table>
</div>

<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<!--
这页的解释要谨慎：w/o RAE 还能有 heatmap，因为 AHD 在；但没有 language reasoning 结果。w/o AHD 主要靠 LVLM，因此缺少 localization evidence。
-->

---
layout: cover
---

# Qualitative Results

<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<!--
定性结果部分用两张图，一张讲理解，一张讲轨迹。
-->

---

# Evidence-grounded multi-turn QA

<div class="absolute top-20 left-6 right-6">
  <div class="bg-white p-2 rounded-lg shadow-lg">
    <img src="/tvau_vis1.png" class="w-full h-auto rounded" />
  </div>
</div>

<div class="absolute bottom-10 left-10 right-10 grid grid-cols-3 gap-4 text-base">
  <div v-click="1" class="bg-white/10 rounded-xl p-4 border border-white/10">
    AHD localizes the abnormal target rather than the whole scene.
  </div>
  <div v-click="2" class="bg-white/10 rounded-xl p-4 border border-white/10">
    RAE guides target-specific appearance and motion descriptions.
  </div>
  <div v-click="3" class="bg-white/10 rounded-xl p-4 border border-white/10">
    The dialogue remains consistent across judgment, features, and trajectory.
  </div>
</div>

<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<!--
先讲左侧 cyclist，再讲右侧 SUV。不要停留在图中文字，强调 visual evidence 和 textual answer 的一致性。
-->

---

# Trajectory consistency

<div class="absolute top-18 left-6 right-6">
  <div class="bg-white p-2 rounded-lg shadow-lg">
    <img src="/tvau_vis2.png" class="w-full h-auto rounded" />
  </div>
</div>

<div class="absolute bottom-18 left-20 right-20 text-center text-xl text-gray-200 leading-relaxed">
  Accumulated predictions follow the ground-truth anomaly regions over time, supporting motion and trajectory reasoning.
</div>

<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<!--
这里点出三行：输入+box、GT heatmap、prediction heatmap。结论：不仅单帧能对齐，跨帧轨迹也能保持一致。
-->

---

# Takeaway

<div class="absolute left-12 top-28 w-[530px]">
  <div class="text-4xl font-semibold leading-tight">
    T-VAU closes the loop from
    <span class="text-green-300">pixel evidence</span>
    to
    <span class="text-pink-300">language reasoning</span>.
  </div>

  <div class="mt-8 space-y-4 text-lg">
    <div v-click="1" class="bg-white/10 rounded-xl p-4 border border-white/10">AHD: threshold-free spatio-temporal anomaly heatmaps</div>
    <div v-click="2" class="bg-white/10 rounded-xl p-4 border border-white/10">RAE: region-aware and motion-aware prompt injection</div>
    <div v-click="3" class="bg-white/10 rounded-xl p-4 border border-white/10">Dataset: target-level appearance, localization, and trajectory supervision</div>
  </div>
</div>

<div class="absolute right-12 top-24 w-[560px]">
  <div class="bg-white p-2 rounded-lg shadow-lg">
    <img src="/tvau_teaser.png" class="w-full rounded" />
  </div>
</div>

<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<!--
结论页保持简洁。不要把所有结果都重复一遍。
-->

---
layout: cover
---

# Thank you

<div class="text-xl text-gray-300 mt-6">
  Questions?
</div>

<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

---
layout: cover
---

# Backup: AI-generated motivation videos

<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<!--
如果有人问 AI-generated content 怎么做，可以用下面几页作为 backup。
-->

---

# How to generate the optional AI video

<div class="absolute left-12 top-22 w-[570px]">
  <div class="text-2xl font-semibold text-pink-300">Recommended workflow</div>
  <div class="mt-6 space-y-3 text-lg leading-relaxed">
    <div class="bg-white/10 rounded-lg p-3">1. Use a generic surveillance-style scene, not a real dataset clip.</div>
    <div class="bg-white/10 rounded-lg p-3">2. Generate a 5–10 second 16:9 clip with static high-angle camera.</div>
    <div class="bg-white/10 rounded-lg p-3">3. Keep anomalies non-graphic: bicycle in pedestrian area, vehicle entering walkway, sudden running.</div>
    <div class="bg-white/10 rounded-lg p-3">4. Export MP4, mute audio, compress to 720p or 1080p.</div>
    <div class="bg-white/10 rounded-lg p-3">5. Add the label: “AI-generated content for motivation only”.</div>
  </div>
</div>

<div class="absolute right-12 top-28 w-[500px] bg-slate-900/80 rounded-xl p-6 text-lg leading-relaxed">
  <div class="text-green-300 font-semibold mb-3">Use in slides</div>
  Put the file in <span class="font-mono text-blue-300">public/ai_motivation_anomaly.mp4</span>.
  The Motivation slide already references this path.
</div>

<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

---

# Prompt template for Firefly / Runway

<div class="absolute left-10 top-20 right-10 bg-white/10 rounded-xl p-6 border border-white/10">
  <div class="text-xl font-semibold text-green-300 mb-4">Text-to-video prompt</div>
  <p class="font-mono text-base leading-relaxed text-gray-200">
    A realistic high-angle CCTV-style shot of a clean university campus walkway in daytime, static camera, wide shot, several pedestrians walking normally. A single cyclist slowly enters the pedestrian-only walkway from the right side and moves diagonally toward the upper-left area. The scene is calm and non-graphic, subtle anomaly, surveillance video aesthetic, muted colors, 24 fps, 5 seconds, 16:9, no text, no logos, no close-up faces.
  </p>
</div>

<div class="absolute left-10 right-10 bottom-18 bg-white/10 rounded-xl p-6 border border-white/10">
  <div class="text-xl font-semibold text-orange-300 mb-4">Negative prompt / avoid</div>
  <p class="font-mono text-base leading-relaxed text-gray-200">
    no blood, no injury, no dramatic violence, no weapons, no crash, no police, no readable text, no watermark, no extreme close-up faces, no cinematic camera shake
  </p>
</div>

<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

---

# Optional post-processing command

<div class="absolute left-12 top-24 right-12">
  <div class="text-2xl font-semibold text-pink-300">Compress for Slidev</div>
  <p class="text-lg mt-4 text-gray-200 leading-relaxed">
    After exporting from the generator, normalize the resolution and frame rate:
  </p>

  <div class="mt-8 bg-black/60 rounded-xl p-6 font-mono text-base text-gray-100">
    ffmpeg -i motivation_raw.mp4 -vf "scale=1280:-2,fps=24" -an -movflags +faststart public/ai_motivation_anomaly.mp4
  </div>

  <div class="mt-8 text-lg text-gray-300 leading-relaxed">
    Keep generated clips as presentation b-roll. Use real benchmark frames only for reported qualitative results.
  </div>
</div>

<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>
