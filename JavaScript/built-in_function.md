# 자바스크립트 내장함수 TIP 정리

## Array함수

**Array.prototype.map()**
    
    배열 내 모든 요소에 callback함수 호출. 결과를 모아 **새로운 배열**을 반환한다. 따라서 메서드 체인에 활용 가능하다.

배열을 반환하기 때문에 메서드 체인에 활용 가능하다. sort()함수의 경우 CompareFunction이 여러번 호출되어 높은 오버헤드가 발생하므로 복잡하면 map()을 사용하라

**Array.prototype.sort()**

    배열 내 요소를 정렬하여 **원배열**을 반환한다.
    
<br>

```javascript
//기본 정렬은 유니코드 포인트를 따른다. 예를들어 sort()를 사용하면 1, 10, 2, 3순으로 정렬된다. 오름차순 정렬을 원하면
// 오름차순
(a,b) => {
  if(a>b) return 1;
  if(a==b) return 0;
  if(a<b) return -1;
}

//(a,b) => a-b; 도 의미는 같다.
```

<br>

<br>

**Array.prototype.foreach()**

    배열 내 모든 요소에 callback함수 호출. 인수는 map함수와 유사하지만 **undefined** 값을 반환한다.
<br>    

**Array.prototype.reduce()**

    배열 내 모든 요소에 리듀서 함수를 실행하여 **하나의 결과값**을 반환한다.
    
 리듀서 함수는 인자 accumulator에 누산값을 축적한다. 초기값은 initial Value를 제공하면 initial Value, 제공하지 않으면 배열의 첫 값이다. 빈 배열에 initial Value를 제공하지 않으면 오류가 발생한다.
<br>

**Array.prototype.toString()**

    배열을 표현하는 문자열을 반환한다.
    
 Object.prototype.toString()의 경우 2~36까지의 기수를 받아 10진수를 다른 진수로 변환 가능하다

<br>

**Array.prototype.filter()**

    주어진 함수의 조건을 통과하는 **새로운 배열**을 반환한다. 

<br>   

**Array.prototype.split()**

    지정한 구분자를 통해 여러 문자열로 나누고 그 문자열들을 담은 **새로운 배열**을 반환한다. 빈 문자열 ''을 제공하면 UTF-16 코드 유닛으로 나눈다. 써로게이트 쌍은 망가질 수 있다. 구분자로는 정규표현식과 문자열을 받는다. 

<br>

**String.prototype.join()**

    주어진 문자열로 배열의 모든 요소를 연결해 **문자열**을 반환한다.
    
 특정 단어로 split()하면 그 단어가 사라진 배열을 반환한다. 그 후 새로운 단어로 join()하면 split()으로 사라진 단어의 자리에 새로운 단어가 들어간 문자열을 반환한다.


---

## String함수
<br>

**String.prototype.charAt()**

    지정된 인덱스의 문자를 반환한다.
<br>  

**String.prototype.charCodeAt()**

    지정된 인덱스의 UTF-16코드 숫자를 반환한다.
    
<br>

**String.prototype.fromCharCode()**

    UTF-16코드 숫자 N개를 받아 문자열을 반환한다.
    
<br>

**Array.prototype.repeat()**

    문자열을 주어진 횟수만큼 반복한다. 정수값이 아니면 나머지는 절삭한다.
    

