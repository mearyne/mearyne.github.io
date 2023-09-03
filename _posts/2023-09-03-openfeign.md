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

### restTemplate을 버리고 갈아타야하는가?
솔직히 잘 쓰고있는 restTemplate를 버리고 갈아탈 만큼의 매리트가 있어 보이지는 않는다.  
나름의 장단점이 존재하고, 각각의 단점들을 상쇄시킬 수 있다고 본다.  
선택의 문제이지 어느게 상위호환이다 그런 느낌은 못받았다.  

### 나는 왜 openfeign을 알아봤는가?
자그마한 미니서비스를 구축하는 과정에서 에러 제어를 위해서 hystrix를 적용하고 있었다.  
지금 시점(2023-08)에선 hystrix보다는 resilience4j를 권장했고, 도전했으나 계속된 실패로 openfeign을 이용하여 제어하는 법을 알아봤다.  




## 참고 사이트
1. [openfeign이란? Openfeign 소개 및 사용법](https://mangkyu.tistory.com/278)  

