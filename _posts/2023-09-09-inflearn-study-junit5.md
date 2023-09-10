---
title: junit5 강의를 보면서 배운점들
date: 2023-09-09 10:04:13 +0900
categories: [java, Spring]
tags: [java, spring, security, junit5]     
---

## Domain 설정법
### @Builder
```java
    @Builder
    public User(Long id, String username, String password, String email, String fullname, UserEnum role, LocalDateTime createdAt, LocalDateTime updatedAt) {
        this.id = id;
        this.username = username;
        this.password = password;
        this.email = email;
        this.fullname = fullname;
        this.role = role;
        this.createdAt = createdAt;
        this.updatedAt = updatedAt;
    }
```
@Builder 어노테이션을 붙이자.  

### ManyToOne(fetch = FetchType.LAZY)
```java
    // 항상 ORM에서 fk의 주인은 Many Entity 쪽이다.
    @ManyToOne(fetch = FetchType.LAZY)
    private User user; // user_id
```
한 명의 유저는 여러 개의 계좌를 얻을 수 있다. 그렇다면 유저와 계좌의 관계는 일대다 관계라 할 수 있다.  
이를 엔티티 코드로 구현을 하려면 account 테이블 코드에서 위와같이 적으면 된다.  
많은 쪽에서 ManyToOne을 적으면 된다.  
이렇게 되면 실제로 작동할때 account.getUser()까지는 LAZY가 작동 안한다.  
account.getUser().getId() 이렇게 되야지 LAZY가 작동한다.  


### @Column
```java
 
### @ManyToOne(fetch = FetchType.LAZY)
```java
    // 항상 ORM에서 fk의 주인은 Many Entity 쪽이다.
    @ManyToOne(fetch = FetchType.LAZY)
    private User user; // user_id
```
한 명의 유저는 여러 개의 계좌를 얻을 수 있다. 그렇다면 유저와 계좌의 관계는 일대다 관계라 할 수 있다.  
이를 엔티티 코드로 구현을 하려면 account 테이블 코드에서 위와같이 적으면 된다.  
많은 쪽에서 ManyToOne을 적으면 된다.  
이렇게 되면 실제로 작동할때 account.getUser()까지는 LAZY가 작동 안한다.  
account.getUser().getId() 이렇게 되야지 LAZY가 작동한다.  


### @Column
```java
    @Column(unique = true, nullable = false, length = 20)
```
unique 여부, nullable 여부, length 여부 등등... 을 설정할 수 있다.  



### Enum 설정법

Enum을 사용해서 객체를 편리하게 관리할 수 있다.  
```java
package shop.mtcoding.bank.domain.user;

import lombok.AllArgsConstructor;
import lombok.Getter;

@AllArgsConstructor
@Getter
public enum UserEnum {
    ADMIN("관리자"), CUSTOEMR("고객");

    private String value;
}
``` 

엔티티에서 해당 Enum을 써먹을때는 다음과 같이 쓴다.  
```java
    @Column(nullable = false)
    @Enumerated(EnumType.STRING)
    private UserEnum role; // ADMIN, CUSTROMER
```

```java
   @Column(unique = true, nullable = false, length = 20)
```
unique 여부, nullable 여부, length 여부 등등... 을 설정할 수 있다.  



### Enum 설정법

Enum을 사용해서 객체를 편리하게 관리할 수 있다.  
```java
package shop.mtcoding.bank.domain.user;

import lombok.AllArgsConstructor;
import lombok.Getter;

@AllArgsConstructor
@Getter
public enum UserEnum {
    ADMIN("관리자"), CUSTOEMR("고객");

    private String value;
}
``` 

엔티티에서 해당 Enum을 써먹을때는 다음과 같이 쓴다.  
```java
    @Column(nullable = false)
    @Enumerated(EnumType.STRING)
    private UserEnum role; // ADMIN, CUSTROMER
```

## Test 사용법

```java
// Spring 관련 Bean들이 하나도 없는 환경!!
@ExtendWith(MockitoExtension.class) // 가짜 환경이다
class UserSerivceTest {

    @InjectMocks
    private UserSerivce userSerivce;

    @Mock
    private UserRepository userRepository;

    @Mock
    private BCryptPasswordEncoder passwordEncoder;

