# redux와 toolkit의 차이점

공식문서에서 정리 [Modern Redux with Redux Toolkit](https://ko.redux.js.org/tutorials/fundamentals/part-8-modern-redux#using-configurestore)

## toolkit package

다음의 package들은 @reduxjs/toolkit에 포함되어있다.

+ redux
+ redux-thunk
+ reselect


## store 만들기

일반적인 redux의 store 작성절차
<br>
> 1. reducer를 모아 root reducer작성
> 2. root reducer를 store에 import
> 3. thunkmiddleware import
> 4. Devtool과 middleware를 포함한 store enhancer 작성 
> 5. createStore
> 6. provider로 전역에 store import

```javascript

//코드로 하면 다음과 같다.

// rootReducer.js

import { combineReducers } from 'redux'

import todosReducer from './features/todos/todosSlice'
import filtersReducer from './features/filters/filtersSlice'

const rootReducer = combineReducers({
  todos: todosReducer,
  filters: filtersReducer
})

export default rootReducer

// store.js

import { createStore, applyMiddleware } from 'redux'
import thunkMiddleware from 'redux-thunk'
import { composeWithDevTools } from 'redux-devtools-extension'
import rootReducer from './reducer'

const composedEnhancer = composeWithDevTools(applyMiddleware(thunkMiddleware))

const store = createStore(rootReducer, composedEnhancer)
export default store

```

그러나 현재 createStore는 권장되지 않을 뿐더러 configureStore를 이용하면 좀 더 간단하게 작성할 수 있다.

```javascript
import { configureStore } from '@reduxjs/toolkit'

import todosReducer from './features/todos/todosSlice'
import filtersReducer from './features/filters/filtersSlice'

const store = configureStore({
  reducer: {
    // Define a top-level state field named `todos`, handled by `todosReducer`
    todos: todosReducer,
    filters: filtersReducer
  }
})

export default store
```

configureStore는
<br>
1. 자동으로 thunk middleware 추가한다.
2. 자동으로 데이터 불변성을 감시하는 middleware추가한다. (createSlice내부에서는 괜찮다)
3. 자동으로 Redux DevTools Extension과 연결한다.
4. reducer객체에 담긴 reducer들로 root reducer를 만든다.
5. root reducer를 사용하여 store를 만든다.


## Slice 만들기 


일반적인 slice 작성절차
<br>
> 1. action type명명, action creater 작성
> 2. root reducer를 store에 import
> 3. thunkmiddleware import
> 4. Devtool과 middleware를 포함한 store enhancer 작성 
> 5. createStore
> 6. provider로 전역에 store import
