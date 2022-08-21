# useInput

```javascript

const useInput = (initialValue = null) => {
    const [state, setState] = useState(initialValue);    
    
    const onChange = (e) => {setState(event.target.value)}
    
    return [state, onChange];
}

// setState는 최초 initialValue로 설정되어 있는 state값을 바꾸기 위해 필요하지만 우리가 그 동작을 알아야 할 필요는 없다.
// useInput 커스텀 훅은 내부에서 setState로 state 값을 변경하는 로직을 처리하고 state와 onChange함수만을 반환해서 보다 편하게 이용할 수 있도록 만들어준다.


// ... ...
const name = useInput(initialValue);


<input type="text" {...name} />
// 또는
<input type="text" value={name.state} onChange={name.onChange} />

// 의문점 스프레드 문법으로 적용했을 때 코드는 짧아지지만 성능상의 차이점은 없을까? 
```
