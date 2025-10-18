---
layout: none
---
<style>
  /* 전체적인 가독성을 위한 스타일 */
  body {
    line-height: 1.6;
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Helvetica, Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji";
    padding: 2em;
    margin: 0;
  }
  /* 메인 프로젝트 제목 (H3) 스타일: 그라데이션 텍스트 */
  #project-title {
    font-size: 2.5em; /* 글자 크기 키우기 */
    font-weight: bold;
    background: linear-gradient(45deg, #0077b6, #00bbf9, #90e0ef); /* 파란색 계열 그라데이션 */
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    text-fill-color: transparent;
    padding-bottom: 10px;
    border-bottom: 2px solid #ddd; /* 밑줄 추가 */
    margin-top: 0;
  }
  /* 제목 안의 위첨자 색상 수정 */
  #project-title sup {
    -webkit-text-fill-color: #0077b6 !important; /* 그라데이션 투명 효과 강제 무효화 */
    color: #0077b6 !important; /* 진한 파란색으로 강제 지정 */
    font-weight: bold; /* 굵기 유지 */
  }
  /* 섹션 제목 (H4) 스타일: 포인트 색상 */
  h4 {
    color: #0077b6; /* 전문적인 파란색 톤 */
    border-bottom: 1px solid #eee;
    padding-bottom: 5px;
    margin-top: 40px; /* 섹션 간 여백 */
  }
  /* 소제목 (H5) 스타일 */
  h5 {
    color: #333;
  }
  /* 인용문 스타일 */
  blockquote {
    border-left: 4px solid #00bbf9;
    color: #555;
    background-color: #f9f9f9;
    padding: 15px;
    margin: 20px 0;
  }
  /* 이미지 스타일 */
  img {
    max-width: 100%; /* 이미지가 부모 요소 너비 초과하지 않도록 */
    height: auto; /* 가로세로 비율 유지 */
    margin-top: 15px; /* 이미지 상단 여백 */
  }
</style>

<h3 id="project-title">S<sup>2</sup>M<sup>2</sup>: Scalable Stereo Matching Model for Reliable Depth Estimation</h3>
**Junhong Min¹, Youngpil Jeon¹, Jimin Kim¹, Minyong Choi¹**
<br>
¹Samsung Electronics
<br>
**International Conference on Computer Vision (ICCV) 2025**

![S2M2 Teaser Image](fig/thumbnail.png)
*<center>Figure 1: Qualitative comparison of 3D point clouds. Compared to SOTA models (Selective-IGEV, FoundationStereo), our model shows more reliable reconstructions in fine structures like bicycle spokes.</center>*

<h4>Resources</h4>

