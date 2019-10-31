---
layout: post
title: "[백준 알고리즘] 나머지, 최대공약수, 최소공배수"
date: 2019-08-08
categories: Programming
tags: algorithm
comments: true
cover: "/assets/post_header/algorithm.jpg"
---

# 1. 나머지 연산 (Modular Arithmetic)
  
* 답을 ~로 나눈 나머지를 출력하라
    * 자료형의 범위 고려 (int, long long)

<details markdown="1">
<summary>P10430 나머지</summary>
<div markdown="1">
  
[https://www.acmicpc.net/problem/10430][baekjoon-10430]
  
{% highlight java %}
import java.util.Scanner;

public class P10430 {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		
		int a = sc.nextInt();
		int b = sc.nextInt();
		int c = sc.nextInt();

		System.out.println((a+b)%c);
		System.out.println((a%c + b%c)%c);
		System.out.println((a*b)%c);
		System.out.println((a%c * b%c)%c);
		
		sc.close();
	}
}
{% endhighlight %}  
</div>
</details>

<br>

---

# 2. 최대공약수와 최소공배수  
  
## 1) 최대공약수 (Greatest Common Divisor; GCD)

* A와 B의 최대공약수
	* A와 B의 공통된 약수 중에서 가장 큰 정수

* **유클리드 호제법(Euclidean algorithm)**

![gcd](https://user-images.githubusercontent.com/40786985/67936369-02037200-fc0f-11e9-9c3b-8b307962572b.jpg)

{% highlight java %}
gcd(int a, int b){
    if(b==0){
        return a;
    } else {
        return gcd(b, a%b);
    }
}
{% endhighlight %}

* A, B, C의 최대공약수  
`gcd(a, b, c) = gcd(gcd(a, b), c);`

<br>

## 2) 최소공배수 (Least Common Multiple; LCD)

* A와 B의 최소공배수
	* A와 B의 공통된 배수 중에서 가장 작은 정수  
`lcm = (a/gcd)*(b/gcd)*gcd;`
<br>  

<details>
<summary>P2609 최대공약수와 최소공배수</summary>
<div markdown="1">

[https://www.acmicpc.net/problem/2609][baekjoon-2609]  
  
{% highlight java %}
import java.util.Scanner;

public class P2609 {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		
		int a, b;
		a = sc.nextInt();
		b = sc.nextInt();
		
		int gcd = gcd(a, b);
		int lcm = (a/gcd)*(b/gcd)*gcd;
		
		System.out.println(gcd);
		System.out.println(lcm);
		
		sc.close();
	}

	public static int gcd(int a, int b) {
		if(b==0) {
			return a;
		} else {
			return gcd(b, a%b);
		}
	}	
}
{% endhighlight %}  
</div>
</details>  

<details>
<summary>P1934 최소공배수</summary>
<div markdown="1">

[https://www.acmicpc.net/problem/1934][baekjoon-1934]

{% highlight java %}
import java.util.Scanner;

public class P1934 {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		
		int T = sc.nextInt();
		
		for(int i=0; i<T; i++) {
			int a = sc.nextInt();
			int b = sc.nextInt();
			
			int gcd = gcd(a, b);
			int lcm = gcd*(a/gcd)*(b/gcd);
			
			System.out.println(lcm);
		}
		
		sc.close();
	}
	
	public static int gcd(int a, int b) {
		if(b==0) {
			return a;
		} else {
			return gcd(b, a%b);
		}
	}
}
{% endhighlight %}  
</div>
</details>
  
<details>
<summary>P9613 GCD 합</summary>
<div markdown="1">

[https://www.acmicpc.net/problem/9613][baekjoon-9613]  
  
{% highlight java %}
import java.util.Scanner;

public class P9613 {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		
		int t = sc.nextInt();
		
		for(int i=0; i<t; i++) {
			long sum = 0;
			int n = sc.nextInt();
			
			int[] Arr = new int[n];
			for(int j=0; j<n; j++) {
				Arr[j] = sc.nextInt();
			}
			
			for(int j=0; j<n-1; j++) {
				for(int k=j+1; k<n; k++) {
					sum += gcd(Arr[j], Arr[k]);
				}
			}
			System.out.println(sum);
		}
		
		sc.close();
	}
	
	public static int gcd(int a, int b) {
		if(b==0) {
			return a;
		} else {
			return gcd(b, a%b);
		}
	}	
}
{% endhighlight %}
</div>
</details>
  
<br>  

[baekjoon-10430]:	https://www.acmicpc.net/problem/10430
[baekjoon-2609]:	https://www.acmicpc.net/problem/2609
[baekjoon-1934]:	https://www.acmicpc.net/problem/1934
[baekjoon-9613]:	https://www.acmicpc.net/problem/9613


