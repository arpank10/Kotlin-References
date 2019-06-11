# Kotlin-References
All the questions and answers to kotlin

### Difference between var and val

1. var : var is like general variable and it's known as a mutable variable in kotlin and can be assigned multiple times.
2. val : val is like Final variable and it's known as immutable in kotlin and can be initialized only single time.

Note : Function parameters can only be val(not to be mentioned explicitly). Previously mutable parameters were allowed to be used in functions, but in the latest version of Kotlin, the support is removed.


### Lateinit and Lazy
 Using lateinit, the initial value does not need to be assigned. But, it needs to be assigned before we use it.
 Using it unassigned will lead to NPE.
 
 A property defined via by lazy is initialized using the supplied lambda upon first use, unless a value had been previously assigned.
 Example : val nameTextView by lazy { view!!.findViewById<TextView>(R.id.nameTextView) }
  
**When to Use Lazy or Lateinit**

Lazy is a good fit for properties that may or may not be accessed. If we never access them, we avoid computing their initial value. They may work for Activities, as long as they are not accessed before setContentView is called. They are not a great fit for referencing views in a Fragment, because the common pattern of configuring views inside onCreateView would cause a crash. They can be used if view configuration is done in onViewCreated.

With Activities or Fragments, it makes more sense to use lateinit for their properties, especially the ones referencing views. While we don’t control the lifecycle, we know when those properties will be properly initialized. The downside is we have to ensure they are initialized in the appropriate lifecycle methods.
