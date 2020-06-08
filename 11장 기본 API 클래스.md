#### 자바 API 도큐먼트

API는 라이브러리(library)라고 부르기도 하는데, **프로그램 개발에 자주 사용되는 클래스 및 인터페이스의 모음을 말한다**.  우리가 사용해 왔던 String 클래스와 System 클래스도 모두 API에 속하는 클래스들이다. 이 API들은 <JDK 설치 경로>  \jre\lib\rt.jar 라는 압축 파일에 저장되어 있다.

API 도큐머트는 쉽게 API를 차아 이용할 수 있도록 문서화한 것을 말한다. 

#### java.lang과 java.util 패키지

자바 애플리케이션을 개발할 때 공통적으로 가장 많이 사용하는 패키지는 java.lang 패키지와 java.util, java.time 패키지일 것이다.

##### java.lang 패키지

java.lang 패키지는 **자바 프로그램의 기본적인 클래스는 담고 있는 패키지**이다. java.lang 패키지에 있는 클래스는 **인터페이스 import 없이 사용**할 수 없다. String과 System 클래스도 java.lang 패키지에 포함되어 있기 때문에 import하지 않고 사용했다.

- Object

자바 클래스의 최상위 클래스로 사용

- System

표준 입력 장치(키보드)로부터 데이터를 입력받을 때 사용

표준 출력 장치(모니터)로 출력하기 위해 사용

자바 가상 기계를 종료시킬 때 사용

쓰레기 수집기를 실행 요청할 때 사용

- Class

클래스를 메모리로 로딩할 때 사용

- String

문자열을 저장하고 여러 가지 정보를 얻을 때 사용

- StringBuffer, StringBuilder

문자열을 저장하고 내부 문자열을 조작할 때 사용

- Math

수학 함수를 이용할 때 사용

- Wrapper
  - Byte, Short, Character, Integer, Float, Double, Boolean, Long

기본 타입의 데이터를 갖는 객체를 만들 때 사용

문자열을 기본 타입으로 변환할 때 사용

입력값 검사에 사용

##### java.util 패키지

java.util패키지는 **컬렉션 클래스**들이 대부분을 차지하고 있다. 

- Arrays

배열을 조작(비교, 복사, 정렬, 찾기)할 때 사용

- Calender

운영체제의 날짜와 시간을 얻을 때 사용

- Date

날짜와 시간 정보를 저장하는 클래스

- Objects

객체 비교, 널(null) 여부 등을 조사할 때 사용

- StringTokenizer

특정 문자로 구분된 문자열을 뽑아낼 때 사용

- Random

난수를 얻을 때 사용



#### Object 클래스

extends 키워드로 다른 클래스를 상속하지 않으면 임시적으로 java.lang.Object 클래스를 상속하게 된다. 따라서 자바의 모든 클래스는 Object 클래스의 자식이거나 자손 클래스이다. Object는 자바의 최상위 부모 클래스에 해당한다.

##### 객체 비교(equals())

```java
public boolean equals(Object obj) {...}
```

equals() 메소드의 타입은 Object인데, 이것은 모든 객체가 매개값으로 대입될 수 있음을 말한다. Object가 최상위 타입으므로 모든 객체는 Object 타입으로 **자동 타입 변환**될 수 있기 때문이다. 비교 연산자인 ==과 동일한 결과를 리턴한다. 논리적으로 동등하다는 것은 같은 객체이건 다른 객체이건 상관없이 객체가 저장하고 있는 데이터가 동일함을 뜻한다. String 객체의 equals() 메소드는 String 객체의 번지를 비교하는 것이 아니라 문자열이 동일한지 조사하는 것이다. equals() 메소드는 직접 사용되지 않고 하위 클래스에서 재정의하여 논리적으로 동등 비교할 대 사용된다.

equals() 메소드를 재정의할 때에는 매개값(비교 객체)이 기준 객체와 동일한 타입의 객체인지 먼저 확인해야 한다. Object 타입의 매개 변수는 모든 객체가 매개값으로 제공될 수 이기 때문에 instanceof 연산자로 기준 객체와 동일한 타입인지 제일 먼저 확인해야 한다. 

##### 객체 해시코드(hashCode())

객체 해시코드란 **객체를 식별할 하나의 정수값**을 말한다. Object의 hashCode() 메소드는 객체의 메모리 번지를 이용해서 해시코드를 만들어 리턴하기 때문에 **객체마다 다른 값**을 가지고 있다. 해시코드의 값이 다르면 다른 객체로 판단하고, **해시코드 값이 같으면 equals() 메소드**로 다시 비교한다.

객체의 동등 비교를 위해서는 Object의 equals() 메소드만 재정의하지 말고 hashCode() 메소드도 재정의해서 논리적 동등 객체일 경우 동일한 해시코드가 리턴되도록 해야 한다.

##### 객체 문자 정보(toString())

Object 클래스의 toString() 메소드는 객체의 문자 정보를 리턴한다. **객체의 문자 정보란 객체를 문자열로 표현한 값을 말한다**. 기본적으로 Object 클래스의 toString() 메소드는 "클래스명@16진수해시코드"로 구성된 문자 정보를 리턴한다.

```java
Object obj = new Object();
System.out.println(obj.toString());
```

```java
java.lang.Object@de5ced
```

Object의 toString() 메소드의 리턴값은 자바 애클리케이션에서는 별 값어치가 없는 정보이므로 Object 하위 클래스는 toString() 메소드를 재정의(오버라이딩)하여 간결하고 유익한 정보를 리턴하도록 되어 있다. java.util 패키지의 Date 클래스는 toString() 메소드를 재정의하여 현재 시스템의 날짜와 시간 정보를 리턴한다. String 클래스는 toString() 메소드를 재정의해서 저장하고 있는 문자열을 리턴한다.

##### 객체 복제(clone())

객체 복제는 **원본 객체의 필드값과 동일한 값을 가지는 새로운 객체를 생성하는 것**을 말한다. 객체를 복제하는 이유는 원본 객체를 안전하게 보호하기 위해서이다. 신뢰하지 않는 영역으로 원본 객체를 넘겨 작업할 경우 원본 객체의 데이터가 훼손될 수 있기 때문에 복제된 객체를 만들어 신뢰하지 않는 영역으로 넘기는 것이 좋다. 복제된 객체의 데이터가 훼손되더라도 원본 객체는 아무런 영향을 받지 않기 때문에 안전하게 데이터를 보호할 수 있게 된다. 객체를 복제하는 방법에는 얕은 복제와 깊은 복제가 있다.

- 얕은 복제(thin clone)

  얕은 복제(thin clone)는 단순히 필드값을 복사해서 객체를 복제하는 것을 말한다. 필드값만 복제하기 때문에 필드가 기본 타입일 경우 값 복사가 일어나고, 필드가 참조 타입일 경우에는 객체의 번지가 복사된다. 만약 복제 객체에서 참조 객체를 변경하면 원본 객체도 변경된 객체를 가지게 된다.Object의 clone() 메소드는 자신과 동일한 필드값을 가진 얕은 복제된 객체를 리턴한다. 이 메소드로 객체를 복제하려면 반드시 java.lang.Cloneable 인터페이스를 구현하고 있어야 한다. 클래스 설계자가 복제를 허용한다는 의도적인 표시를 하기 위해서이다. Cloneable 인터페이스를 구현하지 않으면 clone() 메소드를 호출할 때 CloneNotSupportedException 예외 처리가 필요한 메소드이기 때문에 try-catch 구문이 필요하다

```java
try {
	cloned = (Member) clone();
} catch(CloneNotSupportedException e) {
	return cloned;
}
```

