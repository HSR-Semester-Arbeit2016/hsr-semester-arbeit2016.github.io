# Meeting 21.10.16 Log

Grundsätzlich wir müssen die unten stehende Punkte bearbeiten:

## 1. Render Texture

Ziel: Verzögerung in irgendeine Scene einbauen können.

Code Snippet bearbeitet mit Augenstein während der Sitzung, basiert auf einem Test von mir:

Link: [https://docs.unity3d.com/ScriptReference/MonoBehaviour.OnRenderImage.html](https://docs.unity3d.com/ScriptReference/MonoBehaviour.OnRenderImage.html)

```c#
using UnityEngine;
using System.Collections;
using System.Collections.Generic;

//MonoBehaviour is the base class from which all scripts classes inherit
public class Test : MonoBehaviour {
	
	private Queue myQ;
	public Test() {
		this.myQ = new Queue();
	}
	
	void OnRenderImage(RenderTexture src, RenderTexture dest) {
		myQ.Enqueue (src);
      // RenderTexture.GetTemporary anschauen 
		if (myQ.Count == 20) {	
          // with this we should create a delay, but not working
			src = (RenderTexture)myQ.Dequeue ();
			Graphics.Blit(src,dest);
		} else {
			//	Graphics.Blit(src,dest);
		}
	}
}
```

Diese Klasse würde hinzugefügt zu der StereoCameraLeft in der BlurMotion Scene der VisualEffectSelector App. Es funktioniert so weit, aber ohne sichtbare Effekt. 

Die Methode ```Graphics.Blit(src,dest);``` kopiert das```src``` Objekt in der ```dest``` Objekt. Das klingt dumm am Amfang, aber es ist nötig wegen Optimierung.

Die RenderTexture Objekte können als "Wrapper" Objekte betrachtet werden. Die sind eigentlich nur Referenzen auf eine Datenstruktur die für das Rendering gebraucht wird und  wird in C programmiert.

Sorry, schwierig zu erklären.

In diese Klasse wir sollten die Datenstruktur aus den ```src``` Objekt kopieren, irgendwo auslagern und wieder zurückkopieren bevor die ``Graphics.Blit(src,dest);`` aufrufen.

Die Klasse ```RenderTexture``` offeriert einige Methoden die vielleicht helfen könnten, die ```RenderTexture.GetTemporary```

Methoden. Wie im Code erwähnt, die sollen wir anschauen.

``RenderTexture`` Docs:

[https://docs.unity3d.com/ScriptReference/RenderTexture.GetTemporary.html](https://docs.unity3d.com/ScriptReference/RenderTexture.GetTemporary.html)

## 2. Rauschbrille App

Wir sollen anfangen die App "richtig" zu implementieren. Augenstein meint wir haben schon die nötige Mittel dafür. Wir können auf der VisualEffectSelector App basieren.

Er möchte, dass:

- Konfguration "in App" der Stärke der verschiedenen Filter
- Vielleicht Levels wie wir schon gedacht haben: sober, slightly intoxicated, drunk, very drunk
- Konfiguration persistent 
- Mit oder ohne VR Objects
- Vielleicht wieder mit Simone kontaktieren

Wir sollen vielleicht die Ziele abmachen. Aber wahrscheinlich wäre es gut wenn wir schon etwas nächste Woche zeigen könnten.

Wir sollten auch einige Ideen entwicklen von der "Gamification" der Rauschbrille App, d.h. wie könnte man mit der App spielen. Beispiele:

- Zwei Users tragen die Brille. Eine "Sober", andere "slightly intoxicated". Sie werfen sich gegeinender einen Ball. Wer den ball nicht fängt, verliert
- Zwei Users tragen die Brille. Eine "Sober", andere "slightly intoxicated". Sie müssen Hindernisse in Raum verhindern mit einem Timer. Wenn der Timer abläuft, eine Lampe wechselt von Rot auf Grün. Logischerweise der "slightly intoxicated" sollte das nicht merken
- Zwei Users tragen die Brille. Eine "Sober", andere "slightly intoxicated". Die App erzeugt random VR Objects die die Users fangen sollen. 
- ... 

Meine Fragen wären:

- Wie wollen wir vorgehen?
  - Wollen wir Use Cases schreiben?
  - Vielleicht zuerst "unsere" Use Cases erstellen und danach mit Simone reden? (Augenstein hat so was empfohlen)
  - Irgendeine Zeitplannung? Oder nach der Erstellung der Uses Cases?
  - ...

## 3. Requirements Analyse

Wie am Telefon erwähnt, hier gehts grundsätzlich um eine Game - Idee zu entwicklen für die BA. Aber wir sollten es schon in unsere SA dokumentieren.

Wir sollten:

- Eine Game Idee haben, basiert auf der Verwendung der Rauschbrille App

  - Es könnte sein entweder:
    - Eine reine AR App, mit VR Objects oder ohne
    - Eine reine VR App, ohne AR
    - Daydream? 
    - Whatever
- Als Requirements Engineers wir sollten dokumentieren können was machbar ist und was nicht, oder wie aufwändig irgendeine Feature sein sollte

Die Nutzung der Daydream Controller ist nicht ausgeschlossen. Es würde uns mehr Möglichkeiten geben, und in einige Monate wahrscheinlich wird es mehr Handys geben die Daydream unterstützen. Für die ASN wahrscheinlich würde nicht eine Rolle spielen welche Brille benutzt wird.


Shading, Render Textures and new programming languages
===

Das sind ungefähr die Ergebnisse meiner Research der Woche. Ich habe auch Augenstein davon erzählt.
Writing Image Effects
---

[https://docs.unity3d.com/Manual/WritingImageEffects.html](https://docs.unity3d.com/Manual/WritingImageEffects.html ) 

Cg Programming Language
---

Cg (short for C for Graphics) is a high-level shading language developed by Nvidia in close collaboration with Microsoft for programming vertex and pixel shaders. Cg is based on the C programming language and although they share the same syntax, some features of C were modified and new data types were added to make Cg more suitable for programming graphics processing units. This language is only suitable for GPU programming and is not a general programming language. The Cg compiler outputs DirectX or OpenGL shader programs. Since 2012, Cg is deprecated, with no additional development or support available.

[https://en.wikipedia.org/wiki/Cg_(programming_language)](https://en.wikipedia.org/wiki/Cg_(programming_language))

[https://en.wikipedia.org/wiki/Shader](https://en.wikipedia.org/wiki/Shader)

Shading
---

In computer graphics, shading refers to the process of altering the color of an object/surface/polygon in the 3D scene, based on its angle to lights and its distance from lights to create a photorealistic effect. Shading is performed during the rendering process by a program called a shader.

Shader
---

A shader is a computer program that is used to do shading: the production of appropriate levels of color within an image, or, in the modern era, also to produce special effects or do video post-processing. A definition in layman's terms might be given as "a program that tells a computer how to draw something in a specific and unique way".

Shading Language used in Unity
---

In Unity, shader programs are written in a variant of HLSL language (also called Cg but for most practical uses the two are the same).

**Shader Reference**

https://docs.unity3d.com/Manual/SL-ShadingLanguage.html
https://docs.unity3d.com/Manual/SL-Reference.html
https://docs.unity3d.com/Manual/SL-SurfaceShaderExamples.html

Writing vertex and fragment shaders
---

https://docs.unity3d.com/Manual/SL-ShaderPrograms.html

https://en.wikipedia.org/wiki/High-Level_Shading_Language

Render Textures
---

Unity Tutorial: Render Textures 
https://www.youtube.com/watch?v=pA7ZC8owaeo

Blending
---

https://docs.unity3d.com/Manual/SL-Blend.html    

file:///Applications/Unity/Unity.app/Contents/Documentation/en/ScriptReference/RenderTexture.html





