---
layout: post
title: "Comparison between desired image effects and available image effects"
date: 2016-10-16
categories:
author: "Roberto Cuervo, Konrad Höpli"
---
# Comparison between desired image effects and available image effects

One of our goals is to emulate the alcohol effects on the vision in the AR App. In order to achieve this, we asked Simone Reiser (ASN) for more details in order to categorize or describe this effects and later emulate them. 

## Information about Alcohol Effects on Vision Capabilities

Simone sent us a Mail on 23rd. September 2016 with information about the alcohol effects on vision capabilities. 

- **Tunnel View**: the field of vision encloses usually 180 degrees. But in fact you can see really sharp only in a small field of view. Even though the periferical vision is very important, because so you can react to warning colors or movements. Under alcohol influence this 180 degrees reduce steadily , being this of course dangerous in overtake actions, pedestrians, etc.


* **Bright-/Dark-Blindness**: Our pupils are small or big depending on the light circumstances. The time needed by the pupils adapt to light changes is longer under alcohol influence.  This mean, that you can be blind for 3 seconds or more. Time enough to crash.

* **Red light weakness**: You are not able to differentiate red shades, what is trouble when you must pay attention to brake lights.

* **Blurred view**: The eyes can not display fast and sharp the context. 

* **Double view**: each eye takes an image, and both images combined build a 3D image. Because of this, under alcohol influence you are able see double or triple things. 

* **Inconstancy**: it is important to know that these restrictions are not present in the same way. It can happen that, if you  are sitting, all is more or less sharp. But, as soon as you raise and move, your brain must process the inputs faster. Then the alcohol influence manifest. 

  Apart from visual restrictions, there are more like balance problems, delay in the reactions and motor functions, alll of them playing an important function in traffic.



##  Comparison

Once known the effects, we searched for the available possibilities offered by Unity and Vuforia. As already mentioned in the [Image Effects]({% post_url 2016-10-06-image_effects%}) Post, Unity has the [Image Effects reference](https://docs.unity3d.com/Manual/comp-ImageEffects.html)  or posprocessing effects. Below is a table with the alcohol effect, the corresponding Image Effect used in Unity und the obtained effect in the AR app.

First we show you the image without any effect:

![Sober](/media/sober.png)

| Alcohol Effect             | Unity Image Effect                       | AR App Example                           |
| -------------------------- | ---------------------------------------- | ---------------------------------------- |
| **Tunnel View**            | [Tilt Shift](https://docs.unity3d.com/Manual/script-TiltShiftHdr.html) or [Fish Eye](https://docs.unity3d.com/Manual/script-Fisheye.html)  <img src="https://docs.unity3d.com/uploads/ImageEffects/TiltShiftIris.png" alt="Tilt shift image effect in unity" style="width: 350px;"/> | <img src="/media/tilt_shift.png" alt="Tunnel view in AR app" style="width: 2000px;"/> |
| **Bright-/Dark-Blindness** | The delay in the image processing when appling any image effect creates automatically this effect. We use too the [Camera Motion Blur](https://docs.unity3d.com/Manual/script-CameraMotionBlur.html) <img src="https://docs.unity3d.com/uploads/Main/MbReconstructionBlurExample.png" style="width:350px;"/> | <img src="/media/blur_motion.png" alt="Blur motion in AR app" style="width:700px;"/> Sorry, getting this screenshot is difficult |
| **Red Light weakness**     | [Color Correction Curves](https://docs.unity3d.com/Manual/script-ColorCorrectionCurves.html)  <img src="https://docs.unity3d.com/uploads/Main/saturationAndBlueCurve.png" style="width:350px;"/> | <img src="/media/red_light_scene.png" alt="Red light weakness in AR app" style="width:700px;"/> |
|                            | [Blur Effect and Noise](https://docs.unity3d.com/Manual/script-BlurOptimized.html) <img src="https://docs.unity3d.com/uploads/Main/FxBlurOptimizedExample.png" alt="Unity Blur Image Effect" style="width:350px;"/> | <img src="/media/blur_scene.png" alt="Blur view in AR app" style="width:700px;"/> |
| **Double View**            | This is a combination of different image effects and configurations in Unity and there is no preview | Coming soon                              |
| **Inconstancy**            | Mix of all above with random parameters  | No preview                               |

## Virtual Objects

Another goal of the AR app ist to create virtual objects which the user maybe will have to avoid. The first prototype we built contains just a pair of cubes and a sphere. Attention: this objects are truly virtual objects, you can go through them with your hand , they don't exist in the reality.

<img src="/media/vr_objects.png" alt="First virtual objects" style="width:500 px;"/>

## AR Screenshots bigger

For a better vision of the AR app screenschots, once more them but a bit bigger:

**Sober (without effects)**

![Sober](/media/sober.png)

**Tunnel View**

![Tunnel View](/media/tilt_shift.png)

**Red Light weakness**

![Red Light](/media/red_light_scene.png)

**Bright-/Dark-Blindness**

![Bright -Dark-Blindness](/media/blur_motion.png)

**Blurred view**

![Blurred view](/media/blur_scene.png)