the code 

```C#
public class SingletonController : MonoBehaviour 
{
    private static SingletonController instance = null;
    public static SingletonController Instance  
    {
      get
       {
         if(instance == null)
         {
            instance = FindObjectOfType<SimpleSingleton>();
            if( instance == null) 
            {
              GameObject go = new GameObject();
              go.name = "SingletonController";
              instance = go.AddComponent<SingletonController>(); 
              DontDestroyOnLoad(go); 
            }
          }
           return instance;
        }
       }
        void Awake() 
     {
       if(instance == null ) 
       {
         instance = this; 
         DontDestroyOnLoad(this.gameObject); 
       }
        else
       {
         Destroy(gameObject); 
       }
    }
}
```


Above code solves two different issues, it first searches for instance of SingletonController  in the scene, If it doesn’t find a SingletonController component, a GameObject is created and a SingletonController component is attached to it, so with this it is not necessary for SingletonController to exist in the scene before hand, and  this code will also destroy any additional copies it finds.

As in this implementation we are lazily instantiating the Singleton, so now we did not worry about Null Reference Exception.
