---
title: "Social Compass"
summary: "As a part of my Software Development Class at UCSD, a team of six developers including myself designed and created a Social Compass Mobile App."
date:  2023-03-01T20:48:26-08:00
# weight: 1
aliases: ["/SocialCompass"]
tags: ["Projects", "SocialCompass"]
author: "Me"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: true
draft: false
hidemeta: true
comments: false
description: "Duration: January 2023 - March 2023"
canonicalURL: "https://canonical.url/to/Projects/SocialCompass"
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
Github: https://github.com/CSE-110-Winter-2023/cse-110-project-cse110-team-10

## Project Desciption

As a part of my Software Development Class at UCSD, a team of six developers including myself designed and created a Social Compass Mobile App.
In order to practice Agile Development, our project was structured into Iterations and Milestones.


## Milestone Planning
At the beginning of each milestone, we went through a planning phase that included:

### <b>Risk Analysis</b> and Calculation of <b>Initial Velocity</b>

Before we did anything else, we came up with any potential risks we might encounter during the project. 
This step is vital as it helped us identify and mitiate any challenges before they occur. Moreover, it allowed us to 
calculate an initial velocity that helped us determine an estimate of how much work our team could do over the milestone. 

Example from Milestone 1:
```
Risk: Not Meeting Enough
    Description: We have only 3 hours a week in common where we can all meet
    Severity: High
    Resolution: We have blocked off those three hours in our schedules. We will do our
        stand-ups before class on Mondays and Wednesdays and after class on Fridays. We will
        also be pair programming to keep each other accountable.
    Status: Resolved
```

### Creating <b>User Stories</b> and <b>Planning Poker</b>

When creating our user stories and going through the planning poker, we made sure to iron out any assumptions that we had 
regarding the given story. We then estimated how many hours the stories would take. To describe the stories and their functionality,
we created scenarios that detailed how the user might utilize the topic of our stories.

Example from Milestone 1:
```
User Story 1: Prompt User for Locations
    Priority: High
    Estimation: 8 hrs
    
    As a user,
    I want to be prompted with the locations for one to three locations
    So that I can feel more connected to my family and friends.
```

![Milestone1-UI-Screens](images/Social%20Compass%20-%20m1%20ui%20screens.jpg)

### Creating <b>Tasks</b> for each User Story

After we were settled with our user stories, we split them up into digestible tasks. Each task was also allocated
a certain amount of hours to give us an idea of how best to split up our time.

Example from Milestone 1:
```
User Story 1: Prompt User for Location
    Task 1: Design Location Input UI
        - Design a UI that prompts for up to 3 locations to handle inputting longitude and
        latitude
        - Estimate: 5 hrs
    Task 2: Implement View Connections
        - Implement connections that allow the user to traverse to and from the prompt
        view as needed.
        - Estimate: 1 hrs
    Task 3: Testing and Optimization
        - Test the implementation on different Android devices to ensure compatibility
        - Refine and polish the user interface based on group feedback
        - Estimate: 1 hrs
    Task 4: Input Requirement Handling
        - Set error handling for incorrect inputs in the location prompt
        - Alert the user & reprompt if the following is inputted for the location prompt:
        empty (no value passed in), any input with non-numeric characters
        - Estimate: 1 hrs
```

### Planning out the two <b>Iterations</b> in the Milestone

Since we were limited to a ten week course, we only had two weeks per iteration. Therefore, we had to properly split our stories
based on immediacy and the estimated time required per story.

Example from Milestone 2: 
```
Iteration 1: (Total: 41 hrs)
    User Story 3: Add Friends via UID (16 hours)
    User Story 4: Display Friend’s Location on Compass (24 hours)
    Developer Story 1: Test SBST #3 (1 hour)
Iteration 2: (Total 45 hrs)
    User Story 1: Prompt User for Name (4 hours)
    User Story 2: Display UID to User (8 hours)
    User Story 5: Display GPS Status (8 hours)
    User Story 6: Zoom Out/In on Compass (24 hours)
    Developer Story 2: Test SBST #1, #2 and #4 (1 hour)
```

### Scenario-Based System Tests

Based on the user scenarios given to us, we planned and built system tests to ensure we are correctly implementing the requirements
given to us.

### Population of the <b>Github Boards</b> to reflect all the stories, tasks, and testing 

Finally, all the planning we had done was deployed through Github Boards. This way the six of us were able to cohesively keep 
track of our progress in the project throughout the iterations. Every week, we had three standups where all of the team 
members cut time out of our day to meet and share the progress we made, the progress we plan on making, and also attempted 
to give solutions to problems brought up by other team members. 

Completed Big Board from Milestone 1:

![Milestone-1-Big-Board](images/Social%20Compass%20-%20m1%20big%20board.jpg)

