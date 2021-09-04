---
title: 'Map과 HashMap의 차이점은 무엇인가요?'
author: soultree1984
date: 2021-01-03 18:32:00 +0900
categories: [Interview]
tags: [Collection Framework, Map, HashMap ]
---

> Map과 HashMap의 차이점은 무엇인가요?

몇 년전 모회사에 면접 보러 갔을 때 1차 기술면접 자리에서 면접관이 나에게 했던 질문이었다.<br/>
순간 나는 "**Map** 인터페이스를 구현한 클래스가 **HashMap** 입니다." 라고 대답을 했는데,<br/>
면접관은 아무런 말도 없이 고개만 끄덕였고 지금 생각해봐도 저걸 왜 물어봤는지 도무지 모르겠다.<br/>
설마 저 대답을 원한건 아니었기를... 횡설수설한 기억 뿐인 면접이었지만 의외로 1차는 합격을 했고,<br/>
최종 2차에서 떨어졌다. 😱

## "그럼 HashMap 은 어떻게 동작하나요?"

만약 이후 질문이 저랬다면 버벅대다 대답도 못했을 테지..... 😭<br/>
**HashMap**의 동작에 대해서는 추후에 자세히 다룰 예정이다.<br/>
참고로 [**유투브 포프TV**][1] 를 운영하시는 포프님은 개발자의 기본기를 HashTable 이라고 말씀하시면서,<br/>
개발자 면접때 물어본다고 하셨다.<br/>

[1]:https://www.youtube.com/watch?v=S7vni1hdsZE

다시 주제로 돌아가서 **Map**은 **Collection Framework**에 속한 인터페이스중 하나로 키와 값을 하나의 쌍으로<br/>
묶어서 저장하는 자료 구조 이다.<br/>
`( Collection Framework 란 다수의 데이터를 처리하는 자료 구조를 통칭하는 개념이다.)`

### 키의 중복을 허용하지 않는다는 것이 Map의 핵심.

이러한 **Map**을 구현한 클래스중에 하나가 **HashMap** 이다. <br/>
이외에도 **HashTable, HashMap, ConcurrentHashMap, LinkedHashMap, TreeMap** 등이 있다.<br/>
**HashTable**은 Java 1.0 부터 있던 API 이고, **HashMap**은 Java 1.2 에서 추가된 API 이다.<br/>
비슷한 이름을 가진 두 녀석, **HashTable** 과 **HashMap**의 차이점을 살펴보면,<br/>


비교 | HashTable  | HashMap
------------ | ------------- | -------------
Synchronized  | Y | N
Thread-Safe  | Y | N
Null Key  | N | Y
Null Value  | N | Y

**Multi-Thread** 환경이 아니라면 **Synchronized**가 없는 **HashMap**을 쓰는 것이 아무래도 성능상 이롭다.<br/>
그러나 **Synchronized** 가 필요한 상황일지라도 **HashTable**은 오래된 클래스라서 최근에는 사용하지 않고,<br>
**ConcurrentHashMap** 라는 **HashMap**에서 **Synchronized**가 추가된 클래스를 사용하길 권장한다.<br/>
하지만 **Multi-Thread** 환경에서 개발 해본 적이 없어서 써본적은 없다. 사실 포스팅하면서 처음 봤다... 😱

### 자 이제 설명은 됐고, 코드를 보자.

```java

    Map<String,String> hashMap = new HashMap<>();

    hashMap.put("white","흰색");
    hashMap.put("red","빨강");
    hashMap.put("yellow","노랑");
    hashMap.put("green","녹색");
    hashMap.put("blue","파랑");
    hashMap.put("pink","핑크");

    for(String key : hashMap.keySet()){
        System.out.println("key is : " + key  + ", value is : " + hashMap.get(key));
    }

```

### 출력 결과

```java

// key is : red, value is : 빨강
// key is : pink, value is : 핑크
// key is : green, value is : 녹색
// key is : white, value is : 흰색
// key is : blue, value is : 파랑
// key is : yellow, value is : 노랑

```

결과값을 보면 입력한 순서대로 출력되면 좋겠지만 뒤죽박죽으로 출력이 된다.<br/>
이럴때 필요한게 **TreeMap**, **LinkedHashMap** 이 있다. 위에 얘기했던 면접때 **LinkedHashMap** 에 대한<br/>
질문도 있었는데, 창피하게도 제대로 대답은 못했고 안써봐서 잘 모른다고 했다. <br/>
일할때도 **ArrayList\<HashMap\>** 형태로만 써왔고, 왜 쓰는지에 대해선 생각해본적 없었다.<br/>
그냥 남들이 쓰니까 썼다. 역시 모르면 물어봐야한다.<br/>
돌이켜보면 **LinkedHashMap** 보다 성능상 나아서 다들 그렇게 썼나보다 라고 생각하고 싶지만,<br/>
왠지 그들도 모르고 그냥 쓴 것 같다....... 😰

### 순서를 보장하는 TreeMap 과 LinkedHashMap.

정확하게 얘기 하면 **LinkedHashMap**는 입력된 순서를 보장하고, **TreeMap**는 정렬된 순서를 보장한다.<br/>
 **Collections.sort**에 **Compartor** 구현으로 순서를 변경 할 수 있다.<br/>
기본 정렬 순서는 숫자 > 알파벳 대문자 > 알파벳 소문자 > 한글 순이다.<br/>
`(TreeMap은 내부적으로 Red-Black Tree로 저장한다. Red-Black Tree 대해서는 나중에 다시 정리 할 예정.)`


### 자 이제 설명은 됐고, 코드를 보자.

```java

    Map<String,String> linkedHashMap = new LinkedHashMap<>();

    linkedHashMap.put("white","흰색");
    linkedHashMap.put("red","빨강");
    linkedHashMap.put("yellow","노랑");
    linkedHashMap.put("green","녹색");
    linkedHashMap.put("blue","파랑");
    linkedHashMap.put("pink","핑크");

    for(String key : linkedHashMap.keySet()){
        System.out.println("key is : " + key  + ", value is : " + hashMap.get(key));
    }

```

### 출력 결과

```java

// key is : white, value is : 흰색
// key is : red, value is : 빨강
// key is : yellow, value is : 노랑
// key is : green, value is : 녹색
// key is : blue, value is : 파랑
// key is : pink, value is : 핑크

```

출력결과를 보면 입력된 순서가 보장됨을 확인 할 수 있다.<br/>
**LinkedHashMap** 은 **Doubly-Linked List**를 내부에 유지함으로써 입력된 자료의 순서를 보장한다.<br/>
그리고 이번 포스팅에선 대략적인 내용만 정리하고 동작 방법이나 성능 등 자세한 포스팅은 나중에 다룬다.<br/>

앞으로도 면접 때 들었던 질문을 꾸준히 포스팅 할 예정이다. 👌
