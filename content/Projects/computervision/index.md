---
title: "Computer Vision Projects"
summary: "I built a series of programs which explored different computer vision concepts"
date:  2023-12-16T19:48:26-08:00
# weight: 1
aliases: ["/computervision"]
tags: ["Projects", "computervision"]
author: "Me"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: true
draft: false
hidemeta: true
comments: false
description: "Duration: June 2022 - July 2022" 
canonicalURL: "https://canonical.url/to/Projects/computervision"
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
math: true
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

I built a series of programs which explored different computer vision concepts as a part of my Computer Vision course at UCSD. 

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

## Edge and Corner Detection

To implement edge detection, I first smoothed the images using a 9x9 Gaussian kernel so that I didn't accidently consider any noise as an edge. I then computed the image gradient in the horizontal and vertical directions to finish isolating the edges.

|  |  |  |  |
| - | - | - | - |
| ![hw2_geisel_original](images/hw2_geisel_original.png) Original| ![hw2_geisel_smoothed](images/hw2_geisel_smooth.png) Smoothed| ![hw2_geisel_gradmag](images/hw2_geisel_gradmag.png) Gradient Magnitude| ![hw2_geisel_graddir](images/hw2_geisel_graddir.png) Gradient Direction|

To implement corner detection, we made use of the properties of the second moment matrix of local regions in the image. By making use of this matrix, I was able to find 100 corners with the largest minor eigenvalues.

![hw2_corner_eigenvalues](images/hw2_corner_eigenvalues.png)
![hw2_corner](images/hw2_corner.png)

## SSD and NCC Matching

In order to find matching correspondances between two images, I implemented two methods: Sum Squared Difference(SSD) Matching and Normalized Cross-Correlation(NCC) Matching. The first one computed the "matching score" between two images using the sum squared difference of two windows. Using the NCC Matching function, I then created a naive matching function to find the best matches between two images and display them. 

$$
    SSD = \sum_{x,y} |W_1(x,y) - W_2(x,y)|^2
$$

$$
    NCC = \sum_{x,y} \tilde{W}_1(x,y) \cdot \tilde{W}_2(x,y)
$$
$$
    \text{where } \tilde{W} \text{ is a mean-shifted, normalized version of W}
$$
![hw2_naive_match](images/hw2_naive_match.png)

## Epipolar Geometry

Since the naive matching function had some obvious errors due to the high matching complexity, I further explored epipolar lines as an additional factor to link two images. I began with computing the Fundamental Matrix for each image and plotted the epipolar lines through some corners found using the previous corner method.

| | | |
| - | - | - |
| ![hw2_epipolar_dino1](images/hw2_epipolar_dino1.png) | ![hw2_epipolar_md1](images/hw2_epipolar_md1.png)| ![hw2_epipolar_hammer1](images/hw2_epipolar_hammer1.png)|
| ![hw2_epipolar_dino2](images/hw2_epipolar_dino2.png) | ![hw2_epipolar_md2](images/hw2_epipolar_md2.png)| ![hw2_epipolar_hammer2](images/hw2_epipolar_hammer2.png)|

## Image Classiﬁcation Using Bag-of-words

Putting together everything I have learned, I created a simple classifier using the bag-of-words method. First, I select some regions in the images from which I can extract some features. I did this in two different ways: uniformaly sampling and sample on corners. 

![hw3_interest_points](images/hw3_interest_points.png)

After getting my interest points, I went on to extracting my features through two methods. The first one was OpenCV's SIFT function and the second was by selecting image patches around each feature point. From here, I built a visual vocabulary using k-means clustering as implemented in sklearn's cluster library. I first compared each feature vector with the k-cluster centers and assigned it to the closest cluster. I then updated the cluster center by taking the average of all the points that were assigned to it and repeated these two steps until there were no more changes to the cluster centers. Now that the clusters were defined, I went on to use the k-nearest neighbors to compare test images and classify my images. Following is my resulting test accuracies for 3-NN and 5-NN.

![hw3_test_accuracies](images/hw3_test_acc.png)
