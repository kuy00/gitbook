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

# 구현
- [Github Repository - Flux Pattern](https://github.com/kuy00/react-flux-pattern)