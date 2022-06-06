---
layout: post
title: "stream VS for"
tags: [자료구조]
comments: false
---

## 개요  

반복적인 작업 처리를 위해 for문과 stream을 사용하고 있다.  
성능상 for문이 stream보다 좋다고 하는데 실제 프로젝트 내부에서는 stream으로 된 코드들이 많이 있다.  
차이점을 알고 개발할 필요가 있다 생각되어 공부하고 기록하고자 한다.  

--- 

## for문 
- **전통적 for문**
```java
public static void main(String[] args) {
    List<Integer> list = Arrays.asList(1,2,3,4,5);

    for(int i=0; i<list.size(); i++) {
        System.out.println(list.get(i));
    }
}
```
- **향상된 for문**
```java
public static void main(String[] args) {
    List<Integer> list = Arrays.asList(1,2,3,4,5);

    for(Integer num : list) {
        System.out.println(num);
    }
}
```
for문은 전통적인 for문과 JDK 1.5 이상부터 나온 향상된 for문 두 가지가 있다.  
for-each의 정식 이름을 향상된 for문이라고 하는데 effiective java에서는 향상된 for문 사용을 권장하고 있다.  
전통적 for문과 다르게 인덱스를 직접 입력하는 방식이 아니기 때문에   
index out of bounds exception 예외로부터 안정적이고 가독성도 전통적 for문보다 높기 때문이다.

---

## stream
```java
public static void main(String[] args) {
    List<Integer> list = Arrays.asList(1,2,3,4,5);

    list.stream()
        .filter(num -> num > 3)
        .collect(Collectors.toList());
}
```
stream은 JAVA8 부터 제공되는 기능으로 컬렉션, 배열 등 저장되어있는 요소들을 하나씩 참조하여 반복적인 처리를 가능하게 하는 기능이다.  
stream으로 코드 작성 시 중첩된 for문으로 구성되어 있는 코드보다 depth를 줄여주어 가독성을 높일 수 있다. 

---

## for문 vs stream
위에 설명으로만 보면 stream이 뒤에 나온 기능이고 가독성도 높아 무조건 반복문에서는 stream을 써야하는건가? 
라고 생각될 수 있다. 하지만 stream 사용 시 주의해야할 경우가 있다.
stream은 for에서 할 수 있는 continue, break문을 사용할 수 없다.

```java
// [CASE 1] for문
for(Integer num : list) {
    if (num == 2) {
        // 2번 돌고 반복 종료
        break;
    }
    System.out.println(num);
}
```
```java
// [CASE 2] stream
list.forEach(num -> {
    if(num == 2) {
        // 1000번의 조건을 모두 확인 후 종료
        return;
    }
    System.out.println(num);
});
```
예를 들어 1000개 원소를 가진 list가 있다고 했을 때 stream은 위 코드 케이스에서는 1000번을 모두 확인 후에  
종료가 된다. 동작 결과는 정상으로 보일 수 있어도 성능상에서는 큰 차이가 날 수 있는 케이스이다.  
effective java에서는 forEach 연산은 최종 연산 중 기능이 가장 적고 가장 ‘덜’ 스트림답기 때문에, 
forEach 연산은 스트림 계산 결과를 보고할 때(주로 print 기능)만 사용하고 계산하는 데는 쓰지 말자 라며, stream.forEach()의 사용에 주의를 준다.

## 결론
for문과 stream 각각의 장단점을 알고 상황에 맞춰 써야할 것 같다.
구현하는 로직에 따라 for문이 stream보다 가독성이 높은 경우가 생길 수 있고, 위에 예시처럼 stream이
성능에 문제를 줄 수 있는 케이스도 있을 수 있다. 간결함과 가독성을 위해 stream을 주로 사용하고 있지만 stream 사용 시 
주의점을 알고 상황에 맞춰 사용해야겠다.

---

[참고]
https://tecoble.techcourse.co.kr/post/2020-05-14-foreach-vs-forloop/

