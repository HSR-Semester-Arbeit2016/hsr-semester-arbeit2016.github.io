---
layout: post
title: "Changing Image Effects parameters on runtime"
date: 2016-10-22
categories:
author: "Roberto Cuervo, Konrad Höpli"
---
# Static AR app

Until now our AR app was static, the user could not interact with it too much.  From the main menu you just could choose between some scenes, each one of them with one image effect.

<img src="/media/ar_app_main_menu.png" alt="Main menu in der AR app" style="width:500px;"/>

You can see the effects in our post [Image Effects Comparison]({% post_url 2016-10-16-comparison-image-effects%}).  

Of course it's desirable a bit more interaction between app and user. At least the user should be able to choose the level of some effects.

# Slider

For the first try we decided to use a simple slider in order to select the "blureness" level in the Blur scene, or the scene which shows the Blur Image Effect.

First we added the Slider object to the canvas of the Blur scene. We configured it to look more or less like:



<img src="/media/slider.png" style="width:200px;"/>



The slider is configured with a range (0 to 4 in this case). When the slider head is at the begining (left), this value is 0. As soon as the user "slides" the slider to the right, this value increases. 

We needed a class to coordinate the input value from the slider with the component responsible of creating the "blureness" level. This responsible for this level is the field ```public float blurSize``` in the ```BlurOptimized``` class, which actually implements the "Blur" filter we use. 

For this we created a new class, the ```BlurViewModel``` class. 

````c#
using UnityEngine;
using UnityEngine.UI;
using System;
using UnityStandardAssets.ImageEffects;

public class BlurViewModel : MonoBehaviour {
  
	public void setBlurSize(float newValue) {
		this.setBlurSizeText (newValue);
		this.setDrunkLevelText(newValue);
		this.setBlurSizeValue (newValue);
	}

	private void setBlurSizeText(float value) {
		Text blurValueText = GameObject.Find ("SliderValueText").GetComponent<Text>();
		blurValueText.text = value.ToString();
	}

	private void setBlurSizeValue(float newValue) {
		BlurOptimized cameraLeftBlur = GameObject.Find("StereoCameraLeft").GetComponent<BlurOptimized>();
		cameraLeftBlur.blurSize = newValue;
		BlurOptimized cameraRightBlur = GameObject.Find("StereoCameraRight").GetComponent<BlurOptimized>();
		cameraRightBlur.blurSize = newValue;
   }
}
````

In order to be able to set the "blureness" level on runtime, the actions from the slider have somehow to be reflected in the ```BlurViewModel``` class. Hier Unity helps. The Slider Object has a ```OnValueChanged(single)``` method, which is called when the user "slides" the slider. The method is provided with a float parameter ```single``` containing the value of the slider.

In Unity you can link the call of ```OnValueChanged(single)``` with our ```BlurViewModel``` class, so that when the ```OnValueChanged(single)``` is called, this method calls the ```setBlurSize(float newValue)``` method of the ```BlurViewModel``` class.

In this method first we get the two Vuforia Camera objects, and from them we acces the ```BlurOptimized``` class and finally set the ```blurSize``` to the new value obtained from the slider. The result is that the "blureness " level increases or decreases. 
At the same time we show the user the value he chooses and the corresponding alcohol level.
It's better if you see it:

<img src="/media/slider.gif" style="width:550px;" />



Later we will add this functionality to the another scenes, maybe with another UI components (radio buttons, checkboxes, etc), but for the first try it's not so bad.
