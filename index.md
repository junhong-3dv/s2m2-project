---
layout: none
---


<style>
  /* 전체적인 가독성을 위한 스타일 */
  body {
    line-height: 1.6;
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
  }
  /* 섹션 제목 (H4) 스타일: 포인트 색상 */
  h4 {
    color: #0077b6; /* 전문적인 파란색 톤 */
    border-bottom: 1px solid #eee;
    padding-bottom: 5px;
    margin-top: 40px; /* 섹션 간 여백 */
  }
  /* 인용문 스타일 */
  blockquote {
    border-left: 4px solid #00bbf9;
    color: #555;
    background-color: #f8f8f8;
    padding: 15px;
  }
  /* 코드 블록 스타일 */
  code {
    background-color: #f0f0f0;
    border-radius: 4px;
    padding: 2px 5px;
  }
  pre code {
    background-color: transparent;
  }
</style>

<h3 id="project-title">S<sup>2</sup>M<sup>2</sup>: Scalable Stereo Matching Model for Reliable Depth Estimation</h3>
**Junhong Min¹, Youngpil Jeon¹, Jimin Kim¹, Minyong Choi¹**
<br>
¹Samsung Electronics
<br>
**International Conference on Computer Vision (ICCV) 2025**


*<center>Figure 1: Qualitative comparison of 3D point clouds. Compared to SOTA models (Selective-IGEV, FoundationStereo), our model shows more reliable reconstructions in fine structures like bicycle spokes.</center>*

<h4>Resources</h4>

[[**Paper**]](INSERT_PAPER_PDF_LINK_HERE)] [[**Poster**]](INSERT_POSTER_PDF_LINK_HERE)] [[**Supplementary**]](INSERT_SUPPLEMENTARY_PDF_LINK_HERE)] [[**Code**]](https://github.com/junhong-3dv/s2m2)]

---

<h4>Abstract</h4>
> The pursuit of a generalizable stereo matching model, capable of performing well across varying resolutions and disparity ranges without dataset-specific fine-tuning, has revealed a fundamental trade-off. Iterative local search methods achieve high scores on constrained benchmarks, but their core mechanism inherently limits the global consistency required for true generalization. However, global matching architectures, while theoretically more robust, have historically been rendered infeasible by prohibitive computational and memory costs.
>
> We resolve this dilemma with **S<sup>2</sup>M<sup>2</sup>**: a global matching architecture that achieves state-of-the-art accuracy and high efficiency without relying on cost volume filtering or deep refinement stacks. Our design integrates a multi-resolution transformer for robust long-range correspondence, trained with a novel loss function that concentrates probability on feasible matches. This approach enables a more robust joint estimation of disparity, occlusion, and confidence. S<sup>2</sup>M<sup>2</sup> establishes a new state of the art on Middlebury v3 and ETH3D benchmarks, significantly outperforming prior methods in most metrics while reconstructing high-quality details with competitive efficiency.

---

<h4>Method</h4>
Our proposed model, S<sup>2</sup>M<sup>2</sup>, is designed to revitalize the global matching paradigm by addressing its long-standing scalability challenges. To achieve this, our architecture is composed of four main stages, as illustrated in the figure below: (1) **Feature Extraction**, (2) **Global Matching**, (3) **Refinement**, and (4) **Upsampling**.


*<center>Figure 2: Overview of the S<sup>2</sup>M<sup>2</sup> architecture. It consists of a hierarchical feature extraction stage with a Multi-Resolution Transformer (MRT) and an Adaptive Gated Fusion Layer (AGFL), a global matching stage using Optimal Transport, and iterative refinement and upsampling stages.</center>*

**Key Components:**
* **Multi-Resolution Transformer (MRT):** Employs a hybrid attention strategy—horizontal 1D attention at high resolutions and 2D attention at the coarsest level—to strike a critical balance between performance and computational cost.
* **Adaptive Gated Fusion Layer (AGFL):** Acts as a dynamic gate to selectively fuse features across different scales, ensuring a powerful and coherent multi-scale representation.
* **Optimal Transport for Global Matching:** Establishes robust long-range correspondences by finding a globally optimal transport plan, making it robust to ambiguities like occlusions and repetitive patterns.
* **Probabilistic Mode Concentration (PMC) Loss:** A novel loss function that directly regularizes the matching probability distribution, encouraging it to concentrate on valid disparity candidates. This boosts accuracy and enables confident predictions.

---

<h4>Results</h4>
S<sup>2</sup>M<sup>2</sup> establishes a new state-of-the-art on diverse and challenging benchmarks. Its top performance on both the high-resolution Middlebury v3 benchmark and the small-disparity ETH3D benchmark validates the exceptional versatility and accuracy of our approach.

<h5>Quantitative Results</h5>
Our S<sup>2</sup>M<sup>2</sup>-XL model surpasses prior methods, including the strong FoundationStereo baseline, across the majority of metrics on major benchmarks. It achieves particularly large margins on the most stringent metrics, such as `bad-1.0` and `bad-2.0`.

*[Insert a summary table of key results from ETH3D and Middlebury v3 benchmarks here. For instance, a small table comparing EPE and bad-2.0 metrics for S<sup>2</sup>M<sup>2</sup>-XL, FoundationStereo, and Selective-IGEV would be effective.]*

<h5>Qualitative Results</h5>
The numerical superiority translates to tangible qualitative improvements. As seen below, our model faithfully reconstructs highly intricate structures where many other methods fail.


*<center>Figure 3: Qualitative results on Middlebury v3. S<sup>2</sup>M<sup>2</sup> successfully preserves fine details like bicycle spokes without the over-smoothing effects common in other methods.</center>*

<h5>Scalability Analysis</h5>
Our S<sup>2</sup>M<sup>2</sup> family forms a compelling Pareto front, offering significantly better performance at every level of computational budget and validating the scalability of our architecture.


*<center>Figure 4: Accuracy vs. Efficiency (Synthetic Benchmark). The S<sup>2</sup>M<sup>2</sup> family (red) achieves higher or comparable accuracy with significantly less computation than larger models like FoundationStereo (cyan).</center>*

---

<h4>Critical Re-evaluation of the KITTI Benchmark</h4>
We argue that the KITTI benchmark's leaderboard scores are an unreliable indicator of true generalization due to the inherent noise and systematic biases in its LiDAR-based ground truth.

Our analysis shows a contradiction: while fine-tuning on KITTI improves error metrics like EPE, it simultaneously degrades photometric consistency (measured by SSIM), suggesting overfitting to dataset artifacts. The visualizations below show how fine-tuned models produce distorted structures that align with noisy GT labels rather than the actual image content.


*<center>Figure 5: Negative effects of fine-tuning on KITTI. Zero-shot models (FoundationStereo, S<sup>2</sup>M<sup>2</sup>) reconstruct clean 3D structures, whereas fine-tuned models (S<sup>2</sup>M<sup>2</sup>-Finetune) adapt to noise in the GT annotation, resulting in distorted geometry.</center>*

---

<h4>Citation</h4>
If you find this work useful for your research, please consider citing:
```bibtex
@inproceedings{min2025s2m2,
  title={{S\textsuperscript{2}M\textsuperscript{2}}: Scalable Stereo Matching Model for Reliable Depth Estimation},
  author={Junhong Min and Youngpil Jeon and Jimin Kim and Minyong Choi},
  booktitle={Proceedings of the IEEE/CVF International Conference on Computer Vision (ICCV)},
  year={2025}
}
