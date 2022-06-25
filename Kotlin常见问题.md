

**with**

with()函数是一个内联函数，它把传入的对象作为接受者，在该函数内可以使用this指代该对象来访问其公有的属性和方法。该函数的返回值为函数块最后一行或指定的return表示式。

```kotlin
fun main() {
    val person: Person = Person("hzh", 23)
    val result = with(person) {
        age = 24
        eat()
        work(8) // 返回480
    }
    println("result is:$result")
}
```

```
运行结果：

吃柠檬
work 8 hour,earn ￥480
result is:480
```

```kotlin
fun main() {
    val person: Person = Person("hzh", 23)
    val result = with(person) {
        age = 24
        eat()
        work(8)
        return@with "HaHa" // return表达式，可以省略return@with直接返回最后一行
    }
    println("result is:$result")
}
```

```
运行结果：

吃柠檬
work 8 hour,earn ￥480
result is:HaHa
```

```kotlin
fun main() {
    val person: Person? = Person("hzh", 23)
    val result = with(person) {
        age = 24
        eat()
        work(8)
    }
    println("result is:$result")
}

无法编译:person为可空对象，with()需要在函数块内判定对象是否为空
如：
val result = with(person) {
    this?.age = 24
    this?.eat()
    this?.work(8)
}
```

***let***

let()函数是一个扩展对象函数，它可以对被扩展的对象做统一的判空处理，在函数块内使用it来指代该对象，可以访问对象的公有属性和方法。let()函数的返回值和with()函数一样，为函数块最后一行或指定的return表示式。


```kotlin
fun main() {
    val person: Person? = Person("hzh", 23)
    val result = person?.let {
        it.age = 24
        it.eat()
        it.work(8) // 返回480
    }
    println("result is:$result")
}
```

```
运行结果：

吃柠檬
work 8 hour,earn ￥480
result is:480
```

***run***

run()函数是with()和let()函数的结合体，它可以像with()函数一样直接在函数块中使用this指代该对象，也可以像let()函数一样为对象做统一的判空处理。

```kotlin
fun main() {
    val person: Person? = Person("hzh", 23)
    val result = person?.run {
        age = 24
        eat()
        work(8) // 返回480
    }
    println("result is:$result")
}
```

```
运行结果：

吃柠檬
work 8 hour,earn ￥480
result is:480
```

***apply***

apply()函数和run()函数相似，不同的是，run()函数是以闭包形式返回最后一行代码的值，而apply()函数返回的是传入的对象本身。

```kotlin
fun main() {
    val person: Person? = Person("hzh", 23)
    println("person:$person")
    val result = person?.apply {
        age = 24
        eat()
        work(8) // 返回传入的person对象
    }
    println("result is:$result")
}
```

```
运行结果：

person:Person@610455d6
吃柠檬
work 8 hour,earn ￥480
result is:Person@610455d6
```

***also***

also()函数和apply()函数相似，不同的是，also()函数在函数块中使用it指代该对象，而apply()函数在函数块中使用this指代该对象。

```kotlin
fun main() {
    val person: Person? = Person("hzh", 23)
    println("person:$person")
    val result = person?.also {
        it.age = 24
        it.eat()
        it.work(8) // 返回传入的person对象
    }
    println("result is:$result")
}
```

```
运行结果：

person:Person@610455d6
吃柠檬
work 8 hour,earn ￥480
result is:Person@610455d6
```



|函数名|函数块内使用对象|返回值|是否扩展函数|适用场景|
|-----|-------------|-----|----------|-------|
|with|this|函数块最后一行或return表达式的值|否|适用于调用同一个类多个方法|
|let|it|函数块最后一行或return表达式的值|是|适用于对象统一处理不为空的情况|
|run|this|函数块最后一行或return表达式的值|是|适用with()、let()函数的任何场景|
|apply|this|该对象|是|适用于run()函数的任何场景，通产可用来在初始化一个对象实例时，操作对象属性并最终返回该对象。也可用于多个扩展函数链式调用|
|also|it|该对象|是|适用于let()函数的任何场景，一般可用于多个扩展函数链式调用|