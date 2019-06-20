---
layout: post
title: 'Map과 HashMap 의 차이점은 무엇인가요?'
author: soultree1984
date: 2019-06-12 02:37
categories: ["tech"]
tags: 
- "interview"
- "java"

---

> Map과 HashMap 의 차이점은 무엇인가요?

언젠가 면접 보러 갔을 때 1차 기술면접 자리에서 면접관이 나에게 했던 질문이었다.

순간 나는 "Map 인터페이스를 구현한 클래스가 HashMap 입니다." 라고 대답을 했는데,

면접관은 아무말도없이 고개만 끄덕였는데 지금 생각해봐도 저걸 왜물어봤는지 이해가 되질 않는다.

설마 저 대답을 원한건 아니었기를...

## "HashMap 과 HashTable 의 차이점을 알고 있나요?"

## "TreeMap 과 HashMap 의 차이점을 알고 있나요?"

차라리 이렇게 물어봤으면 좀 더 길게 대답 했을 것이다. 

Java에서 Map 인터페이스를 구현한 클래스는 여러가지가 있다.

Map은 Key와 Value 를 한쌍으로 갖는 자료 구조 이다.

아파트를 예로 들자면 우리집 열쇠로는 우리집만 들어 갈 수 있는 구조가 Map 이다. 

### 키값의 중복을 허용하지 않는다는 것이 Map의 핵심이다.

Map을 구현한 클래스를 살펴보면 대표적으로 

HashTable, HashMap, ConcurrentHashMap, LinkedHashMap, TreeMap 등이 있다.

HashTable은 JDK 1.0 부터 있던 API 이고, HashMap은 Java 1.2 에서 처음 선보인

Java Collections Framework에 속한 API 이다. 여기서 Collections Framework란 쉽게 말해서,

다수의 데이터를 처리하는 자료 구조를 통칭하는 개념이다. 

HashTable 과 HashMap의 차이점을 살펴보면,<br/>


비교 | HashTable  | HashMap
------------ | ------------- | -------------
Synchronized | Y | N
Thread-Safe | Y | N 
Null Key | N | Y
Null Value | N | Y

Multi-Thread 환경이 아니라면 HashMap을 쓰는 것이 아무래도 성능상 이롭다.

그러나 Synchronized 가 필요한 상황일지라도 HashTable은 오래된 클래스라서 최근에는 사용하지 않고, 

ConcurrentHashMap 라는 HashMap에서 Synchronized가 추가된 클래스를 사용하길 권장한다.

### HashTable 과 HashMap은 순서를 보장하지 않는다. 

```java

    Map<String,String> hashMap = new HashMap<>();
    
    hashMap.put("test_A","첫번째");
    hashMap.put("test_B","두번째");
    hashMap.put("test_C","세번째");
    hashMap.put("test_D","네번째");
    hashMap.put("test_E","다섯째");
    hashMap.put("test_F","여섯째");
    
    for(String key : hashMap.keySet()){
    
        System.out.println("hashMap value : " + hashMap.get(key));

    }

```

출력 결과

```java

// hashMap value : 네번째
// hashMap value : 세번째
// hashMap value : 두번째
// hashMap value : 첫번째
// hashMap value : 여섯째
// hashMap value : 다섯째

```

결과값을 보면 입력한 순서대로 출력되면 좋겠지만 뒤죽박죽으로 출력이 된다.

이럴때 필요한게 TreeMap, LinkedHashMap 이 있다.

위에 말했던 면접때 LinkedHashMap 에 대한 질문도 있었는데 제대로 대답을 못했다. 

LinkedHashMap을 잘 모르기도 했고, 일할때도 LinkedHashMap 보다 ArrayList\<HashMap\> 형태로 사용했다.

지금 생각해보면 단순 목록 데이터만 내려주는 형태라 LinkedHashMap 보다 ArrayList<HashMap>로

사용하는게 성능상 나아서 다들 그렇게 썼나 싶다. 

### TreeMap 과 LinkedHashMap 는 순서를 보장한다.

정확히 얘기 하면 LinkedHashMap는 입력된 순서를 보장하고,

TreeMap 정렬된 순서를 보장하며 __Compartor__ 구현으로 순서를 변경 할 수 있다.<br/>
`(내부적으로 Red-Black Tree로 저장하고 Red-Black Tree 대해서는 나중에 다시 정리 할 예정.)`  

기본 정렬 순서는 숫자 > 알파벳 대문자 > 알파벳 소문자 > 한글 순이다.

LinkedHashMap 은 Doubly-Linked List를 내부에 유지함으로써 입력된 자료의 순서를 보장한다.

그리고 이번 포스팅에선 대략적인 내용만 정리하고
 
동작 방법이나 성능 등 좀 더 자세한 포스팅은 나중에 다룬다.