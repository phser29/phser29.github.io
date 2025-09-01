---
layout: single
title: "springboot"
categories: java
tag: spring
toc: true
--- 

# java springboot

## DI(Dependency Injection)

>  소프트웨어 개발에서 중요한 개념, 컴포넌트 간의 의존성을 외부에서 주입함으로써 느슨한 결합을 유지하는 방법

## IOC 컨테이너

> Inversion of Control(제어의 역전) 컨테이너로 스프링 프레임워크의 핵심, 애플리케이션의 구성요소들을 관리하며, 객체의 생성과 의존성 주입을 담당

### 빈 정의 
> 개발자가 스프링 IOC 컨테이너에 의해 관리될  객체에 대한 정보를 제공하는 것 

  - XML 기반 설정
    - XML 파일을 사용하여 빈을 정의하는 방법. ```<bean>``` 태그를 사용하여 객체의 클래스, 이름, 범위 등을 지정
    
    - 스프링 프레임워크에서는 빈 정의와 컴포넌트 스캔을 XML 설정 파일을 사용
    - 스프링부트에서는 자동 설정 기능이 있어서 XML 설정 파일에 컴포넌트 스캔을 설정할 필요가 없고 XML 파일을 사용하지 않는다.

      - 스프링 프레임워크(only)
        - root-context.xml
        : 스프링 IOC 컨테이너를 초기화하고 애플리케이션 전반적인 설정과 빈을 포함. 이 파일은 전역적인 빈 정의 및 서비스 계층. 데이터 액세스 계층과 같은 애플리케이션 전반에 걸친 빈을 설정
        - servlet-context.xml
        : 서블릿 기반 웹 애플리케이션에서 사용되며. 주로 웹 계층과 관련된 빈들을 정의. 이 파일은 주로 웹 컴포넌트와 관련된 빈을 설정

  - 어노테이션 기반 설정
    - @Component : 일반적인 스프링 빈으로 사용
    - @Controller : Spring MVC 컨트롤러로 사용되는 클래스를 나타냄
    - @Service : 비즈니스 로직을 처리하는 서비스 클래스를 나타냄
    - @Repository : 데이터 액세스 객체(DAO)를 나타냄 

  - java Config 기반 설정
    - @Configuration : 클래스를 스프링의 Java 기반 설정 클래스로 지정
    - @Bean : @Configuration 어노테이션을 가진 클래스 내에서 메서드에 부여하여 해당 메서드가 스프링 빈을 생성하고 관리하도록 지정
  
  ### 의존성 자동주입
  > 객체 간의 관계를 설정하고, 한 객체가 다른 객체를 필요로 할 때, 컨테이너가 자동으로 필요한 객체를 주입하는 메커니즘을 의미

  - @Autowired: 의존성 주입을 자동으로 처리하는 어노테이션
- @Qualigier("빈이름"): 여러 개의 동일한 타입의 빈 중 특정 빈을 지정하여 주입할 때 사용하는 어노테이션
- @Component("빈이름"): 해당 클래스를 스프링 빈으로 등록하고, 빈의 이름을 명시적으로 지정하는 어노테이션. 이는 다른 ```@Component``` 어노테이션의 기반이 됨.

- ```@Pathvariable```을 사용시 2버전에선 굳이 명시하지 않아도 인식을 했으나 3버전부턴 명시해야함. 

## HTTP 요청 메시지

- HTTP 메시지의 헤더 정보에는 요청하는 리소스의 타입, 길이, 인코딩 방식 등의 정보가 포함될 수 있음.
- JAVA에서는 HttpURLConnection 클래스를 사용하여 HTTP 요청을 보낼 수 있음

### REST 방식

- 인터페이스 일관성 - 외부에서 호출 가능한 인터페이스가 제공되어야 함
- 무상태 - 호출한 클라이언트의 상태를 서버에서 저장하지 않음
- 캐시 처리 가능 - 보관된 데이터를 제공하는 방식으로 동작할 수 있음
- 계층화 - 데이터를 제공하는 서비스의 구조적인 제한이 없음, 인증이나 암호화 등을 자유롭게 추가가능