- 깊은 복제

  깊은 복제란 참조하고 있는 객체도 복제하는 것을 말한다. 깊은 복제를 하려면 Object의 clone() 메소드를 재정의해서 참조 객체를 복사하는 코드를 직접 작성해야 한다. 

##### 객체 소멸자(finalize())

참조하지 않은 배열이나 객체의 쓰레기 수집기(Garbage Collector)가 힙 영역에서 자동적으로 소멸시킨다. 쓰레기 수집기는 객체를 소멸하기 전에 마지막으로 객체의 소멸자(finalize())를 실행시킨다. 소멸자는 Object의 finalize() 메소드를 말하는데 기본적으로 실행 내용이 없다. 객체가 소멸되기 전에 마지막으로 사용했던 자원(데이터 연결, 파일 등)을 닫고 싶거나, 중요한 데이터를 저장하고 싶다면 Object의 finalize()를 재정의할 수 있다. finalize() 메소드가 실행되면 **번호를 출력하게 해서 어떤 객체가 소멸되는지 확인할 수 있도록 한다**. 프로그램이 종료될 때 즉시 자원을 해제하거나 즉시 데이터를 최종 저장해야 한다면, 일반 메소드에 작성하고 프로그램이 종료될 때 명시적으로 메소드를 호출하는 것이 좋다.



#### Objects 클래스

Object와 유사한 이름을 가진 java.util.Objects 클래스는 객체 비교, 해시코드 생성, null 여부, 객체 문자열 리턴 등의 연산을 수행하는 정적 메소드들로 구성된 Object의 유틸리티 클래스이다.

| 리턴 타입 | 메소드(매개 변수)                                        | 설명                                                         |
| --------- | -------------------------------------------------------- | ------------------------------------------------------------ |
| int       | compare(T a, T b, Comparator\<T> c)                      | 두 객체 a와 b를 Comparator를 사용해서 비교                   |
| boolean   | deepEquals(Object a, Object b)                           | 두 객체의 깊은 비교(배열의 항목까지 비교)                    |
| boolean   | equals(Object a, Object b)                               | 두 객체의 얕은 비교(번지만 비교)                             |
| int       | hash(Object... values)                                   | 매개값이 저장된 배열의 해시코드 생성                         |
| int       | hashCode(Object o)                                       | 객체의 해시코드 생성                                         |
| boolean   | isNull(Object obj)                                       | 객체가 null인지 조사                                         |
| boolean   | nonNull(Object obj)                                      | 객체가 null이 아닌지 조사                                    |
| T         | requireNonNull(T obj)                                    | 객체가 null인 경우 예외 발생                                 |
| T         | requireNonNull(T obj, String message)                    | 객체가 null인 경우 예외 발생(주어진 예외 메시지 포함)        |
| T         | requireNonNull(T obj, Supplier\<String> messageSupplier) | 객체가 null인 겨웅 예외 발생(람다식이 만든 예외 메시지 포함) |
| String    | toString(Object o)                                       | 객체의 toString() 리턴값 리턴                                |
| String    | toString(Object o, String nullDefault)                   | 객체의 toString() 리턴값 리턴, 첫 번째 매개값이 null일 경우 두 번째 매개값 리턴 |

##### 객체 비교(compare(T a, T b, Comparator\<T> c))

Objects.compare(T a, T b, Comparator\<T> c) 메소드는 두 객체를 비교자(Comparator)로 비교해서 int 값을 리턴한다. java.util.Comparator\<T>는 제네릭 인터페이스 타입으로 두 객체를 비교하는 compare(T a, T b) 메소드가 정의되어 있다. T가 비교할 객체 타입이라는 것만 알아두자.

```java
public interface Comparator<T> {
	int compare(T a, T b);
}
```

##### 동등 비교(equals()와 deepEquals())

Objects.equals(Object a, Object b)는 두 객체의 동등을 비교하는데 다음과 같은 결과를 리턴한다.

| a        | b        | Objects.equals(a,b)  |
| -------- | -------- | -------------------- |
| not null | not null | a.equals(b)의 리턴값 |
| null     | not null | false                |
| not null | null     | false                |
| null     | null     | null                 |

Objects.deepEquals(Object a, Object b) 역시 두 객체의 동등을 비교하는데, a와 b가 서로 다른 배열일 경우, 항목 값이 모두 같다면 true를 리턴한다. 이것은 Arrays.deepEquals(Object[] a, Object[] b)와 동일하다

| a                   | b                   | Objects.deepEquals(a, b)       |
| ------------------- | ------------------- | ------------------------------ |
| not null(not array) | not null(not array) | a.equals(b)의 리턴값           |
| not null(array)     | not null(array)     | Array.deepEquals(a,b)의 리턴값 |
| not null            | null                | false                          |
| null                | not null            | false                          |
| null                | null                | true                           |

##### 해시코드 생성(hash(), hashCode())

Objects.hash(Object... values) 메소드는 **매개값으로 주어진 값들을 이용해서 해시 코드를 생성하는 역할**을 하는데, 주어진 매개값들로 배열을 생성하고 Arrays.hashCode(Object[])를 호출해서 해시코드를 얻고 이 값을 리턴한다.  이 메소드는 클래스가 hashCode()를 재정의할 때 리턴값을 생성하기 위해 사용하면 좋다. 클래스가 여러 가지 필드를 가지고 있을 때 이 필드들로부터 해시코드를 생성하게 되면 동일한 필드값을 가지는 객체는 동일한 해시코드를 가질 수 있다.

```java
@Override
public int hashCode() {
	return Objects.hash(field1, field2, field3);
}
```

Objects.hashCode(Object o)는 매개값으로 주어진 객체의 해시코드를 리턴하기 때문에 o.hashCode()의 리턴값과 동일하다. 차이점은 매개값이 null이면 0을 리턴한다.

##### 널 여부 조사(isNull(), nonNull(), requireNonNull())

Objects.isNull(Object obj)는 매개값이 null일 경우 true를 리턴한다. nonNull(Object obj)는 매개값이 not null일 경우 true를 리턴한다. requireNonNull()는 다음 세 가지로 오버로딩되어 있다.

| 리턴 타입 | 메소드(매개 변수)                                    | 설명                                                         |
| --------- | ---------------------------------------------------- | ------------------------------------------------------------ |
| T         | requireNonNull(T obj)                                | not null-> obj, null->NullPointerException                   |
| T         | requireNonNull(T obj, String message)                | not null -> obj, null -> NullPointerException(message)       |
| T         | requireNonNull(T obj, Supplier\<String> msgSupplier) | not null -> obj , null -> NullPointerException(msgSupplier.get()) |

첫 번째 매개값이 not null이면 첫 번째 매개값을 리턴하고, null이면 모두 NullPointrException을 발생시킨다.

##### 객체 문자 정보(toString())

Objects.toString()은 객체의 문자 정보를 리턴하는데, 다음 두 가지로 오버로딩한다

| 리턴 타입 | 메소드(매개 변수)                      | 설명                                          |
| --------- | -------------------------------------- | --------------------------------------------- |
| String    | toString(Object o)                     | not null ->o.toString(), null ->"null"        |
| String    | toString(Object o, String nullDefault) | not null -> o.toString(), null -> nullDefault |

첫 번째 매개값이 not nullㅇ면 toString()으로 얻은 값을 리턴하고, null이면 "null"또는 두 번째 매개값인 nullDefault를 리턴한다.



#### System 클래스

