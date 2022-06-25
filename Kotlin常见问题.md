

**with**
with()函数是一个内联函数，它把传入的对象作为接受者，在该函数内可以使用this指代该对象来访问其公有的属性和方法。该函数的返回值为函数块最后一行或指定的return表示式。

`fun main() {
    val person: Person = Person("hzh", 23)
    val result = with(person) {
        age = 24
        eat()
        work(8) // 返回480
    }
    println("result is:$result")
}
`
