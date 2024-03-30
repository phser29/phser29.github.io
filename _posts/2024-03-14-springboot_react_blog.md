---
layout: single
title: "springboot_react_blog"
categories: java
tag: springboot_react
toc: true
---

# 프로젝트 소개
- 프로젝트 이름: springboot react blog 프로젝트
- 프로젝트 기술: java, springboot, mysql, jpa, react
- 프로젝트 인원: 1명
- 프로젝트 선정 이유: springboot와 react 결합 정도 분석

## 중요사항

- 프록시 설정(포트가 다름)
> npm install http-proxy-middleware --save

- 경로

```
src/main/fronted/src/setupProxy.js

const { createProxyMiddleware } = require('http-proxy-middleware');

module.exports = function(app) {
  app.use(
    '/api',
    createProxyMiddleware({
      target: 'http://localhost:8080',	// 서버 URL or localhost:설정한포트번호
      changeOrigin: true,
    })
  );
};
```

# login(로그인), 

## request 
- 이메일주소: String
- 비밀번호: String

## response
- 성공: 코드: su, 메시지: success
- 실패: 
  - http status - 401 (unauthorized) 코드: sf, message: sign in failed
  - http Status - 500 (Internal Server Error) 

# join (회원가입)

## input
- email: String
- password: String
- nickname: String
- telNumber: String
- address: String
- addressDetail: String

# weeklyTop3 List (주간 상위 3 게시물 리스트)

# currentList (최신 게시물 리스트)

# popularWordList (인기 검색어 리스트)

# searchList (검색 게시물 리스트)

# relativeWordList (관련 검색어 리스트)

# boardDetail (게시물 상세 보기)

# favoriteList (좋아요 리스트)

# putFavorite (좋아요 기능)

# commentList (댓글 리스트)

# postComment (댓글 쓰기)

# boardDelete (댓글 삭제)

# boardWrite (게시물 쓰기)

# boardUpdate (게시물 수정)

# getUser (유저 정보)

# userBoardList (특정 유저 게시물 리스트)

# getFile (파일 불러오기)