자바 프로그램은 운영체제상 바로 실행되는 것이 아니라 JVM 위에서 실행된다. 따라서 운영체제의 모든 기능을 자바 코드로 직접 접근하기란 어렵다. java.lang 패키지에 속하는 System 클래스를 이용하면 운영체제의 일부 기능을 이용할 수 있다. System 클래스의 모든 필드와 메소드는 정적(static) 필드, 메소드로 구성되어 있다.

##### 프로그램 종료(exit())

강제적으로 JVM을 종료시킬 때 System 클래스의 exit() 메소드를 호출하면 된다. exit() 메소드는 현재 실행하고 있는 프로세스를 강제 종료시키는 역할을 한다. exit() 메소드는 int 매개값을 지정하도록 되어 있는데, 이 값을 종료 상태값이라고 한다. 일반저긍로 정상 종료일 경우 0으로 지정하고 비정상 종료일 경우 0 이외의 다른 값을 준다.

```java
System.exit(0);
```

##### 쓰레기 수집기 실행(gc())

쓰레기 수집기는 개발자가 직접 코드로 실행시킬 수는 없고, JVM에게 가능한한 빨리 실행해 달라고 요청할 수는 있다. 이것이 System.gc() 메소드이다. 메소드가 호출되면 쓰레기 수집기가 바로 실행되는 것은 아니고, JVM은 빠른 시간 내에 실행시키기 위해 노력한다.

```java
System.gc();
```

쓰레기가 생길 때마다 쓰레기 수집기가 동작한다면 정작 수행되어야 할 프로그램의 속도가 떨어지기 때문에 성능 측면에서 좋지 않다. gc() 메소드는 메모리가 열악하지 않은 환경이라면 거의 사용할 일이 없다. 

##### 현재 시각 읽기(currentTimeMillis(), nanoTime())

System 클래스의 currentTimeMillis() 메소드와 namoTime() 메소드는 컴퓨터의 시계로부터 현재 시간을 읽어서 밀리세컨드(1/1000초) 단위와 나노세컨드(1/10^9초) 단위의 long 값을 리턴한다.

```java
long time = System.out.currentTimeMillis();
long time = System.namoTime();
```

리턴값은 주로 프로그램의 실행 소요 시간 측정에 사용된다. 

##### 시스템 프로퍼티 읽기(getProperty())

시스템 프로퍼티(System Property)는 JVM이 시작할 때 자동 설정되는 시스템의 속성값을 말한다.  운영체제의 종류 및 자바 프로그램을 실행시킨 사용자 아이디, JVM의 버전, 운영체제에서 사용되는 파일 경로 구분자 등이 여기에 속한다. 시스템 프로퍼티는 키와 값으로 구성되어 있다.

시스템 프로퍼티를 읽어오기 위해서는 System.getProperty() 메소드를 이용하면 된다. 이 메소드느 시스템 프로퍼티의 키 이름을 매개값으로 받고, 해당 키에 대한 값을 문자열로 리턴한다.

```java
String value = System.getProperty(String key);
```

##### 환경 변수 읽기(getenv())

환경 변수는 프로그램상의 변수가 아니라 운영체제에서 이름(Name)과 값(Value)으로 관리되는 문자열 정보이다.

자바 프로그램에서는 환경 변수의 값이 필요한 경우 System.getenv() 메소드를 사용한다. 매개값으로 환경 변수 이름을 주면 값을 리턴한다.

```java
String value = System.getenv(String name);
```



#### Class 클래스

자바는 클래스와 인터페이스의 메타 데이터를 java.lang 패키지에 소속된 Class 클래스로 관리한다. 메타 데이터란 클래스의 이름, 생성자 정보, 필드 정보, 메소드 정보를 말한다.

##### Class 객체 얻기(getClass(), forName())

프로그램에서 Class 객체를 얻기 위해서는 Object 클래스가 가지고 있는 getClass() 메소드를 이용하면 된다. Ojbect는 모든 클래스의 최상위 클래스이므로 모든 클래스에서 getClass() 메소드를 호출할 수 있다.

```java
Class clazz = obj.getClass();
```

getClass() 메소드는 해당 클래스로 객체를 생성했을 때만 사용할 수 있는데, 객체를 생성하기 전 직접 Class 객체를 얻을 수도 있다. Class는 생성자를 감추고 있기 때문에 new 연산자로 객체를 만들 수 없고, 정적 메소드인 forName()을 이용해야 한다. forName() 메소드는 클래스 전체 이름(패키지가 포함된 이름)을 매개갑스로 받고 Class 객체를 리턴한다.

```java
try {
	Class clazz = Class.forName(String className);
} catch (ClassNotFoundException e) {
}
```

##### 리플렉션(getDeclaredConstructors(), getDeclaredFields(), getDeclaredMethods())

Class 객체를 이용하며 클래스의 생성자, 필드, 메소드 정보를 알아낼 수 있다. 이것을 리플렉션(Reflection)이라고 한다.

```java
Constructor[] constructors = clazz.getDeclaredConstructors();
Filed[] fileds = clazz.getDeclaredFields();
Method[] methods = clazz.getDeclaredMethods();
```

세 메소드는 각각 Constructor 배열, Field 배열, Method 배열을 리턴한다. 모두 java.lang.reflect 패키지에 소속되어 있다. 클래스에 선언된 멤버만 가져오고 상속된 멤버는 가져오지 않는다. 만약 상속된 멤버도 얻고 싶다면 getFields(), getMethods()를 이용해야 한다. 

##### 동적 객체 생성(newInstance())

Class 객체를 이용하면 new 연산자를 사용하지 않아도 동적으로 객체를 생성할 수 있다. 코드 작성 시에 클래스 이름을 결정할 수 없고, 런타임 시에 클래스 이름이 결정되는 경우에 매우 유용하게 사용한다. Class.forName() 메소드로 Class 객체를 얻은 다음 newInstance() 메소드를 호출하면 Object 타입의 객체를 얻을 수 있다.

```java
try {
	Class clazz = Class.forName("런타임 시 결정되는 클래스 이름");
	Object obj = clazz.newInstance();
} catch (ClassNotFoundException e) {
} catch (InstantiationException e) {
} catch (IllegalAccessException e) {
}
```

newInstance() 메소드는 기본 생성자를 호출해서 객체를 생성하기 때문에 **반드시 클래스에 기본 생성자가 존재**해야 한다. 만약 매개 변수가 있는 생성자를 호출하고 시다면 리플렉션으로 Constructor 객체를 얻어 newInstance() 메소드를 호출하면 된다. 

InstantiationException 예외는 해당 클래스가 추상 클래스이거나 인터페이스일 경우에 발생하고, IllegalAccessException 예왼느 클래스나 생성자가 접근 제한자로 인해 접근할 수 없을 경우에 발생한다.

newInstance() 메소드의 리턴 타입은 Object이므로 이것을 원래 클래스 타입으로 변환해야만 메소드를 사용할 수 있다. 그렇게 하기 위해서는 강제 타입 변환을 해야 하는데, 클래스 타입을 모르는 상태이므로 변환을 할 수 없다. 이 문제를 해결하려면 인터페이스 사용이 필요하다.

```java
Class clazz = Class.forName("SendAction" 또는 "ReceiveAction");
Action action = (Action) clazz.newInstance();
action.execute();
```



#### String 클래스

##### String 생성자

자바의 문자열은 java.lang 패키지의 String 클래스의 인스턴스로 관리된다. 소스상에서 문자열 리터럴은 String 객체로 자동 생성되지만, String 클래스의 다양한 생성자를 이용해서 직접 Strig 객체를 생성할 수도 있다. String 클래스는 Deprecated(비권장)된 생성자를 제외하고 약 13개의 생성자를 제공한다. 어떤 생성자를 이용해서 String 객체를 생성할지는 제공되는 매개값의 타입에 달려있다.

