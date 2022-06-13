---
layout: post
title: "HashMap과 Hashtable"
tags: [자료구조]
comments: false
---

## 개요
HashMap과 Hashtable의 개념과 차이점을 알아보자

---
## HashMap
- HashMap: Map 인터페이스를 구현한 클래스
- Map : key와 vlaue를 가진 데이터를 보관하는데 사용되는 인터페이스
- Key는 Map에 유일해야 한다.
- key, value에 null 값이 허용된다.
- HashMap과 사용법이 거의 동일한 컬렉션에는 Hashtable이 있다.
- HashMap과 Hashtable의 차이점은 Thread 관점에서 안전하냐(Hashtable) 안전하지 않은 대신 속도가 빠르냐(HashMap)이다.
- HashMap 사용법
```java
public static void main(String[] args) {
    Map<String,Integer> map = new HashMap();
    map.put("A", 100);
    map.put("B", 101);
    map.put("C", 102);
    map.put("C", 103); //중복된 key가 들어갈때는 이전 키,값을 지금의 것으로 업데이트

    System.out.println(map); // {A=100, B=101, C=103}
    System.out.println(map.get("A"));
    System.out.println(map.get("B"));
    System.out.println(map.get("C"));
}
```

---

## Hashtable
- HashMap과 함께 Map 인터페이스를 구현한 클래스
- HashMap과 달리 key, value에 null 값을 허용하지 않는다.
- Hashtable은 key를 가지고 key에 해당하는 value를 찾는다.
- Hashtable은 동기화가 걸려있어 Thread-Safe하다고 할 수 있고, HashMap은 동기화가 없어 unsafe하다고 할 수 있다.
- 안전성이 중요하다면 Hashtable 데이터의 빠른 처리가 중요하다면 HashMap을 쓰면된다.
- Hashtable 사용법
```java
public static void main(String[] args) {
    // 1. put, get 메소드
    Map<String,Integer> map = new Hashtable<>();
    map.put("A", 100);
    map.put("B", 101);
    map.put("C", 102);
    map.put("C", 103);

    System.out.println(map);
    System.out.println(map.get("A"));
    System.out.println(map.get("B"));
    System.out.println(map.get("C"));

    // 2. key값 순회
    for (String key : map.keySet()) {
        System.out.println(key + " " + map.get(key));
    }

    // 3. Hashtable 합치기
    Map<String, Integer> map1 = new Hashtable<>();
    map1.put("A", 100);
    map1.put("B", 101);

    Map<String, Integer> map2 = new Hashtable<>();
    map2.put("A", 101);
    map2.put("C", 102);

    map2.putAll(map1); // map2에 map1 합치기
    System.out.println(map2); // {A=100, C=102, B=101}

    // 4. Hashtable foreach
    map1.forEach((key, value) -> {
        System.out.println(key + " " + value);
    });
}
```

---

## HashMap의 주요 메소드

| 메소드 | 설명 |
|----|----|
| boolean containsKey(Object key)                               | 지정된 key가 포함되어 있는지 여부를 반환한다.                                                    |
| boolean containsValue(Object value)                           | 지정된 value가 포함되어 있는지 여부를 반환한다.                                                  |
| Set entrySet()                                                | 저장된 키와 값을 엔트리(키와 값의 결합)의 형태로 Set에 저장하여 반환한다.                        |
| Set keySet()                                                  | 저장된 모든 key를 Set에 저장하여 반환한다.                                                       |
| void clear()                                                  | 저장된 모든 객체(key, value)를 제거한다.                                                         |
| Object remove(Object key)                                     | 지정된 key에 해당하는 value를 제거한다.                                                          |
| Object getOrDefault(Object key, Object defaultValue)          | 지정된 키의 값을 반환한다. 키가 없을 경우, default Value로 지정된 데이터를 반환한다.             |
| void putAll(Map map)                                          | Map에 저장된 모든 요소를 HashMap에 저장한다.                                                     |
| Object replace(Object key, Object value)                      | 지정된 키의 값을 지정된 value로 대체한다.                                                        |
| boolean replace(Object key, Object oldValue, Object newValue) | 지정된 키와 값(oldValue)가 모두 일치하는 경우에만 새로운 값으로 대체하며, 일치 여부를 반환한다.  |

---

## 결론
- HaspMap, Hashtable은 key와 value를 형태에 자료구조를 가진 map 인터페이스를 구현한 클래스이다.
- Hashtable은 동기화가 걸려있고 HashMap은 동기화가 없다.
- 안전성이 중요하다면 Hashtable 데이터의 빠른 처리가 중요하다면 HashMap을 쓰면된다.

---

[참고] [https://reakwon.tistory.com/151](https://reakwon.tistory.com/151)

