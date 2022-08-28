# Server Side State and Client Side State

리액트에서는 Server Side State에 대해 어떻게 다루어야 할 지 규정하고 있지 않다. redux에서는 Data를 서버와 주고 받는 로직을 작성하는 방법에 대해 일반적인 패턴을 소개하고 있으며 toolkit의 createAsyncThunk를 통해 그 패턴을 추상화한 API를 제공한다. 
이는 Server Side State를 caching하기 위한 장소로 redux store를 사용하는 것이라고 볼 수 있다. 그러나 일반적인 패턴에서 Server Side State는 Client Side State와는 상당히 다른 특성과 목적을 가진다.

## Server Side State의 특징
1. 개발자 자신이 소유하거나 관리하고 있지 않은 원격저장소에 위치한다.
2. 데이터를 주고 받거나 업데이트하는데 비동기 로직을 필요로 한다. 
3. 사용권을 공유하기 때문에 개발자가 모르는 사이에 다른 사람에 의해 state가 변경 될 수 있다.
4. 그렇기 때문에 주의하지 않으면 현재 표시되고 있는 데이터가 갱신되기 이전의 낡은 것일 수 있다.

## Server Side State관리에서 고려해야 할 점
1. 데이터 캐시
2. 동일한 데이터에 대한 중복 요청을 제거 
3. 데이터가 '낡은' 시점 파악
4. 같은 맥락으로, 업데이트된 데이터 반영 ...등등


## Server Side State를 관리하는 새로운 방법
RTK query나 react-query의 소개 페이지에서는 Server Side State를 관리하기 위한 목적으로 만들어진 라이브러리를 따로 사용할 것을 권장한다. 
예를 들어 기존 Client Side State관리 툴인 redux와 RTK query를 함께 사용하거나, react-query + Recoil등의 조합으로 성격이 다른 두 state를 따로 관리할 수 있는 것이다. 
몇몇 특성이 다르기는 하지만, RTK query화 react-query는 공통적으로 개발자가 관리해야 할 Server Side State관련 코드를 간소화하고 표준화하는데 도움을 준다.