```java
//배열 전체를 String 객체로 생성
String str = new String(byte[] bytes);
//지정한 문자셋으로 디코딩
String str = new String(byte[] bytes, String charsetName);

//배열의 offset 인덱스부터 length만큼 String 객체로 생성
String str = new String(byte[] bytes, int offset, int length);
//지정한 문자셋으로 디코딩
String str = new String(byte[] bytes, int offset, int length, String charsetName);
```

##### String 메소드

String은 문자열의 추출, 비교, 찾기, 분리, 변환 등과 같은 다양한 메소드를 가지고 있다.

| 리턴 타입 | 메소드명(매개 변수)                                    | 설명                                                     |
| --------- | ------------------------------------------------------ | -------------------------------------------------------- |
| char      | charAt(int index)                                      | 특정 위치의 문자열 리턴                                  |
| boolean   | equals(Ojbect anObject)                                | 두 문자열을 비교                                         |
| byte[]    | getBytes()                                             | byte[]로 리턴                                            |
| byte[]    | getBytes(Charset charset)                              | 주어진 문자셋으로 인코딩한 byte[]로 리턴                 |
| int       | indexOf(String str)                                    | 문자열 내에서 주어진 문자열의 위치를 리턴                |
| int       | length()                                               | 총 문자의 수를 리턴                                      |
| String    | replace(CharSequence target, CharSequence replacement) | target 부분을 replacement로 대치한 새로운 문자열을 리턴  |
| String    | substring(int beginIndex)                              | beginIndex 위치에서 끝까지 잘라진 새로운 문자열를 리턴   |
| String    | substring(int beginIndex, int endIndex)                | beginIndex 위치에서 endIndex 전까지 새로운 문자열을 리턴 |
| String    | toLowerCase()                                          | 알파벳 소문자로 변환한 새로운 문자열을 리턴              |
| String    | toUpperCase()                                          | 알파벳 대문자로 변환한 새로운 문자열을 리턴              |
| String    | trim()                                                 | 앞뒤 공백을 제거한 새로운 문자열을 리턴                  |
| String    | valueOf(int i \| double d)                             | 기본 타입값을 문자열을 리턴                              |

##### 문자 추출(charAt())

charAt() 메소드는 매개값으로 주어진 인덱스의 문자를 리턴한다. 인덱스란 0에서부터 "문자열길이-1"까지의 번호를 말한다.

```java
String subject = "자바 프로그래밍";
char charValue = subject.charAt(3); //프
```

| 자   | 바   |      | 프   | 로   | 그   | 래   | 밍   |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| 0    | 1    | 2    | 3    | 4    | 5    | 6    | 7    |

##### 문자열 비교(equals())

기본 타입(byte, char, short, int, long, float, double, boolean) 변수의 값을 비교할 때에는 == 연산자를 사용한다. 그러나 문자열을 비교할 때에는 == 연산자를 사용하면 원하지 않는 결과가 나올 수 있다.

```java
String strVar1 = new String("신민철");
String strVar2 = "신민철";
String strVar3 = "신민철";
```

자바는 문자열 리터럴이 동일하다면 동일한 String 객체를 참조하도록 되어 있다. new 연산자로 생성된 다른 String 객체를 참조하기에 strVar1과 strVar2의 == 연산은 false를 산출하고 strVar2와 strVar3의 == 연산은 true를 산출한다. **== 연산자는 각 변수에 저장된 번지를 비교하기 때문에 이러한 결과가 나온다**.

두 String 객체의 문자열만을 비교하고 싶다면 == 연산자 대신 equals() 메소드를 사용해야 한다.

```java
strVar1.equals(strVar3) -> true
strVar2.equals(strVar3) -> true
```

원래 equals()는 Object의 번지 비교 메소드이지만, String 클래스가 오버라이딩해서 문자열을 비교하도록 변경했다.

##### 바이트 배열로 변환(getBytes())

**문자열을 암호화할 때 문자열을 바이트 배열로 변환**한다. 문자열을 바이트 배열로 변환하는 메소드는 다음 두 가지가 있다.

```java
byte[] bytes = "문자열".getBytes();
byte[] bytes = "문자열".getBytes(Charset charset);
```

getBytes() 메소드는 **시스템의 기본 문자셋으로 인코딩된 바이트 배열을 리턴**한다. 만약 특정 문자셋으로 인코딩된 바이트 배열을 얻으려면 두 번째 메소드를 사용하면 된다.

getBytes(Charset charset) 메소드는 잘못된 문자셋을 매개값으로 줄 경우, java.io.UnsupportedEncodingException 예외가 발생하므로 예외 처리가 필요하다.

바이트 배열을 다시 문자열로 변환(디코딩)할 때에는 어떤 문자셋으로 인코딩된 바이트 배열이냐에 따라서 디코딩 방법이 다르다. 단순하게 Strin(byte[] bytes) 생성자를 이용해서 디코딩하면 시스템의 기본 문자셋을 이용한다. 다른 문자셋으로 인코딩된 바이트 배열일 경우 다음 String 생성자를 이용해서 디코딩해야 한다.

```java
String str = new String(byte[] bytes, String charsetName);
```

##### 문자열 찾기(indexOf())

indexOf() 메소드는 매개값으로 주어진 문자열이 시작되는 인덱스를 리턴한다. 만약 주어진 문자열이 포함되어 있지 않으면 -1을 리턴한다.

```java
String subject = "자바 프로그래밍";
int index = subject.indexOf("프로그래밍");
```

##### 문자열 길이(length())

length() 메소드는 **문자열의 길이(문자의 수)를 리턴**한다.

```java
String subject = "자바 프로그래밍";
int length = subject.length();
```

##### 문자열 대치(replace())

replace() 메소드는 **첫 번째 매개값인 문자열을 찾아 두 번째 매개값인 문자열로 대치한 새로운 문자열을 생성하고 리턴**한다

```java
String oldStr = "자바 프로그래밍";
String newStr = oldStr.replace("자바", "JAVA");
```

**String 객체의 문자열은 변겨이 불가한 특성을 갖기 때문에 replace() 메소드가 리턴하는 문자열은 원래 문자열의 수정본이 아니라 와전히 새로운 문자열이다.**

##### 문자열 잘라내기(substring())

**substring() 메소드는 주어진 인덱스에서 문자열을 추출한다.** substring() 메소드는 매개값의 수에 따라 두 가지 형태로 사용된다. substring(int beginIndex, int endIndex)는 주어진 시작과 끝 인덱스 사이의 문자열을 추출하고, substring(int beginIndex)는 주어진 인덱스 이후부터 끝까지 문자열을 추출한다. 

##### 알파벳 대소문자 변경(toLowerCase(), toUpperCase())

toLowerCase() 메소드는 문자열을 **모두 소문자로 바꾼 새로운 문자열을 생성한 후 리턴**한다. 반대로 toUpperCase() 메소드는 문자열을 **모두 대문자로 바꾼 새로운 문자열을 생성한 후 리턴**한다.

toLowerCase()와 toUpperCase() 메소든느 영어로 된 두 문자열을 대소문자와 관계없이 비교할 때 주로 사용된다. equalsIgnoreCase() 메소드를 사용하면 toLowerCase(), toUpperCase() 작업이 생략된다.

##### 문자열 앞뒤 공백 잘라내기(trim())