#### REST 가이드

- 자원의 식별 - 원하는 데이터를 찾을 수 있는 고유의 주소가 존재
- 메시지를 통한 리소스의 조작 - 클라이언트가 보내는 정보 안에는 자원 처리에 
- 자기 서술적 메시지 - 요청/전송하는 정보에 대한 추가적인 데이터가 포함되어야 함
- 하이퍼미디어 제약 - 외부에서 링크 등을 통해서 애플리케이션 내 자원들의 상태를 변경할 수 있어야 함

> null을 효율적 관리가능한 문법 Optional<>

- RestTemplate 
  - Spring에서 제공하는 간단한 HTTP 통신을 위한 클래스

- WebClient
  - 비동기적이고 리액티브한 방식으로 HTTP 요청을 보낼 수 있는 라이브러리

## 동기 & 비동기, 블로킹 & 논블로킹

||블로킹(Blocking)|논블로킹(Non-Blocking)|
|------|---|---|
|동기식|작업이 오나료될 때까지 기다리며 다른 작업을 하지 않음|작업이 완료될 때까지 가다리지만 다른 작업을 할 수 있음|
|비동기식|작업을 요청한 후 다른 작업을 하지 않음|작업을 요청한 후 다른 작업을 할 수 있음|

### 비동기
- 작업을 요천한 후 그 작업이 완료될 때까지 기다리지 않고, 다른 작업을 계속할 수 있는 방식
- 작업이 완료되면 콜백 함수나 이벤트를 통해 결과를 알려줌

### 논블로킹
- 작업을 요청할 때, 그 작업이 즉시 완료되지 않더라도 현재 작업을 멈추지 않고 다른 작업을 계속할 수 있는 방식
- 작업이 완료될 때까지 기다리지 않고 바로 다음 작업을 수행할 수 있음

## Thymeleaf

### 표현식

- ${} : 변수의 값 표현식
- #{} : 속성 파일 값 표현식
- @{} : URL 표현식
- *{} : 선택한 변수의 표현시그 th:object에서 선택한 객체에 접근

### 문법

- th:text : 텍스트를 표현할 때 사용
- th:each : 컬렉션을 반복해서 사용
- th:if : 조건이 true인 때만 표시
- th:unless : 조건이 false인 떄만 표시
- th:href : 이동 경로
- th:with : 변숫값으로 지정
- th:object : 선택한 객체로 지정
- th:value : 서버에서 가져온 값 나타내기

> @EnableJpaAuditing //날짜 자동 업뎃

## Mybatis

- 자바 언어를 기반으로 한 퍼시스턴스 프레임워크로, SQL 쿼리를 XML 파일 또는 애너테이션을 사용하여 정의하고 객체에 매핑하여 데이터베이스를 다루는 것을 용이

- application.properties
```
mybatis.type-aliases-package=hello.board.domain
mybatis.configuration.map-underscore-to-camel-case=true
logging.level.hello.board.repository.mybatis=trace
mybatis.mapper-locations=classpath:mapper/*.xml
```

