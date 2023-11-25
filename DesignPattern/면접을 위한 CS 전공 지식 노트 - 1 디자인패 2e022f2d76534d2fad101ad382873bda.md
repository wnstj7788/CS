# 면접을 위한 CS 전공 지식 노트 - 1. 디자인패턴

태그: BOOK
생성 일시: 2023년 11월 23일 오전 2:10

# 1.1디자인 패턴

- 디자인 패턴 프로그램을 설계할 때 발생했던 문제점을 객체 간의 상호 관계 등을 이용하여 해결 할 수 있는 하나의 “규약” 형태로 만들어 놓은 것

## 1.1.1 싱글톤 패턴(Singleton Pattern)

- 하나의 클래스에 오직 하나의 인스턴스만 가지게 하는 패턴
- 여러개의 개별적인 인스턴스를 만들 수 있지만 그렇게 하지 않고 클래스를 기반으로 단 하나의 인스턴스만 가능하게 만듬 → 데이터 베이스 연결 모듈에서 많이 사용되는 패턴
- 장점 : 인스턴스를 생성 시 비용이 줄어든다
- 단점 : 의존성이 높아진다.

### 기존 코드

```jsx
const obj = {
	 a: 27
}

const obj2 = {
	 a: 27
}

console.log(obj == obj2) => false 
```

### 싱글톤 코드

- a와 b 는 하나의 인스턴스를 가짐

```jsx
class Singleton{
	constructor(){
		if(!Singleton.instacne){
			Singleton.instacne = this
		}
		return Singleton.instance
	}

	getInstance(){
		return this.instance
	}
}

const a = new Singleton()

const b = new Singleton()

console.log(a==b) => ture

```

**단점 : TDD의 걸림돌**

- 싱글톤 TDD를 할 때 걸림돌이 된다.
- 단위 테스트를 주로 사용하게 되는데 단위테스는 “서로가 독립적”이어야 하며 테스트를 어떤 순서로도 할 수 있어야한다.
- 싱글톤 패터은 미리 생성된 하나의 인스턴스를 기반으로 구현하는 패턴이므로 각 테스트마다 “독립적인” 인스턴스를 만들기가 어렵다

의존성을 느슨하게 만들어주기 위해 의존성 주입을 사용함 

![Untitled](%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8%E1%84%8B%E1%85%B3%E1%86%AF%20%E1%84%8B%E1%85%B1%E1%84%92%E1%85%A1%E1%86%AB%20CS%20%E1%84%8C%E1%85%A5%E1%86%AB%E1%84%80%E1%85%A9%E1%86%BC%20%E1%84%8C%E1%85%B5%E1%84%89%E1%85%B5%E1%86%A8%20%E1%84%82%E1%85%A9%E1%84%90%E1%85%B3%20-%201%20%E1%84%83%E1%85%B5%E1%84%8C%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%91%E1%85%A2%202e022f2d76534d2fad101ad382873bda/Untitled.png)

### 의존성 주입

- 모듈 간의 결합도가 강해짐 _ DI를 통해 결합도를 느슨하게 해서 해결할 수 있음
- 메인 모듈이 간접적으로 의존성을 주입하는 것이 효과적임 → “디커플링이 된다”

**의존성 주입의 장점**

- 모듈을 쉽게 교체할 수 있는 구조가 되어 테스팅하고 싶고, 마이그레이션하기 편함
- 추상화 레이어를 넣고 이를 기반으로 구현체를 넣어주기 때문에 의존성 방향이 일관된다.

**의존성 주입의 단점**

- 모듈들의 더욱 더 분리됨 → 복잡성 증가, 약간의 런타임 패널티 발생 가능

 ****

**의존성 주입의 원칙**

- 상위 모듈은 하위 모듈에서 어떤한 것도 가져오지 않아야함

## 1.1.2 팩토리 패턴(factory Pattern)

- 객체를 사용하는 코드에서 객체 생성 부분을 떼어내 추상화한 패턴이자 상속 관계에 있는 두 클래스에서 상위 클래스가 중요한 뼈대를 결정하고, 하위 클래스에서 객체 생성에 관한 구체적인 내용을 결정하는 패턴

