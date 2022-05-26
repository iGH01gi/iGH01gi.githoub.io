---
layout: post
title: 제네릭
date: 2022-05-26 00:00:00+0900
category: Java
published: true
---
# [제네릭 사용 이유] 
```java
public class Box{
    private Object object;
    public void set(Object object) { this.object=object; }
    public Object get() { return object; }
}
```  
제네릭을 사용하지 않으면 Object타입을 사용해서 모든 타입의 객체를 받을 수 있다.  
(Object는 모든 자바 클래스의 최상위 부모 클래스이므로.)  
그러나 이렇게 사용하면 메소드를 사용할때 강제 타입변환을 해줘야 할 일이 생긴다.  
```java
String str=(String) box.get(); //Object타입을 String타입으로 강제 타입 변환해서 얻음
```  
이러한 불편함을 해결하기 위해 나타난 것이 제네릭이다.  

--- 

# [제네릭 타입(class\<T\>, interface\<T\>)]  
제네릭 타입은 타입을 파라미터로 가지는 클래스와 인터페이스를 말한다.  
제네릭 타입은 클래스 또는 인터페이스 이름 뒤에 "\<\>"기호가 붙고, 사이에 타입 파라미터가 위치한다.  
다음 코드에서 타입 파라미터의 이름은 T이다.  
```java
public class 클래스명<T> { ... }
public interface 인터페이스명<T> { ... }
```  
보통 대문자 알파벳 한 글자로 표현한다.  

