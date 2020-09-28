---
title: 파이썬으로 해보는 웹 스크래핑(Web Scraping with Python)[1]
date: 2020-09-28 21:09:44
category: Python
thumbnail: { thumbnailSrc }
draft: false
---

## 웹 크롤링과 웹 스크래핑 
프로젝트를 진행하다가 웹에 있는 데이터들을 모아서 DB에 추가해야되는 상황이 생겼다. 
예전에 자동예약 시스템을 만들면서 대충 웹 크롤링과 스크래핑을 경험 해봤지만 그 때는 정말 단순한 웹 작업일 뿐 직접적인 데이터를 다루진 않았었다.

이번에 할 작업은 정확히 크롤링보다는 스크래핑이기 때문에 향후 글에서는 스크래핑 작업이라고 쓰겠다.
여기서 웹 크롤링과 웹 스크래핑을 간단하게 집고 넘어가자면 `크롤링(Crawling)`은 웹사이트 상의 필요한 모든 페이지를 그대로 복사하는 것을 얘기한다. 
그리고 크롤링한 내용을 토대로 필요에 맞게 재가공하여 사용하는 것이 `스크래핑(Scraping)` 이다. 전혀 중요하지 않은 내용이니 무시해도 좋다.

## 웹 스크래핑 준비사항
- 파이썬 : 스크래핑을 함에 있어 파이썬과 자바스크립트를 많이 사용하는데 개인적으로 파이썬을 더 선호하기 때문에 파이썬으로 진행한다.
- requests : 파이썬에서 HTTP 요청을 보내는 모듈이다.
- BeautifulSoup : 이쁜 이름을 가진 라이브러리로 html 코드를 파이썬 내에서 사용할 수 있도록 파싱(parsing)해주는 역할을 한다.

## Requests 설치하기
스크래핑을 하고자하는 웹에게 http 요청을 보내기 위해 request를 설치해야한다.

```sh
$ pip install requests
```

설치가 됐으면 main.py를 만들어 다음과 같이 입력하고 실행해보자.
```python
import requests

#HTTP GET Request
request = requests.get("https://www.naver.com")
print(request)   #return <Response [200]>
```
실행 결과 값으로 <Response [200]>이 출력되는 것을 확인 할 수 있다.

우리가 이 코드를 통해서 한 일은 네이버 사이트에 GET Request(요청)을 보낸 것이고 이것에 대한 수행 결과로 Response(응답) 값을 코드로써 받게 되었다.

여기서 Response 뒤의 200 코드는 `Status code`로 일상적인 대화에서 대답이라고 보면 된다. 200은 성공응답 중 하나로 OK라는 의미를 가지고 있다.

상태 코드와 관련한 정보는 https://developer.mozilla.org/ko/docs/Web/HTTP/Status 를 참고하자.

네이버 사이트에 대해 GET 요청의 응답이 Ok가 나왔으니 우리는 이제 소스들을 가지고 올 수 있다. 다음을 실행시켜보자.

```python
#HTTP Status
print("상태 코드는" + request.status_code + "입니다.")
#HTML 소스
print("HTML 소스는" + request.text + "입니다.")
```
마지막 줄의 print문으로 출력창에 네이버 사이트의 html코드가 전부 출력될 것이다. 길이가 아주 길고 출력창에서 봤을 때 이게 뭔지 전혀 모르겠다고 생각이들어도 상관없다. 이를 향후에 이용하는 방법에 대해 이어지는 포스팅에서 다루도록 하겠다. 