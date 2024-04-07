# Flutter - Tree

## widget tree
- 위젯의 계층 구조
- 플러터 전체에서 사용하는 위젯 트리는 1개
- main 함수에서 runApp의 파라미터로 전달한 위젯이 루트 노드
- 자식의 위젯이 빌드가 되면 위젯 트리에서는 자식 노드가 생김

![img](/Images/flutter-widget-tree.png)

## build context
- 위젯 트리에서 현재 위젯의 위치를 알려줌
- 모든 위젯은 BuildContext를 가지고 있음
- 부모의 context에는 부모 위젯의 정보만 알 수 있음

## element tree
- widget tree를 기반으로 실제로 그려질 instance를 생성
- element tree의 노드와 widget tree의 노드는 일대일로 대응
- ComponentElement, RenderObjectElement 객체로 구성
    - ComponentElement : 다른 element를 포함하는 역할을 함
    - RenderObjectElement : 실제 화면에 출력할 정보를 가지고 있음

![img](/Images/flutter-element-tree.png)

## render tree
- element tree를 기반으로 실제 화면을 출력하는 render tree 생성
- element tree에 RenderObjectElement 객체만 참조
- RenderObject 클래스를 상속받은 클래스로 구성됨

![img](/Images/flutter-render-tree.png)