- 상위 클래스와 하위 클래스가 분리되기 때문에 느슨한 결합을 가진다
- 상위 클래스에서는 인스턴스 생성 방식에 대해 전혀 알 필요가 없기 때문에 더 많은 유연성을 가짐
- 코드 리펙터링 시 한 곳만 고칠 수 있게 되어 유지 보수성 향상

```jsx
enum CoffeeType {
    LATTE,
    ESPRESSO
}

abstract class Coffee {
    protected String name;

    public String getName() {
        return name;
    }
}

class Latte extends Coffee {
    public Latte() {
        name = "latte";
    }
}

class Espresso extends Coffee {
    public Espresso() {
        name = "Espresso";
    }
}

class CoffeeFactory {
    public static Coffee createCoffee(CoffeeType type) {
        switch (type) {
            case LATTE:
                return new Latte();
            case ESPRESSO:
                return new Espresso();
            default:
                throw new IllegalArgumentException("Invalid coffee type: " + type);
        }
    }
}

public class Main {
    public static void main(String[] args) { 
        Coffee coffee = CoffeeFactory.createCoffee(CoffeeType.LATTE); 
        System.out.println(coffee.getName()); // latte
    }
}
```

## 1.1.3 전략 패턴(Strategy Pattern) = 정책 패턴(policy parttern)

- 객체의 행위를 바꾸고 싶은 경우 “직접” 수정하지 않고 전략(캡슐화 알고리즘) 을 컨텍스트 안에서 바꿔주면서 상호 교체가 가능하게 만드는 패턴을 의미함
- ex) A를 구매할 때 네이버페이, 카카오페이 등 다양한 방법으로 결제하듯 전략적으로 수정하는 패턴

```jsx
import java.text.DecimalFormat;
import java.util.ArrayList;
import java.util.List;
interface PaymentStrategy { 
    public void pay(int amount);
} 

class KAKAOCardStrategy implements PaymentStrategy {
    private String name;
    private String cardNumber;
    private String cvv;
    private String dateOfExpiry;
    
    public KAKAOCardStrategy(String nm, String ccNum, String cvv, String expiryDate){
        this.name=nm;
        this.cardNumber=ccNum;
        this.cvv=cvv;
        this.dateOfExpiry=expiryDate;
    }

    @Override
    public void pay(int amount) {
        System.out.println(amount +" paid using KAKAOCard.");
    }
} 

class LUNACardStrategy implements PaymentStrategy {
    private String emailId;
    private String password;
    
    public LUNACardStrategy(String email, String pwd){
        this.emailId=email;
        this.password=pwd;
    }
    
    @Override
    public void pay(int amount) {
        System.out.println(amount + " paid using LUNACard.");
    }
} 

class Item { 
    private String name;
    private int price; 
    public Item(String name, int cost){
        this.name=name;
        this.price=cost;
    }

    public String getName() {
        return name;
    }

    public int getPrice() {
        return price;
    }
} 

class ShoppingCart { 
    List<Item> items;
    
    public ShoppingCart(){
        this.items=new ArrayList<Item>();
    }
    
    public void addItem(Item item){
        this.items.add(item);
    }
    
    public void removeItem(Item item){
        this.items.remove(item);
    }
    
    public int calculateTotal(){
        int sum = 0;
        for(Item item : items){
            sum += item.getPrice();
        }
        return sum;
    }
    
    public void pay(PaymentStrategy paymentMethod){
        int amount = calculateTotal();
        paymentMethod.pay(amount);
    }
}  

public class HelloWorld{
    public static void main(String []args){
        ShoppingCart cart = new ShoppingCart();
        
        Item A = new Item("kundolA",100);
        Item B = new Item("kundolB",300);
        
        cart.addItem(A);
        cart.addItem(B);
        
        // pay by LUNACard
        cart.pay(new LUNACardStrategy("kundol@example.com", "pukubababo"));
        // pay by KAKAOBank
        cart.pay(new KAKAOCardStrategy("Ju hongchul", "123456789", "123", "12/01"));
    }
}
```

