# Dart - Asynchronous

## future
- 비동기 작업의 결과
- 완료, 미완료 두 가지 상태를 가짐

### 예제
```dart
// 코드
Future<int> futureTest() {
  return Future<int>.delayed(Duration(seconds: 3), () => 100);
}

void main() {
  print('start');

  Future<int> future = futureTest();

  future.then((val) => print('val : $val'))
    .catchError((error) => print('error : $error'));

  print('end');
}

// 출력
start
end
val : 100
```
- futureTest 함수 실행 후 3초 뒤에 Future<int>가 반환
- then 내부의 함수에서 Future<int>의 값을 핸들링
- Future 내부에서 Exception 발생 시 catchError로 Exception이 전달됨

## async / await 
```dart
// 코드
Future<int> futureTest() {
  return Future<int>.delayed(Duration(seconds: 3), () => 100);
}

Future<int> futureTestAsync() async {
  int a = await futureTest();
  return a;
}

void main() async {
  print('start');

  int test = await futureTestAsync();

  print(test);

  print('end');
}

// 출력 
start
100
end
```
- async : 비동기 함수 정의
- await : 해당 동작을 완료 후 다음 구문 실행
- Future 메소드를 await 할 경우 `Future<T>`를 반환 하지 않고 `T`가 반환됨
