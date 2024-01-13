---
title: "American Sign Language Translator"
summary: "Duration: June 2022 - July 2022 | Github: https://github.com/AshwinKTyagi/ASLTranslator"
date:  2022-07-01T20:48:26-08:00
# weight: 1
aliases: ["/ASLTranslator"]
tags: ["Projects", "ASLTranslator"]
author: "Me"
# author: ["Me", "You"] # multiple authors
showToc: false
TocOpen: true
draft: false
hidemeta: true
comments: false
description: "Duration: September 2023 - December 2023"
canonicalURL: "https://canonical.url/to/Projects/ASLTranslator"
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
Github: https://github.com/AshwinKTyagi/ASLTranslator

## Project Desciption

I partnered with a team member to develop an ASL translator that processes live video input, capturing still images,
and utilizing a neural network for real-time translation. 
However, There are some limitations to our design. For starters, we used kaggle's [Sign Language MNIST](https://www.kaggle.com/datasets/datamunge/sign-language-mnist) to train and test our neural network.
While it made training our model rather simple, it was difficult to doctor the inputs to match the format of the train data. 
This led to a much larger error rate in real practice. Moreover, the Sign Language MNIST exclusively comprises images featuring hands with lighter skin tones. It does not include data with hands of darker skin tones, leading to further inaccuracies when testing.

Although the neural network does not always return the correct output, we successfully created a functional ASL translator prototype;
showcasing the potential for real-time sign language translation using computer vision and machine learning.

#### Design Process:
1. Use OpenCV to get video input and process it using MediaPipe's Hands module
    - MediaPipe's Hand module allowed us to grab and focus on specifically the user's hand
2. Build and Save the neural network so that we don't need to train and test the net every single run
3. Combine both these to get a string of outputted characters
4. Run string of characters through SpaCy, a natural language processing module.

#### Current Issues:
- There is no implementation for characters that require movement: J and Z.
- The string prior to the natural language processing is not the cleanest to work with and depends on how often the characters are read in from the video input.
