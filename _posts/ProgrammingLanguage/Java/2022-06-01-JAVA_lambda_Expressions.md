---
layout: post
title: 람다식
date: 2022-06-01 00:00:00+0900
category: Java
published: true
---
# [람다식(Lambda Expressions)이란?]
람다식은 익명 함수를 생성하기 위한 식으로 객체 지향 언어보다는 함수 지향 언어에 가깝다.  
자바에서 람다식을 수용한 이유는 자바 코드가 매우 간결해지고, 컬렉션의 요소를 필터링하거나 매핑해서 원하는 결과를 쉽게 집계할 수 있기 때문.   
람다식의 형태는 매개 변수를 가진 코드 블록이지만, **런타임 시에는 익명 구현 객체**를 생성한다.  
```java
람다식->매개 변수를 가진 코드 블록->익명 구현 객체
```  
---

# [람다식 기본 문법]  
```java
(타입 매개변수, ...)->{실행문; ...}
```  
(타입 매개변수, ...)는 오른쪽 중괄호{} 블록을 실행하기 위해 필요한 값을 제공하는 역할을 한다.  
매개 변수의 이름은 개발자가 자유롭게 줄 수 있다. -> 기호는 매개 변수를 이용해서 중괄호 {}를 실행한다는 뜻으로 해석하면 된다.    
예를 들어 int 매개변수와 a의 값을 콘솔에 출력하기 위해 다음과 같이 람다식을 작성할 수 있다.  
```java
(int a)->{System.out.println(a);}
```  
매개 변수 타입은 런타임 시에 대입되는 값에 따라 자동으로 인식될 수 있기 때문에 람다식에서는 매개 변수의 타입을 일반적으로 언급하지 않는다.  
그래서 위 코드는 다음과 같이 작성할 수 있다.  
```java
(a)->{System.out.println(a);}
```   
하나의 매개 변수만 있다면 괄호 ()를 생략할 수 있고, 하나의 실행문만 있다면 중괄호{}도 생략할 수 있다.  
그래서 위 코드는 다음과 같이 작성할 수도 있다.  
```java
a->System.out.println(a);
```  
만약 매개 변수가 없다면 람다식에서 매개 변수 자리가 없어지므로 다음과 같이 빈 괄호()를 반드시 사용해야 한다.  
```java
()->{실행문;...}
```  
중괄호 {}를 실행하고 결과값을 리턴해야 한다면 다음과 같이 return문으로 결과값을 지정할 수 있다.  
```java
(x,y)->{return x+y;};
```  
중괄호 {}에 return문만 있을 경우, 람다식에서는 return문을 사용하지 않고 다음과 같이 작성하는 것이 정석이다.  
```java
(x,y)->x+y
```  

---

# [타겟 타입과 함수적 인터페이스]   
자바는 메소드를 단독으로 선언할 수 없고 항상 클래스의 구성 멤버로 선언하기 때문에  
람다식은 단순히 메소드를 선언하는 것이 아니라 이 메소드를 가지고 있는 객체를 생성해 낸다.   
그럼 어떤 타입의 객체를 생성하는 것일까?  
```java
인터페이스 변수 = 람다식;
```  
람다식은 인터페이스 변수에 대입된다. 이 말은 람다식은 인터페이스의 익명 구현 객체를 생성한다는 뜻이 된다.  
인터페이스는 직접 객체화할 수 없기 때문에 구현 클래스가 필요한데, 람다식은 익명 구현 클래스를 생성하고 객체화한다.  
람다식은 대입될 인터페이스의 종류에 따라 작성 방법이 달라지기 때문에 람다식이 대입될 인터페이스를 람다식의 **타겟 타입(trget type)**이라고 한다.  

<br>

