---
layout: single
title: "reactCss"
categories: javaScript
tag: react
toc: true
---

# react css

- 리액트로도 부트스트랩 많이 이용
- index.html
> < link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-EVSTQN3/azprG1Anm3QDgpJLIm9Nao0Yz1ztcQTwFspd3yD65VohhpuuCOmLASjC" crossorigin="anonymous"> 추가

- jsx문은 React.createElement 함수 호출코드로 전환
- class -> className, for -> htmlFor

- @import 규칙은 웹 안전 글꼴을 사용해야 한다.

- fontsource : 구글 글꼴과 같은 오픈소스 웹 안전 글꼴을 패키지 형태
> npm i @fontsource/스테이크-표기법-글꼴명

## PostCSS

- 루비로 만든 Sass/SCSS
- autoprefixer : 밴더 접두사 문제를 해결 해주는 플러그인

## 테일윈드 CSS

- 유틸리티 최우선을 가치로 만듬

-설치
> npm i -D postcss autoprefixer tailwindcss

- 구성 파일 만들기
> npx tailwindcss init -p

-부트스트랩과 비슷한 css 컴포넌트를 제공하는 daisyui 플러그인
> npm i -D daisyui