- xml setting
```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="hello.board.repository.mybatis.PostMapper">

<!-- sql 관련 코드  -->

<sql id="boardColumns">
            idx,
            title,
            content,
            writer,
            view_cnt,
            notice_yn,
            secret_yn,
            delte_yn,
            insert_time,
            update_time,
            delte_time
    </sql>

    <insert id="insertBoard" parameterType="BoardDTO">
        INSERT INTO tb_board(
                <include refid="boardColumns"/>
        )VALUES (
                 #{idx},
                 #{title},
                 #{content},
                 #{writer},
                 0,
                 IFNULL(#{notice_yn},'N'),
                 IFNULL(#{secret_yn},'N'),
                 'N',
                 NOW(),
                 NULL,
                 NULL
        )
    </insert>

    <select id="selectBoardDetail" parameterType="Long" resultType="BoardDTO">
        SELECT 
            <include refid="boardColumns"/>
        FROM
            tb_board
        WHERE 
            delete_yn = 'N'
        AND
            idx = #{idx};
    </select>
    
    <update id="updateBoard" parameterType="BoardDTO">
        UPDATE tb_board
        SET
            update_time = NOW(),
            title = #{title},
            content = #{content},
            writer = #{writer},
            notice_yn = IFNULL(#{noticeYn},'N'),
            secret_yn = IFNULL(#{secretYn},'N')
        WHERE 
            idx =#{idx}
    </update>
    
    <update id="deleteBoard">
        UPDATE tb_board
        SET
            delete_yn = 'Y',
            delete_time = NOW()
        WEHRE 
            idx = #{idx}
    </update>
    
    <select id="selectBoardList" parameterType="BoardDTO" resultType="BoardDTO">
        SELECT
            <include refid="boardColumns"/>
        FROM
            tb_board
        WEHRE 
            delete_yn = 'N'
        ORDER BY
            notice_yn ASC,
            idx DESC,
            insert_time DESC
    </select>
    
    <select id="selectBoardToTalCount" parameterType="BoardDTO" resultType="int">
        SELECT
            COUNT(*)
        FROM
            tb_board
        WHERE 
            delete_yn = 'N'
    </select>

</mapper>
```

- useGeneratedKeys와 keyProperty 속성을 설정하여, insert 실행 후에 자동으로 증가된 키 값을 자겨올 수 있음
    > ```<insert id="insert" useGeneratedKeys="true" keyProperty="no">```


## JPA

- Java Persistence API의 약자로 자바의 ORM(Object Relational Mapping) 표준 스펙을 저dml
- JPA의 스펙은 자바의 객체와 데이터베이스를 어떻게 매핑하고 동작해야 하는지를 정의하고 있음

### 영속성 컨테스트

- JPA가 관리하는 엔티티 객체의 집합
- 엔티티 객체가 영속 컨텍스트에 들어오게 되면  JPA는 엔티티 객체의 매핑 정보를 가지고 DB에 반영함
- 엔티티 객체가 영속 컨텍스트에 들어오게 들어오게 되어 관리 대상이 되면 그 객체를 영속 객체라고 부름


## JWT

- '인증 및 권한'과 관련된 정보를 안전하게 전달하기 위한 JSON 형식의 암호화된 문자열
- 헤더, 페이로드, 시그니쳐로 구성
  - 헤더에 토큰의 종류와 암호화 알고리즘
  - 페이로드에는 전송할 정보
  - 시그니쳐에 헤더와 페이로드를 검증하기 위한 정보를 저장

### 구현

- 인증 : 로그인
- 인가 : JWT를 통한 경로별 접근 권한
- 회원가입

### JWT 인증 방식 시큐리티 동작 원리

- 회원가입 : 내부 회원 가입 로직은 세션 방식과 JWT 방식의 차이가 없다. 
- 로그인(인증) : 로그인 요청을 받은 후 세션 방식은 서버 세션이 유저 정보를 저장하지만 JWT 방식은 토큰을 생성하여 응답
- 경로 접근(인가) : JWT Filter를 통해 요청의 헤더에서 JWT를 찾아 검증을 하고 일시적 요청에 대한 Session을 생성

### JWT 필수 의존성

- JWT 토큰을 생성하고 관리하기 위해 JWT 의존성을 필수적으로 설정해야 함

- build.gradle 의존 설정
- 대부분 0.11.5로 구현이 되있지만 최신버전으로 진행
```
	implementation 'io.jsonwebtoken:jjwt-api:0.12.3'
    implementation 'io.jsonwebtoken:jjwt-impl:0.12.3'
    implementation 'io.jsonwebtoken:jjwt-jackson:0.12.3'
```

## Security

### SecurityConfig

```
@Configuration
@EnableWebSecurity
public class SecurityConfig {

  // 패스워드 암호화
  @Bean
  public BCryptPasswordEncoder bCryptPasswordEncoder() {
    return new BCryptPasswordEncoder();
  } 

  // HTTP 접근 설정
  @Bean
  public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {

    http.csrf((auth) -> auth.disable());
    http.formLogin((auth) -> auth.disable());
    http.httpBasic((auth) -> auth.disable());

    http.authorizeHttpRequests(((auth) -> auth
        .requestMatchers("/login", "/", "join").permitAll()
        .requestMatchers("/admin").hasRole("ADMIN")
        .anyRequest().authenticated()
        ));  
    
    http.sessionManagement((session) -> session
        .sessionCreationPolicy(SessionCreationPolicy.STATELESS)); 
    return http.build();
  } 
}
```

