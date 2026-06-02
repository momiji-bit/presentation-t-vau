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
  padding: 34px 48px 34px;
  background: linear-gradient(135deg, #0f172a 0%, #172554 48%, #1e1b4b 100%);
  color: #f8fafc;
}
.slidev-layout h1 {
  font-size: 38px;
  line-height: 1.08;
  font-weight: 760;
  letter-spacing: -0.03em;
  margin: 0 0 22px 0;
}
.slidev-layout h2 {
  font-size: 28px;
  line-height: 1.15;
  font-weight: 680;
  margin: 0;
}
.kicker { color:#f9a8d4; font-weight:700; letter-spacing:.02em; text-transform:uppercase; font-size:14px; }
.subtle { color:#cbd5e1; }
.small { font-size:15px; color:#94a3b8; }
.body { font-size:22px; line-height:1.42; color:#e2e8f0; }
.body-sm { font-size:18px; line-height:1.42; color:#dbeafe; }
.title-page {
  min-height: 610px;
  display: grid;
  grid-template-columns: 1.05fr .95fr;
  gap: 44px;
  align-items: center;
}
.title-main { font-size:56px; line-height:1.02; font-weight:780; letter-spacing:-.04em; }
.title-sub { font-size:28px; color:#cbd5e1; margin-top:20px; font-style:italic; }
.author-line { margin-top:34px; font-size:20px; color:#e2e8f0; }
.badge-row { display:flex; flex-wrap:wrap; gap:12px; margin-top:28px; }
.badge { display:inline-flex; align-items:center; border-radius:999px; padding:8px 14px; background:rgba(255,255,255,.10); border:1px solid rgba(255,255,255,.12); color:#e2e8f0; font-size:15px; }
.panel { background:rgba(15,23,42,.62); border:1px solid rgba(255,255,255,.12); border-radius:20px; box-shadow:0 16px 42px rgba(0,0,0,.28); }
.panel-pad { padding:24px; }
.figure-card { background:#ffffff; border-radius:18px; padding:12px; box-shadow:0 18px 46px rgba(0,0,0,.32); display:flex; align-items:center; justify-content:center; overflow:hidden; }
.figure-card img, .figure-card video { max-width:100%; max-height:100%; object-fit:contain; border-radius:12px; }
.two-col { display:grid; grid-template-columns: 1.05fr .95fr; gap:32px; align-items:stretch; }
.two-col-wide { display:grid; grid-template-columns: 1.25fr .75fr; gap:30px; align-items:stretch; }
.three-col { display:grid; grid-template-columns: repeat(3, 1fr); gap:22px; }
.metric-grid { display:grid; grid-template-columns: repeat(4, 1fr); gap:18px; }
.metric { background:rgba(255,255,255,.10); border:1px solid rgba(255,255,255,.12); border-radius:18px; padding:20px; min-height:126px; }
.metric .num { font-size:42px; line-height:1; font-weight:780; color:#f9a8d4; }
.metric .label { margin-top:10px; font-size:18px; color:#e2e8f0; }
.metric .note { margin-top:8px; font-size:13px; color:#94a3b8; }
.card { background:rgba(255,255,255,.10); border:1px solid rgba(255,255,255,.12); border-radius:18px; padding:20px; }
.card h3 { font-size:25px; font-weight:720; margin:0 0 10px 0; }
.card p { font-size:18px; line-height:1.38; color:#e2e8f0; margin:0; }
.callout { border-left:5px solid #ec4899; padding:16px 18px; background:rgba(236,72,153,.14); border-radius:14px; color:#f8fafc; }
.step { font-size:18px; line-height:1.35; color:#e2e8f0; }
.step b { color:#f9a8d4; }
.clean-table { width:100%; border-collapse:collapse; font-size:18px; overflow:hidden; border-radius:16px; }
.clean-table th { background:rgba(255,255,255,.16); color:#f8fafc; font-weight:700; padding:13px 12px; text-align:left; }
.clean-table td { padding:13px 12px; border-top:1px solid rgba(255,255,255,.12); color:#e2e8f0; }
.clean-table tr.highlight td { background:rgba(236,72,153,.16); color:#ffffff; font-weight:700; }
.divider { height:1px; background:rgba(255,255,255,.13); margin:22px 0; }
.slide-no { position:absolute; right:24px; bottom:16px; font-size:13px; color:#94a3b8; }
.caption { font-size:14px; color:#94a3b8; margin-top:8px; text-align:center; }
.mathbox { font-size:20px; color:#e2e8f0; background:rgba(15,23,42,.72); border:1px solid rgba(255,255,255,.14); border-radius:14px; padding:16px; }
</style>

<div class="title-page">
  <div>
    <div class="kicker">CVPR 2026 SVC Workshop</div>
    <div class="title-main">Text-guided Fine-Grained Video Anomaly Understanding</div>
    <div class="title-sub">Pixel Evidence to Language Reasoning</div>
    <div class="author-line"><b>Jihao (Geo) Gu</b>, Kun Li, He Wang, Kaan Akşit</div>
    <div class="badge-row">
      <span class="badge">T-VAU</span>
      <span class="badge">AHD + RAE</span>
      <span class="badge">Video Anomaly Understanding</span>
    </div>
  </div>
  <div class="figure-card" style="height:520px;">
    <img src="/teaser_tvau.png" alt="T-VAU teaser">
  </div>
</div>

<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

<!--
开场只讲一句：T-VAU 的目标不是再做一个 anomaly score，而是把像素级证据和语言推理接起来。
-->

---

# Motivation: users need actionable anomaly understanding

<div class="two-col-wide">
  <div class="figure-card" style="height:500px;">
    <img src="/tvau_teaser.png" alt="T-VAU full teaser">
  </div>
  <div class="panel panel-pad" style="height:500px; display:flex; flex-direction:column; justify-content:center;">
    <div class="kicker">Core problem</div>
    <h2 style="margin-top:10px;">A binary anomaly score is not enough.</h2>
    <div class="divider"></div>
    <div class="body-sm">
      Real-world anomaly understanding needs five outputs in one loop:
    </div>
    <div class="three-col" style="grid-template-columns:1fr; gap:12px; margin-top:18px;">
      <div class="card"><p><b>Detect</b> whether abnormal behavior exists.</p></div>
      <div class="card"><p><b>Localize</b> the evidence in space and time.</p></div>
      <div class="card"><p><b>Explain</b> target identity, appearance, motion, and trajectory.</p></div>
    </div>
  </div>
</div>

<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

<!--
这页用完整 teaser 直接建立任务定义：Detection / Localization / Identification / Trajectory / Explanation。
-->

---

# Existing paradigms are fragmented

<div class="two-col">
  <div class="figure-card" style="height:500px;">
    <img src="/teaser_comparison.png" alt="Comparison with previous paradigms">
  </div>
  <div class="panel panel-pad" style="height:500px; display:flex; flex-direction:column; justify-content:center;">
    <div class="card" style="margin-bottom:14px;">
      <h3 style="color:#fdba74;">Traditional IAD / VAD</h3>
      <p>Provides heatmaps or anomaly scores, but lacks semantic explanation.</p>
    </div>
    <div class="card" style="margin-bottom:14px;">
      <h3 style="color:#86efac;">General LVLMs</h3>
      <p>Can answer questions, but often miss subtle pixel-level cues.</p>
    </div>
    <div class="card">
      <h3 style="color:#93c5fd;">LVLM + Diffusion hybrids</h3>
      <p>May produce visualizations, but explanations can be unstable or weakly grounded.</p>
    </div>
    <div class="callout" style="margin-top:18px; font-size:20px;">
      T-VAU closes the loop: <b>heatmap evidence → region-aware prompt → language reasoning</b>.
    </div>
  </div>
</div>

<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

<!--
右侧只讲三类方法的缺口，最后落到 T-VAU 的闭环。
-->

---

# T-VAU overview

<div class="figure-card" style="height:430px; margin-top:4px;">
  <img src="/tvau_framework.png" alt="T-VAU framework">
</div>

<div class="three-col" style="margin-top:22px;">
  <div class="card">
    <h3 style="color:#93c5fd;">Input</h3>
    <p>Video clip + multi-turn questions + normal / abnormal text prompts.</p>
  </div>
  <div class="card">
    <h3 style="color:#fb923c;">Pixel evidence</h3>
    <p>AHD generates threshold-free spatio-temporal anomaly heatmaps.</p>
  </div>
  <div class="card">
    <h3 style="color:#f9a8d4;">Language output</h3>
    <p>RAE injects heatmap evidence into the LVLM for grounded responses.</p>
  </div>
</div>

<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

<!--
从左到右讲 framework：UI 输入、视频和 prompt、AHD 生成 heatmap、RAE 转 prompt、LVLM 输出答案。
-->

---

# Formulation: one model, two coupled outputs

<div class="two-col">
  <div class="panel panel-pad" style="height:500px; display:flex; flex-direction:column; justify-content:center;">
    <div class="kicker">Given</div>
    <div class="body" style="margin-top:10px;">
      a video clip <b>V</b>, dialogue history <b>Q≤t, A&lt;t</b>, and class prompts <b>Tc</b>
    </div>
    <div class="mathbox" style="margin-top:28px;">
      $\mathbf{H}, \mathbf{A}_t = \mathcal{M}(\mathcal{V}, \mathbf{Q}_{\leq t}, \mathbf{A}_{\leq t-1}, \mathcal{T}_c; \Theta)$
    </div>
    <div class="divider"></div>
    <div class="body-sm">
      <b>H</b>: pixel-level spatio-temporal anomaly heatmap<br>
      <b>A<sub>t</sub></b>: anomaly judgment, appearance, location, motion, and trajectory response
    </div>
  </div>
  <div class="figure-card" style="height:500px;">
    <img src="/framework_core.png" alt="Core framework crop">
  </div>
</div>

<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

<!--
公式只作为接口定义，不展开推导。强调两个输出不是分开的，而是串联耦合。
-->

---

# Anomaly Heatmap Decoder (AHD)

<div class="two-col-wide">
  <div class="panel panel-pad" style="height:500px;">
    <div class="kicker">Align + ground</div>
    <h2 style="margin-top:10px;">Text prompts become spatial anomaly evidence.</h2>
    <div class="divider"></div>
    <div class="three-col" style="grid-template-columns:1fr; gap:14px;">
      <div class="card"><p><b>1. Text anchors:</b> encode normal / abnormal prompts into semantic prototypes.</p></div>
      <div class="card"><p><b>2. Multiscale tokens:</b> read intermediate ViT blocks to retain spatial details.</p></div>
      <div class="card"><p><b>3. SAF:</b> compute element-wise cosine similarity and fuse layers.</p></div>
      <div class="card"><p><b>4. Output:</b> softmax anomaly channel gives heatmap <b>H</b>.</p></div>
    </div>
  </div>
  <div style="display:grid; grid-template-rows: 1fr 1fr; gap:18px; height:500px;">
    <div class="figure-card"><img src="/framework_saf_block.png" alt="SAF block"></div>
    <div class="figure-card"><img src="/framework_ahd_block.png" alt="AHD block"></div>
  </div>
</div>

<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

<!--
讲法：文本给语义锚点，视觉 token 给空间位置，SAF 把二者相似度转成 heatmap。
-->

---

# Region-aware Anomaly Encoder (RAE)

<div class="two-col-wide">
  <div class="figure-card" style="height:500px;">
    <img src="/framework_rae_focus.png" alt="RAE focus crop">
  </div>
  <div class="panel panel-pad" style="height:500px; display:flex; flex-direction:column; justify-content:center;">
    <div class="kicker">Ground + reason</div>
    <h2 style="margin-top:10px;">Heatmaps are not only visual outputs; they become LVLM prompts.</h2>
    <div class="divider"></div>
    <div class="body-sm">
      RAE converts anomaly heatmaps into structured prompt embeddings:
    </div>
    <div class="card" style="margin-top:16px;"><p><b>Motion cue:</b> temporal difference across consecutive heatmaps.</p></div>
    <div class="card" style="margin-top:12px;"><p><b>Regional cue:</b> 3×3 pooling for local spatial evidence.</p></div>
    <div class="card" style="margin-top:12px;"><p><b>Global cue:</b> clip-level context for anomaly judgment.</p></div>
  </div>
</div>

<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

<!--
核心信息：RAE 不是为了画图，而是把低层 evidence 投影到语言模型可用的 prompt embedding 空间。
-->

---

# Multi-turn reasoning: from evidence to dialogue

<div class="figure-card" style="height:355px; margin-top:4px;">
  <img src="/tvau_vis1.png" alt="Multi-turn qualitative QA">
</div>

<div class="three-col" style="margin-top:24px;">
  <div class="card">
    <h3 style="color:#93c5fd;">Judgment</h3>
    <p>“Is there any anomaly?” is answered with heatmap support.</p>
  </div>
  <div class="card">
    <h3 style="color:#f9a8d4;">Target features</h3>
    <p>Appearance descriptions are tied to the activated region.</p>
  </div>
  <div class="card">
    <h3 style="color:#86efac;">Trajectory</h3>
    <p>Motion phrases are grounded by temporal heatmap changes.</p>
  </div>
</div>

<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

<!--
用两组例子说明：同一模型既能回答是否异常，也能说明特征和轨迹，且文字和 heatmap 对齐。
-->

---

# Fine-grained dataset construction

<div class="figure-card" style="height:300px; margin-top:4px;">
  <img src="/dataset_top.png" alt="Dataset top crop">
</div>

<div class="two-col" style="margin-top:24px; grid-template-columns:.9fr 1.1fr;">
  <div class="panel panel-pad" style="min-height:190px;">
    <div class="kicker">Why</div>
    <h2 style="margin-top:8px;">Pixel masks alone do not teach the model to explain.</h2>
  </div>
  <div class="three-col" style="gap:16px;">
    <div class="card"><p><b>Target</b><br>who causes the anomaly</p></div>
    <div class="card"><p><b>Space–time</b><br>where and when it occurs</p></div>
    <div class="card"><p><b>Motion</b><br>how the state changes</p></div>
  </div>
</div>

<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

<!--
这页解释为什么要做数据集：从 pixel-level label only 扩展到 target description、spatio-temporal info 和 motion trajectory。
-->

---

# Dataset construction pipeline

<div class="three-col" style="margin-top:4px; align-items:start;">
  <div>
    <div class="figure-card" style="height:300px;"><img src="/dataset_step1.png" alt="Dataset step 1"></div>
    <div class="card step" style="margin-top:14px;"><b>Step 1.</b> Structured frame-level prompting extracts target attributes and boxes, then links them into target timelines.</div>
  </div>
  <div>
    <div class="figure-card" style="height:300px;"><img src="/dataset_step2.png" alt="Dataset step 2"></div>
    <div class="card step" style="margin-top:14px;"><b>Step 2.</b> Mask + Gaussian blur suppresses background and re-focuses descriptions on abnormal targets.</div>
  </div>
  <div>
    <div class="figure-card" style="height:300px;"><img src="/dataset_step3.png" alt="Dataset step 3"></div>
    <div class="card step" style="margin-top:14px;"><b>Step 3.</b> Appearance ↔ motion verification filters inconsistent samples before training.</div>
  </div>
</div>

<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

<!--
按三步从左到右讲。每个 step 一句话，不需要展开所有小框。
-->

---

# Resulting supervision

<div class="two-col-wide">
  <div class="figure-card" style="height:500px;">
    <img src="/tvau_dataset.png" alt="Full dataset figure">
  </div>
  <div class="panel panel-pad" style="height:500px; display:flex; flex-direction:column; justify-content:center;">
    <div class="kicker">Supervision scale</div>
    <div class="metric" style="margin-top:14px;">
      <div class="num">4,108 / 1,028</div>
      <div class="label">ShanghaiTech frame-wise annotations</div>
      <div class="note">training / validation</div>
    </div>
    <div class="metric" style="margin-top:16px;">
      <div class="num">5,136</div>
      <div class="label">ShanghaiTech target-aligned descriptions</div>
    </div>
    <div class="metric" style="margin-top:16px;">
      <div class="num">7,912</div>
      <div class="label">UBnormal target-aligned descriptions</div>
    </div>
  </div>
</div>

<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

<!--
这页讲数据集规模和它支撑的监督：appearance、localization、motion trajectory。
-->

---

# Quantitative result: anomaly localization

<div class="metric-grid" style="margin-top:32px;">
  <div class="metric">
    <div class="num">94.8</div>
    <div class="label">Micro-AUC</div>
    <div class="note">UBnormal, AHD-FT</div>
  </div>
  <div class="metric">
    <div class="num">87.8</div>
    <div class="label">Macro-AUC</div>
    <div class="note">UBnormal, AHD-FT</div>
  </div>
  <div class="metric">
    <div class="num">67.8</div>
    <div class="label">RBDC</div>
    <div class="note">region-based localization</div>
  </div>
  <div class="metric">
    <div class="num">76.7</div>
    <div class="label">TBDC</div>
    <div class="note">track-based localization</div>
  </div>
</div>

<div class="panel panel-pad" style="margin-top:34px;">
  <div class="body">
    AHD improves not only frame-level anomaly discrimination, but also region- and track-level localization quality.
  </div>
</div>

<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

<!--
实验页不要堆完整表格。讲四个核心数字：Micro/Macro-AUC + RBDC/TBDC。
-->

---

# Quantitative result: multi-turn dialogue

<div class="panel panel-pad" style="margin-top:8px;">
  <table class="clean-table">
    <thead>
      <tr>
        <th>Dataset</th>
        <th>Target BLEU-4</th>
        <th>Trajectory BLEU-4</th>
        <th>Yes/No Acc.</th>
      </tr>
    </thead>
    <tbody>
      <tr class="highlight">
        <td>ShanghaiTech</td>
        <td>62.67</td>
        <td>88.84</td>
        <td>97.67%</td>
      </tr>
      <tr class="highlight">
        <td>UBnormal</td>
        <td>50.32</td>
        <td>78.10</td>
        <td>89.73%</td>
      </tr>
    </tbody>
  </table>
</div>

<div class="three-col" style="margin-top:34px;">
  <div class="card"><h3 style="color:#93c5fd;">Faithfulness</h3><p>Target descriptions use the heatmap-supported instance.</p></div>
  <div class="card"><h3 style="color:#f9a8d4;">Temporal grounding</h3><p>Trajectory descriptions preserve direction and state changes.</p></div>
  <div class="card"><h3 style="color:#86efac;">Discrimination</h3><p>Yes/No decisions remain strong under one-shot prompting.</p></div>
</div>

<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

<!--
这页强调 RAE 的语言端收益：target、trajectory 和 yes/no 三个维度同时提升。
-->

---

# Ablation: AHD and RAE are complementary

<div class="panel panel-pad" style="margin-top:6px;">
  <table class="clean-table">
    <thead>
      <tr>
        <th>Variant</th>
        <th>Heatmap evidence</th>
        <th>Language reasoning</th>
        <th>Takeaway</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>w/o AHD</td>
        <td>—</td>
        <td>weaker grounding</td>
        <td>no explicit pixel-level evidence path</td>
      </tr>
      <tr>
        <td>w/o RAE</td>
        <td>67.8 / 76.7</td>
        <td>—</td>
        <td>heatmap cannot directly guide the LVLM</td>
      </tr>
      <tr class="highlight">
        <td>T-VAU</td>
        <td>67.8 / 76.7</td>
        <td>62.67 / 88.84 / 97.67%</td>
        <td>closed loop: evidence → prompt → answer</td>
      </tr>
    </tbody>
  </table>
</div>

<div class="callout" style="margin-top:34px; font-size:22px;">
  AHD supplies localization. RAE makes that localization usable by the LVLM.
</div>

<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

<!--
这里不需要讲参数规模。只讲消融逻辑：AHD 负责 evidence，RAE 负责把 evidence 注入语言模型。
-->

---

# Qualitative result: evidence-grounded QA

<div class="two-col" style="grid-template-columns:1fr 1fr; gap:24px;">
  <div>
    <div class="figure-card" style="height:250px;"><img src="/vis1_cyclist.png" alt="Cyclist anomaly QA"></div>
    <div class="card" style="margin-top:16px;"><p><b>Cyclist case:</b> heatmap localizes the bicycle rider and supports appearance and trajectory answers.</p></div>
  </div>
  <div>
    <div class="figure-card" style="height:250px;"><img src="/vis1_suv.png" alt="SUV anomaly QA"></div>
    <div class="card" style="margin-top:16px;"><p><b>SUV case:</b> heatmap follows the vehicle entering from the left and moving upward.</p></div>
  </div>
</div>

<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

<!--
这一页比整张 vis1 更易读。每个 case 只指出一个 grounding 重点。
-->

---

# Qualitative result: localization across scenes

<div class="figure-card" style="height:360px; margin-top:4px;">
  <img src="/tvau_vis2.png" alt="Localization qualitative results">
</div>

<div class="three-col" style="margin-top:24px;">
  <div class="card"><h3 style="color:#93c5fd;">Spatial precision</h3><p>Activations stay close to abnormal targets instead of large background regions.</p></div>
  <div class="card"><h3 style="color:#f9a8d4;">Temporal consistency</h3><p>Elongated responses follow abnormal motion and track-like evidence.</p></div>
  <div class="card"><h3 style="color:#86efac;">Scene robustness</h3><p>The same mechanism works for pedestrian, traffic, and indoor/outdoor cases.</p></div>
</div>

<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

<!--
讲 vis2：上面是输入与 bbox/GT，中间是 GT heatmap，下面是 prediction，重点是形状和目标位置一致。
-->

---

# Takeaway

<div class="two-col">
  <div class="panel panel-pad" style="height:500px; display:flex; flex-direction:column; justify-content:center;">
    <div class="kicker">Summary</div>
    <h2 style="margin-top:8px;">T-VAU turns anomaly detection into anomaly understanding.</h2>
    <div class="divider"></div>
    <div class="card"><p><b>AHD</b> aligns visual features with normal / abnormal text prompts to produce pixel-level heatmaps.</p></div>
    <div class="card" style="margin-top:14px;"><p><b>RAE</b> converts heatmap evidence into region- and motion-aware prompt embeddings.</p></div>
    <div class="card" style="margin-top:14px;"><p><b>Dataset</b> provides target-level appearance, localization, and trajectory supervision.</p></div>
  </div>
  <div class="figure-card" style="height:500px;">
    <img src="/teaser_tvau.png" alt="T-VAU output summary">
  </div>
</div>

<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

<!--
收尾：不是单纯的检测器，也不是没有 grounding 的 LVLM，而是证据和语言之间的闭环。
-->

---

# Backup: optional AI-generated motivation video

<div class="two-col">
  <div class="panel panel-pad" style="height:500px;">
    <div class="kicker">Use case</div>
    <h2 style="margin-top:8px;">Use generated content only as motivation b-roll.</h2>
    <div class="divider"></div>
    <div class="body-sm">
      Place the generated video in <code>public/ai_motivation_anomaly.mp4</code>. Keep all reported qualitative results from the real benchmark figures.
    </div>
    <div class="card" style="margin-top:20px;"><p><b>Prompt:</b> realistic high-angle CCTV-style shot, university campus walkway, several pedestrians walking normally, one cyclist enters a pedestrian-only walkway, static camera, 5 seconds, 16:9, no text or logos.</p></div>
    <div class="card" style="margin-top:14px;"><p><b>Negative prompt:</b> no injury, no dramatic violence, no weapons, no crash, no close-up faces, no watermark.</p></div>
  </div>
  <div class="figure-card" style="height:500px;">
    <img src="/tvau_teaser.png" alt="Fallback poster for AI-generated video slide">
  </div>
</div>

<div class="slide-no"><SlideCurrentNo /> / <SlidesTotal /></div>

<!--
这页只作为 backup。AI 视频只能作为 motivation，不要用作实验结果或 benchmark qualitative results。
-->
