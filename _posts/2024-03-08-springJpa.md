---
layout: single
title: "JPA"
categories: java
tag: spring
toc: true
---

# 영속성의 이해

# JPA 설정

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



