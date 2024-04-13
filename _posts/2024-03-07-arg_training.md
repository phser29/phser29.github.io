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

```
public class MaxOfArrayRand {
	private static int maxOf(int[] a) {
		int max = a[0];
		
		for(int i=0; i<a.length-1; i++) {
			if(a[i] > max) {
				max = a[i];
			}
		}
		
		return max;
	}
	
	public static void main(String[] args) {
		Random ran = new Random();
		Scanner scan = new Scanner(System.in);
		
		System.out.println("키의 최댓값을 구합니다.");
		System.out.print("사람 수: ");
		int num = scan.nextInt();
		
		int[] height = new int[num];
		
		System.out.println("키 값은 아래와 같습니다.");
		for(int i=0; i<num; i++) {
			height[i] = 100 + ran.nextInt(90);
			System.out.println("height[" +i+ "] : " + height[i]);
		}
		
		System.out.println("최댓값은 " +maxOf(height)+ "입니다.");
	}
}
```

### 배열 값 교환

```
public class ReverserArray {
	static void swap(int[] a, int idx1, int idx2) {
		int t = a[idx1];
		a[idx1] = a[idx2];
		a[idx2] = t;
	}
	
	static void reverse(int[] a) {
		for(int i=0; i<a.length/2; i++) {
			swap(a, i, a.length - i - 1);
		}
	}
	
	public static void main(String[] args) {
		Scanner scan = new Scanner(System.in);
		
		System.out.println("요솟수: ");
		int num = scan.nextInt();
		
		int[] x = new int[num];
		
		for(int i=0; i<num; i++) {
			System.out.println("x[" + i + "] : ");
			x[i] = scan.nextInt();
		}
		
		reverse(x);
		
		System.out.println("요소를 역순으로 정렬했습니다.");
		for(int i=0; i<num; i++) {
			System.out.println("x[" + i + "] = " + x[i]);
		}
		
		scan.close();
	}
}
```

## 기수 변환

- 기수의 의미
 - 기수는 수를 나타내는 데 기초가 되는 수

```
public class CardConvRev {
	static int cardConvR(int x, int r, char[] d) {
		int digits = 0;
		String dchar = "0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ";
		
		do {
			d[digits++] = dchar.charAt(x % r);
			x /= r;
		} while(x != 0);
		
		return digits;
	}
	
	public static void main(String[] args) {
		Scanner scan = new Scanner(System.in);
		int no = 0;
		int cd = 0;
		int dno = 0;
		int retry = 0;
		char[] cno = new char[32];
		
		System.out.println("10진수를 기수 변환합니다.");
		do {
			do {
				System.out.print("변환하는 음이 아닌 정수: ");
				no = scan.nextInt();
			}while(no < 0);
			
			do {
				System.out.println("어떤 진수로 변환할까요? (2~36) : ");
				cd = scan.nextInt();
			}while(cd < 2 || cd > 36);
			
			dno = cardConvR(no, cd, cno);
			
			System.out.println(cd + "진수로는 ");
			for(int i=dno-1; i>=0; i--) {
				System.out.print(cno[i]);
			}
			System.out.println("입니다.");
			
			System.out.println("한 번 더 할까요? (1.예/0.아니오) : " );
			retry = scan.nextInt();
		}while(retry == 1);
		
		scan.close();
	}
}
```

### 소수 나열

- 자신과 1 이외의 정수로 나누어 떨어지지 않는 정수
- 나누어 떨어지는 정수가 하나 이상 존재하면 그 수는 합성수

```
public class PrimeNumber1 {
	public static void main(String[] args) {
		int counter = 0;
		
		for(int n=2; n<=1000; n++) {
			int i;
			for(i=2; i<n; i++) {
				counter++;
				if(n % i == 0) {
					break;
				}
			}
			if(n == i) {
				System.out.println(n);
			}
		}
		
		System.err.println("나눗셈을 수행한 횟수 : " + counter);
	}
}
```

- 같은 답을 얻는 알고리즘은 하나가 아니다
- 빠른 알고리즘은 메모리를 많이 요구한다.


# 검색 알고리즘

- 선형 검색: 무작위로 늘어놓은 데이터 모임에서 검생르 수행

- 이진 검색: 일정한 규칙으로 늘어놓은 데이터 모임에서 아주 빠른 검색을 수행

- 해시법: 추가, 삭제가 자주 일어나느 데이터 모임에서 아주 빠른 검색을 수행
	- 체인법: 같은 해시 값의 데이터를 선형 리스트로 연결하는 방법
	- 오픈 주소법: 데이터를 위한 해시 값이 충돌할 때 재해시하는 방법

