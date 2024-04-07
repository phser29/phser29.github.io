---
layout: single
title: "알고리즘 실습"
categories: java
tag: other
toc: true
--- 

# 알고리즘 실습

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
public class SumWhile {
	public static void main(String[] args) {
		Scanner scan = new Scanner(System.in);
		
		System.out.println("1부터 n까지의 합을 구합니다.");
		System.out.println("n의 값: ");
		int n = scan.nextInt();
		
		int sum = 0;
		int i = 0;
		
		while(i <= n) {
			sum += i;
			i++;
		}
		
		System.out.println("1부터 " + n + "까지의 합은 " + sum + "입니다.");
		
		scan.close();
	}
}
```

## 양수만 입력하기

```
public class SumForPos {
	public static void main(String[] args) {
		Scanner scan = new Scanner(System.in);
		int n;
		
		System.out.println("1부터 n까지의 합을 구합니다.");
		
		do {
			System.out.println("n의 값: ");
			n = scan.nextInt();
		}while(n <= 0);
		
		int sum = 0;
		for(int i=0; i<=n; i++) {
			sum += i;
		}
		
		System.out.println("1부터 " + n + "까지의 합은 " + sum + "입니다.");
		
		scan.close();
	}
}
```

## 구조적 프로그래밍

- 하나의 입구와 하나의 출구를 가진 구성 요소만을 계층적으로 배치하여 프로그램을 구성하는 방법

```
public class Digits {
	public static void main(String[] args) {
		Scanner scan = new Scanner(System.in);
		int no;
		
		System.out.println("2자리의 정수를 입력하세요."); 
		
		do {
			System.out.println("입력: ");
			no = scan.nextInt();
		} while(no < 10 || no > 99);
		
		System.out.println("변수 no의 값은 " +no+ "가 되었습니다.");
		
		scan.close();
	}
}
```

- 단축 평가
	- 논리 연산의 식 전체를 평가한 결과가 왼쪽 피연산자의 평가 결과만으로 정확해지는 경우 오른쪽 피연산자의 평가를 수행하지 않는다.

- 드모르간 법칙
	- 각 조건을 부정하고 논리곱을 논리합으로, 논리합을 논리고븡로 바꾸고 다시 전체를 부정하면 원래의 조건이 같다.

## 다중 루프

```
public class Multi99Table {
	public static void main(String[] args) {
		System.out.println("---곱셈표---");
		
		for(int i=1; i<=9; i++) {
			for(int j=1; j<=9; j++) {
				System.out.printf("%3d", i*j);
			}
			System.out.println();
		}
	}
}
```

## 직각 이등변 삼각형 출력

```
public class TriangleLB {
	public static void main(String[] args) {
		Scanner scan = new Scanner(System.in);
		int n;
		
		System.out.println("왼쪽 아래가 직각인 이등변 삼각형을 출력합니다.");
		
		do{
			System.out.print("몇 단 삼각형입니까?");
			n = scan.nextInt();
		}while(n <= 0);
		
		for(int i=1; i<=n; i++) {
			for(int j=1; j<=i; j++) {
				System.out.print("*");
			}
			System.out.println();
		}
	
		scan.close();
	}
}
```

# 자료구조

- 데이터 단위와 데이터 자체 사이의 물리적 또는 논리적인 관계

## 배열

```
public class IntArray {
	public static void main(String[] args) {
		int[] a = new int[5];
		
		a[1] = 37;
		a[2] = 51;
		a[4] = a[1] * 2;
		
		for(int i=0; i<a.length; i++) {
			System.out.println("a[" + i + "] = " + a[i]);
		}
		
	}
}
```

### 배열 복사

```
public class CloneArray {
	public static void main(String[] args) {
		int[] a = {1,2,3,4,5};
		int[] b = a.clone();
		
		b[3] = 0;
		
		System.out.print("a= ");
		for(int i=0; i<a.length; i++) {
			System.out.print(" " + a[i]);
		}
		
		System.out.print("\nb= ");
		for(int i=0; i<b.length; i++) {
			System.out.print(" " + b[i]);
		}
	}
}
```

### 배열 요소의 최댓값 구하기

