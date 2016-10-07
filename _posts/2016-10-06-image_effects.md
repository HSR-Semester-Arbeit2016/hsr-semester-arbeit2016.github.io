---
layout: post
title: "Image Effects"
date: 2016-10-06
categories:
author: "Roberto Cuervo, Konrad Höpli"
---

## *Image Effects*

---

One of our goals in this project is to simulate the effects of alcohol in the vision. In order to achieve that, the research lead us to the [Image Effects reference](https://docs.unity3d.com/Manual/comp-ImageEffects.html) from Unity. 

These effects handle all the render-based image postprocessing effects, which allow us to simulate physical camera properties like Blur and Noise effects. 

From the Unity documentation we can show this example:

Scene with no Image Effects:

![Scene with no Image Effects](https://docs.unity3d.com/uploads/Main/FxNone.png)

Blur Effect and Noise Effect applied to the same camera:

![Scene blurred](https://docs.unity3d.com/uploads/Main/FxBlurNoise.png)



## *Tilt Shift*

In our  [Tunnel View Test Prototype]({% post_url 2016-010-05-tunnel_view_test%}) we used the [Tilt Shift](https://docs.unity3d.com/Manual/script-TiltShiftHdr.html) effect. This effect tries to imitate the narrowing of the sight by blurring the vision edges:

![Tunnel Test Screenshot](/media/tunnel_test.png "Tunnel Test" )

Of course we know that this is still not ideal. We need to be able to configure how much "blurred" ist the image, and to change this during runtime. The research showed that it's possible to write an own image effect by overwriting the ```OnRenderImage``` function:

```
using UnityEngine;
using System.Collections;

public class ExampleClass : MonoBehaviour {
    public Material mat;
    void OnRenderImage(RenderTexture src, RenderTexture dest) {
        Graphics.Blit(src, dest, mat);
    }
}
```

This function allows you to modify final image by processing it with shader based filters. The incoming image is `source` [render texture](https://docs.unity3d.com/Manual/class-RenderTexture.html). The result should end up in `destination` render texture. When there are multiple image filters attached to the camera, they process image sequentially, by passing first filter's destination as the source to the next filter. 

We still have to find out which parameters must be modified in order to achieve the desired effects and configurations.
