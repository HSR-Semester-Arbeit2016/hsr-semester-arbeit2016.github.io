---
layout: post
title: "Project Kickoff with ASN"
date: 2016-09-23
categories: "general"
author: "Roberto Cuervo, Konrad Höpli"
---
## Friday, 23. September 2016, *Project Kickoff with ASN*

Today we had the project kickoff of our student research project together with the initiating company ASN.

## Attendees:
* Simone Reiser
* Dominic Studer
* Oliver Augenstein
* Roberto Cuervo-Alvarez
* Konrad Höpli

## Covered topics in order:
* Introduction
* Project idea and existing tools
* Technical aspects (AR/VR, options therein, filter on running camera)
* Requirements (or lack thereof)
* Organisational aspects (expected progress, license, bachelor-project-potential)
* Test DUI-simulator
* Licenses of used development tools
* Organisation and coordination

## Introduction [Fachstelle: Am Steuer Nie (ASN)](https://www.fachstelle-asn.ch)

The non-profit organisation Fachstelle Am Steuer Nie (ASN) pursues the reduction of the traffic accidents caused by alcohol, drugs or medicaments consumption. The prevention bases on different projects where the user experience is central.
ASN wants to introduce a modern technology like Augmented Reality in order to be more attractive for young people.

## Existing tools of ASN to visualize/simulate alcohol influences

### Influence Glasses 

#### very drunk

- extremely limited field of view & blurryness
- duplicated images
- different focus on individual eyes
- very impactful on well-being

#### drunk:
- limited field of view & blurryness

#### slightly intoxicated:
- limited field of view & blurryness

### Driving Under Influence-Simulations

- Two versions with a couple of differences available (French/German)
- Played from within a kind of car-seat with regular&realistic car-controls with a TV in front
- Small, separate key-pad used to control obstacles and influences:
  - different kinds of weather
  - daylight/nighttime
  - such as lifeforms running onto the road and force the driver to break
- influence-simulation with different levels/stages
  - similar effects to the glasses
  - input-delay (time until actions like steering take effect)
  - after-effect (time the delayed action plays out)
- display of statistics 
  - upon end-of-run
    - average speed and comparison to intended speed (too slow/fast compared to road signs)
    - list of 'misdemeanors'
  - upon crash
    - initial speed when obstacle appeared
    - expected break-time & distance
    - actual break-time & distance

## Technical aspects (AR/VR, options therein, filter on running camera)

#### Virtual Reality (VR)
VR is a term used for an immersive simulation that takes the user into a created environment (either completely synthetic, using real world content or any mixture of the two).
Examples: 360° videos, computer-generated VR

#### Augumented Reality (AR)
AR is used to describe applications that take real world content (typically via camera-feed) and add additional information or objects to it just like an overlay.
Mixed Reality (MR) is another term used to describe the mixture of virtual and real world content, but it currently is not seeing as much attention as AR and in my opinion stands for the same.
Examples: Plane identifier

## Research so far
The goal of our student research project is to create an app, using any mixture of features belonging to the two technological terms explained above available, in order to create an experience to visualize the influences of alcohol.
What we have looked at so far is the [Vuforia-SDK](http://vuforia.com/) that was recommended by Oliver Augenstein and provides a toolset that simplifies the creation of AR applications. There is a version for Xcode, Android Studio as well as Unity and decision to work with Unity did not take too long at all since that one provides some additional features, allows the development for multiple platforms and is a great opportunity for us to learn about one of the biggest Game Engines out there.
The built-in presets, assets as well as functionalities of Unity also are an amazing resource-pool that we will most likely profit from since a lot of the effects (blurryness, fish-eye-vision, limited field-of-view etc.) we want to simulate are not by any means considered 'something new' and it would definitely take us quite a while to implement them all by ourselves.
Using these tools we already managed to build out first, very basic app for Google Cardboard within the first week and by using a filter on the running camera we managed to eliminate the first of our initial doubts about whether this project is possible.

## Requirements (or lack thereof)
As already mentioned the goal of this research project is to create an app that could be used by ASN as a new tool to interact with their target audience and new way to create an experience of the influence of drugs.
However,  ASN does not have any concrete requirements or ideas about for the final product - since the AR/VR-area is just as new for them as it is for us. So first and foremost this project is going to be about researching the options available and estimating the time they take to implement as well as discussing those with Oliver Augenstein and/or ASN as we go on with the project.
Since the exact effects to reproduce are not (yet) clearly identified, we asked for somewhat scientific information about what effects the influence of alcohol actually has on our vision as well as physical abilities - one could say that we lack personal experience on this regard...

Based on our first impression of the topic and features we have discovered so far we tried to get a bit of feedback from ASN in order to get at least a little bit of a direction in a discussion. 

The following points were a part of that:

- Embedding/using the real world is desired (AR)
- Implementing virtual objects for some kind of an obstacle (avoidance) course
- Bad influence on personal well being probably can not be simulated well, but the behaviour of virtual objects can be changed accordingly
- Interaction with virtual objects would be nice and could be used to implement input-delay
- Advanced: external controller to configure the individual, negative influences would be great
- Potential 'lags' due to lack of well-being during the use of Google Cardboard are not an issue since they can be seen as 'adding to the immersion'
- Usage of image-effects & filters should not be excessive since the Cardboard-experience itself comes with its issues

## General information and topics

- The new AR/VR technology is very likely to be a great thing in regards to appealing to teens and young adults that are ASNs primary target audience
- There would be a budget available at ASN in case we would ever need to aquire something specifically for our project
- The license of the finished app will be a shared license between ASN and us (including HSR)
- The app shall be developed for android only even though the used tools would easily allow uf to build it for iOS
- A release within the Android store is not planned or expected so far
- The student research project will have an agile organisation to match the many open questions and goals -> iterative definition of work items and their estimations (potentionally with input from ASN on their importance/desirability)
- Whether this project is eligible to be used as a bachelor thesis will be decided in the final stages or once the overall functionality requirements and possibilities have been worked out