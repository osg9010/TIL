#SOLID
## 좋은 객체 지향 설계의 5가지 원칙

- SRP: 단일 책임 원칙(single responsibility principle)
- OCP: 개방-폐쇄 원칙 (Open/closed principle)
- LSP: 리스코프 치환 원칙 (Liskov substitution principle)
- ISP: 인터페이스 분리 원칙 (Interface segregation principle)
- DIP: 의존관계 역전 원칙 (Dependency inversion principle)


# SRP (단일 책임 원칙(single responsibility principle))

- 한 클래스는 하나의 책임만 가져야 한다.
- 하나의 책임
  - 클수도 있고 작을수 있다.
  - 문맥과 상황에 따라 다르다

- 중요한 기준은 변경이다. 변경이 있을 때 파급 효과가 적으면 SRP를 잘 따른것


# OCP (개방-폐쇄 원칙 (Open/closed principle))

- 가장 중요한 원칙
- 확장에는 열려 있고, 변경에는 닫혀 있어야 한다.
- 다형성
- 역할과 구현의 분리
- 인터페이스 - 구체클래스 
 
#LSP (리스코프 치환 원칙 (Liskov substitution principle))

- 프로그램의 정확성을 깨뜨리지 않으면서 하위 타입의 인스턴스로 교체 가능해야한다.
- 하위 클래스에서는 인터페이스 규약을 다 지켜야 한다는것, 다형성을 지원하기 위한 원칙
- 인터페이스를 구현한 구현체를 믿고 사용하려면 이 원칙이 필요함
- 예) 자동차 엑셀은 앞으로 가는 기능, 이를 뒤로 가게 만들면 LSP 위반

#ISP(인터페이스 분리 원칙 (Interface segregation principle))

- 하나의 거대한 인터페이스보다, 여러 개로 세분화한 인터페이스가 더 좋다.
- 인터페이스가 명확해지고, 대체 가능성이 높아진다.
- 예) 자동차 인터페이스 -> 운전 인터페이스, 정비 인터페이스

# DIP (의존관계 역전 원칙 (Dependency inversion principle))

- 개발자는 "추상화에 의존해야지, 구체화에 의존하면 안된다."
- 쉽게 말해 구현 클래스에 의존하지 말고, 인터페이스에 의존하라는 뜻
- 역할에 의존해야지 구현에 의존하면 안됌
- 인터페이스에 의존해야 유연하게 변경 가능하다. 구현체에 의존하면  변경이 어려워짐.