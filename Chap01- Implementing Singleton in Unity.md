## **Early Singleton in C#**

Singleton is a basic Design Pattern. Classes implementing Singleton pattern will ensure that only one instance of the object ever exists at any one time. It is recommend using Singletons for things that do not need to be copied multiple times during a game.


```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class SingletonController : MonoBehaviour {
public static SingletonController instance;
 
  private void Awake() {
   if (instance != null) {
     Destroy(gameObject);
   }else{
     Instance = this;
   }
 }
}
```

Above code is the simplest implementation of Singleton, but there are some issues which we have to address

- Singleton is not persistent across the Unity scenes.
- All the executable code must be attached to GameObject in the hierarchy.
- It is not recommended to call SingletonController.Instance in any Awake() method because, since we don’t know the order that Awake() will be executed through all scripts, we can end up with a Null Reference Exception.
- This code works only for SingletonController Class, but if you want another singleton controller eg. AudioController. We have to copy paste the same code to AudioController Class and do some minor changes to works, but this leads to boilerplate code .


In order to fix the above issues, we can add the DontDestroyOnLoad(gameObject). Refer to the code below,

```C#

public class SingletonController : MonoBehaviour {
public static SingletonController instance;
 
  private void Awake() {
   if (instance != null) {
     Destroy(gameObject);
   }else{
     Instance = this;
     DontDestroyOnLoad(gameObject);
   }
 }
}
```
