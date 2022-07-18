# Spring
 

- [Spring](#spring)
  - [Spring의 탄생](#spring의-탄생)
  - [POJO](#pojo)
  - [Spring은 왜 사용할까](#spring은-왜-사용할까)
  - [DI](#di)
  - [DI 방법](#di-방법)
    - [생성자 주입](#생성자-주입)
    - [수정자 주입](#수정자-주입)
    - [필드 주입](#필드-주입)
    - [메서드 주입](#메서드-주입)
  - [생성자 주입을 사용하라](#생성자-주입을-사용하라)
    - [객체의 불변성 확보](#객체의-불변성-확보)
    - [테스트 코드의 작성](#테스트-코드의-작성)
    - [순환 참조 에러 방지](#순환-참조-에러-방지)
  - [PSA](#psa)
  - [AOP](#aop)
  - [OOP](#oop)
  - [Spring 컨테이너](#spring-컨테이너)
  - [Bean 객체란](#bean-객체란)
  - [싱글톤 컨테이너](#싱글톤-컨테이너)
  - [싱글톤 주의점](#싱글톤-주의점)
  - [Bean 생명주기](#bean-생명주기)


## Spring의 탄생
Spring은 무겁고 복잡한 EJB를 대체하고자 등장한 프레임워크이다.  
스프링이 등장하기 이전의 EJB와 같은 프레임워크를 사용하기 위해서는 기술을 직접적으로 사용하는 객체를 생성해야 했다.  

스프링은 이러한 무거운 객체들에 종속되는 기술이 아닌 순수한 자바 객체, POJO 방식을 사용하기 위해 등장한 프레임워크이다.  

## POJO
Plain Old Java Object의 약어로 프레임위크에 종속되는 무거운 객체 사용이 아닌 순수 자바 객체를 사용하는 것을 말한다.

## Spring은 왜 사용할까
서비스는 커질수록 안정성이 낮아진다. 그리고 Java + Spring은 서비스의 안정성을 높이는데 탁월하다. Spring의 안정성을 높이는 요인으로는 아래와 같은 것들이 존재한다.  
1. DI : 의존성 주입
2. PSA : 서비스 추상화
3. AOP : 관점지향 프로그래밍

## DI
DI(Dependency Injection)는 외부에서 두 객체 간의 관계를 결정해주는 디자인 패턴이다.  
자바의 다형성을 활용하여 클래스 레벨의 의존관계가 고정되지 않도록 하고 런타임 시에 관계를 동적으로 주입하여 유연성을 확보하고 결합도를 낮출 수 있게 해주며 아래와 같은 장점들을 얻게 해준다. 
- 두 객체 간의 관심사의 분리
- 두 객체 간의 결합도를 낮춤
- 객체의 유연성을 높임
- 테스트 작성을 용이하게 함

## DI 방법
DI(Dependency Injection, 의존성 주입)는 pring 프레임워크의 핵심 기술 중 하나이고, 여러가지 방법이 존재한다. 
<br>

### 생성자 주입  
생성자 주입은 아래의 코드와 같이 생성자를 통해 의존관계를 주입하는 방법이다.
```java
@Service
public class UserService {

    private UserRepository userRepository;
    private MemberService memberService;

    @Autowired
    public UserService(UserRepository userRepository, MemberService memberService) {
        this.userRepository = userRepository;
        this.memberService = memberService;
    }
    
}
```
생성자 주입은 생성자의 호출 시점에 딱 한번 호출된다.  
따라서 주입받은 객체가 변하지 않거나, 반드시 객체의 주입이 필요한 경우에 강제하기 위해 사용한다. 또한 Spring 프레임워크에서는 생성자 주입을 밀고 있기 때문에, 생성자가 1개만 있을 경우에 @Autowired를 생략해도 주입이 가능하도록 편의성을 제공하기도 한다. 

### 수정자 주입
수정자 주입(Setter 주입, Setter Injection)은 필드 값을 변경하는 Setter를 통해서 의존 관계를 주입하는 방법이다.  
Setter 주입은 생성자 주입과 다르게 주입받는 객체가 변경될 가능성이 있는 경우에 사용한다. 하지만, 실제로 변경이 필요한 경우는 극히 드물다.
```java
@Service
public class UserService {

    private UserRepository userRepository;
    private MemberService memberService;

    @Autowired
    public void setUserRepository(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    @Autowired
    public void setMemberService(MemberService memberService) {
        this.memberService = memberService;
    }
}
```

### 필드 주입  
필드 주입(Field Injection)은 필드에 바로 의존 관계를 주입하는 방법이다. 

```JAVA
@Service
public class UserService {

    @Autowired
    private UserRepository userRepository;
    @Autowired
    private MemberService memberService;

}
```
필드 주입은 코드가 간결해져서 과거에 상당히 많이 이용되었던 주입 방법이다.  
하지만 필드 주입은 외부에서 접근이 불가능하다는 단점이 존재하는데, 테스트 코드의 중요성이 부각됨에 따라 필드의 객체를 수정할 수 없는 필드 주입은 거의 사용하지 않는다.  
또한 필드 주입은 반드시 DI 프레임워크가 존재해야 하므로 사용을 지양해야 한다. 

### 메서드 주입
일반 메소드를 통해 의존 관계를 주입하는 방법이다. 수정자 주입과 동일하며 거의 사용할 필요가 없는 주입 방법이다.  
수정자 주입을 사용하면 한 번에 여러 필드를 주입 받을 수 있도록 메소드를 작성할수도 있다.

## 생성자 주입을 사용하라
최근에는 Spring을 포함한 DI 프레임워크의 대부분이 생성자 주입을 권장하는데, 이유는 아래와 같다.  
### 객체의 불변성 확보
수정자 주입이나 일반 메소드 주입을 이용하면 불필요하게 수정의 가능성을 열어두어 유지보수성을 떨어뜨린다.  
따라서 생성자 주입을 통해 변경의 가능성을 배제하고 불변성을 보장하는 것이 좋다.

### 테스트 코드의 작성
테스트는 가능한 순수 자바로 테스트를 작성하는 것이 가장 좋은데, 생성자 주입이 아닌 다른 주입으로 작성된 코드는 순수한 자바 코드로 단위 테스트를 작성하는 것이 어렵다.  

생성자 주입을 사용하면 컴파일 시점에 객체를 주입받아 테스트 코드를 작성할 수 있으며, 주입하는 객체가 누락된 경우 컴파일 시점에 오류를 발견할 수 있다.

### 순환 참조 에러 방지
생성자 주입을 사용하면 애플리케이션 구동 시점(객체의 생성 시점)에 순환 참조 에러를 예방할 수 있다.  
만약 2개의 객체가 서로를 참조한다면, 애플리케이션 메모리에 함수의 callstack이 쌓이게 되고, stack overflow가 발생한다.  

만약 이러한 문제를 발견하지 못하고 서버가 운영된다면 해당 메소드의 호출 시에 stack overflow 에러에 의해 서버가 죽게 된다.  
하지만 생성자 주입을 이용하면 애플리케이션 구동 시점(객체의 생성 시점)에 에러가 발생하기 때문에 순환 참조 문제를 방지할 수 있다.

## PSA
스프링을 사용하면 서비스 추상화를 통해 특정 환경이나 서버, 기술에 종속되지 않으며 유연한 애플리케이션을 개발할 수 있다.  
예를 들어 MyBatis나 JPA 등 세부 기술에 종속적인 에러들을 추상화하여 기술에 종속적이지 않은 에러들로 처리할 수 있도록 하기도 한다.  

또한 스프링을 공부하다 보면 추상화를 위해 프록시(Proxy) 패턴과 같은 디자인 패턴이 매우 자주 사용되는 것을 볼 수있다.

## AOP 

## OOP

## Spring 컨테이너
Spring 컨테이너는 애플리케이션을 구성하는 오브젝트(빈)을 생성하고 관리한다. 또한 객체에 대해 의존성 주입(Dependency Injection, DI)를 통해 두 객체의 결합도를 낮추는 역할을 한다.

## Bean 객체란
Spring 컨테이너가 관리하는 Java 객체를 Bean 객체라고 부른다.

## 싱글톤 컨테이너  
![image](https://user-images.githubusercontent.com/76645095/179488685-99006346-ef2a-440e-90ba-b781a2dadb0f.png)

스프링 컨테이너는 위의 그림과 같이 싱글톤 컨테이너 역할을 하는데, 스프링 컨테이너가 싱글톤 객체를 생성하고 관리하는 기능을 Singleton Registry라고 부른다. 

## 싱글톤 주의점
싱글톤 객체를 multi-thread 환경에서 할때는 내부에 상태정보를 갖지 않는 무상태(Stateless) 방식으로 만들어져야 한다. 만약 여러 쓰레드들이 동시에 상태 정보에 접근하여 이 값을 수정한다면 문제가 발생한다.  

## Bean 생명주기

![image](https://user-images.githubusercontent.com/76645095/179476333-ab189bd4-d7ef-4e86-8abc-e4c5b2173b0c.png)
<br>

스프링 빈은 객체를 생성하고, 의존관계 주입이 다 끝난 다음에야 필요한 데이터를 사용할 수있는 준비가 완료된다. 따라서 초기화 작업은 의존관계 주입이 모두 끝나고 난 뒤에 호출되어야 한다. 

스프링은 의존관계 주입이 완료되면, 스프링 빈에게 콜백 메서드를 통해서 초기화 시점을 알려주는 다양한 기능을 제공한다. 또한 스프링은 스프링 컨테이너가 종료되기 직전에 소멸 콜백을 주기도 한다.

​Reference  
- [인프런](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%ED%95%B5%EC%8B%AC-%EC%9B%90%EB%A6%AC-%EA%B8%B0%EB%B3%B8%ED%8E%B8/unit/55363?tab=curriculum&volume=1.00&quality=1080)  
- [mangkyu.tistory.com](https://mangkyu.tistory.com/)