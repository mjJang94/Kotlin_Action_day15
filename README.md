# 람다 멤버 참조
지금까지 람다를 사용해 코드 블록을 다른 함수에게 인자로 넘기는 방법을 살펴봤는데, 넘기려는 코드가 이미 함수로 정의되어있다면 어떻게 해야할까? 함수를 호출하는 람다를 만들면 그만이지만, 중복된 코드이므로 좋지않다. 그러므로 함수를 넘겨주는 람다를 살펴보자.   
val getAge = Person::age
::를 사용하는 식을 멤버 참조라고 하는데 이는 프로퍼티나 메소드를 단 하나만 호출하는 함수 값을 만들어준다.   
사실 Person::age는 val getAge = { perosn: Person -> person.age }를 더 간략하게 표현한 형태이다. 표현의 형태는 여러가지가 있다.
<code>
<pre>
people.maxBy(Person::age)
people.maxBy( p -> p.age)
people.maxBy( it.age )
</code>
</pre>

최상위에 선언된 함수나 프로퍼티를 참조할 수도 있다.
<code>
<pre>
fun salute() = println("Salute!")
>>> run(::salute)
</code>
</pre>

위 코드에서 run은 라이브러리 함수이다.

람다가 인자가 여럿인 다른 함수한테 작업을 위임하는 경우 람다를 정의하지 않고 직접 위임 함수에 대한 참조를 제공하면 편리하다.
<code>
<pre>
val action = { person: Person, message: String -> //----- sendEmail에게 작업을 위임
  sendEmail(person, message)
}
val nextAction = ::sendEmail //----- 람다 대신 멤버 참조를 쓸 수 있음
</code>
</pre>

생성자 참조를 사용하면 클래스 생성 작업을 연기하거나 저장해둘 수도 있다.
:: 뒤에 클래스 이름을 넣으면 생성자 참조를 만들 수 있다.
<code>
<pre>
data class Person(val name: String, val age: Int)
>>> val createPerson = ::Person
>>> val p = createPerson("Alice", 29)
>>> val println(p)
</code>
</pre>

