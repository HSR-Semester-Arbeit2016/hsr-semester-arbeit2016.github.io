---
layout: post
title: "Virtual objects and interaction in AR"
date: 2016-10-14
categories: 
author: "Roberto Cuervo, Konrad Höpli"
---

# Virtual objects and interaction in AR

After acquiring a better understanding of Unity during the last couple of weeks, I tried to apply some of that knowledge in a little excursion that could be of use for later stages of our project.

The different options available for world-centering I talked about were the basics for the layout of the world around which we could build some virtual objects, but how feasible and difficult is it to actually interact with such objects in an AR environment?

## Static virtual objects

The world center of these objects would be the example stones image target (with perfect stats for identification) that is available on the Vuforia-website and a printed out picture of that image can then be placed literally anywhere. Once the user of the Google Cardboard app looks upon the printout, the virtual objects associated with it will be initialized and displayed.

I used some of the simplest 3D objects (a sphere and a cube) available by default in Unity for the purpose of keeping it simple.
The cube serves as the static platform and is set not to be affected by gravity, so it will remain right on the image target at all times.
The sphere is set to not ignore the gravity and I added a tiny physics component named 'bouncy' to, well, make it bounce off the cube-platform placed directly below.

Fortunately Unity also provides default colliders with these objects so do not have to implement any of those ourselves in order to play actually around with the objects or let them interact with each other.	

## User interaction

Since I actually wanted to test the interaction with the objects and by default there of course is no collider associated with the wearer of the Google Cardboard, I simply attached another static cube to the VR-camera-component and used that instead.
For a game idea later on in the object we could think of this as a type of pointing stick or even better the car within the driving simulator and then serves as an actual object in AR.

Now all you have to do is start the app and look at the printout of the defined target image to see the cubic platform as well as the sphere bouncing on it. If you then use the device somewhat unintuitively to bring there static cube in front of your camera very close to the sphere and manage to collide the two objects, you will actually force the sphere to bounce off in the direction you pushed it to and it will get 'lost in virtual space'.

## Conclusion

So, the answer to the question of feasibility as well as the associated difficulty has found to be very simple. It is very much possible and actually quite simple too!

With this newly acquired information we will be able to come up with or give a better estimation on possible game ideas for applications of our visualization of the visual effects of drinking.
