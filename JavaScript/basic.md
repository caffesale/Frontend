# 자바스크립트 기본지식 정리

<br>
## 자바스크립트의 자료형과 그 특성은 무엇일까?
  
  + 느슨한 타입의 동적 언어
  + 자바스크립트의 형변환
  + 형 변환
  + ==, ===의 차이
  + undifined와 null의 차이
<br> 
### 느슨한 타입(loosely typed)의 동적 언어

자바스크립트는 변수를 선언할 때 타입을 확정하지 않고 실행시점에 정해진다. 따라서 변수가 어떤 특정한 타입에 한정되지 않고 모든 타입의 값으로 재할당 가능하다.   이런 특징을 통해 느슨한 타입의 동적 언어라고 칭한다.

### 자바스크립트의 형변환

암시적 형변환과 명시적 형변환이 있다. 암시적 형변환은 자바스크립트 엔진이 실행 과정에서 필요에 따라 형변환을 하는 것을 말한다. 단항연산자(+)나 다른 타입 간 +연산(n + "")을 통해 의도적으로 발생시킬 수는 있지만 그렇지 않은 경우 의도하지도 않고 찾기도 어려운 오류를 발생시킨다. 반면 명시적 형변환은 parseInt(), Number() 자바스크립트 내장함수를 통해 형을 변환하는 것을 말한다. 

### == ,===의 차이

==는 값만을 비교하는 비교연산자다. String타입인 "2"와 Number타입인 2도 같은 것으로 간주한다. 반면 ===는 값의 타입까지 일치해야 같은 것으로 판정한다. 엄격한 비교를 위해 ===를 선호하는 것이 낫다. 

### undefined와 null의 차이

undefined는 선언되었지만 따로 값이 부여되지 않은 상태에서 가지고 있는 초기값이다. null은 아무 값도 가지고 있지 않다는 것을 나타낸다. 의도적으로 변수에 null값을 부여하지 않는다면 막 선언한 변수를 참조했을 때 undefined값을 반환한다. 위의 undefined와 null은 ==연산자를 적용하면 true이지만 ===연산자를 적용하면 false이다.

### 느슨한 타입의 동적언어의 문제점과 보완할 수 있는 방법

의도치 않은 동작을 방지하기 위해 명시적 형변환과 ===연산자를 사용한다. 가장 좋은 방법은 TypeScript를 도입한다.

<br>
## 자바스크립트 객체와 불변성이란?

  + 기본형 데이터와 참조형 데이터
  + 얕은 복사와 깊은 복사
  + 불변 객체를 만드는 방법

<br>
### 기본형 데이터와 참조형 데이터

자바스크립트는 7종의 Primative(원시) 데이터 타입과 1종의 Object(객체) 데이터 타입을 지원한다. 전자는 Boolean, Null, Undefined, Number, BigInt, String, Symbol이며 후자는 Object이다. 원시값은 변수공간에 값(value)를 그대로 저장하고 객체는 값이 저장된 메모리 주소를 저장한다. 

### 얕은 복사와 깊은 복사

깊은 복사는 원시 데이터 타입에서 일어난다. 변수 공간에 저장된 값을 그대로 복사해 전달하기 때문에 전달받은 변수에 다른 값이 재할당되더라도 원본 변수의 값에 영향을 주지 않는다. 

예를 들어
```
let num =10;
let copyNum = num;
copyNum = 20;

console.log(num); // 10
console.log(copyNum); // 20
```
이다.

얕은 복사는 객체와 같은 참조형 데이터에서 일어난다. 객체가 할당된 변수는 변수공간에 값이 아니라 데이터가 위치하고 있는 메모리의 주소를 저장하고 있기 때문에 객체에 값을 재할당하면 원본과 복사본 모두의 값에 영향을 준다.

예를 들어 
```
const person = {
  name : "Yi Sun-sin"
}
const copyPerson = person;
person.name = "Kim";

console.log(person.name); // Kim
console.log(copyPerson.name); // Kim
```
이다.

### 불변 객체를 만드는 방법

