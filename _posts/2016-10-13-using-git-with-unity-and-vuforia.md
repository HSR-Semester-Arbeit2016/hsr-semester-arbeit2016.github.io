---
layout: post
title: "Using Git with Unity and Vuforia"
date: 2016-10-13
categories: general
author: "Roberto Cuervo, Konrad Höpli"
---
## *Using Git with Unity and Vuforia*
When we created our first Unity-project on our GitHub-repository, we had the option to select a .gitignore-file for Unity-projects and thought that was most definitely all that was important in order to correctly use version-control.

Upon the first checkout we stumbled on a suboptimal result though, since although everything related to the project appeared to have been commited correctly, any scenes added to the projects hierarchy have been removed. They were safely stored within the asset-folder and could be added again without further issues aside from some lost property-settings in the inspector, but that is definitely not how we imagine the expected usage to go.

Our first idea was that the Vuforia-ASK might need a slightly different .gitignore, since the only thing used in the first project was its AR-camera-prefab, but after a quick Google-search and a comparison we were able to quickly eliminate that idea.
We then investigated the save-feature of Unity and whether we used that correctly 


