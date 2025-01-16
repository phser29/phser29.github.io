---
layout: single
title: "springboot shop"
categories: java
tag: springboot_shop
toc: true
---

# 프로젝트 소개
- 프로젝트 이름: Spring 쇼핑몰 프로젝트
- 프로젝트 기술: java, springboot, MariaDB, mybatis, jsp, jquery, ajax, maven
- 프로젝트 인원: 1명
- 프로젝트 선정 이유: 코로나 이후에 핫해진 쇼핑몰 분석

##  login (로그인)

### request

- 아이디: String
- 비밀번호: String

### response
- 성공
  - 코드: ok
  

## signUp (회원가입)

### request
- 아이디: String
- 비밀번호: String
- 비밀번호 확인: String
- 이메일주소: String
- 주소: String

### response
- 성공
  - 코드: ok
  - 메시지: success
- 실패
  - http status - 401(unauthorized)
  코드: sf, message: sign in failed
  - Http Status - 500 (Internal Server Error)

- DataBase Error
  - Http Status - 400 (Bad Request)
  - code: "DE"
  - message: "Datebase Error"

