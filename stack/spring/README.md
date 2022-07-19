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
  - [SOLID](#solid)
    - [SRP](#srp)
    - [OCP](#ocp)
    - [ISP](#isp)
    - [LSP](#lsp)
    - [DIP](#dip)
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
객체지향 프로그래밍 (Object-Oriented-Programming, OOP)는 '역할을 가진 객체들의 협력'으로 프로그램을 작성하는 패러다임이다.
OOP의 특징으로는 아래의 4가지를 꼭 기억해야 한다.  
1. 추상화  
클래스의 공통된 속성을 바탕으로 필요한 부분만을 표현하고 불필요한 부분은 제거하는 기법이다.
<br>
2. 캡슐화  
속성을 외부로 노출시키지 않고, 자신의 클래스에서만 사용할 수 있도록 만드는 기법이다. 따라서 자연스레 은닉화의 특징도 가진다.
<br>

3. 상속  
공통된 속성을 가진 클래스들은 상속으로 코드의 중복을 제거하고, 재정의하여 코드의 재사용성을 높이는 기법이다.
<br>

4. 다형성  
인터페이스를 활용해 같은 형태의 함수이지만, 다른 기능을 할 수있도록 만드는 기법이다.

## SOLID
SOLID는 객체 지향 프로그래밍에서 지켜야 하는 5대 원칙이다.  
1. SRP(단일 책임 원칙)
2. OCP(개방-폐쇄 원칙)
3. LSP(리스코프 치환 원칙)
4. DIP(의존 역전 원칙)
5. ISP(인터페이스 분리 원칙)

### SRP
단일 책임의 원칙(SRP)은 하나의 모듈이 '한가지 책임'을 가져야 한다는 의미를 가지고 이것은 모듈이 변경되는 이유가 한가지여야 함을 의미한다.  
예를들어 아래와 같이 사용자의 정보를 받아서, 비밀번호를 암호화하여 데이터베이스에 저장하는 로직이 있다고 가정하자.

```JAVA
@Service
@RequiredArgsConstructor
public class UserService {

	private final UserRepository userRepository;

	public void addUser(final String email, final String pw) {
		final StringBuilder sb = new StringBuilder();

		for(byte b : pw.getBytes(StandardCharsets.UTF_8)) {
			sb.append(Integer.toString((b & 0xff) + 0x100, 16).substring(1));
		}

		final String encryptedPassword = sb.toString();
		final User user = User.builder()
				.email(email)
				.pw(encryptedPassword).build();

		userRepository.save(user);
	}
}
```
이 UserService의 로직에는 많은 변경이 발생할 수있다. 예를들면 아래와 같은 상황들이 발생한다.
- 기획팀: 사용자를 추가할 때 역할(Role)에 대한 정의가 필요하다.
- 보안팀: 사용자의 비밀번호 암호화 방식에 개신이 필요하다.

이러한 문제가 발생하는 이유는 UserService가 여러 액터로부터 단 하나의 책임을 가지고 있지 못하기 때문이며 이를위해서는 비밀번호 암호화에 대한 책임이 분리되어야 한다.  

```JAVA
@Component
public class SimplePasswordEncoder {

	public void encryptPassword(final String pw) {
		final StringBuilder sb = new StringBuilder();

		for(byte b : pw.getBytes(StandardCharsets.UTF_8)) {
			sb.append(Integer.toString((b & 0xff) + 0x100, 16).substring(1));
		}

		return sb.toString();
	}
}

@Service
@RequiredArgsConstructor
public class UserService {

	private final UserRepository userRepository;
	private final SimplePasswordEncoder passwordEncoder;

	public void addUser(final String email, final String pw) {
		final String encryptedPassword = passwordEncoder.encryptPassword(pw);

		final User user = User.builder()
				.email(email)
				.pw(encryptedPassword).build();

		userRepository.save(user);
	}
}
```
위와같이 암호화를 책임지는 별도의 클래스를 만들어 UserService로부터 이를 추상화하고 해당 클래스를 합성하여 접근 및 사용하면 문제를 해결할 수있다.  

이렇게 단일 책임 원칙을 제대로 지키면 변경이 필요할 때 수정할 대상이 명확해진다.  

또한 서로의 책임이 영향을 주지 않도록 추상화함으로써 애플리케이션의 변화에 손쉽게 대응할 수있다.

### OCP
개방 폐쇄 원칙(Open-Closed Principle, OCP)는 확장에 열려있고, 수정에 대해서는 닫혀있어야 한다는 원칙으로 각각이 갖는 의미는 아래와 같다.  
- 확장에 열려 있다 : 요구사항이 변경될 때 새로운 동작을 추가하여 애플리케이션의 기능을 확장할 수있다.
- 수정에 대해 닫혀있다 : 기존의 코드를 수정하지 않고 애플리케이션의 동작을 추가하거나 변경할 수있다.

아래의 예시를 통해 좀더 자세히 알아보자.  
비밀번호 암호화를 강화해야 한다는 요구사항이 새롭게 들어왔다고 가정하고, SHA-256 알고리즘을 사용하는 새로운 PassEncoder를 생성했다.

``` JAVA
@Component
public class SHA256PasswordEncoder {

	private final static String SHA_256 = "SHA-256";

	public String encryptPassword(final String pw)  {
		final MessageDigest digest;
		try {
			digest = MessageDigest.getInstance(SHA_256);
		} catch (NoSuchAlgorithmException e) {
			throw new IllegalArgumentException();
		}

		final byte[] encodedHash = digest.digest(pw.getBytes(StandardCharsets.UTF_8));

		return bytesToHex(encodedHash);
	}

	private String bytesToHex(final byte[] encodedHash) {
		final StringBuilder hexString = new StringBuilder(2 * encodedHash.length);

		for (final byte hash : encodedHash) {
			final String hex = Integer.toHexString(0xff & hash);
			if (hex.length() == 1) {
				hexString.append('0');
			}
			hexString.append(hex);
		}

		return hexString.toString();
	}
}
```
이제 새로운 비밀번호 암호화 정책을 적용하려고 보니, 새로운 암호화 정책과 무관한 UserService를 수정해야 하는 문제가 발생했다.  

```java
@Service
@RequiredArgsConstructor
public class UserService {

	private final UserRepository userRepository;
	private final SHA256PasswordEncoder passwordEncoder;

	...
    
}
```
이렇게 무관한 코드를 수정하는 것은 기존의 코드를 수정하지 않아야 하는 OCP에 위배된다. 그리고 나중에 또 암호화 정책이 변경된다면 UserService를 또 다시 변경해야 한다.  

OCP 원칙을 지키기 위해서는 '추상화'에 의존해야 한다.  
변하지 않는 부분은 고정하고, 변하는 부분은 추상화 한다면, 변경이 필요한 경우에 추상화된 부분을 수정하여 개방-폐쇄 원칙을 지킬 수 있게 된다.  

위의 예시에서 변화가 요구되는 것은 구체적인 암호화 정책이다.  
그러므로, UserService는 구체적으로 어떤 암호화 정책이 사용되는지 알 필요 없이 단지 PassEncoder라는 객체를 통해 추상적인 암호화 정책을 받기만 하면 된다.  
```JAVA
public interface PasswordEncoder {
    String encryptPassword(final String pw);
}

@Component
public class SHA256PasswordEncoder implements PasswordEncoder {

	@Override
	public String encryptPassword(final String pw)  {
      ...
	}
}

@Service
@RequiredArgsConstructor
public class UserService {

	private final UserRepository userRepository;
	private final PasswordEncoder passwordEncoder;

	public void addUser(final String email, final String pw) {
		final String encryptedPassword = passwordEncoder.encryptPassword(pw);

		final User user = User.builder()
				.email(email)
				.pw(encryptedPassword).build();

		userRepository.save(user);
	}
    
}
```
따라서 위와같이 구체적인 암호화 클래스에 의존하지 않고 인터페이스에 의존하도록 추상화를 하면 OCP 원칙을 지킬 수있게 된다.

### ISP
객체가 충분히 작은 단위로 설계됐더라도, 목적과 관심이 각기 다른 클라이언트가 있다면 인터페이스를 통해 적절히 분배할 필요가 있는데, 이를 인터페이스 분리 원칙 (ISP)라고 부른다.  
<br>
즉, ISP란 클라이언트의 목적과 용도에 적합한 인터페이스만을 제공하는 것이다.  
예를들어 사용자가 비밀번호를 변경할 때 입력한 비밀번호가 기존의 비밀번호와 동일한지 검색해야 하는 로직이 추가된다고 가정하자.  
그러면, 아래와 같이 isCorrectPassword라는 퍼블릭 인터페이스를 추가할 수있을 것이다.

``` JAVA
@Component
public class SHA256PasswordEncoder implements PasswordEncoder {

	@Override
	public String encryptPassword(final String pw)  {
		...
	}

	public String isCorrectPassword(final String rawPw, final String pw) {
		final String encryptedPw = encryptPassword(rawPw);
		return encryptedPw.equals(pw);
	}
}
```

새롭게 추가될 Authentication 클래스는 isCorrectPassword에 접근하기 위해 구체 클래스인 SHA256PasswordEncoderd를 주입 받아야 한다.  
그러면, 불필요한 encryprPassword에 접근할 수있게 되는 것이고, 이는 ISP를 위배하는 것이다.  

이를 해결하기 위해서는 비밀번호 검사를 의미하는 별도의 인터페이스(PasswordChecker)를 만들고, 해당 인터페이스를 Authentication이 주입받도록 하는 것이 좋다.

``` JAVA
public interface PasswordChecker {
    String isCorrectPassword(final String rawPw, final String pw);
}

@Component
public class SHA256PasswordEncoder implements PasswordEncoder, PasswordChecker {

	@Override
	public String encryptPassword(final String pw)  {
		...
	}
  
	@Override
	public String isCorrectPassword(final String rawPw, final String pw) {
		final String encryptedPw = encryptPassword(rawPw);
		return encryptedPw.equals(pw);
	}
}
```
이렇게 클라이언트에 따라 인터페이스를 분리하면 변경에 대한 영향을 더욱 세밀하게 제어할 수있다.

### LSP
리스코프 치환 원칙(LSP)는 '하위 타입'은 '상위 타입'을 대체할 수있어야 한다는 것이다. 즉, 해당 객체를 사용하는 클라이언트는 상위 타입이 하위 타입으로 변경되어도 차이점을 인식하지 못한 채 상위 타입의 퍼블릭 인터페이스를 통해 서브 플래스를 사용할 수있어야 한다.

### DIP
의존 역전 원칙(DIP)란 고수준 모듈이 저수준 모듈의 구현에 의존해서는 안되며, 저수준 모듈이 고수준 모듈에서 정의한 추상 타입에 의존해야 한다는 것이다. 여기서 말하는 고수준 모듈과 저수준 모듈은 아래와 같다.  
- 고수준 모듈 : 변경이 없는 추상화된 클래스 또는 인터페이스
- 저수준 모듈 : 변하기 쉬운 구체 클래스

DIP는 결국 추상화에 의존하며 구체와에는 의존하지 않는 설계 원칙을 말한다. 


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