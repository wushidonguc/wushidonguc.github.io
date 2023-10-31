---
title: "Two-stream CNNs for video action recognition"
layout: post
date: 2018-10-23 20:10
tag: [Deep Learning, Neural Networks, Computer Vision]
headerImage: true
projects: true
hidden: true # don't count this post in blog pagination
description: "We use spatial and temporal stream CNN under the Keras framework to reproduce published results on UCF-101 action recognition dataset."
category: project
author: wushidong
externalLink: false
---

<span style="background-color: #f8f8f8; padding: 20px; border-radius: 0px; display: inline-block; width: calc(100% - 20px);">
Using advanced techniques in spatial and temporal stream convolutional neural networks (CNN) in the Keras framework, we’ve successfully achieved on the state-of-the-art results for the UCF-101 action recognition dataset.<br><br>
[View code >>](https://github.com/wushidonguc/two-stream-action-recognition-keras)<br>
<br>
</span>

<!--
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![DOI](https://zenodo.org/badge/127003611.svg)](https://zenodo.org/badge/latestdoi/127003611)
-->

We build neural networks for video classification by using the spatial and temporal stream CNNs under the Keras framework. We achieved the state-of-the-art results for the [UCF-101 action recognition dataset](https://www.crcv.ucf.edu/data/UCF101.php).

We use UCF101 rgb frames as the spatial input data. We use split #1 for all of our experiments.
We use [the preprocessed tvl1 optical flow dataset](https://github.com/feichtenhofer/twostreamfusion) as the motion input data.
Please refer to our GitHub repo for detailed steps on setting up the above datasets.

## Results
We show the prediction accuracies for the spatial-stream CNN and the temporal-stream CNN and the fused network respectively, and compare with those of the state-of-the-art implmentation.

|      | [Simonyan et al](http://papers.nips.cc/paper/5353-two-stream-convolutional)| Ours  |
------------- | :--------------:    | :----:|
|Spatial      | 72.7%               | 73.1% |
|Temporal     | 81.0%               | 78.8% |
|Fused       | 85.9%               | 82.0% |


## Methods

We implement spatial-stream CNN and temporal-stream CNN and fusion by following [Simonyan et al](http://papers.nips.cc/paper/5353-two-stream-convolutional). The following figure shows the model architecture.
![Project Image]({{ site.url }}/assets/two_stream.png)

### Spatial-stream CNN

We classify each video by looking at a single frame. We use ImageNet pre-trained models and transfer learning to retrain Inception on our data. We first fine-tune the top dense layers for 10 epochs and then retrain the top two inception blocks.

### Temporal-stream CNN

We train the temporal-stream CNN from scratch. In every mini-batch, we randomly select 128 (batch size) videos from 9537 training videos and futher randomly select 1 optical flow stack in each video. We follow the reference paper and use 10 x-channels and 10 y-channels for each optical flow stack, resulting in a input shape of (224, 224, 20).

Multiple workers are utilized in the data generator for faster training.

### Data augmentation

Both streams apply the same data augmentation technique such as corner cropping and random horizontal flipping. Temporally, we pick the starting frame among those early enough to guarantee a desired number of frames. For shorter videos, we looped the video as many times as necessary to satisfy each model’s input interface.


### Testing

We fused the two streams by averaging the softmax scores.

We uniformly sample a number of frames in each video and the video level prediction is the voting result of all frame level predictions. We pick the starting frame among those early enough to guarantee a desired number of frames. For shorter videos, we looped the video as many times as necessary to satisfy each model’s input interface.


<h2>Talks</h2>
<ul class="skill-list">
	<li><b>W. Dong</b>, A. Ozcan, <i>Two-stream convolutional networks for action recognition in videos</i>, Neuroscience Theory Club, Department of Neurobiology, the University of Chicago. (Invited; April 2018)</li>
</ul>

<!--
## References

*  [[1] Two-stream convolutional networks for action recognition in videos](http://papers.nips.cc/paper/5353-two-stream-convolutional)

*  [[2] Convolutional Two-Stream Network Fusion for Video Action Recognition](https://github.com/feichtenhofer/twostreamfusion)

*  [[3] Five video classification methods](https://github.com/harvitronix/five-video-classification-methods/blob/master/README.md)

*  [[4] UCF101: A Dataset of 101 Human Actions Classes From Videos in The Wild](https://arxiv.org/abs/1212.0402)
-->

