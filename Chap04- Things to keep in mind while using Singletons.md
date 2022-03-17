There are a few important issues to be aware of with this approach to creating singletons in Unity.

## Leaking Singleton Oobjects

- If a MonoBehaviour references a singleton during its OnDestroy or OnDisable while running in the editor, the singleton object that was instantiated at runtime will leak into the scene when playback is stopped
- OnDestroy and OnDisable are called by Unity when cleaning up the scene in an attempt to return the scene to its pre-playmode state
- If a singleton object is destroyed before another scripts references it through its Instance property, the singleton object will be re-instantiated after Unity expected it to have been permanently destroyed 


## Execution Order

- The order in which objects have their Awake and Start methods called is not predictable by default
- Persistent singletons are especially susceptible to execution ordering issues. If multiple copies of a singleton exist in the scene, one may destroy the other copies after those copies have had their Awake methods called
- If game state is changed during Awake, this may cause unexpected behavior
- As a general rule, Awake should only ever be used to set up the internal state of an object. Any external object communication should occur during Start
