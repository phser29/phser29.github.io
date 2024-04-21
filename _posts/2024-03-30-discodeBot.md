---
layout: single
title: "discode_bot"
categories: javaScript
tag: other
toc: true
---

# discode bot

- discode 매니저 설정
  - 디스코드 개발자 포털로 접속
  - applications 옵션 클릭
  - 로그인
  - new Application 클릭
  - 봇 이름 설정 후 생성
  - 봇 추가 됬으면 토큰 복사
  - OAuth2 URL Generator bot 클릭 복사
  - 초대전 미리 서버 추가 후 매니저 추가

## 문법(js)

- 디스코드 라이브러리 성치

```
npm install discord.js
npm install --save-dev eslint
```

- 프로젝트에 .eslintrc.json 파일 생성

```
{
	"extends": "eslint:recommended",
	"env": {
		"node": true,
		"es6": true
	},
	"parserOptions": {
		"ecmaVersion": 2021
	},
	"rules": {
		"arrow-spacing": ["warn", { "before": true, "after": true }],
		"brace-style": ["error", "stroustrup", { "allowSingleLine": true }],
		"comma-dangle": ["error", "always-multiline"],
		"comma-spacing": "error",
		"comma-style": "error",
		"curly": ["error", "multi-line", "consistent"],
		"dot-location": ["error", "property"],
		"handle-callback-err": "off",
		"indent": ["error", "tab"],
		"keyword-spacing": "error",
		"max-nested-callbacks": ["error", { "max": 4 }],
		"max-statements-per-line": ["error", { "max": 2 }],
		"no-console": "off",
		"no-empty-function": "error",
		"no-floating-decimal": "error",
		"no-inline-comments": "error",
		"no-lonely-if": "error",
		"no-multi-spaces": "error",
		"no-multiple-empty-lines": ["error", { "max": 2, "maxEOF": 1, "maxBOF": 0 }],
		"no-shadow": ["error", { "allow": ["err", "resolve", "reject"] }],
		"no-trailing-spaces": ["error"],
		"no-var": "error",
		"object-curly-spacing": ["error", "always"],
		"prefer-const": "error",
		"quotes": ["error", "single"],
		"semi": ["error", "always"],
		"space-before-blocks": "error",
		"space-before-function-paren": ["error", {
			"anonymous": "never",
			"named": "never",
			"asyncArrow": "always"
		}],
		"space-in-parens": "error",
		"space-infix-ops": "error",
		"space-unary-ops": "error",
		"spaced-comment": "error",
		"yoda": "error"
	}
}
```

- 모듈 연결

> const Discord = require("discord.js");

- 디코 클라연결

> const client = new Discord.Client({ intents: ["GUILDS", "GUILD_MESSAGES"] });

- 클라 연결

``` 
client.on()

// 메시지 연결
on('message' (msg) => {
  msg.content 
})

//메시지 출력
msg.reply()
```

- 중복방지 

> if(msg.author.bot) return;

- 로그인으로 인한 봇으로 채팅 입력 방지

> if(msg.author.id === client.user.id) return;



