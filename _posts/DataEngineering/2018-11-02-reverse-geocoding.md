---
layout: post
title: "[Reverse Geocoding] 카카오 API 사용해서 역지오코딩 (위·경도로 주소 추출)"
date: 2018-11-02
categories: Python
tags: geocoding
comments: true
cover: "/assets/post_header/conference.jpg"
---

# Problem

`Goal` : 교통사고 데이터의 **위경도**를 통해 **행정동** 주소를 반환

![data](https://user-images.githubusercontent.com/40786985/70517411-eaa79500-1b7b-11ea-9956-7b0b67a75164.jpg)

![data2](https://user-images.githubusercontent.com/40786985/70519959-1cbaf600-1b80-11ea-8088-97fb37237850.jpg)

<br>

---

# 1. 카카오 API

* 카카오 계정으로 로그인 한 뒤, 개발자 계정 등록 [(https://developers.kakao.com/)][kakao-developers]
![kakaodevelopers](https://user-images.githubusercontent.com/40786985/68369663-2f579f00-017e-11ea-8c75-97e551d9e44e.jpg)

<br>

* 앱 만들기
![kakao1](https://user-images.githubusercontent.com/40786985/68370156-2c10e300-017f-11ea-8534-d7fc1b772c40.png)
<br>

* key 발급
![kakao2](https://user-images.githubusercontent.com/40786985/68370508-02a48700-0180-11ea-90c0-5447b7edbe68.png)
<br>

---
# 2. 역지오코딩

* Request, Response 형태
[https://developers.kakao.com/docs/restapi/local#%ED%96%89%EC%A0%95%EA%B5%AC%EC%97%AD%EC%A0%95%EB%B3%B4-%EB%B3%80%ED%99%98][kakao-map]

* 라이브러리, 전역 변수

{% highlight python %}
import json
import sys
import pandas as pd
import requests
from datetime import *

# 전역 변수
accident_data = 'accident.csv'
location_data = 'location.csv'
APP_KEY = ''    # 발급받은 키 입력
URL = 'https://dapi.kakao.com/v2/local/geo/coord2regioncode.json'
{% endhighlight %}
<br>

* json 데이터 요청

![kakao3](https://user-images.githubusercontent.com/40786985/70519030-a23da680-1b7e-11ea-8a44-a2e5f02ca436.jpg)

{% highlight python %}
def json_request(url='', encoding='utf-8', success=None, error=lambda e: print('%s : %s' % (e, datetime.now()), file=sys.stderr)):
    headers = {'Authorization': 'KakaoAK {}'.format(APP_KEY)}
    resp = requests.get(url, headers=headers)
    print('%s : success for request [%s]' % (datetime.now(), url))

    return resp.text
{% endhighlight %}
<br>

* json 데이터 파싱해서 행정동 주소 반환 **(region_3depth_name)**

![kakao4](https://user-images.githubusercontent.com/40786985/70519445-46bfe880-1b7f-11ea-920c-b2b0e68534ee.jpg)

{% highlight python %}
def reverse_geocode(longitude, latitude):
    # 파라미터 최적화하여 url 생성
    url = '%s?x=%s&y=%s' %(URL, longitude, latitude)

    # json request
    try:
        json_req = json_request(url=url)
        json_data = json.loads(json_req)
        json_doc = json_data.get('documents')[1]
        json_name = json_doc.get('region_3depth_name')
    except:
        json_name = 'NaN'

    return json_name
{% endhighlight %}
<br>

* 교통사고 파일에서 경위도 추출해서 동 주소 반환

{% highlight python %}
def get_address(data):
    address = []

    # 경도, 위도 추출해서 동 주소 반환
    for i in range(len(data)):
        longitude = data['경도'][i]
        latitude = data['위도'][i]
        address.append(reverse_geocode(longitude, latitude))

    return address  # 전처리 함수에서 주소 리스트 받아서 데이터프레임에 추가
{% endhighlight %}
<br>

* main 함수

{% highlight python %}
def main():
    # 파일 읽기
    data = pd.read_csv(accident_data, encoding='euc-kr')
    location = pd.read_csv(location_data, encoding='euc-kr')

    address = get_address(data)
    data = preprocess(data, address, location)  # 전처리 함수(생략했음)

    # 최종 파일 저장
    data.to_csv('%s_final.csv' % (accident_data[:-4]), sep=',', encoding='euc-kr')

if __name__ == '__main__':
    main()
{% endhighlight %}

<br>

[kakao-developers]:     https://developers.kakao.com/
[kakao-map]:            https://developers.kakao.com/docs/restapi/local#%ED%96%89%EC%A0%95%EA%B5%AC%EC%97%AD%EC%A0%95%EB%B3%B4-%EB%B3%80%ED%99%98
