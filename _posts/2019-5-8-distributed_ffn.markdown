---
title: "Scaling Distributed Training of Flood-Filling Networks on HPC Infrastructure for Brain Mapping"
layout: post
date: 2019-5-8 15:10
tag: Deep Learning, Distributed Training, HPC, Synchronous SGD, Learning Rate Scaling, Connectomics
headerImage: true
projects: true
hidden: true # don't count this post in blog pagination
description: "Distributed training of Flood-Filling Networks (FFNs) for instance segmentation in 3d volumes implemented with Horovod."
category: project
author: Wushi Dong
externalLink: false
--- 

Mapping all the neurons in the brain requires automatic reconstruction of entire cells from volume electron microscopy data. The raw data and human anotations are shwon in the figures below.

![Project Image]({{ site.url }}/assets/fib25_training1.png)

The Flood-Filling Networks (FFN) architecture can achieve leading performance. 

![Project Image]({{ site.url }}/assets/ffn1.png)

However, the training of the network is computationally very expensive. In order to reduce the training time, we implemented synchronous and data-parallel distributed training using the Horovod framework on top of the published FFN code. We demonstrated the scaling of FFN training up to 2048 Intel Knights Landing (KNL) nodes (131,072 cores) at Argonne Leadership Computing Facility (ALCF). We investigated the training accuracy with dierent optimizers, learning rates, and optional warm-up periods. 

![Project Image]({{ site.url }}/assets/scaling_efficiency.png)

We discovered that square root scaling for learning rate works best beyond 16 nodes, which is contrary to the case of smaller number of nodes, wherelinear learning rate scaling with warm-up performs the best. 

![Project Image]({{ site.url }}/assets/lr_acc.png)

Our distributed training reaches 95% accuracy in approximately 4.5 hours on 1024 KNL nodes using Adam optimizer, which is about 3 times faster then previous best results.

![Project Image]({{ site.url }}/assets/training.png)

We visualize the 3D volume segmentations of neurons in the image below.

![Project Image]({{ site.url }}/assets/fib25_vis1.png)
