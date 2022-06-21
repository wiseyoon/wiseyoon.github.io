---
layout: post
title: "Stack, Queue 문제"
tags: [알고리즘]
comments: false
---
## 개요
Stack, Queue 사용 알고리즘 문제 풀이 개인 기록용

--- 

## [프로그래머스] 기능개발
- 문제 설명 : 배포일마다 배포되는 기능 수
- 문제 링크 : [https://programmers.co.kr/learn/courses/30/lessons/42586](https://programmers.co.kr/learn/courses/30/lessons/42586)

```java
public static String solution(String[] participant, String[] completion) {

    ArrayList<Integer> arrayList = new ArrayList<>();
    int compCnt;
    int days = 1;

    Queue<Integer> que = new LinkedList<>();
    Queue<Integer> spd = new LinkedList<>();

    for (int i = 0; i < progresses.length; i++) {
        que.add(progresses[i]);
    }

    for (int i = 0; i < speeds.length; i++) {
        spd.add(speeds[i]);
    }

    while (!que.isEmpty()) {
        compCnt = 0;
        if (que.peek() + spd.peek() * days >= 100) {
            compCnt++;
            que.remove();
            spd.remove();
            while (!que.isEmpty() && que.peek() + spd.peek() * days >= 100) {
                compCnt++;
                que.remove();
                spd.remove();
            }
            arrayList.add(compCnt);
        }
        days++;
    }

    return arrayList.stream().mapToInt(x-> x).toArray();
}
```

--- 

## [프로그래머스] 프린터
- 문제 설명 : 중요도 높은 순으로 프린터했을 때 location이 출력되는 순서
- 4개의 문서(A, B, C, D)가 순서대로 인쇄 대기목록에 있고 중요도가 2 1 3 2 라면 C D A B 순으로 인쇄하게 됨
- 문제 링크 : [https://programmers.co.kr/learn/courses/30/lessons/42587](https://programmers.co.kr/learn/courses/30/lessons/42587)

```java
public static String solution(int[] priorities, int location) {
    int answer = 0;

    PriorityQueue<Integer> priorityQueue = new PriorityQueue<>(Collections.reverseOrder());

    for (int i=0; i < priorities.length; i++){
        priorityQueue.add(priorities[i]); // 3 2 2 1
    }

    while (!priorityQueue.isEmpty()) {
        for (int i =0; i < priorities.length; i++) {
            if (priorityQueue.peek() == priorities[i]) {
                priorityQueue.remove();
                answer++;
        
                if (location == i)
                    return answer;
            }
        }
    }
    return answer;
}
```
--- 