const 키워드 와 Object.freeze()를 통해 불변 객체를 만들 수 있다. 그러나 둘은 따로 사용했을 때 각자의 특성이 다르다.

    const 키워드는 변수에 객체를 새로 할당할 수는 없으나 객체의 속성은 변경 가능하다.
  
  
예를 들어 
```
let person = {};

person.name = "Kim";

console.log(person); // Kim
```
이다. 반면,

    Object.freeze()는 변수에 객체를 새로 할당할 수 있지만 객체의 속성은 변경 불가능하다.


예를 들어
```
let person = {
  name : "Yi Sun-sin"
};

Object.freeze(person);

person.name = "Kim";

console.log(person); // "Yi Sun-sin"이지만


person = { name : "Kim" }; // 은 가능하다

console.log(person); // "Kim"
```
이다.

따라서 const키워드와 Object.freeze()를 조합하면 변수에 재할당 할 수도, 객체의 속성을 변경할 수도 없는 객체가 만들어진다.
<br>
## 호이스팅과 TDZ는 무엇일까?
<br>
+ 스코프, 호이스팅, TDZ
+ 함수 선언문과 함수 표현식에서 호이스팅 방식의 차이
+ let, const, var, function
+ 실행 컨텍스트와 콜스택
+ 스코프 체인, 변수 은닉화

### 스코프, 호이스팅, TDZ

스코프는 변수에 접근할 수 있는 유효 범위를 뜻한다. 호이스팅은 변수와 함수에서 선언/초기화 부분을 분리한 뒤 선언부만 유효범위의 최상단으로 끌어올리는 것을 의미한다. TDZ는 Temporal Dead Zone의 약자로 초기화 전에 호이스팅된 대상(변수, 클래스등)에 접근하면 동작 방식에 따라 ReferenceError나 Undefined를 반환하는 것을 말한다.

### 함수 선언문과 함수 표현식에서 호이스팅 방식의 차이

함수 선언문은 선언부가 호이스팅된다. 함수 표현식(expression)에서는 호이스팅이 일어나지 않는다.

### let, const, var, function

var로 선언된 변수는 블록스코프가 아니라 전역스코프 혹은 함수스코프로 설정된다. 따라서 지역스코프에서 선언되더라도 블록을 무시하고 모든 스코프에서 접근 가능하다. let과 const는 블록스코프이기 때문에 선언된 블록 안에서만 참조할 수 있다.

호이스팅의 경우 TDZ에서 변수를 참조했을 때 var는 undefined, let과 const는 ReferenceError를 반환한다. 함수에서도 함수 선언문은 정상 작동하지만 호이스팅되지 않는 함수 표현식은 TypeError를 반환한다. 

>변수는 선언 및 초기화시 다음과 같은 과정을 거친다.
>1. 변수를 선언한다.
>2. undefined 값을 할당한다.
>3. 초기화구문에 이르러 초기화 값을 할당한다.

따라서 var로 선언된 변수는 TDZ에서 호출하면 초기화구문에 다다르기 전 2.단계에서 호출되는 것이다. 반면 let과 const로 선언한 변수는 undefined가 할당되지 않고 실제 초기화구분에 도달할 때까지 접근 불가능하다. 엄밀하게 말하자면 let과 const로 변수를 선언해도 호이스팅되는 것은 맞다. 

### 실행 컨텍스트와 콜스택

실행 컨텍스트(Execution Context)는 코드를 실행하기 위해 필요한 환경을 말한다. 실행 컨텍스트의 타입은 전역 실행 컨텍스트(Global Execution Context)와 함수 실행 컨텍스트(Function Execution Context)로 나눠진다.

전역 실행 컨텍스트는 자바스크립트 실행 즉시 전역 객체인 Windows Object를 생성하고 this가 Window 객체를 가리키도록 지정한다. 전역 실행 컨텍스트는 콜스택으로 가장 먼저 push된다. 함수 실행 컨텍스트는 함수가 **호출될 때마다** 함수를 위한 실행 컨텍스트를 생성한다. 

