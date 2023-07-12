---
layout: splash
title:  "MIT Fishery Monitoring With Computer Vision"
date:   2022-02-16
comments: true
categories: Computer-Vision
description: "A computer vision-based system to count fish under various conditions entering Massachusetts Fisheries."
keywords: computer vision, mlops, conservation
show_date: true
---

**A grant-funded computer vision-based system to count fish under various conditions entering Massachusetts Fisheries.**


[![Click to view video](/assets/images/mitfishery/annotated_counter.png)](https://youtu.be/3UxDNxzXF5U)


Public Demo of dashboard
<div style="display: flex; justify-content: center;">
  <iframe
    src="https://aus10powell-mit-fishery-app.hf.space"
    width="1100"
    height="1050"
    display="block"
     scrolling="yes"
      frameBorder="0"
       float="right"
  ></iframe>
</div>

## MIT Fishery
I am currently working on an ongoing project to detect and count fish in Massachusetts Fisheries. This project is funded by a grant from the federal government. I started working on this project in 2022, and I am working individually with a research professor and MIT PhD students. I am responsible taking the initial research project and making it operational: 1) Making model performant enough to count fish  2) Working with research grant funding to set up appropriate infrastructure and 3) deploying the infrastructure.

## Overview
Fisheries populations have a large impact on the U.S. economy. Each year the U.S. fishing industry contributes 90 billion dollars and 1.5 million jobs to the U.S. economy. Each species may serve as a predator or prey for another. In this regard, fisheries populations are interconnected and dependent. While humans may depend on these populations as a source of sustenance (food, goods, etc.), humans can also negatively impact population growth. Barriers to migration, pollution, overfishing, and other forms of human-interference may impact spawning patterns of fisheries species. In 2014, 17% of U.S. fisheries were classified as overfished. Therefore, it is necessary to monitor these fisheries populations to determine when policy must be changed in efforts to maintain healthy oceans.

Many groups, including NOAA Fisheries, state agencies, as well as regional fisheries councils and local municipalities, deploy camera and video equipment to monitor fisheries populations. Large amounts of video and photographic data are gathered at timed intervals. However, not all photos contain aquatic life. Currently, employees at these agencies among others are responsible for manually annotating the gathered videos and photos; this means they identify and count the relevant aquatic specimens in the data. Not only is this an inefficient use of time and resources, but also it can lead to inaccurate results due to human error. NOAA Fisheries Management can make a significant improvement in time and resource use through automation of the annotation process.


Throughout the project, I have made significant progress in addressing these challenges and have achieved promising results. Here's an overview of the key aspects and advancements made:

### Object Detection Algorithm:
The initial challenge involved designing an accurate object detection algorithm specifically tailored for fish tracking. It required careful consideration of model architecture, hyperparameters, and dataset selection. Through iterative experimentation and fine-tuning, I have made substantial improvements in detecting fish instances reliably and effectively.

### Tracking and Counting:
To track and count fish objects effectively, I needed to establish their identity from frame to frame. This approach proved successful in accurately tracking the same fish over time, ensuring continuity in object identification.

The ["botsort" algorithm](https://arxiv.org/abs/2206.14651) leverages motion patterns to estimate object displacement, matches appearances to maintain consistency across frames, and predicts future positions based on historical trajectory data. This comprehensive approach has significantly improved tracking accuracy and facilitated reliable fish counting.

### Dataset Selection and Training:
"garbage in, garbage out." So, I spent a good amount of time curating a diverse dataset with annotated fish images and videos. Lighting conditions, backgrounds, and different fish species – I covered it all. By training the model on this top-notch dataset, I witnessed significant improvements in detection performance.

### Holdout Set for Validation:
To make sure our counting game is on point, I set aside a holdout set of videos with ground truth fish counts. It's like having a benchmark to compare against. I tested the algorithm's count predictions against the ground truth, giving us valuable insights into its accuracy and effectiveness. No fishy business here!

#### Bayesian Optimization with wandb.sweeps:
I gained enough confidence to narrow down my parameter search space. With the help of wandb.sweeps' Bayesian optimization capabilities, I let the algorithm do its magic overnight. It efficiently explored the parameter space and brought me some impressive results. It's like having a super-smart assistant working while I catch some zzz's.

#### Data Augmentation
Due to the extreme varition in camera quality and image quality the following types of image augmentation have become extremely usefuly in the quality of model:

##### Example Image Augmentation
[![Click to view video](/assets/images/mitfishery/example_augmentation.png)]

##### Example of Challenging Atmospheric Conditions for ID-ing of Fish for Purposes of Tracking
[![Click to view video](/assets/images/mitfishery/murky_water_2018.png)]

#### Example of the need for more data when counting AND tracking
[![Click to view video](/assets/images/mitfishery/two_fish_2018.png)]
