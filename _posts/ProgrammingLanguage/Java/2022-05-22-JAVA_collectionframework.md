---
layout: post
title: 컬렉션프레임워크
date: 2022-05-22 00:00:00+0900
category: Java
published: true
---
# [컬렉션 프레임워크란?]  
널리 알려진 자료구조를 바탕으로 객체들을 효율적으로 추가,삭제,검색할 수 있도록 java.util패키지에 컬렉션과 관련된 인터페이스와 클래스들을 포함시켜 놓았는데 이들을 
총칭해서 **컬렉션 프레임워크(Collection Framework)**라고 한다.  
자바 컬렉션은 객체를 수집해서 저장하는 역할을 한다. 프레임워크란 사용 방법을 미리 정해 놓은 라이브러리를 말한다.  
자바 컬렉션 프레임워크는 몇 가지 인터페이스를 통해서 다양한 컬렉션 클래스를 이용할수 있도록 한다.  
컬렉션 프레임워크의 주요 인터페이스로는 **List, Set, Map**이 있다.  
![](\images\java\collection01.png)  
ArrayList, Vector, LinkedList는 List인터페이스를 구현한 클래스로, List인터페이스로 사용 가능함.  
다른 것들도 똑같은 방식.  
List와 Set은 객체를추가,삭제,검색하는 방법에 많은 공통점이 있기 때문에 이 인터페이스들의 공통된 메소드만 모아 Collection인터페이스로 정의해 두고 있음.  
Map은 키와 값을 하나의 쌍으로 묶는 완전히 다른 방법이기 때문에 따로 되어있다.  
다음은 각 인터페이스별로 사용할 수 있는 컬렉션의 특징이다.  
![](\images\java\collectiontable.png)  

---
# [List 컬렉션]
객체를 일렬로 늘어놓은 구조.  
객체를 인덱스로 관리하기 때문에 인덱스로 객체 검색,삭제 가능.  
객체 자체를 저장하는 것이 아닌 객체의 주소를 저장.  
동일한 객체를 중복 저장하면 동일한 주소가 저장됨.  
null도 저장 가능한데 이 경우 해당 인덱스는 객체를 참조하지 않음.  
![](\images\java\listtable.png)   
위 표에서 메소드의 매개 변수 타입과 리턴 타입에 E 타입 파라미터는 List 인터페이스가 제너릭 타입이기 때문이다.  
구체적인 타입은 구현 객체를 생성할 때 결정된다.  

