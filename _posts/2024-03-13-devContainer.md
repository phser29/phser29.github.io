---
layout: single
title: "devContainer"
categories: other
tag: other
toc: true
---

# 데브 기본세팅

- Dev Containers: Add Dev Container Configuration Files...
- Dev containers: Rebuild Without Cache and Reopen in Container
- Dev Containers: Rebuild Container Without Cache

## devcontainer.json 세팅
  - 알맞게 변경해서 사용
```
{
  "name": "Devcontainer test",
  "dockerComposeFile": "docker-compose.yml",
  "service": "app",
  "workspaceFolder": "/workspaces/devcontainer_test",
  "features": {
    "ghcr.io/devcontainers-contrib/features/zsh-plugins:0": {
      "plugins": "",
      "omzPlugins": "https://github.com/zsh-users/zsh-autosuggestions",
      "username": "vscode"
    },
    "github-cli": "latest"
  },
  "forwardPorts": [25432],
  "postCreateCommand": "sh .devcontainer/startup.sh",
  "customizations": {
    "vscode": {
      "extensions": [
        "dbaeumer.vscode-eslint",
        "eamodio.gitlens",
        "esbenp.prettier-vscode",
        "octref.vetur",
        "Orta.vscode-jest",
        "ritwickdey.LiveServer",
        "bradlc.vscode-tailwindcss",
        "mechatroner.rainbow-csv",
        "vmware.vscode-boot-dev-pack",
        "vscjava.vscode-java-pack",
        "vscjava.vscode-lombok",
        "vscjava.vscode-gradle",
        "bierner.markdown-mermaid"
      ],
      "settings": {
        "files.eol": "\n",
        "editor.tabSize": 4,
        "editor.renderWhitespace": "all",
        "typescript.validate.enable": false,
        "eslint.alwaysShowStatus": true,
        "editor.formatOnSave": true,
        "eslint.workingDirectories": [{ "mode": "auto" }],
        "editor.codeActionsOnSave": {
          "source.fixAll.eslint": true
        },
        "spring-boot.ls.java.vmargs": [
          "-Xmx512M"
        ],
        "remote.localPortHost": "allInterfaces",
        "git.detectSubmodulesLimit": 70,
        "editor.tabCompletion": "on",
        "java.format.settings.profile": "GoogleStyle"
      }
    }
  },
  "remoteUser": "vscode"
}
```

## docker-compose 세팅
- mysql db로 변경 실행에 이슈가 있음
```
version: '3.8'
volumes:
  postgres-data:
services:
  app:
    container_name: devcontainer-test
    build: 
      context: .
      dockerfile: Dockerfile
    volumes:
      - ../..:/workspaces:cached
    command: sleep infinity
    network_mode: host
  db:
    container_name: mysqldb
    image: mysql:8.0
    restart: always
    volumes:
      - ./data/mysql/:/var/lib/mysql
    environment:
      MYSQL_ROOT_PASSWORD: your_root_password
      MYSQL_DATABASE: testdb
      MYSQL_USER: your_user
      MYSQL_PASSWORD: your_password
    network_mode: host
```

## docker 세팅

```
FROM mcr.microsoft.com/devcontainers/java:1-17-bullseye

# 시간 및 날짜 설정
ENV TZ Asia/Seoul

RUN apt-get update && \
    apt-get -y install wget curl && \
    echo "DONE"
```

## shartup.sh

```
sed -i 's/codespaces/agnoster/' ~/.zshrc && \
sed -i'' -r -e "/prompt_hg/a\  prompt_newline" ~/.oh-my-zsh/themes/agnoster.zsh-theme && \
echo $(pwd) && \
./gradlew clean && \ 
./gradlew build --refresh-dependencies && \
echo DONE
```

