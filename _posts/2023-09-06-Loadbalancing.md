---
title: Zuul Loadbalancing 실습(작성중)
date: 2023-09-06 13:19:08 +0900
categories: [MSA, zuul]
tags: [msa, loadbalancing, ribbon]     
---

## 로드밸런싱이란?
 서비스 앞에 위치해서 트래픽이 한쪽으로 쏠리지 않고 골고루 퍼지도록 하는 방법을 말한다.  
 로드밸런서는 서버 문제를 자동으로 감지하고 클라이언트 트래픽을 사용 가능한 서버로 리디렉션하여 시스템의 내결합성을 높인다.  
 따라서 다음과 같은 이점을 지닌다.  
 
- 가용성
- 확장성
- 보안
- 성능


## Ribbon이란?
Ribbon은 `Client Side Load Balancer`이다.  
Client Side Load Balancer는 소프트웨어로 구현된 클라이언트에 탑제되는 로드밸런서이다.    

구성요소는 다음과 같다
- ServerList : 로드밸런싱 할 서버 리스트
- Rule : 요청을 보낼 서버를 선택하는 논리
- Ping : 서버가 살아있는지 체크




## 참고 사이트
1. [aws 로드밸런싱이 무엇인가요?](https://aws.amazon.com/ko/what-is/load-balancing/)  
AWS에서 로드밸런싱의 개념, 장점, 알고리즘, 작동원리, 종류, AWS에서 제공하는 로드밸런싱 에 대해서 설명하고 있다.  


2. [Ribbon의 개념과 실습](https://sabarada.tistory.com/54)  
ribbon의 개념과 구성요소, 실습에 대해서 설명함.  