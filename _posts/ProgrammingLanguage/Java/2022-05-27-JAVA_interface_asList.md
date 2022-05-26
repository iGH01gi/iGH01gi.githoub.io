---
layout: post
title: 왜 list인터페이스를 implements했는데 exception을 뱉을까? (+자바도큐먼트의 optional operation 의미)
date: 2022-05-27 00:00:00+0900
category: Java
published: true
---
자바언어로 코딩을 하던 중에 한 가지 의문점을 발견하였다.  
```java
public class Testing {
    public static void main(String[] args) {
        List<String> arrayList = new ArrayList<String>(Arrays.asList("1","2","3","4","5"));
        List<String> arrayList2 = Arrays.asList("11","2222","33","44","55");

        arrayList.add("test"); //OK
        arrayList2.add("test"); // java.lang.UnsupportedOperationException
    }
}
```  
위에서 arrayList.add("test")는 정상적으로 컴파일되지만  
arrayList2.add("test")는 exception을 던졌다.  

<br>
그 이유가 궁금해서 먼저 자바 도큐먼트의 asList를 찾아보았다.   
![aslist도큐먼트](\images\java\aslistdoc.jpg)  
asList메소드는 제네릭 메소드이며, List<T>타입을 반환하고 매개변수로 T타입의 array를 받는다.  
근데 궁금했던것은 List타입으로 반환한다는 것은 반환해주는 객체가 List 인터페이스를 implements한다는 뜻이고,  
그렇다면 List인터페이스에 존재하는 add()메소드를 분명히 구현해놨을텐데 어째서 exception을 던지냐? 하는 것이다.  
<br>
위 도큐먼트에서는 returned list는 리스트 size에 변화를 부르는 메소드가 실행되면 UnsupportedOperationExceptio을 부른다고 써있다.  
그래서 aslist를 좀 더 자세히 찾아보았다.  

![aslist](\images\java\aslist.jpg)  
코드를 자세히보면 aslist는 ArrayList를 리턴해준다고 쓰여있다.  
그러나 여기서 이 ArrayList는 우리가 흔히 아는 콜렉션프레임워크의 ArrayList가 아니다. 
우리가 아는 그것은 java.util.ArrayList이고, **여기의 ArrayList는 java.util.Arrays.ArrayList이다!!!!**  
코드를 보면 알겠지만 이 ArrayList는 AbstractList를 extends하는데 이 AbstractList클래스는 List인터페이스를 implement하고 있고  
implement를 하느라 override한 메소드중 add메소드를 보면 다음과 같다.  
```java
public void add(int index, E element) {
    throw new UnsupportedOperationException();  //ArrayList가 상속받는 AbstractList가 implements한 List인터페이스의 메소드중 오버라이드한 add 메소드.
}
```   
즉, asList메소드가 리턴하는 list객체의 실 타입은 ArrayList(java.util.Arrays.ArrayList임.)이고  
이 클래스가 상속받는 클래스인 AbstractList가 List인터페이스중 add메소드를 오버라이드하고 있고, 그 내용은  
add메소드가 불릴 시 Exception을 던지라는 내용인 것이다.  
그렇기때문에 asList가 비록 List타입 객체를 리턴해주지만 List인터페이스의 메소드중 하나인 add를 사용할 수 없던 것이다.  
이는 asList를 단순히 List형 객체를통해 단순히 원본 array만 조작하는 용도로 만들었기 때문이다.  
그렇기떄문에 실은 원본 array를 조작하는 것이기 때문에 위에서 arrayList2를 이용해 리스트속 값을 변경한다면 원본 array의 값도 마찬가지로 변하게된다.  
<br>
만약 원본 array의 내용은 그대로 이용하면서, 단순히 이를 조작하는것이아닌 진짜 ArrayList형식으로 변환해주어서 add메소드등까지 전부 자유롭게 쓰고싶다면(이 경우는 원본 array는 수정의 영향을 안받음)  
```java
List<String> arrayList = new ArrayList<String>(Arrays.asList("1","2","3","4","5"));
```  
이런식으로 한번 asList를 통해서 List타입이 인식할수 있는 형태로 가공해준 뒤, 이를 이용해서 아예 새로운 ArrayList 객체를 new연산자를 통해 만들어주면 된다.  

<br>
또한 자바 도큐먼트에 보면 예를들어  
list문서의 add메소드에 다음과같이 (optional operation)이라는 표시가 있다.  

![옵션](\images\java\optionaloperation.jpg)  
이는 위에서 말했듯이, list는 인터페이스이므로 구현하는 클래스가 생길텐데, 그때 그 클래스가 해당 메소드의 성질에 대해서 immutable한 특성을 지녀야한다면, Exception을 던지는 등의 방식으로 실질적인 구현을 하지 않아도 된다는 뜻이다.  
(위에서 봤던 AbstractList가 바로 그 예이다.)  