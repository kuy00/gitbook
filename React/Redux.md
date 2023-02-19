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
- [Github Repository - Redux Ducks Pattern](https://github.com/kuy00/react-flux-pattern/tree/redux)