---
layout: post
title: "Stack, Queue"
tags: [자료구조]
comments: false
---
## 개요
Stack과 Queue 자료구조에 대해 알아보자!

--- 

## Stack
- 한 쪽 끝에서만 자료를 넣고 빼는 작업이 이루어지는 자료구조.
- LIFO (Last In First Out) 방식으로 동작.
- 스택의 맨 위 요소 top 에만 접근이 가능하기 때문에 top이 아닌 위치의 데이터에 대한 접근, 삽입, 삭제는 모두 불가능하다.
- top 위치의 데이터에 바로 접근이 가능하기 때문에 데이터 삽입, 삭제의 시간 복잡도는 O(1)이다.
- 순차적으로 데이터를 추가하고 삭제하는 Stack에는 ArrayList와 같은 배열 기반의 컬렉션 클래스가 적합하다.

## 활용
- 재귀 알고리즘
- DFS 알고리즘
- 작업 실행 취소와 같은 역추적 작업이 필요할 때
- 괄호 검사, 후위 연산법, 문자열 역순 출력 등

## 사용법
```java
public static void main(String[] args) {
    Stack<Integer> stack = new Stack<>();
    
    // 데이터 삽입
    stack.push(1);
    stack.push(2);
    stack.push(3);
    
    // 데이터 출력
    stack.peek();   // 3 출력
    
    // 데이터 삭제
    stack.pop();    // 3 제거
    stack.pop();    // 2 제거
    stack.pop();    // 1 제거
    stack.clear();  // 모든 데이터 제거
}
```

--- 

## Queue
- 양쪽 끝에서 데이터의 삽입과 삭제가 각각 이루어지는 자료구조.
- FIFO (First In First Out)으로 동작.
- 데이터가 삽입되는 곳을 rear, 데이터가 제거되는 곳을 front.
- front, rear의 위치로 데이터 삽입 삭제가 바로 이루어지기 때문에 원소 삽입, 삭제의 시간 복잡도는O(1)이다.
- Queue는 데이터를 꺼낼 때 항상 첫 번째 저장된 데이터를 삭제하므로, ArrayList와 같은 배열기반의 컬렉션 클래스를 사용한다면 데이터를 꺼낼 때마다 빈 공간을 채우기 위해 데이터의 복사가 발생하므로 비효울적이다. 
- 그래서 Queue는 ArrayList보다 추가/삭제가 쉬운 LinkedList로 구현하는 것이 적합하다.
- Queue에서 데이터를 추가, 삭제, 검색할 때 제공되는 메소드의 차이는 기능적인 것은 아니고 문제 상황에서 예외를 던지냐 아니면 null 또는 false를 반환하느냐이다.
- 메소드 비교

|  | 예외발생      |값리턴 |
|----|-----------|----|
| 추가(enqueue) | add(e)    | offer(e) |  
| 살제(dequeue) | remove()  | poll() |  
| 검사(peek) | element() | peek() |  


## 활용
- 데이터를 입력된 순서대로 처리해야 할 때
- BFS 알고리즘
- 프로세스 관리
- 대기 순서 관리

## 사용법
```java
public static void main(String[] args) {
    Queue<Integer> queue = new LinkedList<>();
    
    // 데이터 삽입
    queue.offer(1);
    queue.offer(2);
    queue.offer(3);
    
    // 데이터 출력
    queue.peek();   // 1 출력
    queue.poll();   // 1 출력 후 삭제
    
    // 데이터 삭제
    queue.remove(); // 2 삭제
    queue.clear();  // 모든 데이터 제거
}
```

---

[참고] [https://velog.io/@nnnyeong/자료구조-스택-Stack-큐-Queue-덱-Deque](https://velog.io/@nnnyeong/자료구조-스택-Stack-큐-Queue-덱-Deque)