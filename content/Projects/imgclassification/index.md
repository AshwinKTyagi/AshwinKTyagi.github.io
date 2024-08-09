---
title: "Computer Vision Projects"
summary: "I built a series of programs which explored different computer vision concepts"
date:  2023-12-16T19:48:26-08:00
# weight: 1
aliases: ["/imgclassification"]
tags: ["Projects", "imgclassification"]
author: "Me"
# author: ["Me", "You"] # multiple authors
showToc: false
TocOpen: false
draft: true
hidemeta: true
comments: false
description: "Duration: June 2022 - July 2022" 
canonicalURL: "https://canonical.url/to/Projects/imgclassification"
disableHLJS: false # to disable highlightjs
disableShare: false
disableHLJS: true
hideSummary: false
searchHidden: true
ShowReadingTime: false
ShowBreadCrumbs: false
ShowPostNavLinks: false
ShowWordCount: false
ShowRssButtonInSectionTermList: false
UseHugoToc: false
cover:
    image: "<image path/url>" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
editPost:
    URL: "https://github.com/AshwinKTyagi/AshwinKTyagi.github.io/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---
 
## Description

I built a series of programs which explored different computer vision concepts. 

## Photometric Stereo

In this section, I explored the concept of Lambertian Photometric Stereo. Initially, we took in multiple images with a corresponding light source direction and estimated their surface normals and albedo map. After that, we reconstructed the depth map from the surface with a Horn integration technique. Following are the visualizations of the images, albedo map, and surface normals.


|  |  |  |  |
| ------------------- | ------------------- | ------------------- | ------------------- |
| ![hw1_img1](images/hw1_img1.png) Image 1| ![hw1_img2](images/hw1_img2.png) Image 2| ![hw1_img3](images/hw1_img4.png) Image 3| ![hw1_albedo](images/hw1_albedomap.png) Albedo Map|

![hw1_img2](images/hw1_normals_3ch.png) Surface Normals as 3 seperate channels 

|  |  |
| ------------------- | ------------------- | 
| ![hw1_img1](images/hw1_quiver.png) Normals as Quivers | ![hw1_img2](images/hw1_wireframe.png) Wireframe Depth Map|

## Image Rendering

In this part, I rendered an image of a face with two different point light sources using a Lambertian reflectance model. To recreate the 3d image I used two albedo maps, the light sources, and a height map. In the end, I rendered 6 images for each combination of albedo and light source

|  |  |  |
| ------------------- | ------------ | ------------------- | 
| ![hw1_face_albedos](images/hw1_face_albedos.png) Face Albedos | ![hw1_face_heightmap](images/hw1_face_heightmap.png) Heightmap| ![hw1_face_normals](images/hw1_face_normals.png) Surface Normals|

![hw1_face_renders](images/hw1_face_renders.png)