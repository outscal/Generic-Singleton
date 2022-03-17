## Generic Singleton

In orderto solve the boilerplate code issue, we implement generic implementation of Singleton,

```C#
public class GenericSingletonClass<T> : MonoBehaviour where T : Component
{
    private static T instance;
    public static T Instance {
      get {
        if (instance == null) {
           instance = FindObjectOfType<T> ();
           if (instance == null) {
             GameObject obj = new GameObject ();
             obj.name = typeof(T).Name;
             instance = obj.AddComponent<T>();
           }
        }
       return instance;
      }
    }
 
    public virtual void Awake ()
    {
       if (instance == null) {
         instance = this as T;
         DontDestroyOnLoad (this.gameObject);
    } else {
      Destroy (gameObject);
    }
  }
}
```

So with this class we can make any class singleton, without duplicating  the code. Just inherit your class from GenericSingletonClass and it ready to go.