    @Test
    public void join_test() throws Exception {
        // given
        UserSerivce.JoinReqDto joinReqDto = new UserSerivce.JoinReqDto();
        joinReqDto.setUsername("ssar");
        joinReqDto.setPassword("1234");
        joinReqDto.setEmail("ssar@nate.com");
        joinReqDto.setFullname("쌀");

        // stub 1
        when(userRepository.findByUsername(any())).thenReturn(Optional.empty());
//        when(userRepository.findByUsername(anyString())).thenReturn(Optional.of(new User()));

        // stub 2
        User saar = User.builder()
                .id(1L)
                .username("ssar")
                .password("1234")
                .email("ssar@nate.com")
                .fullname("쌀")
                .role(UserEnum.CUSTOEMR)
                .createdAt(LocalDateTime.now())
                .updatedAt(LocalDateTime.now())
                .build();
        when(userRepository.save(any())).thenReturn(saar);

        // when
        UserSerivce.JoinRespDto joinRespDto = userSerivce.join(null);
        System.out.println("테스트 : " + joinRespDto);


        // then
        assertThat(joinRespDto.getId()).isEqualTo(1L);
        assertThat(joinRespDto.getUsername()).isEqualTo("ssar");



    }
}
```
서비스를 테스트 할때는 @Extention(MockitoExtension.class)를 사용한다.  
가짜 환경에는 Bean이 하나도 없다. 따라서 하나하나 넣어줘야한다.  
가짜 환경에 Autowired할때는 @InjectMocks를 쓴다.  
@Mock은 @InjectMocks에 주입시킬 수 있다.  
stub은 가짜로 주입됬기에 실제로 작동하지 않는 메소드를 임시로 인풋값과 리턴값을 지정해주는 것을 말한다.  
즉, @Autowired를 사용하여 메소드를 실행한다면(예를 들면 repo.save()) stub을 지정해줘야 한다.  
@Spy를 사용하면 가짜가 아닌 진짜가 불러와진다.  



### 손쉽게 더미데이터 넣는 방법(재활용)
config 폴더 안에 dummy 폴더를 만든다.  
해당 폴더 안에 DummyObject를 만든다.  
```java
public class DummyObject {

    protected User newUser(String username, String fullname) {
        BCryptPasswordEncoder bCryptPasswordEncoder = new BCryptPasswordEncoder();
        String encPassword = bCryptPasswordEncoder.encode("1234");
        return User.builder()
                .username(username)
                .password(encPassword)
                .email(username + "@nate.com")
                .fullname(fullname)
                .role(UserEnum.CUSTOEMR)
                .build();

    }

    protected User newMockUser(Long id, String username, String fullname) {
        BCryptPasswordEncoder bCryptPasswordEncoder = new BCryptPasswordEncoder();
        String encPassword = bCryptPasswordEncoder.encode("1234");
        return User.builder()
                .id(id)
                .username(username)
                .password(encPassword)
                .email(username + "@nate.com")
                .fullname(fullname)
                .role(UserEnum.CUSTOEMR)
                .createdAt(LocalDateTime.now())
                .updatedAt(LocalDateTime.now())
                .build();
    }

}
```
이렇게 더미데이터를 작성해놓는다.  
위의 코드는 실제 save할때 쓴다.  
아래 코드는 Mock테스트할때 쓴다.  

이것을 활용하는 방법은 다음과 같다.  
```java
@ExtendWith(MockitoExtension.class)
class UserSerivceTest extends DummyObject {
        User ssar = newMockUser(1L, "ssar", "쌀A");
        when(userRepository.save(any())).thenReturn(ssar);

}
```
DummyObject를 불러와서 재활용한다.  





## Security 설정법
spring security는 5에서 6으로 넘어갈때 설정법이 바뀐다.  
아래의 설정는 security5.7.6 에서의 설정법이다.  

@Configuration으로 SecurityConfig 클래스를 생성한다.    

그 안에 @Bean으로 passwordEncoder()를 생성한다.    
그 안에 @Bean으로 filterChain()을 생성한다.   
- csrf 사용여부
- cors 사용여부
    - 어떤 Header를 허용할지
    - 어떤 Method를 허용할지
    - 어떤 OriginPattern(ip주소)을 허용할지
    - 어떤 경로에서 cors를 적용할지
- iframe 사용여부
- jSession 사용여부
- formLogin 사용여부(Security에서 제공하는 기본 form 페이지를 말함)
- httpBasic 사용여부(브라우저가 팝업창을 이용해서 사용자 인증을 진행하는 것을 말함)
- 경로에 따른 인가 여부 설정
- 애러 컨트롤 : 에러를 핸들링하여 받은 값을 내가 원하는 형태로 변형해서 보낼 수 있다

<details>
<summary>코드 내용(skelleton)</summary>

<!-- summary 아래 한칸 공백 두어야함 -->

```java
package shop.mtcoding.bank.config;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.http.SessionCreationPolicy;
import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;
import org.springframework.security.web.SecurityFilterChain;
import org.springframework.web.cors.CorsConfiguration;
import org.springframework.web.cors.CorsConfigurationSource;
import org.springframework.web.cors.UrlBasedCorsConfigurationSource;
import shop.mtcoding.bank.domain.user.UserEnum;