### 함수적 인터페이스(@FunctionalInterface)  
람다식이 하나의 메소드를 정의하기때문에 두 개 이상의 추상 메소드가 선언된 인터페이스는 람다식을 이용해서 구현 객체를 생성할 수 없다.  
하나의 추상 메소드가 선언된 인터페이스만이 람다식의 타겟 타입이 될 수 있는데, 이러한 인터페이스를 **함수적 인터페이스(functional interface)**라고 한다.  
함수적 인터페이스를 작성할 때 두 개 이상의 추상 메소드가 선언되지 않도록 컴파일러가 체킹해주는 기능이 있는데, **인터페이스 선언 시 @FunctionalInterface 어노테이션**을 붙이면 된다.  
이 어노테이션은 두 개 이상의 추상 메소드가 선언되면 컴파일 오류를 발생시킨다.  
```java
@FunctionalInterface
public interface MyFunctionalInterface{
    public void method();
    public void otherMethod(); //컴파일 오류
}
```  
@FunctionalInterface는 선택사항임. 이 어노테이션 안써도 하나의 추상 메소드만 있다면 모두 함수적 인터페이스임.(실수 방지용)  

---
# [함수적 인터페이스에 따른 람다식의 작성 방법]
람다식은 타겟 타입인 함수적 인터페이스가 가지고 있는 추상 메소드의 선언 형태에 따라서 작성 방법이 달라지는데 이에 대해서 작성하겠음.  
### 매개 변수와 리턴값이 없는 람다식  
```java
@FunctionalInterface
public interface MyFunctionalInterface{
    public void method();
}

//method()가 매개변수를 가지지 않기 때문에 람다식도 매개변수가 없음
MyFunctionalInterface fi=()->{...}

//람다식이 대입된 인터페이스의 참조 변수는 다음과 같이 method()호출. method()호출은 람다식의 중괄호{}를 실행시킴.
fi.method();
```  


### 매개 변수가 있는 람다식
```java
@FunctionalInterface
public interface MyFunctionalInterface{
    public void method(int x);
}

//매개변수가 1개인 이유는 method()가 매개 변수를 하나만 가지기 때문.
MyFunctionalInterface fi=(x)->{...} 또는 x->{...}

//람다식이 대입된 인터페이스의 참조 변수는 다음과 같이 method()호출. 5가 매개값으로 사용됨.
fi.method(5);
```  


### 리턴값이 있는 람다식
```java
@FunctionalInterface
public interface MyFunctionalInterface{
    public int method(int x,int y);
}

//method()가 리턴 타입이 있기 때문에 중괄호 {}에는 return문이 있어야 한다.
MyFunctionalInterface fi=(x,y)->{...; return 값; }

//만약 중괄호{}에 return문만 있고, return문 뒤에 연산식이나 메소드 호출이 오는 경우라면 다음과 같이 작성할 수 있다.
MyFunctionalInterface fi=(x,y)->{ return x+y; }를 ==>  MyFunctionalInterface fi=(x+y)->x+y;
MyFunctionalInterface fi=(x,y)->{ return sum(x+y); }를 ==>  MyFunctionalInterface fi=(x+y)->sum(x+y);
``` 

---
# [클래스 멤버와 로컬 변수 사용]
람다식의 실행 블록에는 클래스의 멤버(필드와 메소드) 및 로컬 변수를 사용할 수 있다.  
클래스의 멤버는 제약 사항 없이 사용 가능하지만, 로컬 변수는 제약 사항이 따른다.  

<br>
### 클래스의 멤버 사용  
일반적인 익명 객체 내부에서 this는 익명 객체의 참조이지만, **람다식에서 this**는 내부적으로 생성되는 익명 객체의 참조가 아니라 **람다식을 실행한 객체의 참조이다.!**   
```java
public interface MyFunctionalInterface {
    public void method();
}


public class UsingThis {
    public int outterField=10;

    class Inner{
        int innerField=20;

        void method(){
            MyFunctionalInterface fi=()->{
                System.out.println("outterField: " + outterField);
                System.out.println("outterField: " + UsingThis.this.outterField+"\n"); //바깥 객체의 참조를 얻기 위해서는 클래스명.this 사용

                System.out.println("innerField:" + innerField);
                System.out.println("innerField:" + this.innerField+"\n"); //람다식 내부에서 this는 Inner객체를 참조
            };
            fi.method();
        }
    }
}

public class UsingThisExample{
    public static void main()(String[]args){
        UsingThis usingThis=new UsingThis();
        UsingThis.Inner inner=usingThis.new Inner();
        inner.method();
    }
}
```  
OUTPUT:  
![aslist](\images\java\lambdaoutput.png) 


