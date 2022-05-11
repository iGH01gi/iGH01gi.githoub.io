---
layout: post
title: 예외 처리
date: 2022-05-10 00:00:00+0900
category: Java
published: true
---
# [error와 exception]  
- **error**: 하드웨어 고장등으로 인해 응용프로그램 실행 오류가 발생. JVM실행에 문제가 생긴것이므로 코드랑 무관하게 실행불능.  
- **exception**: 잘못된 코드나 사용자의 잘못된 조작으로 인해 발생하는 프로그램 오류. 에러와 공통점은 예외가 발생되면 프로그램이 종료된다는 것이지만 예외는 예외 처리(exception handling)을 통해 프로그램을 종료하지 않고 정상 실행 상태가 유지되도록 할 수 있음.   

---
# [exception은 2가지로 나뉜다]  
- **일반 예외(Exception)**  
- **실행 예외(Runtime Exception)**  

![예외 계층도](\images\java\java_exception_class_hierarchy.png)   
자바에서는 예외를 클래스로 관리한다. JVM은 프로그램을 실행하는 도중 예외가 발생하면 해당 예외 클래스로 객체를 생성함.  
java.lang.Exception을 바로 상속받는 클래스들은 일반 예외(Exception)들이다.  
**실행 예외(Runtime Exception)는 Exception을 상속받긴하지만 바로 위에 있는 상속은 java.lang.RuntimeException이다.**   
JVM은 그렇기에 RuntimeException을 상속했는지 여부를 보고 실행 예외를 판단한다.  
보통 RuntimeException클래스를 상속받는 자식 클래스들(실행 예외)은 치명적인 예외 상황을 발생시키지 않는 예외들로 구성된다.   

---
# [실행 예외(Runtime Exception)]  
실행 예외는 자바 컴파일러가 체크해주지 않기 때문에 프로그래머가 자신의 판단으로 예외 처리 코드를 삽입해야 한다.  
그렇기때문에 try/catch문을 사용하기보단 코딩할때 신경쓰면서 하는게 더 좋지 않을까 생각함.  
만약 실행 예외에 대해 예외 처리 코드를 넣지 않은 경우, 해당 예외가 발생하면 프로그램은 곧바로 종료된다.   
아래는 자바에서 자주 발생되는 실행 예외들의 예이다.  

- **NullPointerException**  
null값을 갖는 참조 변수로 객체 접근 연산자인 도트(.)를 사용했을 때 발생한다. 객체가 없는 상태에서 객체를 사용하려 한것이므로 예외가 발생한 것이다.  
```java
public class JavaStudy
{
    public static void main(String[] args){
    String data=null;
    System.out.println(data.toString()); //예외 발생
    }
}
```  
![예외사진](\images\java\nullpointerexception.png)   

- **ArrayIndexOutOfBoundsException**  
배열에서 인덱스 범위를 초과하여 사용할 경우.  
```java
public class JavaStudy
{
    public static void main(String[] args){
        int[] test={1,2,3};
        System.out.println(test[3]);
    }
}
```  
![예외사진](\images\java\arrayindexoutofboundsexception.png)  

- **NumberFormatException**   
문자열 데이터를 숫자로 변경할때 숫자로 변환될수 없는 문자가 포함되어 있을때 발생  
```java
public class JavaStudy
{
    public static void main(String[] args){
        String data="a100";
        int value=Integer.parseInt(data);
    }
}
```  
![예외사진](\images\java\numberformatexception.png)   


- **ClassCastException**  
클래스간 잘못된 타입 변환을 했을때 발생.  
```java
public class JavaStudy{
    public static void main(String[] args){
        Animal animal =new Dog();
        Cat cat=(Cat) animal;
    }
}
class Animal{
    //
}
class Animal{
    //
}
class Dog extends  Animal{
    //
}
class Cat extends Animal{
    //
}
```
![예외사진](\images\java\classcastexception.png)   
ClassCastException을 예방하려면 타입 변환 전에 변환이 가능한지 instanceof연산자를 사용해서 확인하는 것이 좋다.  
instanceof연산의 결과가 true이면 좌항 객체를 우항 타입으로 변환이 가능하다는 뜻이다.  
```java
public class JavaStudy
{
    public static void main(String[] args){
        Animal animal =new Dog();
        if(animal instanceof Dog){
            Dog dog=(Dog)animal;
        }
        else if(animal instanceof Cat){
            Cat cat=(Cat) animal;
        }
    }
}
class Animal{
    //
}
class Dog extends  Animal{
    //
}
class Cat extends Animal{
    //
}
```

