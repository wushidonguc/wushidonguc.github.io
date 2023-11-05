---
title: "Scaling Distributed Training of Flood-Filling Networks on HPC Infrastructure for Brain Mapping"
layout: post
date: 2019-5-8 15:10
tag: [Deep Learning, Distributed Training, HPC, Connectomics]
headerImage: true
projects: true
hidden: true # don't count this post in blog pagination
description: "Distributed training of Flood-Filling Networks (FFNs) for instance segmentation in 3d volumes implemented with Horovod."
category: project
author: Wushi Dong
externalLink: false
---

<span style="background-color: #f8f8f8; padding: 20px; border-radius: 0px; display: inline-block; width: calc(100% - 20px);">
Imagine deciphering the complexities of the brain's neural network, one cell at a time. In this project, we've tackled this monumental task by enhancing the efficiency of training the flood-filling network (FFN) architecture, a state-of-the-art neural network in segmenting structures from voluminous electron microscopy data. By implementing cutting-edge distributed training techniques and optimizing batch sizes on the supercomputers, we've not only significantly reduced training time but also achieved remarkable segmentation results, paving the way for a deeper understanding of the brain's intricate workings.<br><br>
[Read paper >>](https://arxiv.org/pdf/1905.06236)<br>
[View code >>](https://github.com/wushidonguc/distributed_ffn)<br>
<br>
</span>

<!--
Paper: ["Scaling Distributed Training of Flood-Filling Networks on HPC Infrastructure for Brain Mapping"](https://ieeexplore.ieee.org/abstract/document/8945106) published in 2019 IEEE/ACM Third Workshop on Deep Learning on Supercomputers (DLS) at SC19.
Paper: ["Dong, Wushi, et al. "Scaling distributed training of flood-filling networks on hpc infrastructure for brain mapping." 2019 IEEE/ACM Third Workshop on Deep Learning on Supercomputers (DLS). IEEE, 2019."](https://arxiv.org/pdf/1905.06236)

Code: [distributed_ffn](https://github.com/wushidonguc/distributed_ffn)
-->

Mapping all the neurons in the brain requires automatic reconstruction of entire cells from volume electron microscopy data. We visualize 2D segmentation of a single slice and 3D volume segmentations of neurons in the images below.

![Project Image]({{ site.url }}/assets/fib25_training1.png)

![Project Image]({{ site.url }}/assets/fib25_vis1.png)

The flood-filling network (FFN) architecture has demonstrated leading performance for segmenting structures from this data. However, the training of the network is computationally expensive. The figure below shows the FFN's workflow: 12 identical convolutional modules implement the operations shown in the top inset box. Mask output provides recurrent feedback to the FFN input.

![Project Image]({{ site.url }}/assets/ffn_diagram2.png)

In order to reduce the training time, we implemented synchronous and data-parallel distributed training using the Horovod library, which is different from the asynchronous training scheme used in the published FFN code.

We demonstrated that our distributed training scaled well up to 2048 Intel Knights Landing (KNL) nodes on the Theta supercomputer. Our trained models achieved similar level of inference performance, but took less training time compared to previous methods. Our study on the effects of different batch sizes on FFN training suggests ways to further improve training efficiency.


## Results

Our distributed training reaches 95% accuracy in approximately 4.5 hours using the Adam optimizer

![Project Image]({{ site.url }}/assets/training.png)

The trained model shows good results on the evaluation data.

![Project Image]({{ site.url }}/assets/evaluation.png)

The training performance achieves a parallel efficiency of about 68% on 2048 KNL nodes.
![Project Image]({{ site.url }}/assets/scaling_efficiency.png)

## Methods

In order to reduce the training time, we implemented synchronous and data-parallel distributed training using the Horovod framework on top of the published FFN code. We demonstrated the scaling of FFN training up to 2048 Intel KNL nodes (131,072 cores) at Argonne Leadership Computing Facility (ALCF). We investigated the training accuracy with different optimizers, learning rates, and optional warm-up periods.

We discovered that square root scaling for learning rate works best beyond 16 nodes, which is contrary to the case of smaller number of nodes, where linear learning rate scaling with warm-up performs the best.

![Project Image]({{ site.url }}/assets/lr_acc.png)

We also evaluate the tradeoff between training throughput and efficiency for large-batch training in the figure below, where we compare training runs with different batch sizes. On the left we compare F1 with wall time. On the right we compare F1 with total number of FOVs processed. Large-batch training is faster (left) to reach a specified level of performance, while small-batch training is more efficient (right).

![Project Image]({{ site.url }}/assets/training_efficiency.png)

Our work is an important step towards a complete simulation pipeline of the human brain, which could produce the same activity — connectivity patterns that produce stereotypical behaviors — seen on the wiring diagram.

<h2>Publication</h2>
* [Dong, Wushi, et al. "Scaling distributed training of flood-filling networks on hpc infrastructure for brain mapping." 2019 IEEE/ACM Third Workshop on Deep Learning on Supercomputers (DLS). IEEE, 2019.](https://arxiv.org/abs/1905.06236)

## Talks
* <b>W. Dong</b>, M. Keceli, R. Vescovi, H. Li, C. Adams, E. Jennings, S. Flender, T. Uram, V. Vishwanath, N. Ferrier, N. Kasthuri, P. B. Littlewood, <i>Scaling Distributed Training of Flood-Filling Networks on HPC Infrastructure for Brain Mapping</i>, 2019 IEEE/ACM Third Workshop on Deep Learning on Supercomputers (DLS) at Supercomputing 2019 (SC19). (November 2019) [View slides >>]({{ site.url }}/assets/191117_SC19_workshop_Wushi_Dong.pdf){:target="\_blank"}

* <b>W. Dong</b>, M. Keceli, R. Vescovi, H. Li, C. Adams, E. Jennings, S. Flender, T. Uram, V. Vishwanath, N. Ferrier, N. Kasthuri, P. B. Littlewood, <i>Scaling Distributed Training of Flood-Filling Networks on HPC Infrastructure for Brain Mapping</i>, 2019 Argonne Leadership Computing Facility (ALCF) Simulation, Data, and Learning Workshop: Success Stories of Science Applications Using Simulations, Machine Learning Tools and Data Science. (Invited; Ocotober 2019)

<h2>Press & Mentions</h2>
* [To map the human brain, researchers first look to the octopus](https://sing.uchicago.edu/2022/08/16/to-map-the-human-brain-researchers-first-look-to-the-octopus/)

* [What’s New in HPC Research: Brain Mapping, Earthquakes, Energy Efficiency & More](https://www.hpcwire.com/2019/06/12/whats-new-in-hpc-research-brain-mapping-earthquakes-energy-efficiency-more/)

* [Argonne Researchers to Share Scientific Computing Insights at SC19](https://www.hpcwire.com/off-the-wire/argonne-researchers-to-share-scientific-computing-insights-at-sc19/)