<br>
만약 int형을 타입파라미터로 받고 싶다면, int(primitive 자료형)가 아닌 Integer(int의 Wrapper 클래스임.객체이다.)로 적어주어야한다.  
다른 primitive자료형에도 마찬가지로 적용된다.  다음은 기본타입과 해당하는 Wrapper class이다.  
![wrapper클래스표](\images\java\wrapper.jpg)  
[Wrapper 클래스란?](http://www.tcpschool.com/java/java_api_wrapper){:target="_blank"}
> 프로그램에 따라 기본 타입의 데이터를 객체로 취급해야 하는 경우가 있습니다.
예를 들어, 메소드의 인수로 객체 타입만이 요구되면, 기본 타입의 데이터를 그대로 사용할 수는 없습니다.  
이때에는 기본 타입의 데이터를 먼저 객체로 변환한 후 작업을 수행해야 합니다.   
이렇게 8개의 기본 타입에 해당하는 데이터를 객체로 포장해 주는 클래스를 래퍼 클래스(Wrapper class)라고 합니다.  
래퍼 클래스는 각각의 타입에 해당하는 데이터를 인수로 전달받아, 해당 값을 가지는 객체로 만들어 줍니다.  
이러한 래퍼 클래스는 모두 java.lang 패키지에 포함되어 제공됩니다.   

---

# [멀티 타입 파라미터(class\<K,V,...>, interface\<K,V,...>)] 
제네릭 타입은 두 개 이상의 멀티 타입 파라미터를 사용할 수 있는데, 이 경우 각 타입 파라미터를 콤마로 구분함.
```java
public class Product<T,M>{
    private T kind;
    private M model;

    public T getKind() { return this.kind; }
    public M getModel() { return this.model; }

    public void setKind(T kind) { this.kind = kind; }
    public void setModel(M model) { this.model = model; }
}

public class ProductExample{
    public static void main(String[] args){
        Product<Tv,String> product1 = new Product<Tv,String>();
        product1.setKind(new Tv());
        product1.setModel("스마트Tv");
        Tv tv=product1.getKind();
        String tvModel=product1.getModel();
    }
}
```  
이때 자바7부터 제네릭 타입 변수 선언과 객체 생성을 동시에 할 때  
타입 파라미터 자리에 구체적인 타입을 지정하는 코드가 중복해서 나오는 것을  
자바 컴파일러가 유추해서 자동으로 설정해준다.  
```java
//자바6 까지
Product<Tv,String> product = new Product<Tv,String>();

//자바7~
Product<Tv,String> product = new Product<>();
```  

--- 

# [제네릭 메소드(\<T,R> R method(T t))]
제네릭 메소드는 매개 타입과 리턴 타입으로 타입 파라미터를 갖는 메소드를 말한다.  
제네릭 메소드를 선언하는 방법은 리턴 타입 앞에 \<> 기호를 추가하고 타입 파라미터를 기술한 다음,  
리턴 타입과 매개 타입으로 타입 파라미터를 사용하면 된다.  
```java
public <타입파라미터,...> 리턴타입 메소드명(매개변수,...) {...}
```  
다음 boxing() 제네릭 메소드는 \<>기호 안에 타입 파라미터 T를 기술한 뒤, 매개 변수 타입으로 T를 사용했고, 리턴 타입으로 제네릭 타입 BOX\<T>를 사용했다.  
```java
public <T> Box<T> boxing(T t) {...}
```  
제네릭 메소드는 두 가지 방식으로 호출가능.  
코드에서 타입 파라미터의 구체적인 타입을 명시적으로 지정해도 되고,  
컴파일러가 매개값의 타입을 보고 구체적인 타입을 추정하도록 할 수도 있음.  
```java
리턴타입 변수 = <구체적타입> 메소드명(매개값); //명시적으로 구체적인 타입을 지정
Box<Integer> box=<Integer>boxing(100); //그 예시 

리턴타입 변수 = 메소드명(매개값); //매개값을 보고 구체적 타입을 추정
Box<Integer> box=boxing(100); //그 예시
``` 

---

# [제한된 타입 파라미터(\<T extends 최상위타입>)]
타입 파라미터에 지정되는 구체적인 타입을 제한할 필요가 종종 있다.  
(ex. 숫자를 연산하는 제네릭 메소드는 매개값으로 Number타입 또는 하위 클래스 타입(Byte,Short,Integer,Long,Double)의 인스턴스만 가져야 함.)  
[넘버타입이란?](https://soongjamm.tistory.com/120){:target="_blank"}  
제한된 타입 파라미터를 선언하려면 타입 파라미터 뒤에 extends키워드를 붙이고 상위 타입을 명시하면 된다.  
상위 타입은 클래스뿐만 아니라 인터페이스도 가능한데, **인터페이스라고 해서 implements를 사용하지 않는다!**  
```java
public <T extends 상위타입> 리턴타입 메소드(매개변수, ...) { ... }
```  
타입 파라미터에 지정되는 구체적인 타입은 상위 타입이거나 상위 타입의 하위 또는 구현 클래스만 가능하다.  
주의할 점은 메소드의 중괄호 {}안에서 타입 파라미터 변수로 사용 가능한 것은 상위 타입의 멤버(필드,메소드)로 제한된다.  
하위 타입에만 있는 필드와 메소드는 사용할 수 없다.  
다음은 숫자 타입만 구체적인 타입으로 갖는 제네릭 메소드 compare()이다. 두 개의 숫자 타입을 매개값으로 받아 차이를 리턴한다.  
```java
public <T extends Number> int compare(T t1, T t2){
    double v1 = t1.doubleValue(); //Number의 doubleValue() 메소드 사용
    double v2 = t2.doubleValue(); //Number의 doubleValue() 메소드 사용
    return Double.compare(v1,v2);
}
```

---
<br>

> 알아두면 좋은 정보: **제네릭 배열은 불가능하다.**  
제네릭 배열을 직접 생성할 순 없지만 와일드카드 타입을 이용하거나, 강제 형변환을 통해 제네릭 배열을 사용할 수 있다.  
[왜 제네릭 배열이 안되는가?](https://pompitzz.github.io/blog/Java/whyCantCreateGenericsArray.html#_2-%E1%84%87%E1%85%A2%E1%84%8B%E1%85%A7%E1%86%AF%E1%84%8B%E1%85%B3%E1%86%AB-%E1%84%85%E1%85%A5%E1%86%AB%E1%84%90%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%B7%E1%84%8B%E1%85%A6-%E1%84%89%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A6%E1%84%92%E1%85%AA-%E1%84%8C%E1%85%A6%E1%84%82%E1%85%A6%E1%84%85%E1%85%B5%E1%86%A8-%E1%84%90%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%B8%E1%84%8B%E1%85%B3%E1%86%AB-%E1%84%85%E1%85%A5%E1%86%AB%E1%84%90%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%B7%E1%84%8B%E1%85%A6-%E1%84%89%E1%85%A9%E1%84%80%E1%85%A5){:target="_blank"}  

# [와일드카드 타입(\<?>, \<? extends ...>, \<? super ...>)]
코드에서 ?를 일반적으로 와일드카드(wildcard)라고 부른다.  
제네릭 타입을 매개값이나 리턴 타입으로 사용할 때 구체적인 타입 대신에 와일드카드를 다음과 같이 세 가지 형태로 사용할 수 있다.  
- **제네릭타입\<?>:** Unbounded Wildcards(제한 없음)  
타입 파라미터를 대치하는 구체적인 타입으로 모든 클래스나 인터페이스 타입이 올 수 있다.  
- **제네릭타입\<? extends 상위타입>:** Upper Bounded Wildcards(상위 클래스 제한)  
타입 파라미터를 대치하는 구체적인 타입으로 상위 타입이나 하위 타입만 올 수 있다.  
- **제네릭타입\<? super 하위타입>:** Lower Bounded Wildcards(하위 클래스 제한)  
타입 파라미터를 대치하는 구체적인 타입으로 하위 타입이나 상위 타입이 올 수 있다.   

<br>
코드를 통해 사용방법을 익혀보자.   
![상속관계](\images\java\persondirect.JPG)  
```java
//Course.java
public class Course<T>{
    private String name;
    private T[] students;

    public Course(String name, int capacity){
        this.name = name;
        students = (T[]) (new Object[capacity]); // 타입 파라미터를 바로 배열로 생성못함. 강제형변환을 통해서 이런식으로는 가능.
    }

    public String getName() { return name; }
    public T[] getStudents() { return students; }
    
    public void add(T t) {
        for(int i=0; i<students.length; i++>){
            if(students[i] == null){
                students[i]=t;
                break;
            }
        }
    }
}

//WildCardExample.java
import java.util.Arrays;

public class WildCardExample{
    public static void registerCourse( Course<?> course ){
        System.out.println(course.getName()+"수강생"+Arrays.toString(course.getStudents()));
    }

    public static void registerCourse( Course<? extends Student> course ){
        System.out.println(course.getName()+"수강생"+Arrays.toString(course.getStudents()));
    }

    public static void registerCourse( Course<? super Worker> course ){
        System.out.println(course.getName()+"수강생"+Arrays.toString(course.getStudents()));
    }

    public static void main(String[] args){
        Course<Person> personCourse=new Course<Person>("일반인과정",5);
        personCourse.add(new Person("일반인"));
        personCourse.add(new Person("직장인"));
        personCourse.add(new Person("학생"));
        personCourse.add(new Person("고등학생"));

        Course<Worker> workerCourse=new Course<Worker>("직장인과정",5);
        workerCourse.add(new Worker("직장인"));

        Course<Student> studentCourse=new Course<Student>("학생과정",5);
        studentCourse.add(new Student("학생"));
        studentCourse.add(new HighStudent("고등학생"));

        Course<HighStuden> highStudentCourse=new Course<HighStudent>("고등학생과정",5);
        highStudentCourse.add(new HighStudent("고등학생"));

        registerCourse(personCourse);
        registerCourse(workerCourse);
        registerCourse(studentCoures);
        registerCourse(highStudentCourse);
        System.out.println();

        //registerCourseStudent(personCourse);  불가능
        //registerCourseStudent(workerCourse);  불가능
        registerCourseStudent(studentCoures);
        registerCourseStudent(highStudentCourse);
        System.out.println();

        registerCourseWorker(personCourse);
        registerCourseWorker(workerCourse);
        //registerCourseWorker(studentCoures);  불가능
        //registerCourseWorker(highStudentCourse);  불가능
    }
}
```  
위 코드의 실행결과는  
```java
일반인과정 수강생:[일반인, 직장인, 학생, 고등학생, null]
직장인과정 수강생:[직장인, null, null, null, null]
학생과정 수강생:[학생, 고등학생, null, null, null]
고등학생과정 수강생:[고등학생, null, null, null, null]

학생과정 수강생:[학생, 고등학생, null, null, null]
고등학생과정 수강생:[고등학생, null, null, null, null]

일반인과정 수강생:[일반인, 직장인, 학생, 고등학생, null]
직장인과정 수강생:[직장인, null, null, null, null]
```  

---

# [제네릭 타입의 상속과 구현]
제네릭 타입도 다른 타입과 마찬가지로 부모 클래스가 될 수 있다.  
다음은 Product<T,M> 제네릭타입을 상속해서 ChildProduct<T,M>타입을 정의한다.  
```java
public class ChildProduct<T,M>extends Product<T,M>{...}
```  
자식 제네릭 타입은 추가적으로 타입 파라미터를 가질 수 있다. 다음은 세 가지 타입 파라미터를 가진 자식 제네릭 타입을 선언한 것이다.  
```java
public class ChildProduct<T,M,C> extends Product<T,M> {...}
```  
그리고 제네릭 인터페이스를 구현한 클래스도 제네릭타입이어야 한다.  