---
# [예외 처리 코드]  
예외가 발생했을때 갑작스러운 종료를 막고, 정상 실행을 유지할 수 있게 처리하는 코드를 예외 처리 코드라고 한다.  
자바 컴파일러는 소스파일을 컴파일할 때 일반 예외가 발생할 가능성이 있는 코드를 발견하면 컴파일 오류를 발생시켜 개발자로 하여금 강제로 예외 처리 코드를 작성하도록 요구한다.  
그러나 실행 예외는 체크해주지 않기때문에 개발자가 알아서 써줘야 한다.  
예외 처리 코드의 기본 형식은 **try-catch-finally**블록이다.  
![예외사진](\images\java\try-catch-finally.webp)   
try블록에는 예외 발생 가능 코드가 위치한다.  이곳에서 예외 발생이 없었다면 catch블록은 실행되지 않는다.  
만약 try블록에서 예외가 발생하면 실행을 멈추고 catch블록으로 이동하여 예외 처리 코드를 실행한다.  
<br>
finally블록은 옵션으로 생략 가능하다.  
finally는 무조건 항상 실행되는 것이 아닌, finally와 연결되어 있는 try블록으로 진입을 하면 무조건 실행되는 영역이다.  
try블록이나 catch블록에서 return이 실행되어도 finally블록은 항상 실행된다.  
finally는 데이터베이스처리나 파일 처리에 특히 필요하다. 데이터베이스나 파일을 열었다면 닫아준 후 프로그램이 종료되어야 하는데 이 부분을 finally부분에서 수행해 주기 때문이다.  

---
# [다중 catch]  
try 블록 내부에서 다양한 종류의 예외가 발생할 수 있는데, 이때 발생되는 예외별로 예외 처리 코드를 다르게 할때 **다중 catch**블록을 작성한다.  
catch 블록의 예외 클래스 타입은 try블록에서 발생된 예외의 종류를 말하는데, try블록에서 해당 타입의 예외가 발생한다면 catch블록을 실행하도록 되어 있다.  
```java
public class JavaStudy
{
    public static void main(String[] args){
      try{
          //ArrayIndexOutOfBoundsException 발생 하면 첫번째 catch로
          
          //NumberFormatException 발생하면 두번째 catch로
      }catch (ArrayIndexOutOfBoundsException e){
          
      }catch (NumberFormatException e){
          
      }
    }
}
```  
그러나 catch 블록이 여러 개라 할지라도 단 하나의 catch블록만 실행된다. 그 이유는 try 블록에서 동시다발적으로 예외가 발생하지 않고, 하나의 예외가 발생하면 즉시 실행을 멈추고 해당 catch 블록으로 이동하기 때문이다.   

---
# [catch 순서]  
다중 catch블록을 작성할 때 상위 예외 클래스가 하위 예외 클래스보다 아래쪽에 위치해야 한다.  
try블록에서 예외가 발생했을 때, 예외를 처리해줄 catch블록은 위에서부터 차례대로 검색되기 때문이다.  
예를 들어 아래와 같이 코딩했을때 try문의 어떤 예외가 발생하든 모든 예외는 Exception을 상속받기 때문에 그 아래 catch문은 실행되지 못하고 첫번째 catch만 실행되게 된다.  
```java
public class JavaStudy
{
    public static void main(String[] args){
      try{
          //ArrayIndexOutOfBoundsException 발생

          //NumberFormatException 발생
      }catch (Exception e){

      }catch (ArrayIndexOutOfBoundsException e){

      }catch (NumberFormatException e){
          
      }
    }
}
```  

---
# [멀티 catch]  
자바 7부터 catch 블록에서 여러 개의 예외를 처리할 수 있도록 multi catch 기능을 추가 했다.  
조건문에서 많이 사용했듯이 | 기호를 이용한다.  
```java
catch(ArrayIndexOutOfBoundsException | NumberFormatException e){

}
```

