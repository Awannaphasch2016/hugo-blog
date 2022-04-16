+++
title = "Type Of Input Graph Construction Explained."
author = ["Anak Wannaphaschaiyong"]
tags = ["WORK", "blockchain", "blog"]
categories = ["PhD"]
draft = true
+++

Dynamic graph construction is out of scope of this paper, but it is important to emphasize that model architecture is heavily dependent on input. Example of input graph construction are aggregated graph (edge-weighted graph (<a href="#citeproc_bib_item_3">Qu et al. 2020</a>)), synthetic link between static graph (<a href="#citeproc_bib_item_1">Kapoor et al. 2020</a>), and different graph.

In particular, according to dynamic graph modeling taxonomy (<a href="#citeproc_bib_item_2">Kazemi et al., n.d.</a>), this paper concerns continuous dynamic graph neural network (continuous DGNN). Continuous DGNN update information for every time an event (edge instance) occurs. Furthermore, these type of model can use temporal difference, time invertal between event, as input parameter. Neural network component can be used to approximate point process parameters. This approach is called temporal point process based model (TPP). On the other hand, neural network can be used to encode temporal pattern by learning representation of time embedding vector. TGN falls into this category.

<div class="csl-bib-body">
  <div class="csl-entry"><a id="citeproc_bib_item_1"></a>Kapoor, Amol, Xue Ben, Luyang Liu, Bryan Perozzi, Matt Barnes, Martin Blais, and Shawn O’Banion. 2020. “Examining Covid-19 Forecasting Using Spatio-Temporal Graph Neural Networks.” <i>Arxiv Preprint Arxiv:2007.03113</i>. <a href="https://arxiv.org/pdf/2007.03113.pdf">https://arxiv.org/pdf/2007.03113.pdf</a>.</div>
  <div class="csl-entry"><a id="citeproc_bib_item_2"></a>Kazemi, Seyed Mehran, Rishab Goel, Kshitij Jain, Ivan Kobyzev, Akshay Sethi, Peter Forsyth, and Pascal Poupart. n.d. “Representation Learning for Dynamic Graphs a Survey,” 73. <a href="https://jmlr.org/papers/volume21/19-447/19-447.pdf">https://jmlr.org/papers/volume21/19-447/19-447.pdf</a>.</div>
  <div class="csl-entry"><a id="citeproc_bib_item_3"></a>Qu, Liang, Huaisheng Zhu, Qiqi Duan, and Yuhui Shi. 2020. “Continuous-Time Link Prediction via Temporal Dependent Graph Neural Network.” In <i>Proceedings of the Web Conference 2020</i>, 3026–32. <a href="https://sci-hub.se/10.1145/3366423.3380073">https://sci-hub.se/10.1145/3366423.3380073</a>.</div>
</div>