trim() 메소드는 **문자열의 앞뒤 공백을 제거한 새로운 문자열을 생성하고 리턴**한다. trim() 메소드는 앞뒤의 공백만 제거할 뿐 **중간의 공백은 제거하지 않는다**. trim() 메소드를 사용한다고 해서 원래 문자열의 공백이 제거되는 것은 아니다.

##### 문자열 변환(valueOf())

valueOf() 메소드는 **기본 타입의 값을 문자열로 변환하는 기능**을 가지고 있다. String 클래스에는 매개 변수의 타입별로 valueOf() 메소드가 다음과 같이 오버로딩 되어있다.

```java
static String valeuOf(boolean b)
static String valeuOf(char c)
static String valeuOf(int i)
static String valeuOf(long i)
static String valeuOf(double d)
static String valeuOf(float f)
```



#### StringTokenizer 클래스

문자열이 특정 구분자(delimiter)로 연결되어 있을 경우, 구분자를 기준으로 부분 문자열을 분리하기 위해서는 String의 split() 메소드를 이용하거나, java.util 패키지의 StringTokenizer 클래스를 이용할 수 있다. split() 은 정규 표현식으로 구분하고, StringTokenizer는 문자로 구분한다.

##### split() 메소드

String 클래스의 split() 메소드는 다음과 같이 호출 되는데, **정규 표현식을 구분자로 해서 문자열을 분리한 후, 배열에 저장하고 리턴**한다.

```java
String[] result = "문자열".split("정규표현식");
```

예를 들어 다음과 같이 문자열이 있다고 가정하다. &, 쉼표(,), -를 제외하고 사람 이름만 따로 뽑아내고 싶을 경우, &, 쉼표(,), -를 파이프(|) 기호로 연결한 정규 표현식을 매개값으로 제공하면 split() 메소드는 이 기호들을 구분자로 해서 부분 문자열을 추출한다.

```
String[] names = text.split("&|,|-")
```

##### StringTokenizer 클래스

**문자열이 한 종류의 구분자로 연결되어 있을 경우, StringTokenizer 클래스를 사용하면 손쉽게 문자열(토큰: token)을 분리**해 낼 수 있다. StringTokenizer 객체를 생성할 때 첫 번째 매개값으로 전체 문자열을 주고, 두 번째 매개값으로 구분자를 주면 된다.

```java
StringTokenizer st = new StringTokenizer("문자열", "구분자");
```

만약 구분자를 생략하면 공백(Space)이 기본 구분자가 된다.

StringTokenizer 객체가 생성되면 부분 문자열을 분리해 낼 수 있는데, 다음 메소드들을 이용해서 전체 토큰 수, 남아 있는 토큰 여부를 확인한 다음, 토큰을 읽으면 된다.

| 메소드  |                 | 설명                            |
| ------- | --------------- | ------------------------------- |
| int     | countTokens()   | 꺼내지 않고 남아 있는 토큰의 수 |
| boolean | hasMoreTokens() | 남아 있는 토큰이 있는지 여부    |
| String  | nextToken()     | 토큰을 하나씩 꺼내옴            |

nextToken() 메소드로 토큰을 하나 꺼내오면 StringTokenizer 객체에는 해당 토큰이 없어진다. 만약 StringTokenizer 객체에서 더 이상 가져올 토큰이 없다면 nextToken() 메소드는 java.lang.util.NoSuchElementException 예외를 발생시킨다. 그래서 hasMoreToken() 메소드로 꺼내올 토큰이 있는지 조사한 후 호출하는 것이 좋은 코딩 방법이다.



#### StringBuffer, StringBuilder 클래스

문자열을 저장하는 String은 내부의 문자열을 수정할 수 없다. 예를 들어 String의 replace() 메소드는 내부의 문자열을 대치하는 것이 아니라, 대치된 새로운 문자열을 리턴한다. String 객체를 + 연산할 경우에도 마찬가지이다.

```java
String data = "ABC";
data += "DEF";
```

String 객체는 내부 데이터를 수정할 수 없으므로 "ABC"에 "DEF"가 추가된 "ABCDEF"라는 새로운 String 객체가 생성된다. data 변수는 새로 생성된 String 객체를 참조하게 된다.

문자열을 결합하는 + 연산자를 많이 사용할수록 String 객체 수가 늘어나기 때문에, 프로그램 성능을 느리게 하는 요인이 된다. java.lang 패키지의 StringBuffer 또는 StringBuilder 클래스를 사용하는 것이 좋다. **내부 버퍼(buffer: 데이터를 임시로 저장하는 메모리)에 문자열을 저장해 두고, 그 안에서 추가, 수정, 삭제 작업을 할 수 있도록 설계되어 있다**. String처럼 새로운 객체를 만들지 않고도 문자열을 조작할 수 있는 것이다.

StringBuffer는 멀티 스레드 환경에서 사용할 수 있도록 동기화가 적용되어 있어 스레드에 안전하지만, StringBudilder는 단일 스레드 환경에서만 사용하돌고 설계되어 있다.

기본 생성자인 StringBuilder()는 16개의 문자들을 저장할 수 있는 초기 버퍼를 만들고 StringBuilder(int capacity) 생성자는 capacity로 주어진 개수만큼 저장할 수 있는 초기 버퍼를 만든다.  StringBuilder 는 버퍼가 부족할 경우 자동으로 버퍼의 크기를 늘리기 때문에 초기 버퍼이 크기는 그다지 중요하지 않다. StringBuilder(String str) 생성자는 str로 주어진 매개값을 초기값으로 저장한다.

StringBuilder 객체가 생성되었다면 버퍼 내에서 문자 추가, 삽입, 삭제 등이 작업을 할 수 있는데 다음 메소드를 이용하면 된다.

| 메소드                                  | 설명                                              |
| :-------------------------------------- | :------------------------------------------------ |
| append(...)                             | 문자열 끝에 주어진 매개값을 추가                  |
| insert(int offset, ...)                 | 문자열 중간에 주어진 매개값을 추가                |
| delete(int start, int end)              | 문자열의 일부분을 삭제                            |
| deleteCharAt(int index)                 | 문자열에서 주어진 index의 문자를 삭제             |
| replace(int start, int end, String str) | 문자열의 일부분을 다른 문자여로 대치              |
| StringBuilder reverse()                 | 문자열의 순서를 뒤바꿈                            |
| setCharAt(int index, char ch)           | 문자열에서 주어진 index의 문자를 다른 문자로 대치 |



#### 정규 표현식과 Pattern 클래스

문자열이 정해져 있는 형식 (정규 표현식: Regular Expression)으로 구성되어 있는지 검증해야 하는 경우가 있다.

##### 정규 표현식 작성 방법

정규 표현식은 문자 또는 숫자 기호와 반보고 기호가 결합된 문자열이다.

| 기호  | 설명                                                         |
| ----- | ------------------------------------------------------------ |
| []    | [abc] a,b,c 중 하나의 문자 \[^abc] a,b,c 이외의 하나의 문자 [a-zA-Z] a~z, A~Z 중 하나의 문자 |
| \d    | 한 개의 숫자, [0-9]와 동일                                   |
| \s    | 공백                                                         |
| \w    | 한 개의 알파벳 또는 하나의 숫자 [a-zA-Z_0-9]와 동일          |
| ?     | 없음 또는 한 개                                              |
| *     | 없음 또는 한 개 이상                                         |
| +     | 한 개 이상                                                   |
| {n}   | 정확히 n개                                                   |
| {n,}  | 최소한 n개                                                   |
| {n,m} | n개에서부터 m개까지                                          |
| ()    | 그룹핑                                                       |

