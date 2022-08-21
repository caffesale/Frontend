# useRef()의 기능과 용도

> useRef(initialValue)는 .current initialValue로 초기화된 .current **객체**를 반환한다. 반환된 객체는 컴포넌트의 생명주기동안 유지된다. .current property에 담기는 값은 변형 가능하다.


일반적으로 DOM에 직접 접근하기 위해 useRef를 사용하지만 반환하는 값이 평범한 자바스크립트 객체이기 때문에 보다 다양한 용도로 활용할 수 있다. 예를 들어 useState와 달리 값이 변화할 때 알리는 기능이 없기 때문에 .current 객체의 값을 변환시킨 것 만으로는 리렌더링이 진행되지 않는다. 
또한, 매번 렌더링이 될 때마다 **같은** 객체를 제공한다.

이는 react와 다른 라이브러리를 병용하는 프로젝트에서 state로 관리하기 까다로운 값을 가볍게 다룰 수 있게 도와준다. 클래스 구현체와 비슷하게 단순히 값을 담는 상자같은 용도로도 활용할 수 있는 것이다

# useState로 한번에 여러 input 값을 받아오기

```javascript
// input 값을 받아올 때 useState를 여러번 이용하는 수고를 줄이려면 두 가지 방법이 있다.
const [value, setValue] = useState({
    id: "",
    password: "",
});

const onChangeHandler = (e) => {
    setValue((prev) => ({...prev, [e.target.name]:e.target.value}))
}

// 이 때 모든 input태그의 onChange 함수에는 같은 onChangeHandler를 적용해준다.
```