### 로컬 변수 사용  
람다식은 메소드 내부에서 주로 작성되기때문에 로컬 익명 구현 객체를 생성시킨다고 봐야 한다.  
람다식에서 바깥 클래스의 필드나 메소드는 제한 없이 사용할 수 있으나, 메소드의 매개 변수 또는 로컬 변수를 사용하면 이 두 변수는 **final 특성**을 가져야 한다.  
<br>

그렇다면 왜 이 경우 **final특성**이 강제될까??  
![메모리구조](\images\java\stackheapstructure.png)  
그 이유는 메소드 내에서 생성된 익명 객체는 메소드 실행이 끝나도 힙 메모리에 존재해서 계속 사용할 수 있기 때문이다.  
반면 매개 변수나 로컬 변수는 메소드 실행이 끝나면 스택 메모리에서 사라지기 때문에 익명 객체에서 사용할 수 없게 됨으로 문제가 발생한다.  
자바에서는 이 문제를 final키워드를 사용하여 해결하라고 하고 있다.  
익명 객체내부에서 사용하는 메소드의 매개 변수에 final키워드를 붙이는 것을 기본으로하고 있고 JAVA8 이후부터는 final선언을 생략할 수 있으나, 자동으로 final속성이 부여된다.   
또한 final 키워드를 적으면 메소드 내부에 지역 변수로 복사되지만, final 키워드가 없다면 익명클래스의 필드로 복사된다.  
결론적으로는 익명 객체에서 사용된 매개 변수와 로컬 변수는 모두 final특성을 갖는다는 것만 알면 된다.  
![변환](\images\java\convert.png)   

<br>
그럼 다시 람다식으로 돌아와서 코드를 보면 

```java
public class UsingLocalVariable{
    void method(int arg){  //arg는 final 특성을 가짐
        int localVar=40; //localVar는 final특성을 가짐

        //arg=31; //final 특성 때문에 수정 불가
        //localVar=41; //final특성때문에 수정 불가

        //람다식
        MyFunctionalInterface fi=()->{
            //로컬 변수 읽기
            System.out.println("arg:" + arg);
            System.out.println("localVar: " + localVar + "\n");
        };
        fi.method();
    }
}
```

---