다음은 02-123-1234 또는 010-1234-5678과 같은 전화번호를 위한 정규 표현식이다.

```
(02|010)-\d{3,4}-\d{4}
```

다음은 white@naver.com과 같은 이메일을 위한 정규 표현식이다.

```
\w+@\w+\.\w+(\.\w+)?
```

\\.과 .은 다른데, \\.은 문자로서의 점(.)을 말하지만,  .은 모든 문자 중에서 한 개의 문자를 뜻한다.

##### Pattern 클래스

문자열을 정규 표현식으로 검증하는 기능은 java.util.regex.Pattern 클래스의 정적 메소드인 matches() 메소드가 제공한다.

```java
boolean result = Pattern.matches("정규식", "검증할 문자열");
```

  

#### Arrays 클래스

**Arrays 클래스는 배열 조작 기능**을 가지고 있다. 배열 조작이란 배열의 복사, 항목 정력, 항목 검색과 같은 기능을 말한다. 단순한 배열 복사는 System.arraycopy() 메소드를 사용할 수 있으나, Arrays는 추가적으로 항목 정렬, 항목 검색, 항목 비교와 같은 기능을 제공해준다. Arrays 클래스의 모든 메소드는 정적(static)이므로 Arryas 클래스로 바로 사요이 가능하다.

| 리턴 타입 | 메소드 이름                                  | 설명                                                         |
| --------- | -------------------------------------------- | ------------------------------------------------------------ |
| int       | binarySearch(배열, 찾는값)                   | 전체 배열 항목에서 찾는 값이 있는 인덱스 리턴                |
| 타겟 배열 | copyOf(원본배열, 복사할길이)                 | 원본 배열의 0번 인덱스에서 복사할 길이만큼 복사한 배열 리턴, 복사할 길이는 원본 배열의 길이보다 커도 되며, 타겟 배열의 길이가 된다 |
| 타겟 배열 | copyOfRange(원본배열, 시작인덱스, 끝 인덱스) | 원본 배열의 시작 인덱스에서 끝 인덱스까지 복사한 배열 리턴   |
| boolean   | deepEquals(배열, 배열)                       | 두 배열의 깊은 비교(중첩 배열이 항목까지 비교)               |
| boolean   | equals(배열, 배열)                           | 두 배열의 얕은 비교(중첩 배열의 항목은 비교하지 않음)        |
| void      | fill(배열, 값)                               | 전체 배열 항목에 동일한 값을 저장                            |
| void      | fill(배열, 시작인덱스, 끝인덱스, 값)         | 시작 인덱스부터 끝 인덱스까지의 항목에만 동일한 값을 저장    |
| void      | sort(배열)                                   | 배열의 정체 항목을 오름차순으로 정렬                         |
| String    | toString(배열)                               | "[값1, 값2, ...]"와 같은 문자열 리턴                         |

##### 배열 복사

배열 복사를 위해 사용할 수 있는 메소드는 copyOf(원본배열, 복사할길이), copyOfRange(원본배열, 시작인덱스, 끝 인덱스)이다.copyOf() 메소드 사용시 복사할 길이는 원본 배열의 길이보다 커도 되며, 타겟 배열의 길이가 된다.

```java
char[] arr1 = {'J' , 'A' , 'V' , 'A'};
char[] arr2 = Arrays.copyOf(arr2, arr2.length);
```

copyOfRange(원본배열, 시작인덱스, 끝 인덱스)는 원본 배열의 시작 인덱스에서 끝 인덱스까지 복사한 배열을 리턴한다. **시작 인덱스는 포함하지만, 끝 인덱스는 포함하지 않는다**. 

```java
char[] arr1 = {'J' , 'A' , 'V' , 'A'};
char[] arr2 = Arrays.copyOf(arr1, 0,3);
```

단순한 배열을 복사할 목적이라면 Array 클래스를 사용하지 않고 System.arraycopy() 메소드를 이용할 수도 있다. System.arraycopy() 메소드는 다음과 같이 5개의 매개값이 필요하다.

```java
System.arraycopy(Object o,int start, Object o2, int end, int length);
System.arraycopy(원본배열, 원본시작인덱스, 타겟배열, 타겟시작인덱스, 복사개수);
```

##### 배열 항목 비교

Arrays의 equals()와 deepEquals()는 배열 항목을 비교한다. equals()는 1차 항목의 값만 비교하고, deepEquals()는 1차 항목이 서로 다른 배열을 참조할 경우 중첩된 배열의 항목까지 비교한다.

##### 배열 항목 정렬

기본 타입 또는 String 배열은 Arrays.sort() 메소드의 매개값으로 지정해주면 자동으로 오름차순 정렬이 된다. 사용자 정의 클래스 타입일 경우에는 클래스가 Comparable 인터페이스를 구현하고 있어야 정렬이 된다. 

##### 배열 항목 검색

배열 항목에서 특정 값이 위치한 인덱스를 얻는 것을 배열 검색이라고 하나. 배열 항목을 검색하려면 먼저 Arrays.sort() 메소드로 항목들을 오름차순 정렬한 후, Arrays.binarySearch() 메소드로 항목을 찾아야 한다



#### Wrapper(포장) 클래스

자바는 기본 타입(byte, char, short, int, long, float, double, boolean)의 값을 갖는 객체를 생성할 수 있다. 이런 객체를 포장(Wrapper) 객체라고 하는데, **그 이유는 기본 타입의 값을 내부에 두고 포장하기 때문이다**. 포장 객체의 특징은 포장하고 있는 기본 타입 값은 외부에서 변경할 수 없다. 만약 내부의 값을 변경하고 싶다면 새로운 포자 객체를 만들어야 한다.

포장 클래스는 java.lang 패키지에 포함되어 있는데, 기본 타입에 대응되는 클래스들이 있다. 기본 타입의 첫 문자를 대문자로 바꾼 이름을 가지고 있다.

| 기본 타입 | 포장 클래스 |
| --------- | ----------- |
| byte      | Byte        |
| char      | Character   |
| short     | Short       |
| int       | Integer     |
| long      | Long        |
| float     | Float       |
| double    | Double      |
| boolean   | Boolean     |

##### 박싱(Boxing)과 언박싱(Unboxing)

기본 타입의 값을 포장 객체로 만드는 과정을 박싱(Boxing)이라고 하고, 포장 객체에서 기본 타입의 값을 얻어내는 과정을 언박싱(Unboxing)이라고 한다. 간단하게 포장 클래스의 생성자 매개값으로 기본 타입의 값 또는 문자열을 넘겨주면 된다.

| 기본 타입의 값을 줄 경우             | 문자열을 줄 경우                   |
| ------------------------------------ | ---------------------------------- |
| Byte obj = new Byte(10);             | Byte obj = new Byte("10");         |
| Character obj = new Character('가'); | 없음                               |
| Short obj = new Short(100);          | Short obj = new Short("100");      |
| Integer obj = new Integer(1000);     | Integer obj = new Integer("1000"); |
| Long obj = new Long(10000);          | Long obj = new Long("10000")'      |
| Float obj = new Float(2.5F);         | Float obj = new Float("2.5F");     |
| Double obj = new Double(3.5);        | Double obj = new Double("3.5");    |
| Boolean obj = new Boolean(true);     | Boolean obj = new Boolean("true"); |

생성자를 이용하지 않아도 각 포장 클래스가 가지고 있는 정적 valueOf() 메소드를 사용할 수도 있다.

```java
Integer obj = Integer.valueOf(1000);
Integer obj = Integer.valueOf("1000"); 
```

