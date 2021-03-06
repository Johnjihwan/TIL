## POJO 란 무엇인가
정의
> Plain Old Java Object 의 약자로 직역을 하자면 평범한 구식 자바 오브젝트이다.  
> 무거운 EJB와 반대로 경량의 자바 객체를 의미한다.

여기서 말하는 EJB란  
Enterprise JavaBean의 약자로 자바 기술 중 하나이다.  

좋은 취지로 나온 기술이지만..  
EJB의 혜택을 얻기 위해서는 기능이 필요하지도 않은 WAS를 구입해야 했고, 고급 IDE 도움 없이는 복잡한 설정에 허우적 대야 했다.

그래서 객체지향 원리에 따라 만들어진 자바 언어의 기본에 충실하게 비지니스 로직을 구현하는 일명 `POJO` 방식으로 돌아와야 한다는 목소리가 높아졌다. (요즘 Jquery가 많이 무거워져 순수 자바스크립트인 바닐라.js로 돌아가는것과 같은 양상이다.)

### POJO 의 특징
POJO는 종속되지 않는 자바 객체를 통칭한다.  

EJB같은 경우에는 `implements, extends`를 사용하는 코드들이 많다.  
그럴 경우에 빈 하나를 만들기 위해 다양한 부모클래스를 참조해야하고, 그러면 클래스간 의존도가 높아져, 나중에는 뭐가 어디서 상속되며 무엇이 있는지 헷갈리기 시작한다.

그래서 POJO는 이러한 복잡한 것은 버리고, 간단한 자바 객체만을 가지고 일을 처리하자는 철학을 가지고 있다.

현재 POJO는 자바빈(Java Bean)으로 사용되고 있다. JavaBean은 기본 생성자와 멤버 필드에 접근 할 수 있는 `getter/setter` 메서드를 가진 단순 자바 오브젝트이다.  

POJO를 이용한 디자인이 널리 쓰임에 따라 POJO 기반의 프레임워크들이 탄생하게 되었는데 그 중에서도 가장 대표적인 것이 스프링이다.

### POJO 하면 가장 대표적으로 들을 수 있는 단어

1. IoC/DI
    - 스프링의 가장 기본이 되는 기술이자 스프링 핵심 개발원칙이다.

2. AOP
    - 핵심 관심사를 분리하여 프로그램의 모듈화를 향상시키는 프로그래밍 스타일이다.

3. PSA
    - 인터페이스가 다른 다양한 구현을 같은 방식으로 사용하도록 중간에 인터페이스 어댑터 역할을 해주는 레이어를 추가하는 방법이다.


