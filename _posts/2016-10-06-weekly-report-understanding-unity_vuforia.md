---
layout: post
title: "Understanding Unity and Vuforia"
date: 2016-10-06
categories: "general"
author: "Roberto Cuervo, Konrad Höpli"
---
## Thursday, 10. October 2016, *Understanding Unity and Vuforia*

My primary goal of this week aside from finishing the setup of our development-environment has been achieving an improved understanding of the tools we are using in this research project.
Only two weeks ago we followed step-by-step guides to build and sligthly customize our very first Google Cardboard-App and while we already were successful back then, the way to it has definitely been everything but smooth.
One of the main reasons for that was the severe lack of documentation on the side of the Vuforia SDK, which we thought was going to be the primary toolkit we would be using in this project. By now we have a better understanding of how the SDK may be essential to easily building a Google Cardboard-App, but we really are only going to use a small fraction of the available features by Vuforia (the AR camera-prefab for example) while relying on a lot of given functionalities of Unity.

## Vuforia

Due to the absence of basically any kind of documentation on the available features and their usage, we had to rely solely on the samples provided on the official website. The additional issue with that is the fact, that these samples are not by any means some kind of step-by-step guide that really lead you to a good understanding of what is happening but instead raise confusion *if you are completely unfamiliar with Unity and its IDE*.
All these samples are in essence just a couple of scenes stiched together that use a subset of all the features Vuforia has to offer and while you get to see them fully implemented and in action if you do it right, the chance that you can implement them yourself or get a remotely decent understanding of when exactly you may need/use certain features is very much lacking in my eyes.
On the bright side, I currently can only see us using up to three features in total aside from the already mentioned AR-Camera and therefor might be able to 'solve the issue by avoidance'...

## Unity
Unity provides a really impressive toolkit regarding both comfort but also size and even though we managed to get stuff to work without writing a single line of code the IDE was just so completely different from everything we are used to and the available features and perspectives also raised an interesting mixture of confusion as well as amazement. But fortunately the amount of documentation and well made tutorial videos available for Unity hardly knows any boundaries and really helped with get a good and fast start.
The following links were the ones that I personally thought were the most essential for basically anyone starting out with Unity, but also our project specifically without covering the existing effect-functionalities that Roberto is having a closer look at:
* [Interface Overview Tutorial](https://unity3d.com/learn/tutorials/topics/interface-essentials/interface-overview?playlist=17090)
* [Scene View Tutorial](https://unity3d.com/learn/tutorials/topics/interface-essentials/scene-view?playlist=17090)
* [Game Object and Components](https://unity3d.com/learn/tutorials/topics/interface-essentials/game-objects-and-components?playlist=17090)

So, what's next after finally getting this basic understanding?
Most likely the first attempt to bring the filter-effects Roberto has been working on and some virtual objects together in a next attempt to see how immersive this can actually get.