박싱된 포장 객체에서 다시 기본 타입의 값을 얻어 내기 위해서는(언박싱하기 위해서는 ) 각 포장 클래슴다 가지고 있는 "기본타입명+Value()" 메소드를 호출하면 된다.

##### 자동 박싱과 언박싱

자동 박싱은 포장 클래스 대입에 기본값이 대입될 경우에 발생한다.

```java
Integer obj = 100;
```

자동 언박싱은 기본 타입에 포장 객체가 대입될 경우에 발생한다.

```java
Integer obj = new Integer(200);
int value1 = obj + 100; // 자동 언박싱
```

컬렉션 객체에 int 값을 저장하면 자동 박싱이 일어나 Integer 객체가 저장된다.

```java
List<Integer> list = new ArrayList<Integer>();
list.add(200); // 자동 박싱
```

##### 문자열을 기본 타입 값으로 반환

포장 클래스의 주요 용도는 기본 입의 값을 박싱해서 포장 객체로 만드는 것이지만, 문자열을 기본 타입 값으로 변환할 때도 많이 사용된다. 포장클래스에는 "parse+기본타입"명으로 되어 있는 정적(static) 메소드가 있다. 이 메소드는 문자열을 매개값으로 받아 기본 타입 값으로 변환한다.

##### 포장 값 비교

포장 객체는 내부의 값을 비교하기 위해 ==와 != 연산자를 사용할 수 없다. **이 연산자는 내부의 값을 비교하는 것이 아니라 포장 객체의 참조를 비교하기 때문이다**.

내부의 값만 비교하려면 언박싱한 값을 얻어 비교해야 한다. 박싱된 값이 다음 표에 나와 있는 값이라면 ==와 != 연산자로 내부의 값을 바로 비교할 수 있다.

| 타입             | 값의 범위       |
| ---------------- | --------------- |
| boolean          | true, false     |
| char             | \u0000 ~ \u007f |
| byte, short, int | -128 ~ 127      |

직접 내부 값을 언박싱해서 비교하거나, equals() 메소드로 내부 값을 비교하는 것이 좋다.



#### Math, Random 클래스

java.lang.Math 클래스는 수학 계산에 사용할 수 있는 메소드를 제공하고 있다. 모두 정적(static) 이므로 Math 클래스로 바로 사용이 가능하다.

| 메소드                 | 설명                          |
| ---------------------- | ----------------------------- |
| int abs(int a)         | 절대값                        |
| double ceil(double a)  | 올림값                        |
| double floor(double b) | 버림값                        |
| int max(int a, int b)  | 최대값                        |
| int min(int a, int b)  | 최소값                        |
| double random()        | 랜덤값                        |
| double rint(double a)  | 가까운 정수의 실수값          |
| long round(double b)   | 소수점 첫째 자리에서 반올림값 |

Math.random() 메소드는 0.0.과 1.0 사이의 범위에 속하는 하나의 double 타입의 값을 리턴한다.

```
0.0		<=	Math.random()	< 1.0
```

```java
//주사위 번호 만들기
int dice = (int)(Math.random()*6)+1;
//로또 번호 뽑기
int lotto = (int)(Math.random()*45)+1;
```

##### Random 클래스

java.util.Random 클래스는 난수를 얻어내기 위해 다양한 메소드를 제공한다. Random 클래스는 boolean, int, long, float, double 난수를 얻을 수 있다. Random 클래스는 종자값(seed)을 설정할 수 있다. 종자값은 난수를 만드는 알고리즘에 사용되는 값으로 **종자값이 같으면 다음과 같은 난수를 얻는다**.

| 생성자            | 설명                                                   |
| ----------------- | ------------------------------------------------------ |
| Random()          | 호출 시마다 다른 종자값(현재시간 이용)이 자동 설정된다 |
| Random(long seed) | 매개값으로 주어진 종자값이 설정된다.                   |

| 리턴값  | 메소드(매개 변수) | 설명                                     |
| ------- | ----------------- | ---------------------------------------- |
| boolean | nextBoolean()     | boolean 타입의 난수를 리턴               |
| double  | nextDouble()      | double 타입의 난수를 리턴(0.0<=~<1.0)    |
| int     | nextInt()         | int 타입의 난수를 리턴(-2^31<=~=2^31-1); |
| int     | nextInt(int n)    | int 타입의 난수를 리턴(0<=~<n)           |



#### Date, Calender 클래스

자바는 시스템의 날짜 및 시각을 읽을 수 있도록 Dat와 Calender 클래스를 제공하고 있다. 이 두 클래스는 모두 java.util 패키지에 포함되어 있다.

##### Date 클래스

Date 클래스는 객체 간의 날짜 정보를 주고 받을 때 주로 사용된다. 여러 개의 생성자가 선언되어 있지만 대부분 Deprecated(비권장)되어 현재는 Date() 생성자만 주로 사용한다. Date() 생성자는 컴퓨터의 현재 날짜를 읽어 Date 객체로 만든다.

```java
Date now = new Date();
```

현재 날짜를 문자열로 얻고 싶다면 toString() 메소드를 사용하면 된다. toString() 메소드는 영문으로 된 날짜를 리턴하느데 만약 특정 문자열 포맷으로 얻고 싶다면 java.text.SimpleDateFormat 클래스를 이용하면 된다.

```java
Date now = new Date();
        String strNow1 = now.toString();
        System.out.println(strNow1);
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy년 MM월 dd일 hh시 mm분 ss초");
        String strNow2 = sdf.format(now);
        System.out.println(strNow2);
```

##### Calender 클래스

Calender 클래스는 달력을 표현한 클래스인데 추상(abstract) 클래스이므로 new 연산자를 사용해서 인스턴스를 생성할 수 없다. Calender 클래스에는 날짜와 시간을 계산하는데 꼭 필요한 메소드들만 선언되어 있고, 특정한 역법을 따르는 계산 로직은 하위 클래스에서 구현하도록 되어있다.

```java
Calender now = Calneder.getInstance();
```

Calender 객체를 얻었다면 get() 메소드를 이용해 날짜와 시간에 대한 정보를 읽을 수 있다.

```java
int year = now.get(Calendar.YEAR); //년도 리턴
int month = now.get(Calendar.MONTH) + 1; //월 리턴
int day = now.get(Calendar.DAY_OF_MONTH); //일 리턴
int week = now.get(Calendar.DAY_OF_WEEK); //요일 리턴
int amPm = now.get(Calendar.AM_PM); //오전/오후 리턴
int hour = now.get(Calendar.HOUR); //시 리턴
int minute = now.get(Calendar.MINUTE); //분 리턴
int second = now.get(Calendar.SECOND); //초 리턴
```

다른 시가대의 해당하는 날짜와 시간을 출력하기 위해서는 운영체제의 시간대를 다른 나라로 바꾸는 것도 있지만, Calendar 클랫의 오버로딩된 다른 getInstance() 메소드를 이용하면 간단하게 다른 시간대의 Calendar를 얻을 수 있다.

```java
TimeZone timeZone = TimeZone.getTimeZone("America/Los_Angeles");
Calendar now = Calendar.getInstance(timeZone);
```



#### Format 클래스

자바에서는 귀찮고 코드가 지저분해지는 문제를 해결하기 위하여 형식 클래스를 제공한다. 형식 클래스는 java.text 패키지에 포함되어 있는데, 숫자 형식을 위해 DecimalFormat, 날짜 형식을 위해 SimpleDateFormat, 매개 변수화된 문자열 형식을 위해 MessageFormat 등을 제공한다.

##### 숫자 형식 클래스