---
# [자동 리소스 닫기]  
자바 7에서 새로 추가된 try-with-resources를 사용하면 예외 발생 여부와 상관없이 사용했던 리소스 객체(각종 입출력 스트림,서버 소켓,소켓,각종 채널)의 close() 메소드를 호출해서 안전하게 리소스를 닫아준다.  
이 기능이 있기 전까지 예를 들어 리소스 객체를 안전하게 닫기 위해서는 다음과 같이 사용했다.   
```java
public class JavaStudy
{

    public static void main(String[] args){
        FileInputStream fis=null;
        try{
          fis=new FileInputStream("file.txt");
        }catch (IOException e){
            ...
        }finally {
            if(fis!=null){
                try{
                    fis.close(); //이런 식으로 안전하게 닫아주었다.
                }catch(IOException e){...}
            }
        }
    }
}
```  
이걸 try-with-resources를 사용하면
```java
public class JavaStudy
{
    public static void main(String[] args){
       try(FileInputStream fis=new FileInputStream("file.txt")){  //이런식으로 간단히 한줄로 줄일 수 있다.
           ...
       }catch(IOException e){
           ...
       }
    }
}
```  
위처럼 try블록이 정상적으로 실행을 완료했거나 도중에 예외가 발생하게 되면 자동으로 FileInputStream의 close() 메소드가 호출된다.  
try{}에서 예외가 발생하면 우선 close()로 리소스를 닫고 catch블록을 실행한다. try()의 괄호 속에 복수 개의 리소스를 넣어서도 사용 가능하다. 

<br>
단, try-with-resources를 사용하기 위해서는 조건이 있는데, 리소스 객체는 java.lang.AutoCloseable 인터페이스를 구현하고 있어야 한다.  
AutoCloseable에는 close() 메소드가 정의되어 있는데 try-with-resources는 바로 이 close() 메소드를 자동 호출한다. 

---
# [예외 떠넘기기]  
메소드를 호출한 곳으로 예외를 떠넘기고 싶을 때 사용.  
사용하는 키워드는 throws.   
throws키워드는 메소드 선언부 끝에 작성되어 메소드에서 처리하지 않은 예외를 호출한 곳으로 떠넘기는 역할을 한다.  
throws 키워드 뒤에는 떠넘길 예외 클래스를 쉼표로 구분해서 나열해주면 된다.  
```java
리턴타입 메소드명(매개변수,...) throws 예외클래스1, 예외클래스2{}
```  
발생할 수 있는 예외의 종류별로 throws 뒤에 나열하는 것이 일반적이지만, 다음과 같이 throws Exception만으로 모든 예외를 간단히 떠넘길 수도 있다.  
```java
리턴타입 메소드명(매개변수,...) throws Exception{}
```   
<br>
**throws 키워드가 붙어있는 메소드는 반드시 try 블록 내에서 호출되어야 한다.**  
그리고 catch 블록에서 떠넘겨 받은 예외를 처리해야 한다. 아니면 throws를 다시 사용해서 예외를 호출한 곳으로 또 떠넘겨줘야한다.  
결국 언젠가는 try-catch문에서 다루어줘야한다. 아래는 그 예시이다.   
```java
public class JavaStudy
{
    public static void main(String[] args) {
        try {
            method2();
        } catch (ClassNotFoundException e) {
            //예외 처리 코드
            System.out.println("클래스가 존재하지 않습니다.");
        }
    }
        public static void method2() throws ClassNotFoundException{
            Class test = Class.forName("java.lang.String2");//Class.forName메소드는 매개값으로 주어진 클래스가 존재하면 Class객체를 리턴하지만 그렇지않으면 ClassNotFoundException 예외를 발생시킴.
        }
}
```  
참고로 main()메소드에서도 throws 키워드를 사용해서 예외를 떠넘길 수 있는데, 결국 JVM이 최종적으로 예외 처리를 하게 된다.  
JVM은 예외의 내용을 콘솔에 출력하는 것으로 예외 처리를 한다.  하지만 이는 좋은 방법은 아니다.   
```java
//좋지 않은 방식
public class JavaStudy
{
    public static void main(String[] args) throws ClassNotFoundException{
            method2();
    }
        public static void method2() throws ClassNotFoundException{
            Class test = Class.forName("java.lang.String2");//Class.forName메소드는 매개값으로 주어진 클래스가 존재하면 Class객체를 리턴하지만 그렇지않으면 ClassNotFoundException 예외를 발생시킴.
        }
}
```

---
# [사용자 정의 예외]  
자바 표준 API에서 제공하는 예외 클래스만으로는 다양한 종류의 예외를 표현할 수 없다.(ex.은행 프로그램에서 잔고보다 많은 출금요청 등)  
그럴때 프로그래머가 직접 정의해서 만들어야 하므로 사용자 정의 예외를 사용한다.  

