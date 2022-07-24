# ECMAScript란?

> ECMA스크립트(ECMAScript)란 Ecma International이 ECMA-262 기술 규격에 따라 정의하고 있는 표준화된 스크립트 프로그래밍 언어를 말한다. 자바스크립트를 표준화하기 위해 만들어졌다.
    
[officialPage](https://www.ecma-international.org/publications-and-standards/standards/ecma-262/)
   


## ES5와 ES6의 차이점

+ let 키워드(블록 스코프)의 도입
+ 템플릿 리터럴
+ 화살표 함수 도입
+ promise 객체 도입
+ iterator, generator 추가

<br>

### let 키워드(블록 스코프)의 도입

이전까지 함수를 초기화하기 위한 var키워드는 선언 위치에 따라 함수, 전역스코프에 속했다. 따라서 블록을 무시하고 호이스팅이 일어났으며 사용자가 실수로 같은 이름의 변수를 재할당했을 때 값을 덮어쓰는 문제가 있었다. 
ES6부터는 let 키워드의 도입으로 블록 스코프 내에서 변수를 다룰 수 있게 되어 재할당에 대한 우려가 사라졌다.


### 템플릿 리터럴

여러번 ''와 단항연산자 +를 사용하지 않고도 간단하게 백틱(``)을 이용해 문자열을 담고 플레이스 홀더${}내에 변수를 표현할 수 있게 되었다.


### 화살표 함수의 도입

자체적으로 this값을 가지지 않는 화살표 함수가 도입되었다. 자체적인 this값을 가지지 않으므로 화살표 함수에서 this를 사용하면 외부 렉시컬 환경을 참조한다. 즉 화살표 함수가 객체의 메서드라면 화살표 함수의 this는 언제나 메서드가 선언된 객체 자신에 해당한다.


### promise 객체 도입

코드가 비동기적(async)인 동작을 요구할 때 ES5에서는 콜백함수를 사용해야만 했다. 이런 환경은 콜백 지옥을 만들어내 코드의 가독성을 떨어뜨리고 유지관리를 힘들게 만들었다. ES6부터는 비동기적 처리에서 promis 객체를 활용할 수 있다. 
promise객체가 반환되면 .then 키워드를 통해 쉽게 반환된 promise객체의 데이터에 접근할 수 있다. 이후 async 함수, await으로도 이어지는 내용이며 최근에는 async함수 없이 await을 사용할 수 있는 기능도 추가되었다.

### iterator, generator추가

어떤 객체에서 Symbol.iterator를 호출할 수 있다면 그것은 반복 가능한(iterable) 객체이다. 반복 가능한 객체는 객체 안의 값을 순환하는 for of문을 사용할 수 있다.

1. for of문이 시작되면 내부적으로 Symbol.iterator를 호출한다. Symbol.iterator는 반복 가능한 객체를 반환한다.
2. for of문은 반환된 반복 가능한 객체만을 대상으로 동작한다.
3. 반복마다 next함수를 호출한다. next는 {done: ... , value: ...}객체를 반환하며 done:true가 되면 반복을 종료한다.

generator는 일반 함수와 달리 여러 개의 값을 반환하는 함수다. 

1. generator함수를 호출하면 본문이 실행되지 않고 generator 객체가 반환된다.
2. next함수를 만나면 가까운 yield 값을 반환한다.
3. done : true 이면 동작을 마친다.

수동으로 generator를 불러줄 수 있지만 generator 역시 반복 가능하다. for of문을 통해 값을 출력하거나 전개문법([...generator])를 사용하여 배열에 담아줄 수 있다.
