---
layout: post
title: "[백준 알고리즘] 브루트 포스-1 (java)"
date: 2019-08-09
categories: Programming
tags: algorithm
comments: true
cover: "/assets/post_header/algorithm.jpg"
---

* 브루트 포스
    * 모든 경우의 수를 다 해보는 것
    * 경우의 수를 다 해보는데 걸리는 시간이 제한 시간을 넘지 않아야 함

* 문제 푸는 단계
    * 문제의 가능한 경우의 수 계산
        * 직접 계산
    * 가능한 모든 경우의 수 만들기
        * 하나도 빠짐 없이 만드는 게 관건
        * 그냥 다 해보기, n중 for문, 순열, 재귀, 비트마스크
    * 답 구하기

<br>

---

# 1. 그냥 다 해보기

### [일곱 난쟁이]

* 9명의 난쟁이 중 7명의 난쟁이의 키의 합이 100인 경우 찾기
* 9명 중에서 7명을 찾는 것보다, 2명을 찾는 게(2중 for문) 효율적 → sum-₉C₂=100
* **정답이 여러 개인 경우 주의! 정답 찾으면 for문 바로 탈출하기**

**[Code]**
* 1) 입력받기: 9명의 난쟁이 키
* 2) 경우의 수: 9명 중 2명 (2중 for문)  
    - 정답 찾으면 for문 탈출

<details>
<summary style="color: #5882FA; font-weight: bold;">P2309 일곱 난쟁이</summary>
<div markdown="1">

[https://www.acmicpc.net/problem/2309][baekjoon-2309]

{% highlight java %}
import java.util.Arrays;
import java.util.Scanner;

public class P2309 {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		
		int[] dwarves = new int[9];
		int sum = 0;
		boolean check = false;
		
		// 1) 입력: 9명의 난쟁이 키
		for(int i=0; i<9; i++) {
			int n = sc.nextInt();
			dwarves[i] = n;
			sum += n;
		}
		
		// 2) 경우의 수: 9명 중 2명 (2중 for문)
		for(int i=0; i<8; i++) {
			for(int j=i+1; j<9; j++) {
				if(sum-dwarves[i]-dwarves[j]==100) {
					dwarves[i] = 0;
					dwarves[j] = 0;
					check = true;
					break;
				}
			}
			// 정답 찾으면 for문 탈출
			if(check) {
				break;
			}
		}

		Arrays.parallelSort(dwarves);
		
		for(int i=2; i<9; i++) {
			System.out.println(dwarves[i]);
		}
		sc.close();
	}
}
{% endhighlight %}  
</div>
</details>

<br>

### [날짜 계산]

* 두 가지 방법으로 풀 수 있음
    * 1) e, s, m ++ 하면서 E, S, M과 동일해지는 year 찾기
    * 2) (year%15=E) & (year%28=S) & (year%19=M) 해당하는 year 찾기

**[Code]**
* 1) 입력받기: E, S, M
* 2) 경우의 수: 1부터 7980(15x28x19)까지 조건에 해당하는 경우 찾기
    - (year%15=E) & (year%28=S) & (year%19=M)

<details>
<summary style="color: #5882FA; font-weight: bold;">P1476 날짜 계산</summary>
<div markdown="1">

[https://www.acmicpc.net/problem/1476][baekjoon-1476]

{% highlight java %}
import java.util.Scanner;

public class P1476 {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		
		// 1) 입력받기: E, S, M
		int E, S, M;
		E = sc.nextInt()-1;
		S = sc.nextInt()-1;
		M = sc.nextInt()-1;
		
		// 2) 경우의 수: 1부터 7980(15*28*19)까지 조건에 해당하는 경우 찾기
		for(int i=0; i<7980; i++) {
			if((i%15==E) && (i%28==S) && (i%19==M)) {
				System.out.println(i+1);
				break;
			}
		}
		sc.close();
	}
}
{% endhighlight %}  
</div>
</details>

<br>

### [테트로미노]

* brute-force는 경우의 수를 빠트리기 쉬워서 dfs로 풀었음

<br>

---

# 2. N중 for문

* N개 중 일부를 선택할 경우
* 보통 2중 for문 넘어가면 재귀함수 사용
    * 소스코드 복잡해지고, 실수하기 쉽기 때문
* 해당 문제는 재귀로 풀었음

<br>


[baekjoon-2309]:    https://www.acmicpc.net/problem/2309
[baekjoon-1476]:    https://www.acmicpc.net/problem/1476
