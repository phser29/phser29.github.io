---
layout: single
title: "springboot_TDD_order"
categories: java
tag: springboot_TDD_order
toc: true
---

# TDD 방식 주문 개발

## 의존 주입

```
	implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
	implementation 'org.springframework.boot:spring-boot-starter-web'
	compileOnly 'org.projectlombok:lombok'
	runtimeOnly 'com.h2database:h2'
	annotationProcessor 'org.projectlombok:lombok'
	testImplementation 'org.springframework.boot:spring-boot-starter-test'
```

## 자주 사용되는 TDD 문법

- Assert : 인수를 검증하고 조건에 맞지 않는 경우 IllegalArgumentException 또는 IllegalStateException를 발생
	- doesNotContain : 해당 문자열안에 subString이 포함되어있다면 ERROR
	- hasLength :	null이 아니고 비어있는 문자열("")이 아니어야함
	- hasText :	null이 아니고 공백이 아닌 유효한 문자가 존재하는 문자열이어야함
	- isTrue : 해당 조건식이 참이면 OK
	- isNull :	해당 객체가 null이면 OK
	- notNull :	해당 객체가 not null이면 OK
	- notEmpty : 해당 Array가 null이 아니고, 1개 이상의 Element를 가지고 있다면 OK
	- noNullElements : 해당 Array에 null인 객체가 없다면 OK
	- state	해당 조건식이 참이면 OK


- Test 상황에서 사용되는 어노테이션
	- @BeforeAll
		- 해당 테스트 클래스를 초기화할 때 딱 한번 수행되는 메서드
		- 메서드 시그니쳐는 static 으로 선언
	- @BeforeEach : 테스트 메서드 실행 이전에 수행
	- @AfterAll : 

## 