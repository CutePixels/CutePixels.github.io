---
layout: post
title: CutePixelsEvent 1.0 was released
subtitle: woo hoo
tags: [event, project]
gh-repo: CutePixels/CutePixelsEvent
gh-badge: [star, fork, follow]
---

CutePixelsEvent 纯纯一事件总线
### 食用方法
To use CutePixelsEvent in your project, you can include it in your Gradle build file.

```groovy
repositories {
    maven {
        name = 'CutePixels Projects'
        url = 'https://raw.githubusercontent.com/CutePixels/mvn-repo/main'
    }
}
dependencies {
    implementation('cute.pixels:event:{VERSION}')
}
```
Kotlin DSL:

```kotlin
repositories {
    maven {
        name = 'CutePixels Projects'
        url = uri('https://raw.githubusercontent.com/CutePixels/mvn-repo/main')
    }
}
dependencies {
    implementation('cute.pixels:event:{VERSION}')
}
```
Subscribe to events:

```kotlin
import cute.pixels.event.*

object Listeners {
    // Listen anywhere except inline functions
    @EventHandler
    fun onEvent(event: MyEvent) {
        // handle event
    }
    
}
```
Register Event Listener(s):

```kotlin
fun register() {
    // register a Listener
    EventBus.registerListener(Listeners, "onEvent", MyEvent::class.java)
    // register all Listener in a object
    EventBus.registerListeners(Listeners)
}
```

Create an event:

```kotlin
import cute.pixels.event.*
class MyEvent : Event() {
    fun getMessage(): String {
        return "xxx"
    }
}
```
Create a cancellable event(if cancelled, other listener will not executed):

```kotlin
import cute.pixels.event.*
class MyCancellableEvent : Event(), Cancellable {
    override var isCancelled: Boolean = false
        get() = field
        set(value) {field=value}
    fun getMessage(): String {
        return "xxx"
    }
}
```

Post an event:

```kotlin
fun postEvents() {
    EventBus.post(MyCancellableEvent)
    EventBus.post(MyEvent)
}
```

If you are using Java, you might need to append `.Companion` to `EventBus` when using the code.
