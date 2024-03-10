# Flutter - Widget

## widget
- UI를 구성하는 기본 단위
- 종류
    - Stateless Widget : 상태가 없는 정적인 위젯
    - Stateful Widget : 상태에 따라 동적으로 변하는 위젯

## widget 생명 주기
- Stateless Widget은 최초 한 번 생성 후 갱신할 수 없으므로 생명주기가 없음
- Stateful Widget 생명주기
    - createState() 함수 호출, 위젯의 상태 생성
    - 위젯 마운트
    - initState() 함수 호출, 위젯 초기화 시 최초 한 번 실행
    - didChangeDependencies() 함수 호출, 위젯이 의존하는 데이터 객체 호출될 때 마다 호훌됨
    - 이 때 위젯이 dirty 상태가 되어 다시 빌드 후 clean 상태가 됨
    - setState 메소드 호출 시 위젯은 dirty 상태가 됨
    - 부모 위젯에서 자식 위젯을 다시 빌드하도록 요청 시 didUpdateWidget() 함수를 통해 위젯은 dirty 상태가 됨
    - dirty 상태가 된 위젯은 다시 build 후 clean 상태로 돌아옴
    - 위젯이 더 이상 사용되지 않을 경우 dispose 됨

![img](/Images/flutter-widget-life-cycle.png)
