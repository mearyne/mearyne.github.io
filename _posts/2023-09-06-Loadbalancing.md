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


## Ribbon
### Ribbon이란?
Ribbon은 `Client Side Load Balancer`이다.  
Client Side Load Balancer는 소프트웨어로 구현된 클라이언트에 탑제되는 로드밸런서이다.    

구성요소는 다음과 같다
- ServerList : 로드밸런싱 할 서버 리스트
- Rule : 요청을 보낼 서버를 선택하는 논리
- Ping : 서버가 살아있는지 체크

### 버전 호환성
![replacements of ribbon](https://raw.githubusercontent.com/mearyne/mdImgHost/master/_posts/2023-09-06-loadbalancing.md/64750310230948.png)  
springboot 2.4.x 이상부터 Zuul, Ribbon을 사용할 수 없다.  


### Zuul에서 로드밸런싱 확인
User - Zuul - API1(application name = ribbon-api)  
                - API2(application name = ribbon-api)  
이렇게 구성이 되있다고 가정하자.  
이때 유저는 Zuul에게 통신을 쏜다. 유저는 API1, API2의 주소를 알 수 없고 (Zuul의 리버스 프록시 때문에) Zuul은 Eureka로부터 받아온 주소를 사용해서 통신을 전달하게 된다.  
API1, API2 둘의 어플리케이션 이름은 ribbon-api로 동일하기에, API1에서 통신을 했다면 다음 단계에서는 API2에서 통신하게 된다.  

![error in 14100](https://raw.githubusercontent.com/mearyne/mdImgHost/master/_posts/2023-09-06-loadbalancing.md/103034510249374.png)

처음은 API1에 오류가 뜨는걸 확인했다.  
다시 postman으로 쏜다면 오류가 발생한 API1이 아닌 API2로 전달된다.  
Ribbon은 디폴트로 Round Robbin 방식을 체택하기 때문에 오류발생여부와는 상관없이 API2로 전달한다(성공하든 실패하든 다음 통신은 API2이다).  



### Zuul에서 retry 확인
spring-retry 라이브러리를 설치해야한다.  
```xml
	<dependency>
			 <groupId>org.springframework.retry</groupId>
			 <artifactId>spring-retry</artifactId>
	</dependency>
```

```properties

# ribbon
zuul.retryable=true

ribbon.retryableStatusCodes=500
ribbon.OkToRetryOnAllOperations=true
ribbon.MaxAutoRetries=1
ribbon.MaxAutoRetriesNextServer=1
```
properties 설정에서 zuul과 ribbon만 쓰이기에 당연히 ribbon 라이브러리 안에 retry 코드가 들어있는줄 알았다.    
하지만 위의 spring-retry를 설치해주지 않으면 위의 설정이 제대로 작동되지 않는다.    
재시도 횟수는 (MaxAutoRetries + 1)번이다.   
다음 서버로 넘어가는 횟수는 (MaxAutoRetriesNextServer + 1)번이다.  
모두 실패한다고 가정하면, 2회 x 2회 = 4회를 시도하게 된다.  



## error
### RequestRejectedException error
```
The requestURI was rejected because it can only contain only printable ASCII characters
```
API1에서 return 타입을 String으로 했을때 뜨는 오류.  
포스트맨에는 404로 뜨기도 한다.  
이때 return 타입을 ResponseEntity<>로 해주면 해결된다.  




## 참고 사이트
1. [aws 로드밸런싱이 무엇인가요?](https://aws.amazon.com/ko/what-is/load-balancing/)  
AWS에서 로드밸런싱의 개념, 장점, 알고리즘, 작동원리, 종류, AWS에서 제공하는 로드밸런싱 에 대해서 설명하고 있다.  


2. [Ribbon의 개념과 실습](https://sabarada.tistory.com/54)  
ribbon의 개념과 구성요소, 실습에 대해서 설명함.  


3. [Client Side Load Balancer: Ribbon](https://cloud.spring.io/spring-cloud-netflix/multi/multi_spring-cloud-ribbon.html)  
공식 사이트에서 설명하는 Ribbon 개념  


4. [API-재시도를-처리할수-있는-여러가지-방안들](https://velog.io/@garden6/API-재시도를-처리할수-있는-여러가지-방안들)  
retry를 하는 5가지 방법  
