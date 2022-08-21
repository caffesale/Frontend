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
> 1. action type명명
> 2. action creater 작성
> 3. slice reducer 작성
> 4. 필요하다면 middleware에 해당하는 action type, action creater 추가 작성
> 5. middleware작성


```javascript

//코드로 하면 다음과 같다.

// Actions

const LOAD = 'todos/todolisted'
const ADD = 'todos/todoAdded';
const DELETE = 'todos/todoDeleted';
const EDIT = 'todos/todoEdited';

const initialState = {
    list: [
        {
            id: 1,
            title: "리액트 공부하기",
            body: "리액트 기초를 공부해봅시다.",
            isDone: false,
        },
        {
            id: 2,
            title: "리액트 공부하기",
            body: "리액트 기초를 공부해봅시다.",
            isDone: false,
        },
    ]
};

// action creater
export function todolist(todo_list) {
    return {type:LOAD, todo_list};
}

export function addTodo(task) {
    return {type: ADD, task };
}

export function removeTodo(task) {
    return {type: DELETE, task}
}

export function editTodo(id) {
    return {type: EDIT, id}
}

//thunk function


// reducers
export default function todosReducer(state = initialState, action = {}) {
    switch (action.type) {
        case LOAD: {
            console.log(action)
            return { list: action.datalist}
        }


        case ADD: {
            const added_list = [...state.list, action.task]
            console.log(action);

            return { list: added_list };
        }

        case DELETE: {
            const removed_list = state.list.filter((value) => {
                return value.id !== action.task;
            });
            return { list : removed_list};
        }

        case EDIT: {
            const edited_list = state.list.map((value) => {
                if(value.id === action.id){
                    return {...value, isDone:!value.isDone}
                }
                else{
                    return {...value}
                }
            });
            return { list: edited_list};
        }

        default:
            return state;
    }
}

```

createSlice를 사용할 경우 이것 역시 다음과 같이 축약 가능하다.

```javascript

import { createSlice } from '@reduxjs/toolkit'

const initialState = {
    list: [
        {
            id: 1,
            title: "리액트 공부하기",
            body: "리액트 기초를 공부해봅시다.",
            isDone: false,
        },
        {
            id: 2,
            title: "리액트 공부하기",
            body: "리액트 기초를 공부해봅시다.",
            isDone: false,
        },
    ]
};

const todosSlice = createSlice({
  name: 'todos',
  initialState,
  reducers: {
    addTodo(state, action) {
      // ✅ This "mutating" code is okay inside of createSlice!
      state.push(action.payload)
    },
    editTodo(state, action) {
      const todo = state.find(todo => todo.id === action.payload)
      todo.completed = !todo.completed
    },
    // ......
    }
  }
})

export const { addTodo, editTodo } = todosSlice.actions

export default todosSlice.reducer
```

createSlice Api는 
<br>
1. 내부에서 state의 변화를 허용한다. (immer를 통해 불변성을 유지하기 때문에)
2. 기본적으로 현재 state를 자동반환한다. 
3. reducer 객체를 안에서 reducer 함수를 만들 수 있다.
4. action creater를 자동생성한다. ('name'/'reducername' ex:'todos/addTodo')
5. 기존대로 불변성을 유지하기 위한 spread문법도 허용한다.


## Thunk function

기존에는 
1. 해당하는 것이 없다면 action type, action creater를 작성한다. 
2. Thunk function을 작성한다.
3. 기존 컴포넌트에서 이벤트가 발생했을 때 reducer function이 아닌 thunk function에게 dispatch 하도록 수정한다.
4. thunk function에서 비동기 작업 후 다시 reducer에게 dispatch한다.

그러나 툴킷에서는 createAsyncThunk와 extrareducer를 통해 처리가 좀 달라진다.

```javascript
import { createSlice, createAsyncThunk } from '@reduxjs/toolkit'

// omit imports and state

export const fetchTodos = createAsyncThunk('todos/fetchTodos', async () => {
  const response = await client.get('/fakeApi/todos')
  return response.todos
})

const todosSlice = createSlice({
  name: 'todos',
  initialState,
  reducers: {
    // omit reducer cases
  },
  extraReducers: builder => {
    builder
      .addCase(fetchTodos.pending, (state, action) => {
        state.status = 'loading'
      })
      .addCase(fetchTodos.fulfilled, (state, action) => {
        const newEntities = {}
        action.payload.forEach(todo => {
          newEntities[todo.id] = todo
        })
        state.entities = newEntities
        state.status = 'idle'
      })
  }
})

// omit exports
```

+ createAsyncThunk는 문자열과 콜백함수를 인자로 받는다. 문자열은 actionType을 생성하는데 사용하고 콜백함수는 비동기처리를 한다.
+ createSlice는 extraReducers를 통해 다른 액션 타입을 하나의 리듀서에 추가할 수 있다.

 즉, 비동기처리를 위한 thunk function으로 dispatch -> 다시 thunk function 내부에서 reducer로 dispatch에서
 createAsyncThunk로 비동기처리 -> pending, fulfilled, rejected에 따라 extraReducers를 덧붙여 처리로 흐름이 간략화되었다.




