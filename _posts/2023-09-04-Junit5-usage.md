---
title: Junit5 사용법 정리(작성중)
date: 2023-09-04 19:08:57 +0900
categories: [java, Junit5]
tags: [spring, junit5, java, yet]     
---

## Junit이란?
자바 개발자가 가장 많이 사용하는 테스팅 기반 프레임워크다.  


## 실행환경
- org.springframework.boot:spring-boot-starter-test:3.1.0
- org.junit.jupiter:junit-jupiter-api:5.9.3
- springboot 3.1.0
- jdk 17
- h2
- multi modules

## 종류
```java
assertEquals(excpected, actual)
assertNotNull(actual)
assertTrue(boolean)
assertAll(excutables...) // 모든 확인 구문 확인
assertThrows(expectedType, excutable) // 예외 발생 확인
assertTimeout(duration, executable) // 특정 시간 안에 실행이 완료되는지 확인
```

## 사용종류
### 조건에 따라서 실행여부 결정
조건에 따라서 테스트를 진행할지를 결정할 수 있다.  
OS가 MAC인지 WIN인지(@EnabledOS)에 따라서 결정할 수 있고, 자바 버전이 몇버전인지(@EnabledJRE)에 대해서 실행여부를 설정해줄 수 있다.  
환경변수값이 특정 값(@EnabledIfEnvironmentVariable)일때 작동시키게 할 수 있다.  

### 태깅 및 필터링
테스트에 태그를 붙여서 원하는대로 작동시키거나 할 수 있다.  
```
@Tag("")
```




## 사용법
### assert() 안의 supplier는 람다로 표현하기!

```
assertEquals(StudyStatus.DRAFT, study.getStatus(), () -> "스터디를 처음 만들면" + StudyStatus.DRAFT + "상태다.");
assertEquals(StudyStatus.DRAFT, study.getStatus(), "스터디를 처음 만들면" + StudyStatus.DRAFT + "상태다.");
```
위와 아래의 코드는 서로 동일하지 않을때, 메시지를 띄우도록 하는 코드이다.  
하지만 아래의 코드는 성공을 해도 연산을 진행하는 반면에, 위의 코드는 실패했을 때만 연산한다.  
따라서 위의 방식대로 작성하는 것이 더 효율적이다.  



## 문제점
### 윈도우에서 h2 데이터베이스 생성 안되는 오류(IO Exception)
![h2-database-create-fail-problem](https://raw.githubusercontent.com/mearyne/mdImgHost/master/_posts/2023-09-04-junit5-usage.md/198923911242847.png)
윈도우에서 작업할때 h2아이콘 우클릭 후 데이터베이스를 생성하려고 했으나 위와 같은 오류가 떴다.  
맥북에서는 콘솔로 h2.sh를 실행한 것을 기억하고 터미널을 연 다음에 h2.bat을 실행했다.  
그리고 다시 데이터베이스를 실했했을때 좀더 자세한 오류 내용을 확인할 수 있었다.  


![h2-database-create-fail](https://raw.githubusercontent.com/mearyne/mdImgHost/master/_posts/2023-09-04-junit5-usage.md/403083811233900.png)

권한 부여 문제였다.  
관리자 권한으로 실행해서 생성하니까 제대로 작동한다.     

![success-to-create-database-in-h2](https://raw.githubusercontent.com/mearyne/mdImgHost/master/_posts/2023-09-04-junit5-usage.md/339754511235732.png)
성공!


### 콘솔 hibernate에는 제대로 테이블이 생성됐지만 정작 h2 콘솔에서는 해당 테이블을 확인할 수 없는 현상.   
ddl-auto create로 프로젝트가 실행될때 테이블이 생성되도록 했다.  
프로젝트에 오류는 없었고, 연결도 정상적으로 이루어졌다.  


###  @autowired가 제대로 안먹히는 문제
멀티모듈 환경에서 @Test와 @Autowired를 사용하고자 할때 의존성 주입이 제대로 안이뤄진다.  
class에 @SpringBootTest를 붙여도 제대로 작동하지 않는다.  
분명 김영한 님의 강의를 봤을때는 문제없이 의존성 주입이 됐던거 같은데 그때는 어떻게 바로 됐는지 이해가 가지 않는다.  




## 참고사이트
1. [Junit5 기본 사용법 정리](https://insight-bgh.tistory.com/507)
Junit의 기본 개념, 구조, 