# [표준 API의 함수적 인터페이스]
자바에서 제공되는 표준 API에서 한 개의 추상 메소드를 가지는 인터페이스들은 모두 람다식을 이용해서 익명 구현 객체로 표현이 가능하다.  
자바8부터는 빈번하게 사용되는 함수적 인터페이스는 java.util.function표준 API패키지로 제공한다.  
이 패키지에서 제공하는 함수적 인터페이스의 목적은 메소드 또는 생성자의 매개 타입으로 사용되어 람다식을 대입할 수 있도록 하기 위해서이다.  
java.util.function패키지의 함수적 인터페이스는 크게 Consumer,Supplier,Function,Operator,Predicate로 구분된다.(구분 기준은 인터페이스에 선언된 추상 메소드의 매개값과 리턴값의 유무이다.)   
[해당 블로그표 인용](https://altongmon.tistory.com/245){:target="_blank"}  
![자바유틸펑션패키지표](\images\java\functiontable.png)   
이와 관련된 모든 내용은 다음 도큐먼트에 상세히 기술되어있다.  
[java.util.function 도큐먼트](https://docs.oracle.com/en/java/javase/18/docs/api/java.base/java/util/function/package-summary.html){:target="_blank"}    

---

# [함수적 인터페이스의 디폴트 메소드]  
디폴트 및 정적 메소드는 추상 메소드가 아니기 때문에 함수적 인터페이스에 선언되어도 여전히 함수적 인터페이스의 성질을 잃지 않는다.  
디폴트 메소드란?  
```java
interface MyInterface { 
    default void printHello() {  //디폴트메소드
    	System.out.println("Hello World"); 
        } 
} 

class MyClass implements MyInterface {} 

public class DefaultMethod { 
    public static void main(String[] args) { 
    	MyClass myClass = new MyClass(); 
        myClass.printHello(); //실행결과 Hello World 출력 
    } 
}
```   
함수적 인터페이스 성질이란 하나의 추상 메소드를 갖고 있고, 람다식으로 익명 구현 객체를 생성할 수 있는 것을 말한다.   
java.util.function패키지의 함수적 인터페이스는 하나 이상의 디폴트 및 정적 메소드를 가지고 있다.  

<br>

### -andThen()과 compose() 디폴트 메소드
Consumer,Function,Operator 종류의 함수적 인터페이스는 andThen()과 compose() 디폴트 메소드를 가지고 있다.  
이 두가지 디폴트 메소드는 두 개의 함수적 인터페이스를 순차적으로 연결하고, 첫 번째 처리 결과를 두 번째 매개값으로 제공해서 최종 결과값을 얻을 때 사용함.  
차이점은 다음과 같다.  
```java
인터페이스AB = 인터페이스A.andThen(인터페이스B);
최종결과 = 인터페이스AB.method(); 
//인터페이스AB의 method()를 호출하면 우선 인터페이스A부터 처리하고 결과를 인터페이스B의 매개값으로 제공한다.
//그러면 인터페이스B는 제공받은 매개값을 가지고 처리한 후 최종 결과를 리턴함.  

인터페이스AB = 인터페이스A.compose(인터페이스B);
최종결과 = 인터페이스AB.method();  
//인터페이스AB의 method()를 호출하면 우선 인터페이스B부터 처리하고 결과를 인터페이스A의 매개값으로 제공한다.  
인터페이스A는 제공받은 매개값을 가지고 처리한 후 최종 결과를 리턴한다.  
```   
다음은 andThen()과 compose()디폴트 메소드를 제공하는 java.util.function 패키지의 함수적 인터페이스들이다.  
![andThen()이랑compose()표](\images\java\andthencompose.png)   
상세 사항은 마찬가지로 도큐먼트를 참고하는게 좋을 것 같다. [java.util.function 도큐먼트](https://docs.oracle.com/en/java/javase/18/docs/api/java.base/java/util/function/package-summary.html){:target="_blank"}     

### -and(),or(),negate() 디폴트 메소드와 isEqual() 정적 메소드
Predicate 종류의 함수적 인터페이스는 and(),or(),negate()디폴트 메소드를 갖고 있다.  
이 메소드들은 각각 논리 연산자인 &&,||,!과 대응된다.  
**and()**메소드는 두 Predicate가 모두 true를 리턴하면 최종적으로 true를 리턴하는 Predicate를 생성함.  
**or()**는 두 Predicate중 하나만 true를 리턴하더라도 최종적으로는 true를 리턴하는 Predicate를 생성함.  
**negate()**는 원래 Predicat의 결과과 true이면 false로, false면 true를 리턴하는 새로운 Predicate를 생성함.   
다음은 and(),or(),negate()디폴트 메소드를 제공하는 java.util.function 패키지의 함수적 인터페이스이다.  
![and(),or(),negate() 표](\images\java\andornegate.png)    
**Predicate\<T\> 함수적 인터페이스는 isEqual()정적 메소드를 추가로 제공한다.**   
isEqual()메소드는 test()매개값인 sourceObject와 isEqual()의 매개값인 targetObject를 java.util.Objects클래스의 equals()의 매개값으로 제공하고,  
Objects.equals(sourceObject,targetObject)의 리턴값을 얻어 새로운 Predicate<T>를 생성한다.   
```java
Predicate<Object> predicate = Predicate.isEqual(targetObject);
boolean result = predicate.test(sourceObject); //이렇게하면 Objects.equals(sourceObject,targetObject)가 실행됨.
```  
Objects.equals(sourceObject,targetObject)는 다음과 같은 리턴값을 제공한다.  
![and(),or(),negate() 표](\images\java\isequal.png)    

### -mainBy(),maxBy()정적 메소드 
BinaryOperator\<T\>함수적 인터페이스는 minBy()와 maxBy() 정적 메소드를 제공한다.  
이 두 메소드는 매개값으로 제공되는 Comparator를 이용해서 최대 T와 최소 T를 얻는 BinaryOperator\<T\>를 리턴한다.  
![minBy(),maxBy() 표](\images\java\maniby.png)   
참고로 Comparator\<T\>는 다음과 같이 선언된 함수적 인터페이스다. o1과 o2를 비교해서 o1이 작으면 음수를, o1과 o2가 동일하면 0을, o1이 크면 양수를 리턴하는 compare()메소드가 선언되어 있다.  
```java
@functionalInterface
public interface Comparator<T>{
    public int compare(T o1, T o2);
}
```
---
<br>

# [메소드 참조]  
메소드 참조는 메소드를 참조해서 매개 변수의 정보 및 리턴 타입을 알아내어, 람다식에서 불필요한 매개 변수를 제거하는 것이 목적이다.  
람다식은 종종 기존 메소드를 단순히 호출만 하는 경우가 많다.  예를들어  Math클래스의 max()정적 메소드를 호출하는 람다식은 다음과 같다.  
```java
(left,right)->Math.math(left,right); 
//이 경우 다음과 같이 메소드 참조를 이용하면 깔끔하게 가능  
Math::max;
```  
메소드 참조도 람다식과 마찬가지로 인터페이스의 익명 구현 객체로 생성되므로 타겟 타입인 인터페이스의 추상 메소드가 어떤 매개 변수를 가지고, 리턴 타입이 무엇인가에 따라 달라진다.  
IntBinaryOperator 인터페이스는 두 개의 int 매개값을 받아 int값을 리턴하므로 Math::max메소드 참조를 대입할 수 있다.  
```java
IntBinaryOperator operator = Math::max;
```  
메소드 참조는 정적 또는 인스턴스 메소드를 참조할 수 있고, 생성자 참조도 가능하다.  

<br>

### -정적 메소드 참조  
```java
클래스 :: 메소드 //정적(static)메소드를 참조할 경우 클래스 이름 뒤 ::기호를 붙이고 정적 메소드 이름을 기술
```  

### -인스턴스 메소드 참조
```java
참조변수 :: 메소드 //인스턴스 메소드는 먼저 객체를 생성한 다음 참조 변수 뒤에::기호를 붙이고 인스턴스 메소드이름을 적으면 됨.  
```

### -매개 변수의 메소드 참조
다음과 같이 람다식에서 제공되는 a 매개 변수의 메소드를 호출해서 b매개 변수를 매개값으로 사용하는 경우
```java
(a,b)->{a.instanceMethod(b);}
```  
이것을 메소드 참조로 표현하면 다음과 같다.  
```java
a의 클래스 이름 :: instanceMethod
//작성 방법은 정적 메소드 참조와 동일하지만, a의 인스턴스 메소드가 참조되므로 전혀 다른 코드가 실행됨.
```  

### -생성자 참조
```java
(a,b)->{return new 클래스(a,b);}
```  
이를 생성자 참조로 표현하려면, 클래스 이름 뒤에 ::기호를 붙이고 new 연산자를 기술하면 된다.  
생성자가 오버라이딩되어 여러 개가 있을 경우, 컴파일러는 함수적 인터페이스의 추상 메소드와 동일한 매개 변수 타입과 개수를 갖는 생성자를 찾아 실행한다.  
만약 해당 생성자가 존재하지 않으면 컴파일 오류가 발생함.  
```java
클래스::new
```