## 1.1.4 옵저버 패턴(observer pattern)

- 객체의 상태를 관찰하다가 상태 변화가 있을 때 마다 메서드 등을 통해 옵저버 목록에 있는 옵저버에게 변화를 알려주는 디자인 패턴입니다.
- 주체 : 객체의 상태 변화를 보고 있는 관찰자
- 옵저버 : 이 객체의 상태 변화에 따라 전달되는 메서드 등을 기반으로 “추가 변화 사항”이 생기는 객체
- 대표적인 서비스 : 트위터
- 팔로워 등 응답을 주는데 사용을 많이 하며 MVC 패턴에서도 많이 사용되는 기법임

## 1.1.5 프록시 패턴과 프록시 서버

### 프록시 패턴

- 대상 객체에 접근하기 전 그 접근에 대한 흐름을 가로채 대상 객체 앞단의 인터페이스 역할을 하는 패턴
- 이를 통해 객체의 속성, 변화 등을 보안하며 보안, 테이터 검증, 캐싱, 로깅에 사용된다.

![Untitled](%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8%E1%84%8B%E1%85%B3%E1%86%AF%20%E1%84%8B%E1%85%B1%E1%84%92%E1%85%A1%E1%86%AB%20CS%20%E1%84%8C%E1%85%A5%E1%86%AB%E1%84%80%E1%85%A9%E1%86%BC%20%E1%84%8C%E1%85%B5%E1%84%89%E1%85%B5%E1%86%A8%20%E1%84%82%E1%85%A9%E1%84%90%E1%85%B3%20-%201%20%E1%84%83%E1%85%B5%E1%84%8C%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%91%E1%85%A2%202e022f2d76534d2fad101ad382873bda/Untitled%201.png)

### 프록시 서버

- 서버와 클라이언트 사이에서 클라이언트가 자신을 통해 다른 네트워크 서비스에 간접적으로 접속 할 수 있게 해주는 컴퓨터 시스템이나 응용 프로그램을 의미한다.

**Nginx : 대표적인 프록시 서버** 

- 디동기 이벤트 기반의 구조와 다수의 연결을 효과적으로 처리 가능한 웹 서버이며, 주로 Node.js 서버 앞단의 프록시 서버로 활용된다.
- 이를 통해 익명 사용자가 직접적으로 서버에 접근하는 것을 차단하고 , 간접적으로 한 단계를 더 거치게 함으로 보안을 강화할 수 있다 (버퍼 오버플로우 취약점을 막는데 효과적임 )
- 실제 포트를 숨길 수 잇고 정적자원을 압축하거나, 메인 서버 앞단에서의 로깅을 할 수 잇음

![Untitled](%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8%E1%84%8B%E1%85%B3%E1%86%AF%20%E1%84%8B%E1%85%B1%E1%84%92%E1%85%A1%E1%86%AB%20CS%20%E1%84%8C%E1%85%A5%E1%86%AB%E1%84%80%E1%85%A9%E1%86%BC%20%E1%84%8C%E1%85%B5%E1%84%89%E1%85%B5%E1%86%A8%20%E1%84%82%E1%85%A9%E1%84%90%E1%85%B3%20-%201%20%E1%84%83%E1%85%B5%E1%84%8C%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%91%E1%85%A2%202e022f2d76534d2fad101ad382873bda/Untitled%202.png)

**CloudFlare : 대표적인 프록시 서버 2** 

- 세계적인 분산 서버가 있어 시스템의 컨텐츠를 빠르게 전달할 수 있는  CDN 서비스
    - CDN : Content Delivery Network
    - 사용자가 인터넷에 접속하는 곳과 가까운 곳에서 콘테츠를 캐싱 또는 배포하는 서버 네트워크를 말함
    - 이를 통해 사용자가 웹 서버로 부터 콘텐츠를 다운로드하는 시간을 줄일 수 있음
- 웹 서버 앞단에 두어 DDOS 방어, HTTPS 구축을 위해 사용
- 배포 후 의심스러운 트래픽이 많이 발생하면 먼전 판단해 CAPTCHA등을 기반으로 이를 사전에 막아주는 역할도 함

