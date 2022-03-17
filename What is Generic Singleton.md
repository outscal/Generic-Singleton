## **The Generic Singleton Pattern in C#**

A Singleton is a class of which only one instance can exist in the application domain. 

Then, once we decide it's a good idea to create a singleton, we just pass it as a generic parameter to a GenericSingleton class and voila: we have a construction that ensures there can be only one instance of our class! 


```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Singleton<T> : MonoBehaviour where T : Singleton<T>
{
    private static T instance;// Declare a type as T Static variables for ,T It can be replaced by any type, such as GameManager
    public static T Instance // Declare a type attribute to wrap instancce, Make it possible for external access to him 
    {
        get { return instance; }
    }

    protected virtual void Awake()// Declare that a can only be   Virtual methods accessed by inherited classes 
    {
        if (instance != null)
        {
            Destroy(gameObject);
        }
        else
        {
            instance = (T)this;
        }
        //DontDestroyOnLoad(gameObject);
    }

    public static bool IsInitialized {// Declare a return value of bool The property of type returns whether the instance is initialized 

        get { return instance != null;  }
    }

    protected virtual void OnDestroy()// Declare that a can only be   Virtual methods accessed by inherited classes 
    {
        if(instance == this)
        {
            instance = null;
        }
    }
```

While the above code provides thread safety and enforces that only one instance of class T can be created through the Singleton class, it has a major drawback. The generic constraint 'new()' on the type parameter means that the class T will have to provide a public parameterless constructor. This means that any client code will be able to create as many instances of class T as it likes. Thus, this breaks the Singleton pattern. It only works if the client code is willing to only access class T via the Singleton class. 