콜스택은 코드가 실행되면서 생성되는 실행 컨텍스트를 저장하는 자료구조이다. 가장 밑바닥에는 전역 실행 컨텍스트가 위치하고 있으며 함수가 호출될 때마다 그 위로 함수 실행 컨텍스트가 추가된다.  

컨텍스트가 추가될 때마다 그 안에 VariableEnvironment, LexicalEnvironment이 구성된다.

VariableEnvironment는 최초 실행시의 스냅샷을 유지한다. 컨텍스트 내의 식별자(변수)들에 대한 정보, 외부 환경정보를 저장해 LexicalEnvironment에 넘겨준다. 따라서 초기치는 LexicalEnvironment와 같다. 다만 ES6에서 차이점이 하나 생기는데 VariableEnvironment는 변수 var만 저장하고 LexicalEnvironment는 함수 선언과 let, const, 바인딩을 저장하게 되었다. 

LexicalEnvironment는 실질적으로 식별자를 확인하기 위한 공간이다. 변수와 해당 변수에 대입된 값이 매핑되어있다. 만일 참조하려는 변수의 값을 내부에서 찾을 수 없으면 outerEnvironmentReference를 통해 호출된 함수가 **선언될 당시의** LexicalEnvironment를 참조한다. 즉, 보다 바깥에 위치한 스코프의 LexicalEnvironment를 확인한다. 참고로 LexicalEnvironment에서 This binding을 통해 this 값도 할당한다. 

### 스코프 체인과 변수 은닉화

스코프 체인이란 위에서 언급한대로 식별자를 찾을 때 자신이 **선언될 당시에** 속한 스코프에서부터 그 외부에 중첩된 함수, 전역객체까지 이어지는 연결고리를 뜻한다. 

변수 은닉화는, 이에 대해 설명하기 전에 클로저에 대해 먼저 소개하고자 한다. 

> 클로저(closure)는 외부 실행 컨텍스트가 종료된 이후에도 외부 변수를 기억하고 이 외부 변수에 접근할 수 있는 함수를 의미한다. 

```
function increaseNum(){
  let num = 0;
	
  return function(){
    return num++;
  }
}

let count = increaseNum();

alert(count()); // 0

```
>
> 자바스크립트에서 함수는 특수한 프로퍼티[[Environment]]를 통해 자신이 선언된 곳을 기억하기 때문에 거의 모든 함수가 클로저가 된다. 다만 new Function을 통해 만든 함수는 전역 렉시컬 환경을 참조하므로 외부변수에 접근할 수 없다.

함수 내에 직접적으로 은닉해야하는 속성값, 변수가 있다면 이 클로저를 활용해 접근을 차단할 수 있다. 함수 내부에 this 키워드와 프로퍼티를 사용해 만드는 대신

```
//함수 내부에 this 키워드와 프로퍼티를 사용해 만드는 대신 변수와 메서드를 만들dj 메서드를 리턴하는 식으로
function Greeting(name){
  let _name  = name;
  return function(){
    console.log(`Hello + ${_name}`);
  }
}
```
<br>
## 실습과제 
<br>
```
let b = 1;

function hi () {
  const a = 1;

  let b = 100;

  b++;

  console.log(a,b);
}

//console.log(a); 전역 스코프에서 함수 스코프를 참조할 수 없으므로(LexicalEnvironment의 outerEnvironmentReference는 단일방향 리스트로 구성되어 있음) ReferenceError가 표시된다 오류가 나지 않게 하려면 변수 b처럼 전역 변수를 따로 선언해주어야 한다.

console.log(b); // 전역 스코프를 참조해 1을 표시한다. 

hi(); // 함수 내부에 변수 b가 선언되어 있으므로 내부 스코프를 참조한다. a=1, b = 100으로 초기화되고 이후 b만 1이 증가하여 101로 표기된다. console.log(a,b)이므로 전체 표기는 1 101이다.

console.log(b); // 전역 스코프를 참조해 1을 표시한다. 

```
