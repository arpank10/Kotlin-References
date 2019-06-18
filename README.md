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


### Objects and Companion Objects

Objects are used to define singletons in Kotlin i.e a class that has only one instance. We use the **object** keyword to declare the singleton instead of the **class** keyword.

```kotlin
object CarFactory {
    val cars = mutableListOf<Car>()
    
    fun makeCar(horsepowers: Int): Car {
        val car = Car(horsepowers)
        cars.add(car)
        return car
    }
}
```

Companion Objects are useful when we want some static methods or data members. Declaring such methods and variables in a companion object allows us to use those as static ones from directly the class without instantiating any object for it.

```kotlin
class Car(val horsepowers: Int) {
    companion object Factory {
        val cars = mutableListOf<Car>()

        fun makeCar(horsepowers: Int): Car {
            val car = Car(horsepowers)
            cars.add(car)
            return car
        }
    }
}
```

### Useful Kotlin Libraries

1. **Anko** : [https://github.com/Kotlin/anko] It is a library which makes android development easier in Kotlin. It has several parts :
     * Anko Commons: a lightweight library full of helpers for intents, dialogs, logging and so on;
     * Anko Layouts: a fast and type-safe way to write dynamic Android layouts;
     * Anko SQLite: a query DSL and parser collection for Android SQLite;
     * Anko Coroutines: utilities based on the kotlinx.coroutines library.
2. **Fuel** : [https://github.com/kittinunf/fuel] Its github page describes it to be the "The easiest HTTP networking library for Kotlin/Android". It's features includes:
     * HTTP GET/POST/PUT/DELETE/HEAD/PATCH requests in a fluent style interface;
     * Asynchronous and blocking requests;
     * Downloading as a file;
     * Uploading files, blobs as multipart/data;
     * Cancelling asynchronous requests;
     * Request as coroutines
     * Deserialization into POJO/POKO
     * API routing
