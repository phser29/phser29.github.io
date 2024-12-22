---
layout: single
title: "springboot"
categories: spring
tag: spring
toc: true
--- 

# java springboot


## JPA

- yml h2 DB 설정
```
  datasource:
    url: jdbc:h2:mem:testdb
  h2:
    console:
      enabled: true
```

- 직열화
  - 자바 시스템 내부에서 사용되는 개체를 외부에서 사용하도록 데이터를 변환하는 작업
- 역직렬화
  - 외부에서 사용하는 데이터를 자바의 객체 형태로 변환하는 작업

- given-when-then
  - Given : 블로그 글 추가에 필요한 요청 객체를 만듬 
  - When : 블로그 글 추가 API에 요청을 보냅니다. 이때 요청은 JSON이며 given젤에서 미리 만들어 둔 객체를 요청 본문으로 함께 보냄
  - Then : 응답 코드가 201인지 확인 Blog를 전체 조회해 크기가 1인지 확인하고,  실제로 저장된 데이터와 요청 값을 비교

## 영속성 컨텍스트
> JPA의 중요한 특징 중 하나로, 엔티티를 관리하는 가상의 공간

- 1차 케시
- 쓰기 지연
- 변경 감지
- 지연 로딩

## JPA 설정

- spring.jpa.hibernate.ddl-auto 설정
  - create : 기존 테이블 삭제 후 다시 생성(DROP + UPDATE)
  - create-drop : create와 같으나 종료 시점에 테이블 DROP
  - update : 변경분만 반영(개발 환경에서만 사용할 것)
  - validate : 엔티티와 테이블이 정상적인지만 확인
  - none : DDL 처리에 관여하지 않음

- spring.jpa.properties.hibernate.format_sql=true
  - 스프링 부트가 실행되면서 사용하는 SQL들의 포맷팅을 의미하는데 true인 경우 줄바꿈 처리가 되서 알아보기 쉬움

- spring.jpa.show-sql=true
  - 실행 과정에서 만들어지는 SQL을 출력할 것인지를 의미

# JWT

- '인증 및 권한'과 관련된 정보를 안전하게 전달하기 위한 JSON 형식의 암호화된 문자열
- 헤더, 페이로드, 시그니쳐로 구성
  - 헤더에 토큰의 종류와 암호화 알고리즘
  - 페이로드에는 전송할 정보
  - 시그니쳐에 헤더와 페이로드를 검증하기 위한 정보를 저장


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

> @EnableJpaAuditing //날짜 자동 업뎃

## REST 방식

- 인터페이스 일관성 - 외부에서 호출 가능한 인터페이스가 제공되어야 함
- 무상태 - 호출한 클라이언트의 상태를 서버에서 저장하지 않음
- 캐시 처리 가능 - 보관된 데이터를 제공하는 방식으로 동작할 수 있음
- 계층화 - 데이터를 제공하는 서비스의 구조적인 제한이 없음, 인증이나 암호화 등을 자유롭게 추가가능

### REST 가이드

- 자원의 식별 - 원하는 데이터를 찾을 수 있는 고유의 주소가 존재
- 메시지를 통한 리소스의 조작 - 클라이언트가 보내는 정보 안에는 자원 처리에 
- 자기 서술적 메시지 - 요청/전송하는 정보에 대한 추가적인 데이터가 포함되어야 함
- 하이퍼미디어 제약 - 외부에서 링크 등을 통해서 애플리케이션 내 자원들의 상태를 변경할 수 있어야 함