![Untitled](%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8%E1%84%8B%E1%85%B3%E1%86%AF%20%E1%84%8B%E1%85%B1%E1%84%92%E1%85%A1%E1%86%AB%20CS%20%E1%84%8C%E1%85%A5%E1%86%AB%E1%84%80%E1%85%A9%E1%86%BC%20%E1%84%8C%E1%85%B5%E1%84%89%E1%85%B5%E1%86%A8%20%E1%84%82%E1%85%A9%E1%84%90%E1%85%B3%20-%201%20%E1%84%83%E1%85%B5%E1%84%8C%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%91%E1%85%A2%202e022f2d76534d2fad101ad382873bda/Untitled%203.png)

- DDOS 방어
    - 거대한 네트워크 용량과 캐싱 전략으로 소규모 DDOS공격은 쉽게 막을 수 있으며 이러한 공격에 대한 방화벽 대시보드도 제공함
- HTTPS 구축
    - CloudFlare를 사용하면 별도의 인증서 설치 과정없이 HTTPS 구축 가능

### CORS 와 프론트 엔드 프록시 서버

**CORS(Cross-Origin Resource Sharing)는 서버가 웹 브라우저에서 리소스를 로드할 때 다른 오리진을 통해 로드하지 못하게 하는 HTTP 헤더 기반 메커니즘** 

오리진 : 프로토콜과 호스트이름, 포트의 조합 

