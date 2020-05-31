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


I have gotten poison oak multiple times. 


### Important Lessons:
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