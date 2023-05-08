# 관심사의 분리(Separation of Concerns)

인간에게는 한계가 존재한다.
그렇기때문에 유지보수가 가능하도록 적절하게 나누고, 그룹화 해야한다.
ex: Java 패캐지가 대표적으로 존재한다.


그렇다면 인간의 한계를 극복하여 프로그래밍을 하기위해서는 어떤 기능을 사용해야할까?
---------------------------------------
# Layered Architecture
다층구조(Multi-tier Architecture)로 나워 관리한다.
기능별로 나누어 관리하기때문에 유지보수에 용이하다.
---------------------------------------
# Identifier
식별자를 만들기위한 기능을 Spring에서 제공한다.

## UUID
```java
String id = UUID.randomUUID().toString().replace("-", "");
```

## ULID
build.gradle에 의존성 추가.
```java
build.gradle에 의존성 추가.
```
ID 생성.
```java
build.gradle에 의존성 추가.
```

## TSID
build.gradle에 의존성 추가.
```java
implementation 'com.github.f4b6a3:tsid-creator:5.2.0'
```
ID 생성.
```java
implementation 'com.github.f4b6a3:tsid-creator:5.2.0'
```

---------------------------------------
# Service
근래에는 application이라고 한다.
관심사의 분리에 따라서 코드를 분리하고 배치하하는 것 = 설계
설계를 개선하는 것, 더 편리하게 설계를 바꿔주는 것 = 리팩토링
