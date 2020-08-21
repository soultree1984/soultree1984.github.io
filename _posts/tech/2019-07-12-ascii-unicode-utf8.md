---
layout: post
title: '[면접] ASCII, Unicode, UTF-8 란?'
author: soultree1984
date: 2019-07-12 10:22
categories: ["tech"]
tags: 
- "interview"
---

> ASCII는 **A**merican **S**tandard **C**ode for **I**nformation **I**nterchange의 약자로<br/>
> ANSI라는 미국 국립 표준 협회에서 표준화한 정보교환용 7비트 부호 체계이다.

## 컴퓨터는 2진수로 표현을 한다면서 갑자기 7 bit 가 왜 나와?

1 byte 를 구성하는 8 bit 중에 7 bit 만 쓰는 이유는 나머지 1 bit 는 에러검출용 비트(패리티비트)로<br/> 
사용하기 때문이다. 7 bit는 2 <sup>7</sup> 이라서 **128**개 ( 0 ~ 127 ) 를 표현 할 수 있다.

아래 그림처럼 0 ~ 127 까지 고유한 값이 할당 되어있는걸 알 수 있다.

<img src="/assets/images/ascll_table.png" width->

ASCII 코드는 영문을 표시하기에는 부족함이 없었지만 다른 언어를 표현하기에
7 bit 로는 부족했고 이를 극복하기 위해 1 bit 를 확장한 8 bit 의 ASCII 코드가 나왔는데
이것이 바로 ANSI 코드 이다. <br/> 8 bit 는 2 <sup>8</sup> 즉 **256**개를 표현 할 수 있다.
<br/><br/>
하지만 여전히 한국,중국,일본등의 글자를 표현하기에는 제한이 있었고,<br/>
이에 **2 byte (16 bit)** 로 확장한 **UNICODE**가 등장했다.
16 bit는 2 <sup>16</sup> 즉 **65536**개를 표현 할 수 있다.

> Unicode는 Universal Coded Character Set의 약자로서 문자를 16bit의 숫자로 표현한 것 

여기까지 정리하면 **ASCII, ANSI Code, Unicode**는 표현할수 있는 문자의 가지수가 다른 
1:1로 매핑된 **문자집합** 이다.

위 ASCII Table과 같이 [Unicode Table][1] 은 [링크][1]에서 확인 할 수있다.

[1]:http://www.tamasoft.co.jp/en/general-info/unicode.html

## 그래서 UTF-8은 뭐냐고?

UTF-8을 얘기하기 전에 Encoding(인코딩)을 먼저 알아야 하는데,
인코딩이란 문자나 기호들의 집합을 컴퓨터에 저장하거나 통신에 사용할 목적으로
부호화 하는 방법을 말한다. 이러한 인코딩의 반대 개념으로 Decoding(디코딩)이 있는데
부호화된 정보를 부호화되기 전으로 되돌리는 처리방식으로 복호화라고 한다.<br/>
### Encoding(부호화)  <-> Decoding(복호화)  <br/>
여기서 부호화를 수행하는 장치나 회로, 소프트웨어 및 알고리즘을 **인코더**라고 이야기 하고, 복호화를 수행해주는것을 **디코더**라고 한다.

인코딩과 디코딩을 하는 이유는 위에서 이야기한 표준화된 문자집합을 사용하기 위함이다.<br/>
표준화된 데이터 표현 방법이 없다면 데이터를 주고 받을때 호환성이 떨어진다.

## 아니 그래서 UTF-8은 언제 얘기 할꺼냐고?

Unicode는 2 byte 로 표현하기 때문에 1 byte 만으로도 충분한 영어권 사용자들은
메모리가 2배로 낭비 된다. 따라서 문자에 따라서 1 ~4 byte 가변길이로 인코딩 하는
UTF-8 이 탄생했다. 

> UTF-8은 Universal Coded Character Set + Transformation Format – 8-bit 의 약자이다.

UTF-8 의 경우 **숫자/영문**은 **1 byte** 로 처리하고
**한글**은 초성, 중성, 종성을 각각 1 byte 조합형으로<br/>도합 **3 byte** 로 처리한다.

UTF-8은 8 bit 단위로 처리하고, UTF-16은 16 bit 단위로 처리하고, UTF-32은 32 bit 단위로 처리한다.<br/>
대게 UTF-8로 사용하고 있으니 16,32 는 개념정도만 알고 있으면 된다.

어디선가 한번쯤 들어봤을 EUC-KR은 완성형 인코딩 방식으로 한글을 2 byte로 표현한다.
 
## 복잡하게 들어가면 끝도 없으니 이정도로 마무리한다.


