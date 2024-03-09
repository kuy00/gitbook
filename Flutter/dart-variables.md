#  Dart 문법 - Variables

## var
```dart
var test = 123; // test typeof int
test = 456; // pass
test = 'test'; // fail
```
- 초기값의 타입을 추론
- 변수 선언 후 초기값의 타입 외에 다른 타입의 값으로 변경 불가

## dynamic
```dart
dyanmic test = 123; // test typeof int
test = 456; // pass
test = 'test'; // pass
```
- 할달할 값으로 타입이 동적으로 바뀜
- var과 다르게 초기값의 타입 상관 없이 타입 변경 가능

## final
```dart
final test = 123;
test = 456; // fail
test = 'test'; // fail
```
- 변수의 값 변경 불가
- 상수, 변수 모두 대입 가능
- 런타임 시점에 정해지는 값 대입 가능

## const
```dart
const test = 123;
test = 456; // fail
test = 'test'; // fail
```
- 변수의 값 변경 불가
- 컴파일 시점에 고정된 값으로만 대입 가능
- 런타임 시점에 정해지는 값 대입 불가능

## late
```dart
late final test;
test = 123;
```
- 변수 초기화 지연
- nullable 변수와 구부을 하기 위해 사용

## num
```dart
num a = 123;
num b = 1.23;

print(a); // 123
print(b); // 1.23

b = a;
print(b); // 123
```
- int, double type 상위의 타입
- num 타입을 통해 int, double의 형변환 가능

## type casting
```dart
int n = 123;
dobule m = n; // fail
dobule m = n as dobule; // pass
```
- 자동 형변환 불가
- 명시적으로 형변환해서 대입

## null safety
```dart
int test = 123;
print(test); // 123
test = null; // fail

int? test = 123;
print(test); // 123
test = null; // pass
print(test?.isNotEmpty); // null
```
- 기본 적으로 Not-Nullable 하게 선언됨
- Nullable 하게 선언이 필요 시 ? 키워드를 추가
- Nullable한 변수에 접근 시 ?. 키워드를 통해 접근
