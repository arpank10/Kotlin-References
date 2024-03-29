# Kotlin-References

### Language Specific Features

- No new keyword for instantiaing objects : `val x = Person("Arpan")`

- **Pair** can be used to assign two variables at a time :

  ```kotlin
  val(d: String, c: Person) = {
  	if(x<10) Pair("Arpan", Person("x"))
  	else Pair("ARPAN", Person("y"))
  }
  ```

- We can omit the type of a variable if it can be inferred from the context. But kotlin is a **statically typed language**, every expression has a type.

- We can use when instead of if :

  ```kotlin
  val(d: String, c: Person) = when {
  	x<10 -> Pair("Arpan", Person("x"))
  	else -> Pair("ARPAN", Person("y"))
  }
  ```

- Functions can be defined at the top level, i.e at the package level.

- **main** function can be written with without any arguments unlike java.

- **if** can be used as an expression and it's result can be assigned to a variable.

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

1. [Anko](https://github.com/Kotlin/anko) It is a library which makes android development easier in Kotlin. It has several parts :

   - Anko Commons: a lightweight library full of helpers for intents, dialogs, logging and so on;
   - Anko Layouts: a fast and type-safe way to write dynamic Android layouts;
   - Anko SQLite: a query DSL and parser collection for Android SQLite;
   - Anko Coroutines: utilities based on the kotlinx.coroutines library.

2. [Fuel](https://github.com/kittinunf/fuel) Its github page describes it to be the "The easiest HTTP networking library for Kotlin/Android". It's features includes:

   - HTTP GET/POST/PUT/DELETE/HEAD/PATCH requests in a fluent style interface;
   - Asynchronous and blocking requests;
   - Downloading as a file;
   - Uploading files, blobs as multipart/data;
   - Cancelling asynchronous requests;
   - Request as coroutines
   - Deserialization into POJO/POKO
   - API routing

3. [khttp](https://github.com/jkcclemens/khttp) It is http without the bullshit. It mimics python's requests module to send http requests. It's features includes:

   - Sessions with cookie persistence
   - Basic authentication
   - Elegant key/value cookies
   - Automatic decompression
   - Unicode response bodies
   - Connection timeouts

4. [klaxon](https://github.com/cbeust/klaxon) With this one, you can parse json in kotlin with ease. It has different APIs for parsing :

   - **An object binding API** to bind JSON documents directly to your objects, and vice versa.
   - **A streaming API** to process your JSON documents as they're being read.
   - **A low level API** to manipulate JSON objects and use queries on them.
   - **A JSON path query API** to extract specific parts of your JSON document while streaming.

5. [KotterKnife](https://github.com/JakeWharton/kotterknife) You must have used butterknife, the view injection library for android in Java. This library is from the same author, Jake Wharton. It is butterknife's counterpart in Kotlin. It is used for **view binding**.

6. [KotlinPreferences](https://github.com/MarcinMoskala/KotlinPreferences) This is one of the two libraries of Marcin Moskala, which makes preference usage simple and fun.

7. [PreferenceHolder](https://github.com/MarcinMoskala/PreferenceHolder)  This is described as the brother of the KotlinPreferences library, also made by Marcin Moskala. Apart from helping with preferences, it also has a test mode and gson serialization.

8. [kbinding](https://github.com/BennyWang/KBinding) This is a android MVVM framework written in Kotlin. It has four binding modes :

   - OneWay: Binding from model to view
   - TwoWay: Binding from model to view and view to model
   - OneWayToSource: Binding from view to model
   - OneTime: Binding from model to view, and auto release after first emit	
     It supports both simple and multiple binding.

9. [RxDownload](https://github.com/ssseasonnn/RxDownload) It is a multi-threaded download tool written with RxJava and Kotlin. This can handle all your download needs.

10. [RxKotlin](https://github.com/ReactiveX/RxKotlin) This is the extension of RxJava in kotlin. It leverages language features of Kotlin (like extension functions) that streamlines the usage of RxJava even more.

11. [Kluent](https://github.com/MarkusAmshove/Kluent) Kluent is a "Fluent Assertions" library written specifically for Kotlin. It uses the Infix-Notations and Extension Functions of Kotlin to provide a fluent wrapper around the JUnit-Asserts and Mockito.

12. [Kotlin Wrappers](https://github.com/JetBrains/kotlin-wrappers) This is a repository which has a number of Kotlin wrappers over popular Javascript frameworks. All the wrappers can be installed using npm and they have a few cool examples there.

13. [Moshi](https://github.com/square/moshi) Here goes another Json parsing library from Square. It is built on [Okio](https://github.com/square/okio/) , and is quite similar to Gson. It also has support for annotations to customize the data bindings. It has built-in type adapters and custom type adapters. It has quite an extensive readme which contains all the details that you'll ever need.

14. [Arrow](https://github.com/arrow-kt/arrow) Arrow is a library for Typed Functional Programming in Kotlin. It empowers users to write pure FP apps and libraries built atop higher order abstractions.

15. [Mockk](https://github.com/mockk/mockk) This is a mocking library for Kotlin. It's features are:

    - **Argument Capturing** 
    - **Relaxed Mocks**
    - **Spies**
    - **Annotations**

16. [KBus](https://github.com/adrielcafe/KBus) Described to be a dead simple EventBus build on Kotlin, it seems quite minimalisitic.

17. [Kotlin-logging](https://github.com/MicroUtils/kotlin-logging) It is a lightweight kotlin logging library by MicroUtils. It wraps **slf4j** with Kotlin extensions.

18. [KotlinTest](https://github.com/kotlintest/kotlintest) Another testing library for Kotlin, it has a whole lot of features( a whole lot to mention here). A few of them are : Writing in StringSpec style,  over 120 mathcers to test assertions, automatically generated test data, etc.

19.  [Bansa](https://github.com/brianegan/bansa) This is an interesting one. It is basically a state container for Java and Kotlin, inspired by none other than redux. If you have previously made applications using react-native and redux, you will find this one to be quite similar, at least in it's purpose.

20. [KillerTask](https://github.com/inaka/KillerTask) A wrapper over AsyncTasks. Easy to use, a little too easy.

21. [Kodein- DI](https://github.com/Kodein-Framework/Kodein-DI/) You must have heard the term dependency injection by now (Dagger might ring a few bells!)

    Kodein is also a dependency retrieval container. It's advantages as mentioned in it's docs are :

    - It proposes a very simple and readable declarative DSL
    - It is not subject to type erasure (as Java is)
    - It integrates nicely with Android
    - It proposes a very kotlin-esque idiomatic API
    - It is fast and optimized (makes extensive use of `inline`)
    - It can be used in plain Java

22. [Kovert](https://github.com/kohesive/kovert) It is a REST framework. More so, it is the "invisible" REST framework, as it does not invade the code and uses only annotations for exception cases. 

    It is quite an extensive library. Building web backends with Kotlin just got a lot easier!

23. [Jackson Module Kotlin](https://github.com/FasterXML/jackson-module-kotlin) Module that adds support for serialization/deserialization of classes and data classes. 

    Previously a default constructor must have existed on the Kotlin object for Jackson to deserialize into the object. With this module, single constructor classes can be used automatically, and those with secondary constructors or static factories are also supported.

24. [KAndroid](https://github.com/pawegio/KAndroid) It provides extensions to eliminate boilerplate code while writing android applications using Kotlin.

    Intents, toast messages, system services, logging, layout inflation, animations, etc everything becomes much simpler while using this library. If you are making an application in Kotlin, I highly recommend using this one.

    

