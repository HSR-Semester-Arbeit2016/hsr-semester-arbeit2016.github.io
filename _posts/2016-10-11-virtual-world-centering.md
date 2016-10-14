---
layout: post
title: "Virtual World Centering"
date: 2016-10-11
categories: "general"
author: "Roberto Cuervo, Konrad Höpli"
---
## *Virtual World Centering*

One of the topics I focused on after I felt like I managed to establish a decent, first understanding of the Unity-Engine as well as -IDE, was the implementation of virtual objects or even a virtual world since we are planning to develop an AR-app after all.

The first issue that arises when integrating virtual object is where you establish the virtual 'world center' that is used as a central point to which all objects can be placed in relation to and this is a regular setting on the Vuforia ARCamera-asset in Unity.

By default you get the option to choose between a target-oriented and camera/device-oriented center and the decision might between the two might be more complex than one might imagine at first and I for example was expecting there to be an option to set this to 'None' or rather 'Fixed', but a short internet-research indicated, that those would be possible by manually overriding them in code (which allegedly would be against the 'spirit of Unity').
Choosing one of those somewhat unsupported choices would probably araise further issues anyways when it comes to linking the virtual objects to the real world - since for example the floor in the virtual world should match the XY-pane exactly so objects do not just float somewhere in space by default.

### Target-oriented center
Contrary to my very first assumption the 'target' is not directly associated with the specific point the camera is directed at as in the object you have your eyes focused at, but rather some object that is identifiable by the application on the camera image (using the Vuforia-SDK).

Of course the recognition of an object simply using a running camera is not exactly simple (but luckily for us we will not have to implement that at all) and thus the object is required to incorporate a set of features/identifiers in order to ensure a safe recognition and [this website helps](https://library.vuforia.com/articles/Best_Practices/Attributes-of-an-Ideal-Image-Target) with getting a better idea of what this means.


Anyways, the target-oriented center then allows you to build your based on that discovered target (either the first one or one in particular) as a point zero, which is most likely the best option to implement static obstacles for a little parcour as long as it is made sure that there is enough space available around it.
If there was not enough space available, it wouldn't really be an issue for the virtual objects, but since they will then be trying to float behind walls for example that will probably have a negative influence on the immersion that we want to uphold even though we sadly had to realize, that the Vuforia-VR-Camera combined with Google Cardboard only provides a 2D view...

### Camera-oriented center
The camera-oriented center is rather self-explanatory since it assumes the position of the camera/device as point-zero and then binds all objects in relation to it.

This option is definitely more convenient when it comes to non-static objects, that we want the user to deal with, but will take a bit more effort when implementing the movement since more parameters will have to be adjusted - for example an object just moving from right to left from the camera perspective would have to integrate Z-axis-movement based on the users current speed.

When toying around with the individual centers in Unity I quickly had to discover that all virtual objects get bound in relation to the camera-center regardless of the selected center-option on the AR-camera and the objects position in the hierarchy - so the ImageTarget-function provided by the Vuforia SDK seems to be more of a requirement in case we want to include static objects anywhere.

### Conclusion
All things considered I suspect us to use a combination of the options listed above - so the camera will probably end up being the center, but at least one image target will be added to add static content in relation to the real world surrounding the user.
In order to correctly achieve that we will be using the 'Extended Tracking' feature of the Vuforia-SDK, since otherwise the static content bound to a specific image target will only be displayed as long as the ImageTarget remains within the camera of the user and that is definitely not something we can tolerate upon our attempt to creat a immersive parcour-experience.


