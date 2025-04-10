---
title: "Machine Learning Projects"
summary: "I completed a series of assignments in a machine learning course, demonstrating proficiency in implementing and analyzing supervised learning algorithms and cross-validation techniques."
date:  2023-12-16T19:48:26-08:00
# weight: 1
aliases: ["/mlprojects"]
tags: ["Projects", "Machine Learning Projects"]
author: "Me"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: true #change this to publish
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
UseHugoToc: true
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

The course began by applying the nearest neighbor algorithm to the MNIST dataset. This dataset includes 60,000 training images and 10,000 testing images, each of which are 28x28 grids depicting hand-written numbers. Each image has a correspoding label which is used as a classifier. For my nearest neighbor algorithm, I first defined a function to find euclidian distance.

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

To improve the accuracy, I implemented k-fold cross validation:

```
    Given a value k, split the dataset into k equally-sized folds.
    for each fold:
        create the corresponding test and training set
        
        get the accuracy of the nearest neighbor algorithm on these sets

    return the average accuracy from all the folds 
```

By running this algorithm on 20 different values for k ranging from 5-100, I was able to recognize that increasing the number of folds would improve the accuracy by reducing the bias but at a higher computational cost. 

### Classifying MNIST digits using generative modeling

To study generative modeling, I revisited the MNIST digits dataset. To test the accuracy of our test, we first created a validation set using 10,000 of the 60,000 training points. This was simply done by spliting off the last 10,000 training set into the new set. From there, I created an a function that found the parameters needed to fit the Gaussian model: the average vectors, mu; the covariance vectors sigma, and the frequencies, Pi. This is the algorithm I used:
    

```
    for each label [0-9]:
        // Fit a Gaussian generative model to the training data

        c = regularization term(I used 3,000)
        mu vector(784) = np.mean of all training vectors with current label
        Sigma vector(794) = np.cov of all training vectors + (c * identity matrix)

        Pi(1) = frequency of current label
    
    //combine all the found values into our parameters such that they have following dimensions
    return parameters mu(10x784), sigma(10x784x784), and Pi(10x1)
```

Displaying the mu parameters gave the expected representation for each label. To make predictions, I used the `skikit.learn`'s `multivariate_norm` function and got noticed that of the 10,000 values in the validation set, the model made 426 errors. This gave me an error rate of 0.0426. Of these errors, it was clear how the images were similar to the average images for the predicted label.

![gaussian_wrong_predictions](images/gaussian_wrong_predictions.png)

### Ridge and Lasso Regression

In learning other regression methods, I covered Ridge and Lasso Regression. Both of these are extensions of linear regression in that they add a regularization term to handle different qualities of our desired model. Ridge regression uses the L2-norm of the coefficients to shrink the coefficients while Lasso uses the L1-norm. Since the L2-norm uses the squares of the magnitudes of the coefficients, the Ridge regression is better in situations where all features are relevant. On the other hand, Lasso regression has the potential to completely eliminate features, since the L1-norm is found using the absolute value of the difference in the coefficients. This makes Lasso regression suitable in cases where we need to cut down the number of features to find the most relavent ones. 

### Binary Logistic Regression

To practice binary logistic regression, I used a shortened version of UCI's heart disease dataset which consists of 303 datapoints, each of which are vectors of length 14: 13 attributes and a binary label. I first partitioned the dataset into 200 training points and 103 test points. After that, I fit a binary logistic model using the `sklearn.linear_model`'s function by the same name. The test error I received was 0.1553. Using 5-fold cross-validation, my error estimate on the training set was 0.18. 

### Stepwise Forward Selection



### Coordinate Descent

### Binary Perceptron

### Kernel Perceptron

### Multiclass Perceptron
