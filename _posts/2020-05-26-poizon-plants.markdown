---
layout: post
title:  "Poizon Plants"
date:   202-05-26
comments: true
#image: ../assets/images/poizon_plants/
categories: Computer Vision AI Machine-Learning Poison-Oak Plants
description: "An attempt to make a vision classifier for poison oak practical."
---
*Classifying poison oak "in the wild"*

## Motivation 
I have gotten poison oak multiple times. While it is debated whether continued exposure to the oil found on the plant that causes the allergic reaction gets worse over time or better, the fact remains it not fun. Particularly in certain areas of your body.

What is confirmed is that while some people do not have an allergic reaction, there will be no rash with continued exposure per [American Osteopathic College of Dermatology](https://www.aocd.org/page/PoisonIvyDermatiti) (among other sources). So basically no one is really safe.

Those of us living in California for more than a few years are likely familiar with or at least have heard of poison oak. But very few people native to California (much less one of the millions of tourists) actually are able to identify it it is not in it's signature glowing, oily red.

### Cold-start problem
Perhaps the obvious place to start for labeled images of poison oak was Google. The easiest method I've found so far to do this is a Chrome extension [here](https://chrome.google.com/webstore/detail/imageye-image-downloader/agionbommeaifngbhincahgmoflcikhm?hl=en).
Interestingly enough, there were already a few apps on the iOS store that were simple classification apps like the one I proposed. When I tested these against my gold-standard dataset, they had very similar performance the model that had been trained on Google Images. Go figure.

## Modeling


## Important Lessons:
* **Think your data is well-labeled? Think again...and again:** 
    * Despite having gone through and labeled, by hand, thousands of images, examining images with top log-loss showed the my human error. I think one reason for this is during the labeling process, I had additional context for "yes this is poison oak" due to having walked by a large bush of poison oak already. When looking only at the photo that was taken with no additional context, which is what the neural net is doing, it was not clear to my human eye.
* **How do you know when your data is enough?**
    * Particularly for the practicality of my problem where a region taken with your phone "may contain poison oak", it wasn't immediately clear if I had pictures with sufficient variation. An example of when this issue first surfaced was when a plant that was not poison oak but was reddish immedietly caused trouble for the algorithm. It was a bit of a Catch-22, because while red is such strong indicator (for humans and neural nets) for being a sumac plant, *red is definitly **not*** a rule for a plant being poison oak.
    <figure class="half">
    <a href="/assets/images/poizon_plants/IMG_2268.jpg"><img src="/assets/images/poizon_plants/IMG_2268.jpg" style="width:100%;height:90%"></a>
    <a href="/assets/images/poizon_plants/IMG_3408.jpg"><img src="/assets/images/poizon_plants/IMG_3408.jpg" style="width:100%;height:90%"></a>
    <figcaption>Strong red color can be indicative of poison oak but also a strong false positive.</figcaption>
    </figure>

* **A great comparison:**
    <figure class="half">
        <a href="/assets/images/poizon_plants/IMG_4273.jpg" ><img src="/assets/images/poizon_plants/IMG_4273.jpg"  ></a>
        <a href="/assets/images/poizon_plants/IMG_4274.jpg"><img src="/assets/images/poizon_plants/IMG_4274.jpg"  ></a>
        <figcaption>Caption describing these two images.</figcaption>
    </figure>

### References
* **[Poizon Plant iOS app](https://apps.apple.com/us/app/poizon-plant/id1475980295 "Link to iOS App")**

### Papers I checked out
* [A Leaf Recognition Algorithm for Plant Classification Using Probabilistic Neural Network](https://ieeexplore.ieee.org/abstract/document/4458016)
* [Plant Disease Detection Using Deep learning](https://arxiv.org/abs/2003.05379)