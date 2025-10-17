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
  /* 코드 블록 스타일 */
  code {
    background-color: #f0f0f0;
    border-radius: 4px;
    padding: 2px 5px;
  }
  pre {
    background-color: #f8f8f8;
    border: 1px solid #ddd;
    border-radius: 5px;
    padding: 15px;
  }
  pre code {
    background-color: transparent;
    padding: 0;
  }
</style>

<h3 id="project-title">S<sup>2</sup>M<sup>2</sup>: Scalable Stereo Matching Model for Reliable Depth Estimation</h3>
**Junhong Min¹, Youngpil Jeon¹, Jimin Kim¹, Minyong Choi¹**
<br>
¹Samsung Electronics
<br>
**International Conference on Computer Vision (ICCV) 2025**

[Image of Teaser figure showing bicycle spoke reconstructions]
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

[Image of S²M² architecture diagram]
*<center>Figure 2: Overview of the S<sup>2</sup>M<sup>2</sup> architecture. It consists of a hierarchical feature extraction stage with a Multi-Resolution Transformer (MRT) and an Adaptive Gated Fusion Layer (AGFL), a global matching stage using Optimal Transport, and iterative refinement and upsampling stages.</center>*

**Key Components:**
* **Multi-Resolution Transformer (MRT):** Employs a hybrid attention strategy—horizontal 1D attention at high resolutions and 2D attention at the coarsest level—to strike a critical balance between performance and computational cost.
* **Adaptive Gated Fusion Layer (AGFL):** Acts as a dynamic gate to selectively fuse features across different scales, ensuring a powerful and coherent multi-scale representation.
* **Optimal Transport for Global Matching:** Establishes robust long-range correspondences by finding a globally optimal transport plan, making it robust to ambiguities like occlusions and repetitive patterns.
*