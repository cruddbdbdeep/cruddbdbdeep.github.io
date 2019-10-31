---
layout: post
title: "[백준 알고리즘] 소수, 에라토스테네스의 체"
date: 2019-08-08
categories: Programming
tags: algorithm
comments: true
cover: "/assets/post_header/algorithm.jpg"
---

# 1. 소수 (Prime Number)

* **약수가 1과 자기 자신밖에 없는 수**
* 2보다 크거나 같고, `(n-1)`보다 작거나 같은 자연수로 나누어 떨어지면 안됨
    * 시간복잡도 O(n)
{% highlight java %}
bool prime(int n){
    if(n<2){
        return false;
    }
    for(int i=2; i<=n-1; i++){
        if(n%i==0){
            return false;
        }
    }
    return true;
}
{% endhighlight %}

* 2보다 크거나 같고, `(n/2)`보다 작거나 같은 자연수로 나누어 떨어지면 안됨  
    * 시간복잡도 O(n/2)
    * n의 약수 중에 가장 큰 것은 n/2보다 작거나 같으므로 n/2까지만 확인해도 됨
    * ex) 20의 약수: 1, 2, 4, 5, 10, 20 → 10 ≤ (20/2)
{% highlight java %}
bool prime(int n){
    if(n<2){
        return false;
    }
    for(int i=2; i<=n/2; i++){
        if(n%i==0){
            return false;
        }
    }
    return true;
}
{% endhighlight %}

* 2보다 크거나 같고, `sqrt(n)`보다 작거나 같은 자연수로 나누어 떨어지면 안됨
    * 시간복잡도 O(sqrt(n))
    * ab=n; 두 수 a, b의 차이가 가장 작은 경우는 sqrt(n)이므로 sqrt(n)까지만 확인해도 됨
    * ex) 24의 약수: 1, 2, 3, 4, 6, 8, 12, 24 → 4 ≤ sqrt(24)≒4.xxx
{% highlight java %}
bool prime(int n){
    if(n<2){
        return false;
    }
    for(int i=2; i*i<=n; i++){
        if(n%i==0){
            return false;
        }
    }
    return true;
}
{% endhighlight %}

<br>

## 소수와 관련된 알고리즘 문제  
* n이 소수인지 판별 → i*i<=n 범위 내에서 소수 정의 활용
* [0, n] 범위의 모든 자연수 중에서 소수 찾기 → 에라토스테네스의 체 활용, 배열에 소수 저장

<details>
<summary style="color: #5882FA; font-weight: bold;">P1978 소수 찾기</summary>
<div markdown="1">

[https://www.acmicpc.net/problem/1978][baekjoon-1978]  
  
{% highlight java %}
import java.util.Scanner;

public class P1978 {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		
		int n = sc.nextInt();
		int cnt = 0;
		
		for(int i=0; i<n; i++) {
			int a = sc.nextInt();
			if(isPrime(a)) {
				cnt++;
			}
		}
		System.out.println(cnt);
		sc.close();
	}
	
	public static boolean isPrime(int n) {
		if(n<2) {
			return false;
		}
		for(int i=2; i*i<=n; i++) {
			if(n%i==0) {
				return false;
			}
		}
		return true;
	}
}
{% endhighlight %}  
</div>
</details>  

<br>

---

# 2. 에라토스테네스의 체 (Sieve of Eratosthenes)

* 2부터 n까지 모든 수 나열
* 지워지지 않은 수 중에서 가장 작은 수 찾기
* 그 수는 소수
* 그 수의 배수를 모두 제거

![eratosthenes](https://user-images.githubusercontent.com/40786985/67957339-c67d9d80-fc38-11e9-9c83-3249968597cf.png)

{% highlight java %}
int prime[100];
int pn=0;
bool check[101];
int n=100;
for(int i=2; i<=n; i++){
    if(check[i]==false){
        prime[pn++]=j;
        for(int j=i*i; j<=n; j+=i){
            check[j]=true;
        }
    }
}
{% endhighlight %}

<details>
<summary style="color: #5882FA; font-weight: bold;">P1929 소수 구하기</summary>
<div markdown="1">

[https://www.acmicpc.net/problem/1929][baekjoon-1929]  
  
{% highlight java %}
import java.util.Scanner;

public class Main {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
	
		int m = sc.nextInt();
		int n = sc.nextInt();
		
		int[] numArr = new int[n+1];
		for(int i=2; i<=n; i++) {
			numArr[i] = i;
		}
		
		for(int i=2; i<=n; i++) {
			if(numArr[i]==0) {
				continue;
			}
			for(int j=i+i; j<=n; j+=i) {
				numArr[j] = 0;
			}
		}
		
		for(int i=m; i<=n; i++) {
			if(numArr[i]!=0) {
				System.out.println(numArr[i]);
			}
		}
    }
}
{% endhighlight %}  
</div>
</details> 

<br>

## 골드바흐의 추측 (Goldbach's conjecture)

* 2보다 큰 모든 짝수는 두 소수의 합으로 표현 가능
* 에라토스테네스의 체를 배열에 미리 저장

<details>
<summary style="color: #5882FA; font-weight: bold;">P6588 골드바흐의 추측</summary>
<div markdown="1">

[https://www.acmicpc.net/problem/6588][baekjoon-6588]  
  
{% highlight java %}
import java.util.Scanner;

public class Main {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
	
		int m = sc.nextInt();
		int n = sc.nextInt();
		
		int[] numArr = new int[n+1];
		for(int i=2; i<=n; i++) {
			numArr[i] = i;
		}
		
		for(int i=2; i<=n; i++) {
			if(numArr[i]==0) {
				continue;
			}
			for(int j=i+i; j<=n; j+=i) {
				numArr[j] = 0;
			}
		}
		
		for(int i=m; i<=n; i++) {
			if(numArr[i]!=0) {
				System.out.println(numArr[i]);
			}
		}
    }
}
{% endhighlight %}  
</div>
</details> 

<br>

[baekjoon-1978]:	https://www.acmicpc.net/problem/1978
[baekjoon-1929]:    https://www.acmicpc.net/problem/1929
[baekjoon-6588]:    https://www.acmicpc.net/problem/6588

