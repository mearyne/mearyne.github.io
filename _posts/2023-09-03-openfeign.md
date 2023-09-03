---
title: openfeign 
date: 2023-09-03 17:58:43 +0900
categories: []
tags: []     
---

## openfeign이란?
Netfilx에 의해 만들어진 선언적인(Declearative) HTTP Client 도구로써, 외부 API 호출을 쉽게 할 수 있다.  
어노테이션 @FeignClient를 붙여서 인터페이스를 선언하고, 해당 인터페이스를 가져와서 restTemplate처럼 써먹을 수 있다.  

### 장점
1. 적어야 되는 코드의 양이 줄어듬
2. 익숙한 MVC 어노테이션으로 익숙함
3. 다른 Spring Cloud 기술들(Eureka, Circuit Breaker, LoadBalancer) 과의 통합이 쉬움

### RestTemplate보다 좋은 점은?
restTemplate를 사용하기 위해서는 선언해야 하는 것들이 많다.  



## 참고 사이트
1. [openfeign이란? Openfeign 소개 및 사용법](https://mangkyu.tistory.com/278)  

