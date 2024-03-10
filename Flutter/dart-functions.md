# Dart - Functions

## 선언
```dart
test(a, b) {
    return a + b;
}

String test2(String a, String b) {
    return a + b;
}

void test3(){
    print('call test3 function');
}

var test4 = (String a) {
    print(a);
}

print(test(1, 2)); // 3
print(test('te', 'st')); // test
print(test2('te', 'st')); // test
test3(); // call test3 function
test4('test4'); // test4
```

## Fat Arrow
```dart
String test(String name) => 'test $name';
print(test('aa')); // test aa
```
- {} 중괄호 삭제 하고 함수 정의 가능

## Named Parameter
```dart
String test({
    String name = 'kuy',
    int age = 25,
}) {
    return 'name : $name, age : $age';
}

String test2({
    required String name,
    required String age,
}) {
    return 'name : $name, age : $age';
}

print(test(name: 'kuy', 25)); // name : kuy, age : 25
print(test2(name: 'kuy', 25)); // name : kuy, age : 25
```
- 매개변수 명을 지정하여 호출 시 함수에서 파라미터를 중괄호로 묶어야함
- null safety로 인해 파라미터는 null이며 안됨
- default 값 지정 또는 required 옵션을 지정해야함

## Optional Positional Parameters
```dart
void test (int a, int b, [int? c]) {
    print('a = $a, b = $b, c = $c');
}

void test2 (int a, int b, [int c = 3]) {
    print('a = $a, b = $b, c = $c');
}

test(1, 2); // a = 1, b = 2, c = null
test(1, 2); // a = 1, b = 2, c = 3
```
- [] 감싸진 파라미터를 optional positional parameter라고 함
- 기본값을 지정 안하면 null이므로 파라미터가 nullable해야함
