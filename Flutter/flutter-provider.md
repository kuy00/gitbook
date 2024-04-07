# Flutter - Provider

## state
- Ephemeral State : 현재 위젯만 필요한 state
- App State : 여러 위젯들이 접근 가능한 state

## state 관리
- 루트 노드에서 관리하는 state가 존재
- 최하위 노드에서 이 state가 필요한 경우 생성자로 state를 최화위 노드까지 전달 해야함
- 편하게 부모의 state에 접근하기 위해 provider 사용

## provider
- ChangeNotifier : state를 담을 클래스
- ChangeNotifierProvider : 자식 위젯에 state를 전달해줄 위젯
- Consumer : 
    - ChangeNotifier 클래스에서 notifyListeners 함수 호출 시 실행됨
    - 자식 위젯 rebuild
- Provider.of : 자식 위젯에서 Provider가 제공한 state 접근
- Selector : 지정한 조건이 만족할 경우 자식 위젯 rebuild
- context.watch<T> : 값의 변화를 감지하여 위젯 rebuild
- context.read<T> : 변경된 값만 가지고 옴 