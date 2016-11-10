---
layout: post
title: "Problems in the effect randomness implementation"
date: 2016-11-05
categories:
author: "Roberto Cuervo, Konrad Höpli"
---
# Randomness in the image effects

As shown In our post [Comparison Image Effects]({% post_url 2016-10-16-comparison-image-effects%}), there is one effect we must implement too. This is the **Inconstancy**, or the random change of the image effects intensity. 

In order to achieve this, we need two things:

1. A function able to generate random numbers inside a given range
2. A timer function, which triggers the random number generator function above after a configured time interval. This time interval should be later random too.

## C Sharp Random Class

C Sharp offers a [Random Class](https://msdn.microsoft.com/en-us/library/system.random(v=vs.110).aspx), able to produce a sequence of numbers that meet statistical requirements for randomness.

As all the parameters needed by the Image Effects (Blur, Tunnel Vision) methods are ```ìntegers``` within a certain range, we just need a method generating them. Like:

````c#
private int GenerateRandomNumber(int from, int to) {
  Random random = new Random();
  return random.Next(from, to);
}
````

So we can call ```GenerateRandomNumber``` and get a random number which we can set into the corresponding image effect method, obtaining the desired inconsistency. Even each eye should have different image effects.

Next step is a timer, which should trigger the ```GenerateRandomNumber``` call after the threshold is exceeded. 

Again C Sharp has an appropriate class for this, the [Timer Class](https://msdn.microsoft.com/en-us/library/system.timers.timer(v=vs.110).aspx). From the MSDN documentation we got the example:

````c#
using System;
using System.Timers;

public class Example {
   private static System.Timers.Timer aTimer;

   public static void Main()
   {
      SetTimer();
      Console.WriteLine("\nPress the Enter key to exit the application...\n");
      Console.WriteLine("The application started at {0:HH:mm:ss.fff}", DateTime.Now);
      Console.ReadLine();
      aTimer.Stop();
      aTimer.Dispose();
      Console.WriteLine("Terminating the application...");
   }

   private static void SetTimer()
   {
        // Create a timer with a two second interval.
        aTimer = new System.Timers.Timer(2000);
        // Hook up the Elapsed event for the timer. 
        aTimer.Elapsed += OnTimedEvent;
        aTimer.AutoReset = true;
        aTimer.Enabled = true;
    }

    private static void OnTimedEvent(Object source, ElapsedEventArgs e)
    {
        Console.WriteLine("The Elapsed event was raised at {0:HH:mm:ss.fff}", e.SignalTime);
    }
}
// The example displays output like the following:
//       Press the Enter key to exit the application...
//
//       The application started at 09:40:29.068
//       The Elapsed event was raised at 09:40:31.084
//       The Elapsed event was raised at 09:40:33.100
//		.....
//       Terminating the application...
````

## Problems with the Timer Class in Unity

As already explained, our idea is to set a timer and when the timer is out the ``GenerateRandomNumber`` method shall be called. We implemented this in a little example, and we found out two problems.

Our example code:

````c#
 private void OnTimedEvent(Object source, ElapsedEventArgs e)
    {
    	int randomNumber = this.GenerateRandomNumber(0, 4);
   		this.SetBlurSize(randomNumber);
   		//etc...
    }
````

### 1. Main Thread

The method (from example above) ```OnTimedEvent```is raised when the (previously defined) time interval elapses.  If the [AutoReset](https://msdn.microsoft.com/en-us/library/system.timers.timer.autoreset(v=vs.110).aspx) property is **true**, the event is raised repeatedly at the defined interval; otherwise, the event is raised only once, the first time the interval value elapses.

The problem we found out is that the Elapsed event (the ``OnTimedEvent``call) is raised on a [ThreadPool](https://msdn.microsoft.com/en-us/library/system.threading.threadpool(v=vs.110).aspx) thread. That means, that the body of the ``OnTimedEvent`` method is executed in a separated thread. And Unity does not allow this, an exception ````GenerateRandomNumber can only be called from the main thread````  is thrown.

### 2. Task Parallel Libray not available in Unity

In order to solve this problem, we tried to execute the ``OnTimedEvent`` call asynchronously by using the C# Task Parallel Library.

````c#
using System.Threading.Tasks;
// ...
timer.Elapsed += async ( sender, e ) => await HandleTimer();
// ....

private static Task HandleTimer()
   {
  		int randomNumber = this.GenerateRandomNumber(0, 4);
   		this.SetBlurSize(randomNumber);
   		//etc...
	}
````

But here we discovered that Unity does not support the ```System.Threading.Tasks``` library form C Sharp, this code does not compile even.
The reason for that most likely is, that Unity uses an own compiler for C# and therewith only a subset of the features and libraries available in C#.NET:

The following quote can be found on [the respective page in the Unity-manual](https://docs.unity3d.com/Manual/VisualStudioIntegration.html):
> "Visual Studio’s C# compiler has some more features than Unity’s C# compiler currently has. This means that some code (especially newer c# features) will not give an error in Visual Studio but will give an error in Unity." > 

We are obliged to find another solution in order to achieve the **Inconstancy** effect.

---