---
layout: post
title: "Delay Effect"
date: 2016-10-28
categories:
author: "Roberto Cuervo, Konrad Höpli"

---

# Delay Effect

One image effect we did not treat properly untill now is the delay effect. Although we already have a delay effect caused by the time needed to process the video, this is an uncontrolled delay. 

Prof. Augenstein insisted that we should search a way in order to implement a custom delay, which should be parametrized and controlled.

The research lead us to the [```OnRenderImage(RenderTexture src, RenderTexture dest)```](https://docs.unity3d.com/ScriptReference/MonoBehaviour.OnRenderImage.html) method of the ```MonoBehaviour``` class.

````c#
using UnityEngine;
using System.Collections;

public class ExampleClass : MonoBehaviour {
    public Material mat;
    void OnRenderImage(RenderTexture src, RenderTexture dest) {
        Graphics.Blit(src, dest, mat);
    }
}
````

It's important to mention that ```OnRenderImage``` is called after all rendering is complete to render image. This will be significant later. 

But before going on, we have to explain what is a ```RenderTexture```.

## RenderTexture

[As described in the Unity Documentation](https://docs.unity3d.com/ScriptReference/RenderTexture.html), Render textures are textures that can be rendered to. They can be used to implement image based rendering effects, dynamic shadows, projectors, reflections or surveillance cameras.

## First Attempt

"Image based rendering effects" was exactly what we were looking for.  As the method ```OnRenderImage(RenderTexture src, RenderTexture dest)``` provide us with two ```RenderTexture```objects, our first approach was simple.

We save some ```RenderTexture src```objects in a ```Collection```, we wait a few time and we pass them on to the ``` Graphics.Blit(src, dest, mat);``` method. So we generate a delay.

```c#
using UnityEngine;
using System.Collections;
using System.Collections.Generic;

//MonoBehaviour is the base class from which all scripts classes inherit
public class DelayTest : MonoBehaviour {
	
	private Queue myQ;
	public DelayTest() {
		this.myQ = new Queue();
	}
	
	void OnRenderImage(RenderTexture src, RenderTexture dest) {
		myQ.Enqueue (src);
		if (myQ.Count == 20) {	
          // with this we should create a delay
			src = (RenderTexture)myQ.Dequeue ();
			Graphics.Blit(src,dest);
		} else {
			Graphics.Blit(src,dest);
		}
	}
}
```

This class was added (as a script) to both  StereoCameraLeft and StereoCameraRight of the Blur Scene of the [VisualEffectSelector](https://github.com/HSR-Semester-Arbeit2016/VisualEffectSelector) App, hierarchically after the Blur Effect. 

But there was no visible effect, we were missing something.

## Second Attempt

In our weekly meeting with Prof. Augenstein he suggested us to look deeper in the ```RenderTexture``` class. The class has a method interesting four us, the [```GetTemporary```](https://docs.unity3d.com/ScriptReference/RenderTexture.GetTemporary.html) method.

> This method allocates a temporary render texture. Internally Unity keeps a pool of temporary  render textures, so a call to GetTemporary most often just returns an already created one. [...] These temporary render textures are actually destroyed when they aren't used for a couple of frames.

This means, that we can get a temporary render texture from the ```RenderTexture src``` object, save it in the ```Collection```and (same as in Attempt 1) later pass it on to the ``` Graphics.Blit(src, dest, mat);``` method 

For better understanding, we need first to explain what is exactly blit. 

In computer graphic [blit](https://en.wikipedia.org/wiki/Bit_blit) is an operation in which  several [bitmaps](https://en.wikipedia.org/wiki/Bitmap) are combined into one using a boolean function.
The operation involves at least two bitmaps, one source and destination. The pixels of each are combined bitwise according to the specified raster operation (ROP) and the result is then written to the destination. The ROP is essentially a [boolean](https://en.wikipedia.org/wiki/Boolean_logic) formula. The most obvious ROP overwrites the destination with the source. 

In our case, the bitmaps are wrapped in the two ``RenderTexture`` objects, ```src```and ```dest```.The method [```Graphics.Blit(src,dest);```](https://docs.unity3d.com/ScriptReference/Graphics.Blit.html) copies the ```src``` texture into ```dest``` render texture with a shader. A shader is a program  which produce special effects or do video post-processing, but without significance for us in this case, as we just want to create some delay and no special effect.  The shader would be the ROP formula mentioned above. 

In our improved code we obtain a ```RenderTexture temporary``` from the ```GetTemporary``` method called with ```src``` as argument. Then, as the documentation says that```temporary```can be ```null```, we check it with the ```IsCreated()```method and if not, we put it in the queue.

If ```temporary```is ```null```, we put the original ```src```in the queue, in order to not interrupt the image flow. 

Then, after a given configurable delay (```delayQueueCount```) we get the former ```temporary```object, we assign it to ```src```and finally we pass it on to the``Graphics.Blit()`` method.

````c#
using UnityEngine;
using System.Collections;
using System.Collections.Generic;
using System.Threading;

public class Delay : MonoBehaviour {
    private Queue<RenderTexture> myQ;
	private int delayQueueCount = 80;
	public int DelayQueueCount {
		get { return delayQueueCount; }
		set {delayQueueCount = value;} 
	}

	public Delay() {
		this.myQ = new Queue();
	}	

	void OnRenderImage(RenderTexture src, RenderTexture dest) {
		RenderTexture temporary = RenderTexture.GetTemporary (src.width, src.height);
		if (temporary.IsCreated ()) {
			Debug.Log ("Delay");
			myQ.Enqueue (temporary);
		} else {				
			myQ.Enqueue (src);
		}
		if (myQ.Count == DelayQueueCount) {
			src = (RenderTexture)myQ.Dequeue ();
			Graphics.Blit(src,dest);
		} 
	}
}
````

And this works!! See:

<img src="/media/Delay.gif" />



## Pitfalls of the Delay class

1. As we already mentioned before, the ```OnRenderImage```method is called after all rendering is complete. As we later discovered this means that is always necessary to have some image effect _before_ the ```Delay```class is used. This is not a big problem at the moment, but it is not an elegant solution.
2. The real problem appeared as we tested the delay effect in a mobile phone. When we use just the delay effect, it works perfectly. But as soon as we try to combine this effect with another (f.e. the blur effect), the app crashes. We think that this is possibly a RAM capacity issue, as we save several milliseconds of video directly in the RAM. We keep looking for a solution.







---