[`https://aaa.com](https://aaa.com)/test` 라는 주소에서 [`https://aaa.com:9999`](https://aaa.com:9999) 을 뜻 함 

- 프론트엔드 개발 시 프론트엔드 서버를 만들어서 백엔드 서버와 통신할 때 주로 CORS 에러를 마주침
- 이를 해결하기 위해 프론트엔드에서 프록시 서버를 만들기도함

**예시** 

- 127.0.0.1:3000 으로 테스팅을 하는데 백앤드 서버는 127.0.0.1:12010 이라면 포트 번호가 다르기 때문에 CORS가 난다. 이때 프록시 서버를 둬서 프론트앤드 서버에서 요청되는 오리진을 127.0.0.1:12010으로 바꾸는 것
    - 아래처럼 프론트엔드 서버 앞단에 프록시 서버를 두고 api1 요청은 api1보내고 자연스레 CORS 에러 해결은 물론 다양한 API에러 해결은 물론이며 다양한 API 서버와의 통신도 매끄럽게 할 수 있음

![Untitled](%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8%E1%84%8B%E1%85%B3%E1%86%AF%20%E1%84%8B%E1%85%B1%E1%84%92%E1%85%A1%E1%86%AB%20CS%20%E1%84%8C%E1%85%A5%E1%86%AB%E1%84%80%E1%85%A9%E1%86%BC%20%E1%84%8C%E1%85%B5%E1%84%89%E1%85%B5%E1%86%A8%20%E1%84%82%E1%85%A9%E1%84%90%E1%85%B3%20-%201%20%E1%84%83%E1%85%B5%E1%84%8C%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%91%E1%85%A2%202e022f2d76534d2fad101ad382873bda/Untitled%204.png)

![Untitled](%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8%E1%84%8B%E1%85%B3%E1%86%AF%20%E1%84%8B%E1%85%B1%E1%84%92%E1%85%A1%E1%86%AB%20CS%20%E1%84%8C%E1%85%A5%E1%86%AB%E1%84%80%E1%85%A9%E1%86%BC%20%E1%84%8C%E1%85%B5%E1%84%89%E1%85%B5%E1%86%A8%20%E1%84%82%E1%85%A9%E1%84%90%E1%85%B3%20-%201%20%E1%84%83%E1%85%B5%E1%84%8C%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%91%E1%85%A2%202e022f2d76534d2fad101ad382873bda/Untitled%205.png)

## 1.1.6 이터레이터 패턴

- itreator를 사용하여 collection의 요소들에 접근하는 디자인 패턴
- 순회할 수 있는 여러 가지 자료형의 구조와는 상관없이 이터레이터라는 하나의 인터페이스로 순회가 가능하다.

## 1.1.7 노출 패턴

- Revealing module parttern 은 즉시 실행 함수를 통해 private, public 같은 접근 제어자를 만드는 패턴을 의미함

![Untitled](%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8%E1%84%8B%E1%85%B3%E1%86%AF%20%E1%84%8B%E1%85%B1%E1%84%92%E1%85%A1%E1%86%AB%20CS%20%E1%84%8C%E1%85%A5%E1%86%AB%E1%84%80%E1%85%A9%E1%86%BC%20%E1%84%8C%E1%85%B5%E1%84%89%E1%85%B5%E1%86%A8%20%E1%84%82%E1%85%A9%E1%84%90%E1%85%B3%20-%201%20%E1%84%83%E1%85%B5%E1%84%8C%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%91%E1%85%A2%202e022f2d76534d2fad101ad382873bda/Untitled%206.png)

## 1.1.8 MVC 패턴

- Model, View, Controller 로 이루어진 디자인 패턴
- 구성 요소를 세 가지 역할로 구분하여 개발 프로세스에서 각각의 구성 요소에만 집중해서 개발할 수 있다.

**장점** : 재사용성과 확장성이 용이하다

**단점** :  복잡해질수록 모델과 뷰의 관계가 복잡해진다

![Untitled](%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8%E1%84%8B%E1%85%B3%E1%86%AF%20%E1%84%8B%E1%85%B1%E1%84%92%E1%85%A1%E1%86%AB%20CS%20%E1%84%8C%E1%85%A5%E1%86%AB%E1%84%80%E1%85%A9%E1%86%BC%20%E1%84%8C%E1%85%B5%E1%84%89%E1%85%B5%E1%86%A8%20%E1%84%82%E1%85%A9%E1%84%90%E1%85%B3%20-%201%20%E1%84%83%E1%85%B5%E1%84%8C%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%91%E1%85%A2%202e022f2d76534d2fad101ad382873bda/Untitled%207.png)

### Model

- 어플리케이션의 데이터인 데이터 베이스, 상수, 변수 등을 의미한다.
- 사각형의 모양 박스 안에 글자가 있다면 \
    - 박스 위치 정보, 글자 내용, 글자 위치, 글자 폼멧 등 데이터에 관한 모든 정도를 가지고 있어야한다.
    - 뷰에서 데이터를 생성하거나 수정하면 컨트롤러를 통해 모델을 생성하거나 갱신함

### View

- InputBox, CheckBox, TextArea 등 사용자 인터페이스 요소를 나타냄
- 모델을 기반으로 사용자가 볼 수 있는 화면을 뜻함
- 화면에 대한 정보만 가지고 있고 모델이 가지고 있는 정보를 가지고 있지 않아야함
- 변경이 이러나면 Controller에 전달함

### Controller

- 하나 이상의 모델과 하나 이상의 뷰를 잇는 다리 역할을 하며 이벤트 등 메인 로직을 담당
- 모델과 뷰의 생명주기를 관리하며, 모델이나 뷰의 변경 통지를 받으면 이를 해석해서 각각의 각각의 요소에 해당하는 내용에 대해 알려줌

### 대표적인 예시 _ Spring 프레임워크

- Web MVC 웹 서비스를 구축하는데 편리한 기능을 제공

## 1.1.9 MVP 패턴

- MVC의 C 가 프레젠터(Presenter)로 변경된 패턴을 의미한다
- 뷰와 프레젠트는 일대 일 관계이기 때문에 MVC패턴보다 더 강한 결합을 가지고 있음

![Untitled](%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8%E1%84%8B%E1%85%B3%E1%86%AF%20%E1%84%8B%E1%85%B1%E1%84%92%E1%85%A1%E1%86%AB%20CS%20%E1%84%8C%E1%85%A5%E1%86%AB%E1%84%80%E1%85%A9%E1%86%BC%20%E1%84%8C%E1%85%B5%E1%84%89%E1%85%B5%E1%86%A8%20%E1%84%82%E1%85%A9%E1%84%90%E1%85%B3%20-%201%20%E1%84%83%E1%85%B5%E1%84%8C%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%91%E1%85%A2%202e022f2d76534d2fad101ad382873bda/Untitled%208.png)

## 1.1.10 MVVM 패턴

- MVC의 C가 ViewModel로 변경된 패턴을 의미

![Untitled](%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8%E1%84%8B%E1%85%B3%E1%86%AF%20%E1%84%8B%E1%85%B1%E1%84%92%E1%85%A1%E1%86%AB%20CS%20%E1%84%8C%E1%85%A5%E1%86%AB%E1%84%80%E1%85%A9%E1%86%BC%20%E1%84%8C%E1%85%B5%E1%84%89%E1%85%B5%E1%86%A8%20%E1%84%82%E1%85%A9%E1%84%90%E1%85%B3%20-%201%20%E1%84%83%E1%85%B5%E1%84%8C%E1%85%A1%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%91%E1%85%A2%202e022f2d76534d2fad101ad382873bda/Untitled%209.png)

- ViewModel : View를 추상화한 계층
- MVC와 다르게 커멘드와 데이터 바인딩을 가지는 것이 특징
- 뷰와 뷰모델 사이의 양방햔 데이터 바인딩을 지원하며 UI를 별도의 코드 수정 없이 재사용할 수 있고 단위 테스트하기 쉽다는 장점이 있음

### MVVM 패턴의 대표적인 예  : Vue.js

- Vue.js : 반응형이 특징인 프론트 프레임워크
- Watch, computed등을 통해 쉽게 반응형적인 값을 구축할 수 있음
- 함수를 사용하지 않고 값 대입만으로 변수가 변경되며 양방향 바인딩, html을 토대로 컴포넌트를 구축할 수 있다는 점이 특징, 재사용 가능한 컴포넌트 기반으로 UI를 구축할 수 있음

> 커맨드 
- 여러 요소에 대한 처리를 하나의 액션으로 처리할 수 있음

데이터 바인딩
- 화면에 보이는 데이터와 웹 브라우저의 메모리 데이터 타입을 일치 시키는 기법으로 뷰 모델을 변경하면 뷰가 변경된다.
> 

# 예상 가능 질문

### 옵저버 패턴을 어떤식으로 구현할 수 있나요?

- 프록시 객체를 사용하곤 합니다.
- 프록시 객체를 통해 객체의 속성이나 메서드 변화를 감지하고 이를 미리 설정해놓은 옵저버들에게 전달하는 방식으로 구현이 가능합니다

### 프로시 서버를 설명하고 사용 사례에 대해서 설명해주세요

- 프록시 서버란 클라이언트로 직접적인 접근이 아닌 간접적인 접근을 할 수 있게해주는 서버를 말합니다.
- 주로 서버 앞 단에서 접근에 대한 캐싱, 로깅 등은 담당하게 되며 서버는 직접적인 포트를 숨길 수 있어 보안적으로도 유리합니다. 뿐 아니라 공격자의 DDOS를 방어하는데 효과적이며 Node.js 앞단에 두어 버퍼오버플로우를 방지할 수 있습니다.

### MVC을 설명하고  MVVM와의 차이를 말해주세요

- MVC는 Model, View, Controller로 어플리케이션을 3단계로 구성하는 것을 의미합니다. 그로인해 각각의 프로세스에만 집중할 수 있으며 재사용성 및 유지보수성이 향상된다는 장점이 있으며 단점으로는 복잡해질 수록 view와 model의 관계가 복잡해진다는 단점이 존재합니다. 대표적인 프레임워크는 Spring이 존재합니다. MVVC 모델의 경우 MVC의 C가 ViewModel로 변경된 패턴으로 Model, View, ViewModel의 형태를 가지고 있습니다. 가장 큰 차이점은 커멘드와 데이터 바인딩을 지원하는점이여 코드의 수정없이 UI를 재사용할 수 있는 특징을 가집니다. 이를 통해 재사용성이 증가되고 단위 테스트하기에 더욱 더 적합해집니다.