- **ArrayList**  
ArrayList는 List인터페이스의 구현 클래스로, ArrayList에 객체를 추가하면 객체가 인덱스로 관리됨.  
배열과 다르게 저장용량을 초과한 객체들이 들어오면 자동적으로 저장 용량이 늘어난다.  
```java
List<String> list = new ArrayList<String>(); //String을 저장하는 Arraylist
//기본 생성자로 ArrayList객체를 생성하면 내부에 10개의 객체를 저장할 수 있는 초기용량을 가짐.  
//처음부터 용량을 크게 잡고 싶다면 용량의 크기를 매개값으로 받는 생성자를 이용하면 된다.  
List<String> list = new ArrayList<String>(30); //String 객체30개를 저장할 수 있는 초기값 
```  
특정 인덱스의 객체를 제거하면 바로 뒤 인덱스부터 마지막 인덱스까지 모두 앞으로 1씩 당겨짐.  
마찬가지로 특정 인덱스에 객체를 삽입하면 해당 인덱스부터 마지막 인덱스까지 모두 1씩 밀려남.  
따라서 빈번한 객체 삭제와 삽입이 일어나는 곳에서는 ArrayList를 사용하는 것이 바람직하지 않다.  
이런 경우라면 LinkedList를 사용하는 것이 좋다.  
그러나 인덱스 검색이나, 맨 마지막에 객체를 추가하는 경우에는 ArrayList가 더 좋은 성능을 발휘함.  
[Arraylist 도큐먼트](https://docs.oracle.com/en/java/javase/18/docs/api/java.base/java/util/ArrayList.html)  
<br>

- **Vector**  
Vector는 ArrayList와 동일한 내부 구조를 가지고 있다.  
```java
List<E> list = new Vector<E>(); //Vector를 생성하기 위해서는 저장할 객체타입을 타입 파라미터로 표기하고 기본 생성자를 호출하면 된다.
```    
ArrayList와 다른 점은 Vector는 동기화된(synchronized)메소드로 구성되어 있기 때문에 멀티스레드가 동시에 이 메소드들을 실행할 수 없고, 하나의 스레드가 실행을 완료해야만 다른 스레드를 실행할 수 있다.  
그래서 멀티 스레드 환경에서 안전하게 객체를 추가,삭제할 수 있다. 이것을 스레드가 안전(Thread Safe)하다라고 말한다.  
[Vector 도큐먼트](https://docs.oracle.com/en/java/javase/18/docs/api/java.base/java/util/Vector.html)   
<br>

- **LinkedList**  
LinkedList는 List구현 클래스이므로 ArrayList와 사용 방법은 똑같지만 내부 구조는 완전 다르다. ArrayList는 내부 배열에 객체를 저장해서 인덱스로 관리하지만, LinkedList는 인접 참조를 링크해서 체인처럼 관리한다.   
```java
//LinkedList를 생성하기 위해서는 저장할 객체 타입을 타입 파라미터(E)에 표기하고 기본 생성자를 호출하면 된다.
List<E> list = new LinkedList<E>();
```    
[LinkedList 도큐먼트](https://docs.oracle.com/en/java/javase/18/docs/api/java.base/java/util/LinkedList.html)  
<br>

---
# [Set 컬렉션]  
List 컬렉션은 저장 순서를 유지하지만, Set 컬렉션은 저장 순서가 유지되지 않는다. 또한 객체를 중복해서 저장할 수 없고, 하나의 null만 저장할 수 있다.  
Set 컬렉션은 수학의 집합에 비유될 수 있다. 집합은 순서와 상관없고 중복이 허용되지 않기 때문이다.  
Set 컬렉션은 또한 구슬 주머니와도 같다. 동일한 구슬을 두 개 넣을 수 없고, 들어갈(저장할) 때의 순서와 나올(찾을)때의 순서가 다를 수도 있기 때문이다.  
<br>
Set 컬렉션에는 HashSet,LinkedHashSet,TreeSet등이 있는데, 다음은 Set 컬렉션에서 공통적으로 사용 가능한 Set 인터페이스의 메소드들이다. 
인덱스로 관리하지 않기 때문에 인덱스를 매개값으로 갖는 메소드가 없다.   
![](\images\java\settable.png)   
[Set 도큐먼트](https://docs.oracle.com/en/java/javase/18/docs/api/java.base/java/util/Set.html)  
Set 컬렉션은 인덱스로 객체를 검색해서 가져오는 메소드가 없다. 대신, 전체 객체를 대상으로 한 번씩 반복해서 가져오는 반복자(Iterator)를 제공한다.  
반복자는 Iterator 인터페이스를 구현한 객체를 말하는데, iterator()메소드를 호출하면 얻을 수 있다.  
다음은 Iterator 인터페이스에 선언된 메소드들이다.  
![](\images\java\iteratortable.png)  
[Iterator 도큐먼트](https://docs.oracle.com/en/java/javase/18/docs/api/java.base/java/util/Iterator.html)  
<br>

- **HashSet**  
HashSet은 Set 인터페이스의 구현 클래스이다.  
HashSet은 객체들을 순서 없이 저장하고 동일한 객체는 중복 저장하지 않는다. HashSet이 판단하는 동일한 객체란 꼭 같은 인스턴스를 뜻하지는 않는다.  
HashSet은 객체를 저장하기 전에 먼저 객체의 hashCode() 메소드를 호출해서 해시코드를 얻어낸다. 그리고 이미 저장되어 있는 객체들의 해시코드와 비교한다. 만약 동일한 해시코드가 있다면 다시 equals() 메소드로 두 객체를 비교해서 true가 나오면 동일한 객체로 판단하고 중복 저장을 하지 않는다.  
[HashSet 도큐먼트](https://docs.oracle.com/en/java/javase/18/docs/api/java.base/java/util/HashSet.html)  
<br>

---
# [Map 컬렉션]  
Map 컬렉션은 key와 value로 구성된 Entry객체를 저장하는 구조를 가지고 있다. 여기서 키와 값은 모두 객체이다.  
키는 중복 저장될 수 없지만 값은 중복 저장될 수 있다.  
만약 기존에 저장된 키와 동일한 키로 값을 저장하면 기존의 값은 없어지고 새로운 값으로 대처된다.  

<br>
Map 컬렉션에는 HashMap, Hashtable, LinkedHashMap, Properties, TreeMap 등이 있다.  
다음은 Map 컬렉션에서 공통적으로 사용 가능한 Map 인터페이스의 메소드들이다.  
키로 객체들을 관리하기 때문에 키를 매개값으로 갖는 메소드가 많다.  
![](\images\java\maptable.png)  
위 표에서 메소드의 매개 변수 타입과 리턴 타입에 K와 V라는 타입 파라미터가 있는데, 이것은 Map 인터페이스가 제네릭 타입이기 때문이다.  
[Map 도큐먼트](https://docs.oracle.com/en/java/javase/18/docs/api/java.base/java/util/Map.html)  