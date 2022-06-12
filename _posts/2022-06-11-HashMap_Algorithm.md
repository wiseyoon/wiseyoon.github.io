---
layout: post
title: "HashMap 문제"
tags: [알고리즘]
comments: false
---
## 개요
HashMap 사용 알고리즘 문제 풀이 개인 기록용  

--- 

## [프로그래머스] 완주하지 못한 선수
- 문제 설명 : 참여자 중에서 완주하지 못한 선수 리턴
- 문제 링크 : [https://programmers.co.kr/learn/courses/30/lessons/42576](https://programmers.co.kr/learn/courses/30/lessons/42576)

```java
public static String solution(String[] participant, String[] completion) {

    // 1. 참여자 Map
    Map<String,Integer> partMap = new HashMap<>();
    for (String part : participant) {
        partMap.put(part, partMap.getOrDefault(part,0) + 1);
    }

    // 2. 완주자 제외
    for (String comp : completion) {
        partMap.put(comp, partMap.get(comp) - 1);
    }

    // 3. 완주하지 못한 선수 찾기
    for (String part : partMap.keySet()) {
        if (partMap.get(part) != 0) {
            return part;
        }
    }

    return "";
}
```

--- 

## [프로그래머스] 전화번호 목록
- 문제 설명 : 어떤 번호가 다른 번호의 접두어인 경우 false 리턴
- 문제 링크 : [https://programmers.co.kr/learn/courses/30/lessons/42577](https://programmers.co.kr/learn/courses/30/lessons/42577)

```java
public static String solution(String[] phone_book) {
    Map<String, Integer> map = new HashMap<>();

    // 1. 전화번호 목록 map
    for (String num : phone_book) {
        map.put(num, num.length());
    }

    // 2. 접두어 있는지 찾기
    for (int i=0; i < phone_book.length; i++) {
        for (int j=1; j < phone_book[i].length(); j++) {
            if (map.containsKey(phone_book[i].substring(0,j)))
                return false;
        }
    }

    return true;
}
```

--- 

## [프로그래머스] 위장
- 문제 설명 : 서로 다른 옷의 조합 수 구하기
- 문제 링크 : [https://programmers.co.kr/learn/courses/30/lessons/42578](https://programmers.co.kr/learn/courses/30/lessons/42578)

```java
public static String solution(String[][] clothes) {
    int answer = 1;

    // 1. 의상 종류별 map
    Map<String, Integer> map = new HashMap<>();
    for (String[] clothe : clothes) {
        String type = clothe[1];
        map.put(type, map.getOrDefault(type, 0) + 1);
    }

    // 2. 조합 수 구하기
    for (String key : map.keySet()) {
        answer *= (map.get(key) + 1);
    }

    return answer -1;
}
```

--- 

## [프로그래머스] 베스트앨범
- 문제 설명 : 많이 재생된 순으로 장르별 가장 많이 재생된 두 곡 나열
- 문제 링크 : [https://programmers.co.kr/learn/courses/30/lessons/42579](https://programmers.co.kr/learn/courses/30/lessons/42579)

```java
public static String solution(String[] genres, int[] plays) {
    List<Integer> list = new ArrayList<>();

    // 1. 장르별 count수 합하기
    Map<String, Integer> map = new HashMap<>();
    for (int i=0; i < genres.length; i++) {
        map.put(genres[i], map.getOrDefault(genres[i],0) + plays[i]);
    }
    
    List<String> keySetList = new ArrayList<>(map.keySet());
    Collections.sort(keySetList, (val1, val2) -> (map.get(val2).compareTo(map.get(val1))));

    // 2. 장르별 두 곡 찾기
    for (String key : keySetList) {
        int max = 0;
        int fir = 0;
        int sec = 0;

        // 첫번째 곡
        for (int i=0; i < genres.length; i++) {
            if (genres[i].equals(key)) {
                if (plays[i] > max) {
                    max = plays[i];
                    fir = i;
                }
            }
        }

        // 두번째 곡
        max = 0;
        for (int i=0; i < genres.length; i++) {
            if (genres[i].equals(key)) {
                if (i != fir && plays[i] > max) {
                    max = plays[i];
                    sec = i;
                }
            }
        }

        list.add(fir);

        // 장르별 곡이 1개인 경우 있음
        if (max != 0) {
            list.add(sec);
        }
    }

    int[] answer = new int[list.size()];
    for (int i=0 ; i < list.size(); i++) {
        answer[i] = list.get(i);
    }

    return answer;
}
```