@Configuration
public class SecurityConfig {
    private final Logger log = LoggerFactory.getLogger(getClass());

    @Bean // Ioc 컨테이너에 BCryptPasswordEncoder() 객체가 등록됨.
    public BCryptPasswordEncoder passwordEncoder() {
        log.debug("디버그 : BCryptPasswordEncoder 빈 등록됨");
        return new BCryptPasswordEncoder();
    }

    // JWT 서버를 만들 예정!! Session을 사용안함.
    @Bean
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
        log.debug("디버그 : filterChain 빈 등록됨");
        http.headers().frameOptions().disable(); // iframe 허용안함.
        http.csrf().disable(); // enable이면 postman 작동안함(메타코딩 유튜브에 시큐리티 강의)
        http.cors().configurationSource(configurationSource());

        // jSessionId를 서버쪽에서 관리안하겠다는 뜻!!
        http.sessionManagement().sessionCreationPolicy(SessionCreationPolicy.STATELESS);
        // react, 앱으로 요청할 예정
        http.formLogin().disable();
        // httpBasic은 브라우저가 팝업창을 이용해서 사용자 인증을 진행한다.
        http.httpBasic().disable();
        
        // Exception 가로채기
        // 이걸 설정 안했을 경우 : postman, intellij test, web상에서 접근 -> 이 세가지의 return 값이 다르게 표시된다.
        // 설정하면 : 애러를 가로채서 커스텀한다. 세가지 모두 동일한 return값을 받을 수 있다. -> 이렇게 해서 테스트를 한다.
        http.exceptionHandling().authenticationEntryPoint((request, response, authenticationException) -> {
            CustomResponseUtil.unAuthentication(response, "로그인을 진행해 주세요");
        });


        http.authorizeRequests()
                .antMatchers("/api/s/**").authenticated()
                .antMatchers("/api/admin/**").hasRole("" + UserEnum.ADMIN)
                .anyRequest().permitAll();

        return http.build();
    }

    public CorsConfigurationSource configurationSource() {
        log.debug("디버그 : configurationSource cors 설정이 SecurityFilterChain에 등록됨");
        CorsConfiguration configuration = new CorsConfiguration();
        configuration.addAllowedHeader("*");
        configuration.addAllowedMethod("*"); // GET, POST, PUT, DELETE (Javascript 요청 허용)
        configuration.addAllowedOriginPattern("*"); // 모든 IP 주소 허용(frontend 쪽 IP만 허용 react)
        configuration.setAllowCredentials(true); // 클라이언트에서 쿠키 요청 허용

        UrlBasedCorsConfigurationSource source = new UrlBasedCorsConfigurationSource();
        source.registerCorsConfiguration("/**", configuration);
        return source;
    }
}
```

</details>




## 참조 사이트
1. [inflearn - junit5 테스트](https://www.inflearn.com/course/lecture?courseSlug=스프링부트-junit-테스트&unitId=147275)  
테스트코드 강의를 구매해서 듣고있다.  
security와 junit5를 사용해서 간단한 은행 입출금 뱅크를 만들고 있다.  

2. [builder패턴을 써야하는 이유](https://pamyferret.tistory.com/67)  
builer어노테이션을 써서 객체를 생성하면 더 가독성있고 더 쉽게 객체를 생성할 수 있게 된다.  