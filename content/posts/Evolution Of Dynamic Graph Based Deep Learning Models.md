+++
title = "Evolution Of Dynamic Graph Based Deep Learning Models"
author = ["Anak Wannaphaschaiyong"]
tags = ["WORK", "blockchain", "blog"]
categories = ["PhD"]
draft = true
+++

The goal of the writing this blog is to summarize the evolution of dynamic graph based deep learning models.

History of deep learning solution of dynamic graph models can be traced back to 2016. At the time, literature explored methods of aggregating information on graph from node neighbor with varying weight, such as using tree like structure for NLP tasks and grid like structure. Furthermore, RNN had been used to learn temporal features while structure features are learned by CNN, GNN, or random walk. This can be done either by simply stacking temporal layer to structure layer or integrate temporal and structure components in to one layer (<a href="#citeproc_bib_item_3">Seo et al. 2018</a>). Note that 2016 is around the peak of RNN hype. Around the same time, research effort was put toward the development of convolution filters. We discuss related work on this topic in Static Graph Modeling section. Later, Xu et al. (<a href="#citeproc_bib_item_4">Xu et al. 2019</a>) purposed G-GCN. The models disregard time and take into consideration only topology changes. This is done by extending variational Graph Autoencoder (VGAE) (<a href="#citeproc_bib_item_2">Kipf and Welling 2016</a>) to predict unseen node.

In particular, according to dynamic graph modeling taxonomy (<a href="#citeproc_bib_item_1">Kazemi et al., n.d.</a>), this paper concerns continuous dynamic graph neural network (continuous DGNN). Continuous DGNN update information for every time an event (edge instance) occurs. Furthermore, these type of model can use temporal difference, time invertal between event, as input parameter. Neural network component can be used to approximate point process parameters. This approach is called temporal point process based model (TPP). On the other hand, neural network can be used to encode temporal pattern by learning representation of time embedding vector. TGN falls into this category.

<div class="csl-bib-body">
  <div class="csl-entry"><a id="citeproc_bib_item_1"></a>Kazemi, Seyed Mehran, Rishab Goel, Kshitij Jain, Ivan Kobyzev, Akshay Sethi, Peter Forsyth, and Pascal Poupart. n.d. “Representation Learning for Dynamic Graphs a Survey,” 73. <a href="https://jmlr.org/papers/volume21/19-447/19-447.pdf">https://jmlr.org/papers/volume21/19-447/19-447.pdf</a>.</div>
  <div class="csl-entry"><a id="citeproc_bib_item_2"></a>Kipf, Thomas N, and Max Welling. 2016. “Variational Graph Auto-Encoders.” <i>Arxiv Preprint Arxiv:1611.07308</i>. <a href="https://arxiv.org/pdf/1611.07308.pdf%5D">https://arxiv.org/pdf/1611.07308.pdf%5D</a>.</div>
  <div class="csl-entry"><a id="citeproc_bib_item_3"></a>Seo, Youngjoo, Michaël Defferrard, Pierre Vandergheynst, and Xavier Bresson. 2018. “Structured Sequence Modeling with Graph Convolutional Recurrent Networks.” In <i>International Conference on Neural Information Processing</i>, 362–73. Springer. <a href="https://arxiv.org/pdf/1612.07659.pdf?ref=https://githubhelp.com">https://arxiv.org/pdf/1612.07659.pdf?ref=https://githubhelp.com</a>.</div>
  <div class="csl-entry"><a id="citeproc_bib_item_4"></a>Xu, Da, Chuanwei Ruan, Kamiya Motwani, Evren Korpeoglu, Sushant Kumar, and Kannan Achan. 2019. “Generative Graph Convolutional Network for Growing Graphs.” In <i>Icassp 2019-2019 Ieee International Conference on Acoustics, Speech and Signal Processing (Icassp)</i>, 3167–71. IEEE. <a href="https://sci-hub.se/10.1109/icassp.2019.8682360">https://sci-hub.se/10.1109/icassp.2019.8682360</a>.</div>
</div>