<br>
- **사용자 정의 예외 클래스 선언**  
일반 예외로 선언할 경우 Exception을 상속,  
실행 예외로 선언할 경우 RuntimeException을 상속하면 된다.
사용자 정의 예외 클래스 이름은 Exception으로 끝내는 것이 관례이다.  
사용자 정의 예외 클래스도 필드,생성자,메소드 선언들을 포함할 수 있지만 대부분 생성자 선언만을 포함한다.  
```java
public class ~~~Exception extends [ Exception | RuntimeException ]{
        public ~~~Exception() {} //매개 변수가 없는 기본 생성자
        public ~~~Exception(String message) { super(message); } //예외 메시지를 전달하기 위한 생성자
}
```  
위와같이 생성자는 두 개를 선언하는 것이 보통인데, 하나는 매개변수가 없는 기본 생성자이고, 다른 하나는 예외 발생 원인(예외 메시지)을 전달하기 위해 String 타입의 매개변수를 갖는 생성자이다.  
String 타입의 매개 변수를 갖는 생성자는 상위 클래스의 생성자를 호출하여 예외 메시지를 넘겨준다.  
예외 메시지의 용도는 catch{}블록의 예외 처리 코드에서 이용하기 위함이다.  
<br>
- **예외 발생시키기**  
사용자 정의 예외든 자바 표준 예외든 예외를 발생시키는 방법은 다음과 같이 **throw**를 사용한다. throws가 아닌 throw다.
```java
throw new ~~~Exception();
throw new ~~~Exception("메시지");
```  
예외 객체를 생성할 때는 기본 생성자 또는 예외 메시지를 갖는 생성자 중 어떤것을 사용해도 된다.  
만약 catch 블록에서 예외 메시지가 필요하다면 예외 메시지를 갖는 생성자를 이용한다.  
그리고 예외 발생 코드를 갖고 있는 메소드는 내부에서 try-catch 블록으로 예외를 처리할 수 있지만, 대부분은 자신을 호출한 곳에서 예외를 처리하도록 throws 키워드로 예외를 떠넘긴다.  
```java
public void method() throws ~~~Exception{
    throw new ~~~Exception("메시지");
}
```  
그렇기에 throws 키워드를 포함하고 있는 메소드는 호출한 곳에서 다음과 같이 예외 처리를 해주어야 한다.  
```java
try{
    method();
}
catch(~~~Exception e){
    //예외처리
}
```  
아래는 출금(withdraw) 메소드에서 잔고(balance) 필드와 출금액을 비교해서 잔고가 부족하면 BalanceInsufficientException을 발생시키게 한 예시다.

```java
public class BalanceInsufficientException extends Exception{ //사용자 정의 예외 클래스
    public BalanceInsufficientException(){ }
    public BalanceInsufficientException(String message){
        super(message); //나중에 catch블록에서 예외 처리 코드에서 이용하기 위해서
    }
}

public class Account{
    private long balance;

    public void withdraw(int money) throws BalanceInsufficientException{ //예외 떠넘기기
        if(balance < money){ //출금액에 비해 잔고가 부족하면 예외 발생
            throw new BalanceInsufficientException("잔고부족:"+(money-balance)+" 모자람");
        }
        balance-=money;
    }
}
```
<br>
- **예외 정보 얻기**  
try블록에서 예외가 발생하면 예외 객체는 catch 블록의 매개 변수에서 참조하므로 매개 변수를 이용하면 예외 객체의 정보를 알 수 있다.  
모든 예외 객체는 Exception 클래스를 상속하기 때문에 Exception이 갖고 있는 메소드들을 모든 예외 객체에서 호출할 수 있다.  
그중 가장 많이 사용되는 메소드는 getMessage()와 printStackTrace()이다.  
**getMessage()**는 예외객체 내부에 저장된 메시지를 리턴값으로 얻기위한 메소드이고  
**printStackTrace()**는 예외 발생 코드를 추적해서 모두 콘솔에 출력한다.어떤 예외가 어디에서 발생했는지 상세히 출력하기에 디버깅할때 자주 활용된다.    
```java
try{
    //예외가 발생
}catch(예외클래스 e){
    //예외가 가지고 있는 Message 얻기
    String message = e.getMessage();

    //예외의 발생 경로를 추적
    e.printStackTrace();
}
```
