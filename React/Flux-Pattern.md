# Flux

## 데이터 흐름
- 단방향으로 데이터 핸들링
- 유저 액션을 통해 Action을 생성
- 생성된 Action은 Dispatcher에 전달
- Dispatcher에서 Store에 접근하여 데이터 변경

![This is an image](https://haruair.github.io/flux/img/flux-simple-f8-diagram-with-client-action-1300w.png)

## Action
- Action Creator
- 유저액션을 통해 발생한 Action Type, Payload를 담아 놓는 객체
```javascript
const ADD_TODO = 'ADD_TODO';

export const addTodo = (payload) => {
  return {
    type: ADD_TODO,
    payload,
  };
};
```

## Dispatcher
- Action 객체가 전달이 됨
- 전달된 Action 객체를 확인하여, 등록된 콜백을 실행하여 Stroe에 데이터를 전달

## Store
- 데이터, 상태 저장소
- 상태가 변경되면 View에 변경된 데이터를 전달

# Redux

## Store
- 애플리케이션 상태 관리
- getState: Store에 있는 상태
- dispatch: Store에 등록한 Reducer에 액션 객체를 전달
- subscribe: Store 상태 변경을 감지
```javascript
import { createStore } from 'redux';

const store = createStore(reducer);
export default store;
```

## Reducer
- 현재 상태, 액션 객체를 받아서 새로운 상태로 반환
- Reducer가 Action의 Type을 확인하여 Store의 상태 업데이트
- dispatch 함수를 통해서 Action 객체를 Reducer에 전달
```javascript
const todo = (state, action) => {
  const { type, payload } = action;

  switch (type) {
    case ADD:
      return {
        ...state,
        todos: state.todos.concat(
          {
            id: (state.todos.length + 1),
            ...payload,
          }
        ),
      };
      return state;
  }
}
export default todo;
```

## Hooks
- useSelector: Store의 데이터를 조회
- useDispatch: Action 객체를 Reducer에 전달

## Ducks Pattern

### Module
- Action Type, Action Creator, Reducer 하나의 모듈로 관리
- Reducer은 Export Default 처리
- Action Creator는 Export 처리
- Action Type은 reducer/ACTION_TYPE 으로 정의
```javascript
// Action Types
const ADD = 'todo/ADD';

// Action Creators
export const add = (payload) => {
  return { type: ADD, payload };
};

// Reducer
const reducer = (state = {}, action) => {
  const { type, payload } = action;

  switch (type) {
    case ADD:
      return {
        ...state,
        todos: state.todos.concat(
          {
            id: (state.todos.length + 1),
            ...payload,
          }
        ),
      };
    default:
      return state;
  }
}
export default reducer;
```

# 구현
- [Github Repository - Flux Pattern](https://github.com/kuy00/react-flux-pattern)
- [Github Repository - Redux Ducks Pattern](https://github.com/kuy00/react-flux-pattern/tree/redux)