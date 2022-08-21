# nomalizing State

``` javascript

//지금까지 사용해온 redux store의 initialValue는 대략 이런 형태였다.

initialValue = {
  [
    {
      id : "user1",
      nickname: "flog",
      introduce: "잘 부탁드립니다!"
    },
    {
      id : "user2",
      nickname: "raven",
      introduce: "hello!"
    }
  ]
}

// 이렇게 활용하더라도 문제는 없으나, 리덕스에서는 상태를 정규화할 것을 권장한다.
// 정규화(nomalization)된 state란 entity와 그 키가 되는 id값을 따로 저장하고, 배열 형태로 저장된 id를 통해 entity에 접근할 수 있는 자료형태를 말한다.
// 개인적인 판단으로는 일종의 의사적인 해시테이블을 만드는 것으로 보인다.

initialValue = {
  ids: ["user1", "user2"],
  entities: {
    "user1": {
      id: "user1",
      nickname: "flog",
      introduce: "잘 부탁드립니다!"
    },
    "user2": {
      id : "user2",
      nickname: "raven",
      introduce: "hello!"
    },
    // ... ...
  }
}

```

## createEntityAdapter

위에서 예시로 든 데이터는 redux-toolkit의 api인 createEntityAdapter에서 제공하는 state형태를 모방했다.
createEntityAdapter는 정규화된 state형태를 제공할 뿐만 아니라 CRUD기능과 관련된 리듀서 함수들을 처음부터 가지고 있다.
다만, createEntityAdapter를 활용할 경우 Adapter에서 제공하는 리듀서 이외의 함수를 활용해 값을 변경할 때 새로 변경된 데이터는 자동으로 정규화되지 않는다. 
