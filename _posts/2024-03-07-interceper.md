---
layout: single
title: "인터셉터 적용"
categories: java
tag: spring
toc: true
---

# 로그인, 관리자 메서드 인터셉터 적용

- 세션 체크 로직처럼 웹을 실행하기 위한 핵심 로직은 아니지만 반드시 필요한 로직들을 한 번의 작성으로
- 일괄적으로 관리해 줄 수 있도록 해주는 수단으로써 Interceptor가 있음 
- 이 Interceptor는  Controller를 호출하기 전과 후에 요청과 응답을 참조하거나 가공할 수 있는 일종의 필터

## 인터셉터란
- 컨트롤러(Controller)의 '핸들러(Handler)'를 호출하기 전과 후에 요청과 응답을 참조하거나 가공할 수 있는 일종의 필터

- 스프링에서 제공해주는 HandlerInterceptor 인터페이스와 HandlerInterceptorAdapter 추상 클래스에 정의되어 있는 메서드는 
- preHandle(), postHandle(), afterCompletion() 3가지. 

가. preHandle()

- 컨트롤러가 호출되기 전에 실행됩니다.
-  컨트롤러가 실행 이전에 처리해야 할 작업이 있는 경우 혹은 요청정보를 가공하거나 추가하는 경우에 사용합니다.
- 실행되어야 할 '핸들러'에 대한 정보를 인자 값으로 받기 때문에 '서블릿 필터'에 비해 보다 세밀하게 로직을 구성할 수 있습니다.
- 리턴 값이 boolean입니다. ture를 리턴하게 된다면 preHandle() 실행 후 핸들러에 접근을 합니다. false를 리턴하게 되면 작업을 중단하기 때문에 컨트롤러와 남은 
- 인터셉트가 실행되지 않습니다.
 
나. postHandle()

- 핸들러가 실행은 완료되었지만 아직 View가 생성되기 이전에 호출됩니다.
- ModelAndView 타입의 정보가 인자 값으로 받습니다. 따라서 Controller에서 View에 정보를 전달하기 위해 작업한 Model 객체의 정보를 참조하거나 조작할 수 있습니다.
- preHandle()에서 리턴 값이 false인 경우 실행되지 않습니다.
- 적용 중인 interceptor가 여러 개인 경우 preHandle()는 역순으로 호출됩니다.
- 비동기적 요청 처리 시에는 처리되지 않는다.
 
다. afterCompletion()

- 모든 View에서 최종 결과를 생성하는 일을 포함한 모든 작업이 완료된 후에 실행됩니다.
- 요청 처리 중에 사용한 리소스를 반환해주기 적당한 메서드입니다.
- preHandle()에서 리턴 값이 false인 경우 실행되지 않습니다.
- 적용 중인 interceptor가 여러 개인 경우 preHandle()는 역순으로 호출됩니다.
- 비동기적 요청 처리 시에는 호출되지 않습니다.

```
	//라이브러리 추가
  <dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-web</artifactId>
    <version>${org.springframework-version}</version>
  </dependency>

	// 서블릿 적용 인터셉터 적용
  <interceptors>
    <interceptor>
        <mapping path="/member/login.do"></mapping>
        <beans:bean id="loginIntreceptor" class="com.vam.interceptor.LoginInterceptor"></beans:bean>
    </interceptor>
    <interceptor>
        <mapping path="/admin/**"></mapping>
        <beans:bean id="AdminIntreceptor" class="com.vam.interceptor.AdminInterceptor"></beans:bean>
    </interceptor>
  </interceptors>

  // 인터셉터 클래스 작성후 세션 적용
	public class AdminInterceptor implements HandlerInterceptor {
	
	@Override
		public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler)
				throws Exception {
			
			HttpSession session = request.getSession();
			
			MemberVO lvo = (MemberVO)session.getAttribute("member");
			
			if(lvo == null || lvo.getAdminCk() == 0) {
				response.sendRedirect("/main");
				return false;
			}
		
			return true;
		}
	}
```




