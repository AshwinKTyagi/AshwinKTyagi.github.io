---
title: "Machine Learning Projects"
summary: "I completed a series of assignments in a machine learning course, demonstrating proficiency in implementing and analyzing supervised learning algorithms and cross-validation techniques."
date:  2023-12-16T19:48:26-08:00
# weight: 1
aliases: ["/mlprojects"]
tags: ["Projects", "Machine Learning Projects"]
author: "Me"
# author: ["Me", "You"] # multiple authors
showToc: false
TocOpen: false
draft: false
math: true
hidemeta: true
comments: false
description: "Duration: September 2023 - December 2023" 
canonicalURL: "https://canonical.url/to/Projects/mlprojects"
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

I completed a series of assignments in a machine learning course, in which I learned the basics behind the subject. Since these were part of my classes, I will not be able to share the code for these notebooks and will instead explain my work and findings.

### Nearest Neighbor

The course began by applying the nearest neighbor algorithm to the MNIST dataset. This dataset includes 60,000 training images and 10,000 testing images, each of which are 28x28 grids depicting hand-written numbers. Each image has a correspoding label which is used as a classifier. For my  nearest neighbor algorithm, I first defined a function to find euclidian distance.

$$
    ||x-y||^2 = \sum_{i=1}^{d} (x_i-y_i)^2
$$

Which simply became:

```
np.sum(np.square(x-y))
```

Then, for a vector x, I computed the distances for every row in the training data and returned the one with the minimum distance. The resulting vector was the nearest neighbor.

To analyze my results, I built a confusion matrix using `sklearn`'s built-in function.

### Cross-Validation for Nearest Neighbor

My next assignment helped us learn how to analyze the quality of a classifier. To do so, I used leave-one-out cross validation(LOOCV) to estimate my accuracy for a 1-NN classifer on the `wine` dataset. This dataset included 178 samples, each with 13 features that capture different qualites of the wine. There were three labels for this dataset, `{1,2,3}`, indicating the three possible wineries that the wines originate from.

Pseduocode for LOOCV accuracy:
```
    for every vector in dataset
        find nearest neighbor

        if the prediction is not correct
            errors += 1

    accuracy = errors / length of dataset         
```

My calculated accuracy was 0.77.

To improve te accuracy, I implemented k-fold cross validation:

```
    Given a value k, split the dataset into k equally-sized folds.
    for each fold:
        create the corresponding test and training set
        
        get the accuracy of the nearest neighbor algorithm on these sets

    return the average accuracy from all the folds 
```

By running this algorithm on 20 different values for k ranging from 5-100, I was able to recognize that increasing the number of folds would improve the accuracy by reducing the bias but at a higher computational cost. 



### Classifying MNIST digits using generative modeling

### Ridge and Lasso Regression

### Binary Logistic Regression and Stepwise Forward Selection

### Coordinate Descent

### Binary Perceptron

### Kernel Perceptron

### Multiclass Perceptron