[**Paper**](https://arxiv.org/abs/2507.13229) | [**Supplement**](ICCV_2025_supp_camera_ready.pdf) | [**Poster**](iccv25_poster_final_v2.png) | [**Code**](https://github.com/junhong-3dv/s2m2)

---

<h4>Motivation</h4>
[cite_start]Prior stereo matching models struggled to generalize across diverse input conditions[cite: 1063]. [cite_start]Attempts to scale models often led to inefficiencies, revealing a need for a more adaptable solution[cite: 1064]. [cite_start]We aim to develop a unified architecture that achieves both **Input Scalability** (robust performance across varying image resolutions and disparity ranges) and **Model Scalability** (consistent performance gains with increased model capacity) [cite: 1065-1067].

---

<h4>Abstract</h4>
> [cite_start]The pursuit of a generalizable stereo matching model, capable of performing well across varying resolutions and disparity ranges without dataset-specific fine-tuning, has revealed a fundamental trade-off[cite: 11]. [cite_start]Iterative local search methods achieve high scores on constrained benchmarks, but their core mechanism inherently limits the global consistency required for true generalization[cite: 12]. [cite_start]However, global matching architectures, while theoretically more robust, have historically been rendered infeasible by prohibitive computational and memory costs[cite: 13]. [cite_start]We resolve this dilemma with S<sup>2</sup>M<sup>2</sup>: a global matching architecture that achieves state-of-the-art accuracy and high efficiency without relying on cost volume filtering or deep refinement stacks[cite: 14]. [cite_start]Our design integrates a multi-resolution transformer for robust long-range correspondence, trained with a novel loss function that concentrates probability on feasible matches[cite: 15]. [cite_start]This approach enables a more robust joint estimation of disparity, occlusion, and confidence[cite: 16]. [cite_start]S<sup>2</sup>M<sup>2</sup> establishes a new state of the art on Middlebury v3 and ETH3D benchmarks, significantly outperforming prior methods in most metrics while reconstructing high-quality details with competitive efficiency[cite: 17, 18].

---

<h4>Method</h4>
[cite_start]Our proposed model, S<sup>2</sup>M<sup>2</sup>, is designed to revitalize the global matching paradigm by addressing its long-standing scalability challenges[cite: 122]. [cite_start]To achieve this, our architecture is composed of four main stages, as illustrated in the figure below: (1) **Feature Extraction**, (2) **Global Matching**, (3) **Refinement**, and (4) **Upsampling** [cite: 123-127].

![S2M2 Architecture Overview](fig/overview.png)
*<center>Figure 2: Overview of the S<sup>2</sup>M<sup>2</sup> architecture. It consists of a hierarchical feature extraction stage with a Multi-Resolution Transformer (MRT) and an Adaptive Gated Fusion Layer (AGFL), a global matching stage using Optimal Transport, and iterative refinement and upsampling stages [cite: 94-97].</center>*

**Key Components:**
* [cite_start]**Multi-Resolution Transformer (MRT):** Employs a hybrid attention strategy—horizontal 1D attention at high resolutions and 2D attention at the coarsest level—to strike a critical balance between performance and computational cost [cite: 135-138, 1078].
* [cite_start]**Adaptive Gated Fusion Layer (AGFL):** Acts as a dynamic gate to selectively fuse features across different scales, ensuring a powerful and coherent multi-scale representation [cite: 147-149, 1079].
* [cite_start]**Optimal Transport for Global Matching:** Establishes robust long-range correspondences by finding a globally optimal transport plan, making it robust to ambiguities like occlusions and repetitive patterns[cite: 158, 159, 1081].
* [cite_start]**Probabilistic Mode Concentration (PMC) Loss:** Our model is trained with a composite loss function that combines standard L1 losses with our novel PMC loss[cite: 1086]. [cite_start]Since global matching is performed on 1/4-downsampled features, a more direct mechanism is required to guide the matching probabilities[cite: 1087]. [cite_start]PMC loss directly regularizes the matching probability distribution, encouraging it to concentrate on valid disparity candidates, which boosts accuracy and enables confident predictions[cite: 1088].

![PMC Loss Illustration](fig/PMC_loss_new.PNG)
[cite_start]*<center>Illustration of our Probabilistic Mode Concentration (PMC) Loss[cite: 210, 211].</center>*

---

<h4>Results</h4>
[cite_start]S<sup>2</sup>M<sup>2</sup> establishes a new state-of-the-art on diverse and challenging benchmarks[cite: 17, 71]. [cite_start]**As of July 2025, it ranks first on both the [ETH3D](https://www.eth3d.net/low_res_two_view) and [Middlebury v3](https://vision.middlebury.edu/stereo/eval3/) leaderboards**[cite: 770].

[![ETH3D Leaderboard](fig/ETH3D_learderboard.jpg)](https://www.eth3d.net/low_res_two_view)
[cite_start]*<center>ETH3D low-res two-view benchmark (July 2025)[cite: 877].</center>*

[![Middlebury V3 Leaderboard](fig/Middlebury_leaderboard.jpg)](https://vision.middlebury.edu/stereo/eval3/)
[cite_start]*<center>Middlebury v3 benchmark (July 2025)[cite: 985].</center>*

<h5>Quantitative Results & Scalability</h5>

![Real Benchmark Results](fig/real_benchmark.png)
[cite_start]*<center>Quantitative comparison on real-world benchmarks[cite: 63].</center>*

![Scalability Analysis](fig/scalability.png)
[cite_start]*<center>Accuracy vs. Efficiency (Synthetic Benchmark)[cite: 294]. [cite_start]The S<sup>2</sup>M<sup>2</sup> family (red) achieves higher or comparable accuracy with significantly less computation than larger models like FoundationStereo (cyan)[cite: 275].</center>*


<h5>Our High-Resolution Synthetic Dataset</h5>
To rigorously test our model, we created a new high-resolution synthetic dataset using Blender[cite: 512]. This dataset includes challenging scenarios like complex objects, reflective surfaces, and large disparity ranges, which are often not covered by existing benchmarks[cite: 538, 542].

![Synthetic Dataset Overview](fig/blender_dataset_overview.png)
*<center>Overview of our high-resolution synthetic data generation using Blender[cite: 509, 521].</center>*

---

<h4>Critical Re-evaluation of the KITTI Benchmark</h4>
We argue that the KITTI benchmark's leaderboard scores are an unreliable indicator of true generalization due to the inherent noise and systematic biases in its LiDAR-based ground truth[cite: 309].

Our analysis shows a contradiction: while fine-tuning on KITTI improves error metrics like EPE, it simultaneously degrades photometric consistency (measured by SSIM), suggesting overfitting to dataset artifacts [cite: 586-592]. The visualizations below show how fine-tuned models produce distorted structures that align with noisy GT labels rather than the actual image content [cite: 607-609].

![KITTI Fine-tuning Comparison](fig/kitti_finetune_compare.png)
*<center>Figure 5: Negative effects of fine-tuning on KITTI[cite: 619]. [cite_start]Zero-shot models (FoundationStereo, S<sup>2</sup>M<sup>2</sup>) reconstruct clean 3D structures, whereas fine-tuned models adapt to noise in the GT annotation, resulting in distorted geometry[cite: 603, 608].</center>*