# Class 상속

Class는 ES6에 등장한 문법이면서 클래스 기반 객체지향 프로그래밍에 익숙한 프로그래머가 constructor function대신 사용할 수 있는 문법이다. 그러나 Class 키워드는 다음과 같은 차이점 때문에 단순한 syntatic sugar라고 할 수 없다.

* 클래스는 new키워드 없이 호출 불가
* extends super키워드 제공
* 호이스팅이 발생하지 않는 것처럼 동작한다
* 내부에 strict mode가 자동으로 적용된다
* 내부 constructor, 프로토타입 메서드, 정적 메서드의 [[Enumerable]]값이 false다

## new 키워드

ES5까지의 함수는 생성자 함수와 일반 함수의 구별이 없었다. 즉 선언문으로 선언한 함수는 내부 슬롯[[constructor]]의 값이 true이기 때문에 일반 함수로 사용하기 위해 선언했더라도 new 키워드로 불러내는 것이 가능했으며 그 역도 성립했다. 그러나 이는 컨벤션으로 나누더라도 개발자가 실수할 가능성을 배제할 수 없다. 이런 상황해서 class 키워드에 부여된 성질은 class가 일반 함수처럼 호출되는 것을 막아 개발자의 실수를 방지할 수 있게 디자인되었다.

## super

상위 Class를 상속하는 하위클래스에서는 반드시 super를 호출해야 한다. 이것은 내부적으로 하위클래스의 constructor가 상위클래스의 constructor에 의존하기 때문이다. 그러나 new키워드로 하위 클래스가 새로운 인스턴스를 생성했을 때 new.target은 새 인스턴스이다.

## extends

extends는 String, Number, Array같은 표준 빌트인 객체에서도 확장 가능하다. 즉 Array 생성자 함수를 상속받아 확장한 클래스의 인스턴스는 Array.prototype의 모든 메서드를 사용할 수 있다.


