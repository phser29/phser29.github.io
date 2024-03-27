---
layout: single
title: "spring join"
categories: java
tag: spring_shop
toc: true
---

# 프로젝트 소개
- 프로젝트 이름: Spring 쇼핑몰 프로젝트
- 프로젝트 기술: java, spring, Mysql, mybatis, jquery, ajax
- 프로젝트 인원: 1명
- 프로젝트 선정 이유: 코로나 이후에 핫해진 쇼핑몰 분석

# 회원가입

- BOOK_MEMBER table

```
CREATE TABLE BOOK_MEMBER(
  memberId VARCHAR(50),
  memberPw VARCHAR(100) NOT NULL,
  memberName VARCHAR(30) NOT NULL,
  memberMail VARCHAR(100) NOT NULL,
  memberAddr1 VARCHAR(100) NOT NULL,
  memberAddr2 VARCHAR(100) NOT NULL,
  memberAddr3 VARCHAR(100) NOT NULL,
  adminCk int NOT NULL,
  regDate DATE NOT NULL,
  money int NOT NULL,
  point int NOT NULL,
  PRIMARY KEY(memberId)
);
```

- 회원가입 query

```

```

- id 중복 체크

```

```