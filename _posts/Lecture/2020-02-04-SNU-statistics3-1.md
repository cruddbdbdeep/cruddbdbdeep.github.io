---
layout: post
title: "[경제통계학] 3. 평균과 표준편차-1 평균과 중앙값"
date: 2020-02-04
categories: DS
tags: data statistics
comments: true
cover: "/assets/post_header/data.jpg"
---

* 자료의 중심: 평균, 중앙값, 최빈치
* 중앙값(Median Voter Theorem)
* 평균과 중앙값의 관계
  * 평균과 중앙값
  * 히스토그램의 세 가지 꼬리 유형
* 야구통계
  * 희생번트의 득실
  * 2010년 한국 프로야구 성적

<br>

---

# 1. 자료의 중심: 평균, 중앙값, 최빈치

* 금융자산에 투자한다고 했을 때 
  * 1년 동안 얼마 정도의 수익을 기대하느냐? **(평균)**
  * 앞으로 1년 동안 실제 실현되는 수익률이 기대했던 수익률과 어느 정도 편차가 날 것이냐? 편차들의 대푯값? **(표준편차)**

* 데이터에 나타나는 평균적인 값, 평균적인 값으로부터 표준적으로 떨어져 있는 거리
    ![1](https://user-images.githubusercontent.com/40786985/76705869-b87f7380-6726-11ea-8afa-23afb5874650.jpg)
    * `대표적으로 떨어져 있는 거리`가 첫번째 그림은 작고, 두번째 그림은 크다.
    * `중심`은 동일하고, `편차`는 두번째 그림이 크다.
    * 예시
        * 첫번째 그림; 한국전력 주식 수익률
        * 두번째 그림; 삼성전자 주식 수익률 (편차가 큰 쪽이 투자 위험 크다)
* 히스토그램에서 자료 요약할 때
  * **중심(평균, 중앙값)**
  * **중심 주위로 퍼진 정도(표준편차, 사분위수 범위)**

<br>

## 1) 평균(Mean)

![2'](https://user-images.githubusercontent.com/40786985/76706498-3f364f80-672b-11ea-9f87-88c4b6c0f1b6.jpg)
* 평균 = 관측치 총합/관측치 개수
* 평균이 중요하지만 전부는 아님
    ![2](https://user-images.githubusercontent.com/40786985/76705870-b9b0a080-6726-11ea-9f38-b6536acc956c.jpg)
    * **첫번째 그림**은 모든 자료가 평균 근처로 몰려 있으니까 평균만 알면 다 아는 것
      * 평균에 담긴 의미가 굉장히 강하다.
    * **두번째 그림**은 좌우로 약간 차이는 있지만 평균 주위에 데이터가 집중되어 있어 평균만 알면 상당히 많은 것을 알 수 있음
    * **세번째 그림**은 평균이 중간값인데 평균 근처에 데이터가 없음
      * 평균이 기하학적으로 보면 히스토그램을 좌우 균형시키는 무게중심점 같은 것이나 그 이상 특별한 의미 없음
      * ex) Yellowstone의 Old Faithful

<br>

## 2) 중앙값(Median)

* 절반 이상의 숫자들이 이 값보다 크거나 같고 동시에 절반 이상의 숫자들이 이 값 보다 작거나 같은 수
* 히스토그램은 중앙값에서 그 면적이 양분됨
* **n=홀수**; (n+1)/2번째로 크거나 작은 숫자
* **n=짝수**; n/2번째 숫자와 (n+1)/2번째 숫자의 평균으로 정의

<br>

## 3) 최빈치(Mode)

* 가장 빈번하게 발생하는 값
* 히스토그램은 최빈치에서 그 높이가 제일 높음
* ex) 베이브 루스의 홈런, 46개

<br>

---

# 2. 중앙값(Median Voter Theorem)

### Median Voter Theorem

![2'''](https://user-images.githubusercontent.com/40786985/76849591-07ddb500-6889-11ea-9be8-df4502778bba.jpg)

* **가로축**은 유권자 개개인이 선호하는 세율
* 두 후보가 캐치플레이즈로 세금을 많이 걷는 큰 정부, 세금을 적게 걷는 작은 정부를 운영한다고 제시
* 상대방이 중앙값 위치를 선언했는데 내가 중앙값이 아닌 위치를 선정하면 패배
* 결국 `중앙값 투표자(median voter)`의 성향을 대표할 수 밖에 없다.
* 경제정책 면에서는 민주당, 공화당 후보의 경제정책이 상당한 정도로 수렴한다.

<br>

---

# 3. 평균과 중앙값의 관계

### 평균과 중앙값

* **좌우대칭 히스토그램**
  ![3](https://user-images.githubusercontent.com/40786985/76706022-d00b2c00-6727-11ea-8ece-9cf66e4b956b.jpg)
  * `좌우 대칭`이면 **평균=중앙값**
  * 히스토그램의 중심(평균, 중앙값) = 2

* **숫자열의 변화에 따른 평균의 변화**
  ![4](https://user-images.githubusercontent.com/40786985/76706023-d0a3c280-6727-11ea-8fa6-69fd62adc777.jpg)
  * 1,2,2,5
    * **평균** 2 → 2.5 (히스토그램의 무게중심점)
    * **중앙값** 2
  * 1,2,2,7
    * **평균** 2 → 3 (히스토그램의 무게중심점)
    * **중앙값** 2

* **극단적인 값이 존재할 때 평균은 극단적인 값이 영향을 더 받고, 중앙값은 덜 받는다.**
* **히스토그램이 `좌우대칭`이면 평균과 중앙값이 같다.**
* **히스토그램이 `비대칭적`이면 평균보다는 중앙값 개념이 중심의 척도로서 적절하다.**

<br>

### 히스토그램의 세 가지 꼬리 유형

![5](https://user-images.githubusercontent.com/40786985/76706024-d13c5900-6727-11ea-90ba-f3f36deb90b4.jpg)

* **첫번째 히스토그램**은 꼬리가 오른쪽이 길게 늘어져 있음 `(right-skewed)`
  * `중앙값 < 평균`
  * ex) 소득 분포
    * 어느 사회, 어느 시대든 아주 소수의 부자들 존재
    * 50% 위치에 있는 사람의 가구소득 < 4인 기준 약 8천 만원 (1인당 GDP 2만 달러*4)
* **두번째 히스토그램**은 좌우대칭
* **세번째 히스토그램**은 꼬리가 왼쪽이 길게 늘어져 있음 `(left-skewed)`

<br>

---

# 4. 야구통계

### 희생번트의 득실

![6](https://user-images.githubusercontent.com/40786985/76706112-8242f380-6728-11ea-885c-9c1ba7c2a56d.jpg)

* **무사 주자 1루 상황에서 희생번트를 하는 게 값어치가 있는가?**
  * 무사 주자 1루 (첫번째 행)
    * 1728건 중에 39.6% 득점으로 이어졌고, 평균 득점은 0,8점
    * 0.813(모든 득점 카운트) > 0.396(득점했으면 1, 아니면 0)
  * 1사 주자 2루 (두번째 행)
    * 희생번트가 성공해서 번트를 한 타자는 죽고 1루에 있는 주자는 2루로 진출
    * 657건 중에 39% 득점으로 이어졌고, 평균 득점은 0.67점
  * **희생번트가 성공해봐야 득점확률이 올라가지도 않고, 평균득점이 올라가지도 않고, 성공해도 남는 게 없다.**

* **무사 주자 1,2루 상황에서 희생번트를 하는 게 값어치가 있는가?**
  * 무사 주자 1,2루
    * 367건 중에 60% 득점으로 이어졌고, 평균 득점은 1.47점
  * 1아웃 주자 2,3루 (마지막 행)
    * 176건 중에 73% 득점으로 이어졌고, 평균 득점은 1.56점
  * **노아웃 주자 1,2루 상황에서는 희생번트가 성공만 한다고 하면 득점 가능성도 올라가고 평균득점도 올라가기 때문에 남는 장사이다.**

<br>

### 2010년 한국 프로야구 성적

* **팀별 공격력과 수비력**
    ![7](https://user-images.githubusercontent.com/40786985/76706184-01d0c280-6729-11ea-9e60-d5958c331e14.jpg)
    * 종합적으로 보면 공수양면에서 4위 안에 들어서 밸런스를 갖추고 있는 팀이 SK이고 SK가 우승
    
* **투수 순위**
![8](https://user-images.githubusercontent.com/40786985/76706185-0301ef80-6729-11ea-9d92-78be240590d8.jpg)

* **타자 순위**
![9](https://user-images.githubusercontent.com/40786985/76706187-039a8600-6729-11ea-90fe-dee65d4b4a45.jpg)

<br>