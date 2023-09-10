---
title: controller 테스트하는 법
date: 2023-09-10 20:18:15 +0900
categories: [java, Spring]
tags: [java, spring, junit, mock]     
---

## controller 테스트? postman으로 하면 되는거 아니야?
라고 생각했었다.  
실제로 포스트맨은 test 기능을 제공했고, 그것을 이용하면 테스트를 구현하면 되지 않을까 생각했다.  
하지만 4명 이상부터는 돈을 내야지 더 사람을 공유할 수 있다는 점과, 익숙하지 않은 형태의 테스트 코드를 다시 익혀야 한다는 점이 거슬렸다(JUnit도 익히는건 똑같지만).  
Intellij의 httpRequest 파일을 잘 이용하면 비슷하게 테스트를 만들 수 있지 않을까 싶었다.  
그런 생각을 한 이유는 그냥 JUnit을 이용해서 컨트롤러를 테스트 하는 법을 몰랐기 때문이기도 했다.  



## 사용법
```java
@AutoConfigureMockMvc
@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.MOCK)
class UserControllerTest extends DummyObject {
    @Autowired
    private MockMvc mvc;

    @Autowired
    private ObjectMapper om;

    @Test
    void join_success_test() throws Exception {
        // given
        UserReqDto.JoinReqDto joinReqDto = newJoinReqDto("love", "love@nate.com", "러브");
        String requestBody = om.writeValueAsString(joinReqDto); // 객체인 UserReqDto를 json 형태로 변형하기 위해서 사용함

        // when
        ResultActions resultActions = mvc.perform(post("/api/join").content(requestBody).contentType(MediaType.APPLICATION_JSON));
        String responseBody = resultActions.andReturn().getResponse().getContentAsString();
//        System.out.println("테스트 : " + responseBody);

        // then
        resultActions.andExpect(status().isCreated());

    }
}
```
- @AutoConfigureMockMvc와 @SpringBootTest를 적는다
- MockMvc를 이용해서 가상으로 통신을 쏜다  
- ObjectMapper를 이용해서 Dto를 String으로 변환한다  
- mvc.perform(메소드 + 주소).컨텐츠(바디값).컨텐츠타입(타입값); : post 통신을 날리는 코드
- resultActions.andReturn().getResponse().getContentAsString(); : return 값을 확인하고 싶을때 사용한다
- resultActions.andExpect(status().상태값); : 실제 테스트하는 코드



## 참고 사이트
1. [inflearn - junit5 테스트](https://www.inflearn.com/course/lecture?courseSlug=스프링부트-junit-테스트&unitId=147275)  
테스트코드 강의를 구매해서 듣고있다.  
security와 junit5를 사용해서 간단한 은행 입출금 뱅크를 만들고 있다.  