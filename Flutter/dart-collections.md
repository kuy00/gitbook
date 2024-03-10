# Dart - Collections

## list
```dart
List<int> list = [1,3,4];

print(list); // [1,3,4]

list.add(5);
print(list); // [1,3,4,5]

list.remove(3);
print(list); // [1,4,5]

print(list.length); // 3
```
- var 키워드로 타입을 추론 시켜 선언 가능

## map
```dart
Map<String, int> map = {
    'a': 1,
    'b': 2,
}
print(map['a']); // 1
print(map['c']); // null
```
- var 키워드로 타입을 추론 시켜 선언 가능
- map에 존재 하지 않은 키 조회 시 null 반환

## set
```dart
var test = Set();
Set<String> test = {'a', 'b'};

print(test); // {'a', 'b'}

test.add('a')
print(test); // {'a', 'b'}
```
- var 키워드로 타입을 추론 시켜 선언 가능
- 중복된 요소 추가 불가
- 중복된 요소 추가 시 변화 없음

## spread operator
```dart
List<int> list = [1, 2, 3];
List<int> list2 = [...list, 4];

print(list2); // [1,2,3,4]
```
- ...키워드를 통해 list를 분해하여 새로운 list에 추가

## collection if
```dart
bool flag = true;
List<int> test = [
    1,
    2,
    3,
    if(flag) 5,
];
print(test); // [1,2,3,4,5]
```
- if 구문을 통해 조건에 따라 리스트 내에 요소를 추가할 수 있음

## collection for
```dart
List<int> list = [1, 2, 3];
List<int> list2 = [
    4,
    5,
    for (var i in list) '$i'
]
```
- for 구문을 통해 반복문을 통해 리스트 내에 요소를 추가할 수 있음