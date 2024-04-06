---
layout: single
title: "알고리즘 실습"
categories: java
tag: other
toc: true
--- 

# 알고리즌 실습

- 문제를 해결하기 위한 것으로, 명확하게 정의되고 순서가 있는 유한 개의 규칙으로 이루어진 집합

## 최댓값

- 프로그램의 실행 흐름을 변경하는 if문을 선택구조라고 함.

```
public class Max3 {
	public static void main(String[] args) {
		Scanner stdIn = new Scanner(System.in);
		
		System.out.println("세 정수의 최댓값");
		System.out.println("a의 값: ");
		int a = stdIn.nextInt();
		System.out.println("b의 값: ");
		int b = stdIn.nextInt();
		System.out.println("c의 값: ");
		int c = stdIn.nextInt();
		
		int max = a;
		
		if(b > max) {
			max = b;
		} 
		if(c > max) {
			max = c;
		}
		
		System.out.println("최댓값은 " + max + "입니다.");
		
		stdIn.close();
	}
}
```

## 중앙값

- 퀵 정렬을 이용

```
public class Median {
	
//	static int med3(int a, int b, int c) {
//		if(a >= b) {
//			if(b >= c) {
//				return b;
//			} else if(a <= c) {
//				return a;
//			} else {
//				return c;
//			}
//		} else if(a > c) {
//			return a;
//		} else if(b > c) {
//			return c;
//		} else {
//			return b;
//		}
//	}
	
	static int med3(int a, int b, int c) {
		if((b >= a && c <= a) || (b <= a && c >= a)) {
			return a;
		} else if((a > b && c < b) || (a < b && c > b)) {
			return b;
		}
		return c;
	}
	
	public static void main(String[] args) {
		Scanner scan = new Scanner(System.in);
		
		System.out.println("세 정수의 중앙값을 구합니다.");
		System.out.println("a의 값: ");
		int a = scan.nextInt();
		System.out.println("b의 값: ");
		int b = scan.nextInt();
		System.out.println("c의 값: ");
		int c = scan.nextInt();
		
		System.out.println("중앙값은 " + med3(a, b, c) + "입니다.");
		
		scan.close();
	}
}
```

# 반복

## 1부터 n까지의 정수 합 구하기

```

```