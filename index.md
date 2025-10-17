# S²M²: Scalable Stereo Matching Model for Reliable Depth Estimation

**Junhong Min, Youngpil Jeon, Jimin Kim, Minyong Choi**
<br>
*Samsung Electronics*
<br>
**ICCV 2025**

---

### Abstract

The pursuit of a generalizable stereo matching model, capable of performing well across varying resolutions and disparity ranges without dataset-specific fine-tuning, has revealed a fundamental trade-off. Iterative local search methods achieve high scores on constrained benchmarks, but their core mechanism inherently limits the global consistency required for true generalization. However, global matching architectures, while theoretically more robust, have historically been rendered infeasible by prohibitive computational and memory costs.

We resolve this dilemma with S²M²: a global matching architecture that achieves state-of-the-art accuracy and high efficiency without relying on cost volume filtering or deep refinement stacks. Our design integrates a multi-resolution transformer for robust long-range correspondence, trained with a novel loss function that concentrates probability on feasible matches. This approach enables a more robust joint estimation of disparity, occlusion, and confidence. S²M² establishes a new state of the art on Middlebury v3 and ETH3D benchmarks, significantly outperforming prior methods in most metrics while reconstructing high-quality details with competitive efficiency.

---

### Resources

* [Paper](INSERT_PAPER_LINK_HERE)
* [Poster](INSERT_POSTER_LINK_HERE)
* [Supplementary](INSERT_SUPPLEMENTARY_LINK_HERE)
* [Code](https://github.com/junhong-3dv/s2m2)

---

### Citation