## 선형 검색

- 요소가 직선 모양으로 늘어선 배열에서의 검색은 원하는 키 값을 갖는 요소를 만날 때까지 맨 앞부터 순서대로 요소를 검색하는 것 순차 검색이라고도 함

- 배열 검색의 종료 조건
	- 1. 검색할 값을 발견하지 못하고 배열의 끝을 지나간 경우
	- 2. 검색할 값과 같은 요소를 발견한 경우

```
public class SeqSearch {
	static int seqSearch(int[] a, int n, int key) {
//		int i = 0;
//		
//		while(true) {
//			if(i == n) {
//				return -1;
//			}
//			if(a[i] == key) {
//				return i;
//			}
//			i++;
//		}
		for(int i=0; i<n; i++) {
			if(a[i] == key) {
				return i;
			}
		}
		return -1;
	}
	
	public static void main(String[] args) {
		Scanner scan = new Scanner(System.in);
		
		System.out.print("요솟수: ");
		int num = scan.nextInt();
		int[] x = new int[num];
		
		for(int i=0; i< num; i++) {
			System.out.print("x["+i+"] : ");
			x[i] = scan.nextInt();
		}
		
		System.out.print("검색할 값: ");
		int ky = scan.nextInt();
		int idx = seqSearch(x, num, ky);
		
		if(idx == -1) {
			System.out.println("그 값의 요소가 없습니다.");
		} else {
			System.out.println(ky +"은(는) x[" +idx+ "]에 있습니다.");
		}
		
		scan.close();
	}
}
```

### 보초법 

- 위 비용을 반으로 줄이는 방법

```
public class SeqSearchSen {
	static int seqSearchSen(int[] a, int n, int key) {
		int i=0;
		
		a[n] = 7;
		
		while(true) {
			if(a[i] == key) {
				break;
			}
			i++;
		}
		
		return i == n ? -1 : i;
	}
	
	public static void main(String[] args) {
		Scanner scan = new Scanner(System.in);
		
		System.out.print("요솟수: ");
		int num = scan.nextInt();
		int[] x = new int[num+1]; //보초법으로 인한 마지막 요소 추가
		
		for(int i=0; i<num; i++) {
			System.out.print("x["+i+"] : ");
			x[i] = scan.nextInt();
		}
		
		System.out.print("검색할 값: ");
		int ky = scan.nextInt();
		
		int idx = seqSearchSen(x, num, ky);
		
		if(idx == -1) {
			System.out.println("그 요소의 값이 없습니다.");
		} else {
			System.out.println(ky+"은 x["+idx+"]에 있습니다.");
		}
		
		scan.close();
	}
}
```

## 이진 검색

- 요소가 오름차순 또는 내림차순으로 정렬된 배열에서 검색하는 알고리즘

```
public class BinSearch {
	static int binSearch(int[] a, int n, int key) {
		int pl = 0;
		int pr = n - 1;
		
		do {
			int pc = (pl + pr) / 2;
			if(a[pc]==key) {
				return pc;
			} else if(a[pc] < key) {
				pl = pc + 1;
			} else {
				pr = pc - 1;
			}
		} while(pl <= pr);
		
		return -1;
	}
	
	public static void main(String[] args) {
		Scanner scan = new Scanner(System.in);
		
		System.out.print("요솟수: ");
		int num = scan.nextInt();
		int[] x = new int[num];
		
		System.out.println("오름차순으로 입력하세요.");
		
		System.out.print("x[0] : ");
		x[0] = scan.nextInt();
		
		for(int i=1; i<num; i++) {
			do {
				System.out.print("x["+i+"] : ");
				x[i] = scan.nextInt();
			}while(x[i] < x[i-1]);
		}
		
		System.out.print("검색할 값: ");
		int ky = scan.nextInt();
		
		int idx = binSearch(x, num, ky);
		
		if(idx == -1) {
			System.out.println("그 값의 요소가 없습니다.");
		} else {
			System.out.println(ky+"은 x["+idx+"]에 있습니다.");
		}
		
		scan.close();
	}
}
```

### 복잡도

- 알고리즘의 성능을 객관적으로 평가하는 기준
	1. 시간 복잡도 : 실행에 필요한 시간을 평가하는 것
	2. 공간 복잡도 : 기억 영역과 파일 공간이 얼마나 필요한가 평가한 것

- Arrays.binarySearch
	1. 이진 검색 메서드를 직접 코딩할 필요가 없다.
	2. 모든 자료형 배열에서 검색하 수 있다.

```

```


