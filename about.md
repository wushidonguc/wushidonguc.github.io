---
title: About
layout: page
---
![Profile Image]({{ site.url }}/assets/images/profile.jpg)

<h2>Bio</h2>
Hi, my name is Wushi Dong. I recently obtained my Ph.D. in Physics from the University of Chicago this August. <br/>

My latest project is on scaling distributed training of Flood Filling Network (FFN) for brain mapping at the Argonne Leadership Computing Facilities (ALCF), where I implemented synchronous and data-parallel distributed training on top of the published Google’s FFN code. My developed code was successfully scaled to 2048 Knights Land (KNL) nodes (131,072 cores) on the Theta supercomputer, achieving the same accuracy as previous best methods with significantly less time cost. <br/>

I gained my deep learning training during an internship at IBM Research, where I worked on developing a state-of-the-art video action recognition algorithm. My developed software at that time was later published on GitHub and now ranks top-5 in popularity among 40 repositories under the same category. <br/>

As for my PhD training, I completed an innovational project on developing a novel computational pipeline for modeling quantum electron transport in semiconductor devices, where I efficiently implemented numerical methods including Finite Difference Method (FDM), non-linear Poisson solver, self-consistent iteration, etc. This project resulted in both first-author publication in the American Chemical Society's (ACS) leading journal in the field, and {\it swan}, an original open-source parallel software in C++ with MPI. <br/>

Equipped with the knowledge of both software and hardware, I am passionate about tackling big real-world problems by combining deep learning and massive modern computing power. <br/>

<h2>Competencies</h2>
<ul class="skill-list">
	<li>Deep learning (Keras, TensorFlow, Horovod distributed training)</li>
	<li>High-performance computing (MPI, cloud computing)</li>
	<li>Python</li>
	<li>C++</li>
	<li>Theoretical physics</li>
	<li>Device modeling</li>
	<li>Computer vision (3D segmentation, video classification)</li>
</ul>

<h2>Projects</h2>

<ul>
	<li><a href="{{ site.url }}/distributed_ffn">Scaling distributed training of Flood-Filling Networks (FFN) on HPC infrastructure for brain mapping</a></li>
	<li><a href="{{ site.url }}/two-stream-action-recognition-keras">Two-stream CNNs for video action recognition (Keras)</a></li>
 	<li><a href="{{ site.url }}/swan"> Swan: An open-source C++ software for nanoscale quantum electron transport simulations</a></li>
</ul>