DecimalFormat은 숫자 데이터를 원하는 형식으로 표현하기 위해서 패턴을 사용한다. 적용할 패턴을 선택했다면 DecimalFormat 생성자 매개값으로 지정해서 객체를 생성하면 된다. 그리고 나서 format() 메소드를 호출해서 패턴이 적용된 문자열을 얻으면 된다.

```java
DecimalFormat df = new DecimalFormat("#,###.0");
String result = df.format(1234567.89);
```

##### 날짜 형식 클래스(SimpleDateFormat)

Date 클래스의 toString() 메소드는 영문으로된 날짜를 리턴하는데 만약 특정 문자열 포맷으로 얻고 싶다면 java.text.SimpleDateFormat 클래스를 이용하면 된다. SimpleDateFormat 클래스도 날짜를 원하는 형식으로 표한하기 위해서 패턴을 사용한다.

| 패턴 문자 | 의미                     | 패턴 문자 | 의미                 |
| --------- | ------------------------ | --------- | -------------------- |
| y         | 년                       | H         | 시(0~23)             |
| M         | 월                       | h         | 시(1~12)             |
| d         | 일                       | K         | 시(0~11)             |
| D         | 월 구분이 없는 일(1~365) | k         | 시(1~24)             |
| E         | 요일                     | m         | 분                   |
| a         | 오전/오후                | s         | 초                   |
| w         | 년의 몇 번째 주          | S         | 밀리세컨드(1/1000초) |
| W         | 월의 몇 번째 주          |           |                      |

패턴에는 자릿수에 맞게 기호를 반복해서 작성할 수 있다. 작용할 패턴을 작성했다면 이 패턴을 SimpleDateFormat의 생성자 매개값으로 지정해서 객체를 생성하면 된다. 그리고 format() 메소드를 호출해서 패턴이 적용된 문자열을 얻으면 된다.

```java
SimpleDateFormat sdf = new SimpleDateFormat("yyyy년 MM월 dd일");
String strDate = sdf.format(new Date());
```

##### 문자열 형식 클래스(MessageFormat)

데이터를 파일에 저장하거나, 네트워크로 전송할 때, 데이터베이스 SQL문을 작성하 때 등 많은 부분에서 일정한 형식의 문자열을 사용한다. MessageFormat 클래스를 사용하면 문자열에 데이터가 들어갈 자리를 표시해 두고, 프로그램이 실행되면서 동적으로 데이터를 삽입해 문자열을 완성시킬 수 있다.

```java
String message = "회원 ID: {0} \n회원 이름: {1}\n회원 전화: {2}";
String result = MessageFormat.format(message, id, name, tel);
```

MessageFormat은 정적 format() 메소드를 호출해서 완성된 문자열을 리턴시킨다. format() 메소드의 첫 번째 매개값은 매개 변수화된 문자열을 지정하고, 두 번째 이후의 매개값은 인덱스 순서에 맞게 나열하면 된다.

```java
String text = "회원 ID: {0} \n회원 이름: {1}\n회원 전화: {2}";
Object[] arguments = {id, name, tel};
String result  MessageFormat.format(text, arguments);
```



#### java.time 패키지

Date 클래스의 대부분의 메소드는 Deprecated 되었고, Date의 용도는 단순히 특정 시점의 날짜 정보를 저장하는 역할만 한다. Calendar 클래스는 날짜와 시간 정보를 읻기에는 충분하지만, 날짜와 시간을 조작하거나 비교하는 기능이 불충분하다. 그래서 자바 8부터 날짜와 시간을 나타내는 여러 가지 API를 새롭게 추가했다.

| 패키지             | 설명                                                         |
| ------------------ | ------------------------------------------------------------ |
| java.time          | 날짜와 시간을 나타내는 핵심 API를 포함했다                   |
| java.time.chrono   | ISO-8601에 정의된 달력 시스템 이외의 달느 달력 시스템이 필요할 때 사용할 수 있는 API포함 |
| java.time.format   | 날짜와 시간을 파싱하고 포맷팅하는 API포함                    |
| java.time.temporal | 날짜와 시간을 연산하기 위한 보조 API 포함                    |
| java.time.zone     | 타임존을 지원하는 API들이 포함                               |

##### 날짜와 시간 객체 생성

- LocalDate

LocalDate는 **로컬 날짜 클래스**로 날짜 정보만을 저장할 수 있다. 두 가지 정적 메소드를 얻을 수 있는데, now()는 컴퓨터의 헌재 날짜 정보를 저장한 LocalDate 객체를 리턴하고 of()는 매개값으로 주어진 날짜 정보를 저장한 LocalDate 객체를 리턴한다.

```java
LocalDate currDate = LocalDate.now();
LocalDate targetDate = LocalDate.of(int year, int month, int dayOfMonth);
```

- LocalTime

LocalTime은 **로컬 시간 클래스**로 시간 정보만을 저장할 수 있다. LocalTime 객체도 마찬가지로 두 가지 static 메서드를 얻을 수 있습니다.  now()는 컴퓨터의 현재 시간 정보를 저장한 LocalTime 객체를 리턴하고 of() 는 매개값으로 주어진 시간 정보를 저장한 LocalTime 객체를 리턴한다.

```java
LocalTime currTime = LocalTime.now();
LocalTime targetTime = LocalTime.of(int hour, int minute, int second, int nanoOfSecond);
```

- LocalDateTime

LocalDateTime 는 LocalDate 와 LocalTime 를 결합한 클래스라고 보면 되는데, 날짜와 시간 정보를 모두 저장할 수 있다. LocalDateTime 객체도 마찬가지로 두 가지 static 메서드를 얻을 수 있습니다. now()는 컴퓨터의 현재 날짜와 시간 정보를 저장한 LocalDateTime 객체를 리턴하고  of() 는 매개값으로 주어진 날짜와 시간 정보를 저장한 LocalDateTime 객체를 리턴하고 of()는 매개값으로 주어진 날짜와 시간 정보를 저장한 LocalDateTime 객체를 리턴한다.

```java
LocalDateTime currTime = LocalDateTime.now(); LocalDateTime targetTime = LocalDateTime.of(int year, int month, int dayOfMonth, int hour, int minute, int second, int nanoOfSecond);
```

- ZonedDateTime

ZonedDateTime은 ISO-8601 달력 시스템에서 정의하고 있는 타임존(time-zone)의 날짜와 시간을 저장하는 클래스이다. ZonedDateTime은 now() 정적 메소드에 ZoneId를 매개값으로 주고 얻을 수 있다. of()의 매개값은 java.util.TimeZone의 getAvailableIDs() 메소드가 리턴하는 유효한 값 중 하나이다.

```java
ZonedDateTime utcDateTime =ZonedDateTime.now(ZonedId.of("UTC"));
ZonedDateTime londonDateTime=ZonedDateTime.now(ZonedId.of("Europe/London"));
ZonedDateTime seoulDateTime=ZonedDateTime.now(ZonedId.of("Asia/Seoul"));
```

- Instant

Instant 클래스는 날짜와 시간의 정보를 얻거나 조작하는데 사용하지 않고, 특정 시점의 타임스탬프(Time-Stamp)로 사용된다. 주로 특정한 두 시점 간의 시간적 우선순위를 따질 때 사용한다.

```java
Instant instant1 = Instant.now();
Instant instant2 = Instant.now();
if(instant1.isBefore(instant2)) { System.out.println("instant1이 빠릅니다.");}
else if(instant1.isAfter(instant2)) { System.out.println("instant2가 빠릅니다.");}
else{System.out.println("동일한 시간입니다..");}
System.out.println("차이(nanos) :" instant1.until(instant2, ChronoUnit.NANOS));
```

