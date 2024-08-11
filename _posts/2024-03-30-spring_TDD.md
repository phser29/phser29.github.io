---
layout: single
title: "spring_TDD"
categories: java
tag: spring
toc: true
---

# TDD

- 스프링부트 스타터 테스트 목록
    - JUnit : 자바 프로그래밍 언어용 단위 테스트 프레임워크
    - Spring Boot Test : 스프링 부트 애플리케이션을 위한 통합 테스트 지원
    - AssertJ : 검증문인 어설션을 작성하는 데 사용되는 라이브러리
    - Hamcrest : 표현식을 이해하기 쉽게 만드는 데 사용되는 Matcher 라이브러리
    - Mamcrest : 표현식을 이해하기 쉽게 만드는 데 사용된느 Matcher 라이브러리
    - Mockito : 테스트에 사용할 가짜 객체인 목 객체를 쉽게 만들고, 관리하고, 검증할 수 있게 지원하는 테스트 프레임워크
    - JSONNassert : JSON용 어설션 라이브러리
    - JsonPath : JSON 데이터에서 특정 데이터를 선택하고 검색하기 위한 라이브러리

## JUnit

- 단위 테스트
    - 작성한 코드가 의도대로 작동하는지 작은 단위로 검증하는 것을 의미

- 특징
    - 테스트 방식을 구분할 수 있는 애너테이션을 제공
    - @Test 애너테이션으로 메서드를 호출할 때마다 새 인스턴스를 생성, 독립 테스트 가능
    - 예상 결과를 검증하는 어설션 메서드 제공
    - 사용 방법이 단순, 테스트 코드 작성 시간이 적음
    - 자동 실행, 자체 결과를 확인하고 즉각적인 피드백을 제공

- 어노테이션
    - @BeforAll : 전체 테스트를 시작하기 전에 처음으로 한 번만 실행
    - @BeforeEach : 테스트 케이스를 시작하기 전에 매번 실행
    - @AfterAll : 전체 테스트를 마치고 종료하기 전에 한 번만 실행, 전체 테스트 실행 주기에서 한번만 호출되어야 하므로 메서드를 static으로 선언해야 함.
    - @AfterEach : 각 테스트 케이스를 종료하기 전 매번 실행

-  AssertJ
    - assertThat()
        - isEqualTo() : A값과 같은지 검증
        - isNotEqualTo() : A값과 다른지 검증
        - contains : A 값을 포함하는지 검증
        - doesNotContain() : A 값을 포함하지 않는지 검증
        - startsWith : 접두사가 A인지 검증
        - endsWith() : 접미사가 A인지 검증
        - isNotEmpty() : 비어 있는 값인지 검증
        - isPositive() : 양수인지 검증
        - isNegative() : 음수인지 검증
        - isGreaterThan() : 1보다 큰 값인지 검증
        - isLessThan() : 1보다 작은 값인지 검증