* 생성자를 주입받아서 데이터를 연결
```
package org.zerock.jwt.service;

import org.springframework.security.crypto.password.PasswordEncoder;
import org.springframework.stereotype.Service;
import org.zerock.jwt.dto.JoinDTO;
import org.zerock.jwt.repository.UserRepository;

@Service
public class JoinService {

  private final UserRepository userRepository;

  private final BCryptPasswordEncoder passwordEncoder;

  public JoinService(UserRepository userRepository, BCryptPasswordEncoder bpasswordEncoder) {
      this.userRepository = userRepository;
      this.bpasswordEncoder = bpasswordEncoder;
  }  

  public void joinProcess(JoinDTO dto) {
    String username = dto.getUsername();
    String password = dto.getPassword();

    Boolean isExist = userRepository.existsByUsername(username);
    if (isExist) {
      return;
    }

    UserEntity data = new UserEntity();
    data.setUsername(username);
    // 패스워드 암호화 주입
    data.setPassword(bpasswordEncoder.encode(password));
    data.setRole("ROLE_ADMIN");

    userRepository.save(data);
  }

}
```

### 스프링 시큐리티 필터 동작 원리

- 클라이언트의 요청이 여려개의 필터를 거쳐 DispatcherServlet으로 향하는 중간 필터에서 요청을 가로챈 후 검증을 진행

  - 클라이트 요청 -> 서블릿 필터 -> 서블릿 (컨트롤러)
  - Delegating Filter Proxy : 서블릿 컨테이너에 존재하는 필터 체인에 DelegatingFilter를 등록한 뒤 모든 요청을 가로챈다.
    - Servlet <-> Filter <-> DelegatingFilterProxy(Bean Filter) <-> Client

  - 서블릿 필터 체인의 DelegatingFilter - Security 필터 체인 (내부 처리 후) -> 서블릿 필터 체인의 DlelegatingFilter 

  - Servlet <-> Filter <-> DelegatingFilterProxy(Bean Filter) <-> Client   ---->> SecurityFilterChain(/api/**)

- security config
```
@Configuration
@EnableWebSecurity
public class SecurityConfig {

  private final AuthenticationConfiguration authenticationConfiguration;

  public SecurityConfig(AuthenticationConfiguration authenticationConfiguration) {
    this.authenticationConfiguration = authenticationConfiguration;
  }

  @Bean
  AuthenticationManager authenticationManager(AuthenticationConfiguration configuration) throws Exception {
    return configuration.getAuthenticationManager();
  }

  @Bean
  public BCryptPasswordEncoder bCryptPasswordEncoder() {
    return new BCryptPasswordEncoder();
  } 

  @Bean
  public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {

    http.csrf((auth) -> auth.disable());
    http.formLogin((auth) -> auth.disable());
    http.httpBasic((auth) -> auth.disable());

    //인가 설정
    http.authorizeHttpRequests(((auth) -> auth
        .requestMatchers("/login", "/", "join").permitAll()
        .requestMatchers("/admin").hasRole("ADMIN")
        .anyRequest().authenticated()
        )); 
    
    http.addFilterAt(new LoginFilter(authenticationManager(authenticationConfiguration)), UsernamePasswordAuthenticationFilter.class);

    http.sessionManagement((session) -> session
        .sessionCreationPolicy(SessionCreationPolicy.STATELESS)); 
    return http.build();
  } 
}
```

### 로그인 요청 받기 : 커스텀 UsernamePasswordAuthentication

- 로그인 필터
```
public class LoginFilter extends UsernamePasswordAuthenticationFilter {

  private final AuthenticationManager authenticationManager;

  public LoginFilter(AuthenticationManager authenticationManager) {
    this.authenticationManager = authenticationManager;
  }

  @Override
  public Authentication attemptAuthentication(HttpServletRequest request, HttpServletResponse response)
      throws AuthenticationException {
    
    String username = obtainUsername(request);
    String password = obtainPassword(request);

    UsernamePasswordAuthenticationToken authToken = new UsernamePasswordAuthenticationToken(username, password);

    return authenticationManager.authenticate(authToken);
  }

  @Override
  protected void successfulAuthentication(HttpServletRequest request, HttpServletResponse response, FilterChain chain,
      Authentication authResult) throws IOException, ServletException {

    super.successfulAuthentication(request, response, chain, authResult);
  }

  @Override
  protected void unsuccessfulAuthentication(HttpServletRequest request, HttpServletResponse response,
      AuthenticationException failed) throws IOException, ServletException {
        
    super.unsuccessfulAuthentication(request, response, failed);
  }
}
```

### DB기반 로그인 검증 로직

```
public interface UserRepository extends JpaRepository<UserEntity, Integer> {
  
  Boolean existsByUsername(String username);
  
  // username을 받아 DB 테이블에서 회원을 조회하는 메소드 작성
  UserEntity findByUsername(String username);

} 
```

- UserDetailsService 커스텀 구현
```
@Service
public class CustomUserDetailsService implements UserDetailsService  {

  private final UserRepository userRepository;

  public CustomUserDetailsService(UserRepository userRepository) {
    this.userRepository = userRepository;
  }

  @Override
  public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {
   
    UserEntity userData = userRepository.findByUsername(username);
    
    if(userData != null) {
      return new CustomUserDetails(userData);
    }
    
    return null;
  }
}
```


- CustomUserDetails
```
public class CustomUserDetails implements UserDetails {

  private final UserEntity userEntity;

  public CustomUserDetails(UserEntity userEntity) {
    this.userEntity = userEntity;
  }

  @Override
  public Collection<? extends GrantedAuthority> getAuthorities() {

    Collection<GrantedAuthority> collectors = new java.util.ArrayList<>();
    collectors.add( new GrantedAuthority() {
      @Override
      public String getAuthority() {

        return userEntity.getRole();
      }
    });

    return collectors;
  }

  @Override
  public String getPassword() {

    return userEntity.getPassword();
  }

  @Override
  public String getUsername() {
  
    return userEntity.getUsername(); 
  }

  @Override
  public boolean isAccountNonExpired() {
    return true;
  }

  @Override
  public boolean isAccountNonLocked() {
    return true;
  }

  @Override
  public boolean isCredentialsNonExpired() {
    return true;
  }

  @Override
  public boolean isEnabled() {
    return true;
  }
}
```

### JWT 발급 및 검증 클래스

- JWT 발급과 검증
  - 로그인시 -> 성공 -> JWT 발급
  - 접근시 -> JWT 검증


- JWT는 Header, Payload, Signature  구조
  - Header
    - JWT임을 명시
    - 사용된 암호화 알고리즘
  - Payload
    - 정보
  - Signature
    - 암호화알고리즘(BASE64(Header)) + (BASE64(Payload)) + 암호화키


#### JWT 암호화 방식

- 암호화 종류
  - 양방향
    - 대칭키 : 이 프로젝트는 양방향 대칭키 방식 사용 : HS256
    - 비대칭키

#### 암호화 키 저장

- 암호화 키는 하드코딩 방식으로 구현 내부에 탑재하는 것을 지양하기 떄문에 변수 설정 파일에 저장

- application.properties
```
spring.jwt.secret=vmfhaltmskdlstkfkdgodyroqkfwkdbalaaaaaaaaaaaaaaaabbbbb
```

#### JWTUtil
- 토큰 Payload에 저장될 정보
  - 

## springboot db 연동

### DB 연동

```
spring.datasource.url=jdbc:mysql://localhost:3306/jwt
spring.datasource.username=root
spring.datasource.password=1234
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
```

### Hibernate 설정

```
spring.jpa.hibernate.ddl-auto=none
spring.jpa.hibernate.naming.physical-strategy=org.hibernate.boot.model.naming.PhysicalNamingStrategyStandardImpl
```



