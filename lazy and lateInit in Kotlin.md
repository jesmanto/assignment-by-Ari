# lazy and lateInit in Kotlin
Lazy / LateInit initialization is the postponing of a variable initialization to a later time. 
This is a very handy feature, as we don’t need to initialize something that until we need it, or simply because we can’t initialize something until we have all we need.

Lazy is a good fit for properties that may or may not be accessed.
If we never access them, we avoid computing their initial value.
They may work for Activities, as long as they are not accessed before _setContentView_ is called. They are not a great fit for referencing views in a Fragment, because the common pattern of configuring views inside onCreateView would cause a crash. They can be used if view configuration is done in onViewCreated.

With Activities or Fragments, it makes more sense to use **lateinit** for their properties, especially the ones referencing views. While we don’t control the lifecycle, we know when those properties will be properly initialized. The downside is we have to ensure they are initialized in the appropriate lifecycle methods.

1. If they are mutable (i.e. might change at a later stage) use lateInit
2. If they are set externally (e.g. need to pass in some external variable to set it), use lateinit. There’s still a workaround to use lazy but not as direct.
3. If they are only meant to initialized once and shared by all, and it’s more internally set (dependent on variable internal to the class), then use lazy. Tactically, you could still use lateinit, but using lazy would better encapsulate your initialization code.
