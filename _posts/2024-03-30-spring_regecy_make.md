---
layout: single
title: "spring_regecy_make"
categories: java
tag: spring
toc: true
---

# spring_regecy_make

- Dynamic 프로젝트 생성

- web 생성 -> maven 프로젝트로 전환

- spring core, context, webmvc, tx, test 생성
- WEB-INF에서 root-context, servlet-context 생성
 - root-context: context, servlet-context: context, mvc

 - spring-framework/docs 세팅 해야됨 index로 가서 ctrl+ f: xsi

- web.xml 설정

```
    <listener>
        <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
   	</listener>

    <context-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>/WEB-INF/serv-context.xml</param-value>
    </context-param>

    <servlet>
        <servlet-name>app</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>/WEB-INF/servlet-context.xml</param-value>
        </init-param>
        <load-on-startup>1</load-on-startup>
    </servlet>

    <servlet-mapping>
        <servlet-name>app</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>
```

- 참고
> https://velog.io/@seowj0710/Spring-servlet-context.xml-application-context.xml-web.xml-%EC%84%A4%EC%A0%95


## Log4jdbc-log4je

```
<!-- https://mvnrepository.com/artifact/org.bgee.log4jdbc-log4j2/log4jdbc-log4j2-jdbc4 -->
<dependency>
    <groupId>org.bgee.log4jdbc-log4j2</groupId>
    <artifactId>log4jdbc-log4j2-jdbc4</artifactId>
    <version>1.16</version>
</dependency>
```

- resources에 log4jdbclog4jdbc.log4j2 properties파일 생성

> log4jdbc.spylogdelegator.name=net.sf.log4jdbc.log.slf4j.Slf4jSpyLogDelegator

- 설정 후 // Dynamic web project에서는 사용불가

```
<bean id="hikariConfig" class="com.zaxxer.hikari.HikariConfig">
	<property name="driverClassName" value="net.sf.log4jdbc.sql.jdbcapi.DriverSpy"></property>
	<property name="jdbcUrl" value="jdbc:log4jdbc:mariadb://localhost:3307/shop"></property>
	<property name="username" value="root"></property>
	<property name="password" value="1234"></property>
</bean>
```


# 쇼핑몰 회원가입

