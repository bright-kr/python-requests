# Python Requests 라이브러리에 대한 완전한 가이드

[![Bright Data Promo](https://github.com/bright-kr/LinkedIn-Scraper/raw/main/Proxies%20and%20scrapers%20GitHub%20bonus%20banner.png)](https://brightdata.co.kr/)

이 튜토리얼에서는 Webスクレイピング을 위해 Python에서 Requests 라이브러리를 사용하는 방법을 시연합니다:

- [Requests 라이브러리 소개](#introduction-to-the-requests-library)
- [HTTP 메서드](#http-methods)
- [Requests의 Response 객체 상세 분석](#breaking-down-a-response-object-from-requests)
- [Python Requests 라이브러리를 사용한 리クエスト 커스터마이징](#request-customization-with-the-python-requests-library)
- [기타 구성](#other-configurations)

## Introduction to the Requests Library

[`Requests`](https://github.com/psf/requests)는 Python을 위한 간단하고 사용자 친화적인 HTTP 툴킷입니다. 자세히 말해, HTTP リクエスト를 만들고 レスポンス를 쉽고 이해하기 쉬운 방식으로 처리할 수 있는 직관적인 API를 제공합니다. [GitHub에서 50k 이상의 star](https://github.com/psf/requests)와 매일 수백만 건의 다운로드를 보유한 Requests는 Python에서 가장 인기 있는 HTTP 클라이언트를 대표합니다.

이 라이브러리가 제공하는 주요 기능에는 모든 HTTP 메서드를 포괄하는 종합적인 API, 서버 응답 처리, リクエスト 커스터마이징, 로그인 메커니즘, 보안 인증서 처리 등이 포함됩니다. 또한 Python Requests 모듈은 기본적으로 [HTTP/1.1](https://datatracker.ietf.org/doc/html/rfc2616)을 지원합니다.

### Setting up

Requests를 설치하는 가장 쉽고 권장되는 방법은 `pip`를 사용하는 것입니다. 특히 Requests 라이브러리와 연결된 `pip` 패키지는 `requests`입니다. 따라서 다음 명령으로 HTTP 클라이언트를 설치할 수 있습니다:

```sh
pip install requests
```

Python 스크립트에서 `requests`를 사용하려면 아래 줄로 import합니다:

```python
import requests
```

좋습니다! 이제 Requests 패키지가 설치되었으며 사용할 준비가 되었습니다.

### Use Cases

Python `requests` 라이브러리의 주요 사용 사례는 다음과 같습니다:

- **웹 서버에 HTTP リクエスト 보내기**: GET リクエ스트를 전송하여 웹 서버에서 데이터를 가져옵니다.
- **API 사용**: API エンドポイント에 リクエ스트를 보내고 レスポンス를 처리하여 다양한 웹 서비스와 상호작용하고 데이터를 액세스합니다.
- **Webスクレイピング**: 웹 페이지에 연결된 HTML 문서를 가져오며, 이후 [ `BeautifulSoup` 같은 라이브러리로 파싱](https://brightdata.co.kr/blog/how-tos/beautiful-soup-web-scraping)하여 특정 정보를 추출할 수 있습니다.
- **웹 애플리케이션 테스트**: HTTP リクエ스트를 시뮬레이션하고 レスポンス를 검증하여 테스트 프로세스를 자동화하고 웹 서비스의 정상 동작을 보장합니다.
- **파일 다운로드**: 각 URL에 HTTP `GET` リクエスト를 전송하여 이미지, 문서 또는 기타 미디어 파일과 같은 파일을 웹 서버에서 가져옵니다.

**Methods**

다음 표에서 `requests` 라이브러리가 공개하는 public 메서드를 확인해 보십시오:

|     |     |
| --- | --- |
| **Method** | **Description** |
| [`requests.request()`](https://requests.readthedocs.io/en/latest/api/#requests.request) | 지정된 메서드로 주어진 URL에 커스텀 HTTP リクエスト를 전송합니다 |
| [`requests.get()`](https://requests.readthedocs.io/en/latest/api/#requests.get) | 지정된 URL에 `GET` リクエ스트를 전송합니다 |
| [`requests.post()`](https://requests.readthedocs.io/en/latest/api/#requests.post) | 지정된 URL에 `POST` リクエ스트를 전송합니다 |
| [`requests.put()`](https://requests.readthedocs.io/en/latest/api/#requests.put) | 지정된 URL에 `PUT` リクエ스트를 전송합니다 |
| [`requests.patch()`](https://requests.readthedocs.io/en/latest/api/#requests.patch) | 지정된 URL에 `PATCH` リクエ스트를 전송합니다 |
| [`requests.delete()`](https://requests.readthedocs.io/en/latest/api/#requests.delete) | 지정된 URL에 `DELETE` リクエ스트를 전송합니다 |
| [`requests.head()`](https://requests.readthedocs.io/en/latest/api/#requests.head) | 지정된 URL에 `HEAD` リクエ스트를 전송합니다 |

이들은 가장 유용한 HTTP リクエ스트 메서드를 다룹니다. 사용 방법에 대한 자세한 내용은 [공식 API 문서](https://requests.readthedocs.io/en/latest/api/)에서 확인하십시오.

## HTTP Methods

HTTP에서 `GET`, `POST`, `PUT`, `DELETE`, `HEAD` 메서드를 다룰 때 `requests` Python 라이브러리가 어떻게 동작하는지 살펴보겠습니다.

### GET

HTTP에서 [`GET`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/GET) 메서드는 서버로부터 특정 리소스를 요청하는 데 사용됩니다. `requests.get()`로 HTTP `GET` リクエ스트를 만드는 방법은 다음과 같습니다:

```python
import requests

# send a GET request to the specified URL

response = requests.get('https://api.example.com/data')
```

아래와 같이 `requests.request()`로도 동일한 결과를 얻을 수 있습니다:

```python
import requests

response = requests.request('GET', 'https://api.example.com/data')
```

이 경우 추가 문자열 변수로 사용할 HTTP 메서드를 수동으로 지정해야 합니다.

### POST

HTTP `POST` 메서드는 서버에 데이터를 제출하여 추가 처리를 수행하는 데 사용됩니다. `requests.post()`로 `POST` リクエ스트를 보내는 방법은 다음과 같습니다:

```python
import requests

# data to be sent in the POST request

product = {

'name': 'Limitor 500',

'description': 'The Limitor 500 is a high-performance electronic device designed to regulate power consumption in industrial settings. It offers advanced features such as real-time monitoring, adjustable settings, and remote access for efficient energy management.',

'price': 199.99,

'manufacturer': 'TechCorp Inc.',

'category': 'Electronics',

'availability': 'In Stock'

}

# send a POST request to the specified URL

response = requests.post('https://api.example.com/product', data=product)
```

`GET` リクエ스트와 비교하면, 이번에는 `data` 옵션을 통해 서버로 전송할 데이터를 지정해야 합니다. `requests`는 이 데이터를 HTTP リクエ스트의 body에 추가합니다.

JSON body의 경우, `data` 대신 `json` 옵션에 데이터 객체를 전달하십시오:

```python
response = requests.post('https://api.example.com/product', json=product)
```

동일하게 다음과 같이 `request.request()`로도 같은 リクエ스트를 수행할 수 있습니다:

```python
import requests

product = {

'name': 'Limitor 500',

'description': 'The Limitor 500 is a high-performance electronic device designed to regulate power consumption in industrial settings. It offers advanced features such as real-time monitoring, adjustable settings, and remote access for efficient energy management.',

'price': 199.99,

'manufacturer': 'TechCorp Inc.',

'category': 'Electronics',

'availability': 'In Stock'

}

response = requests.request('POST', 'https://api.example.com/product', data=product)
```

### PUT

[`PUT`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/PUT) 메서드는 서버의 리소스를 업데이트하거나 교체하는 데 사용됩니다. Python `requests` 모듈로 `PUT` リクエ스트를 보내는 것은 쉽고 POST リクエ스트와 유사한 패턴을 따릅니다. 달라지는 점은 사용할 메서드가 `requests.put()`이라는 것입니다. 또한 `requests.request()`에서 HTTP 메서드 문자열은 `'PUT'`가 됩니다.

### PATCH

[`PATCH`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/PATCH) 메서드는 온라인 리소스에 부분 수정 사항을 적용하는 데 사용됩니다. `PUT` リクエ스트와 마찬가지로 Python `requests` 라이브러리에서 `PATCH` リクエ스트를 보내는 방식은 POST リクエ스트와 유사합니다. 달라지는 점은 사용할 메서드가 `requests.patch()`이고 `requests.request()`에서 HTTP 메서드 문자열이 `'PATCH'`라는 것입니다.

### DELETE

[`DELETE`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/DELETE) 메서드는 주어진 URI로 식별되는 리소스를 삭제하는 데 사용됩니다. `delete()` 메서드를 사용하여 `requests`에서 HTTP `DELETE` リクエ스트를 만드는 방법은 다음과 같습니다:

```python
import requests

# send a DELETE request for the product with id = 75

response = requests.delete('https://api.example.com/products/75')
```

동일하게 `requests.request()`로 DELETE リクエ스트를 수행할 수 있습니다:

```python
import requests

response = requests.request('DELETE', 'https://api.example.com/products/75')
```

### HEAD

[`HEAD`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/HEAD) 메서드는 `GET`과 유사하지만, 실제 body 콘텐츠 없이 レスポンス의 ヘッダー만 요청합니다. 따라서 서버가 `HEAD` リクエスト에 대해 반환하는 レスポンス는 `GET` リクエ스트의 레スポンス와 동등하지만 body 데이터가 없습니다.

Python에서 `requests.head()`를 사용하여 HTTP `HEAD` リクエスト를 수행하십시오:

```python
import requests

# send a HEAD request to the specified URL

response = requests.head('https://api.example.com/resource')
```

같은 방식으로 `requests.request()`로도 `HEAD` リクエスト를 수행할 수 있습니다:

```python
import requests

response = requests.request('HEAD', 'https://api.example.com/resource')
```

## Breaking Down a Response Object From Requests

レスポンス 객체를 다루는 방법을 살펴보겠습니다.

### Response Object

HTTP リクエ스트를 수행한 후 `requests`는 서버로부터 レスポンス를 수신하고 이를 특별한 [Response](https://requests.readthedocs.io/en/latest/api/#requests.Response) 객체로 매핑합니다.

아래의 Python `requests` 예제를 확인해 보십시오:

```python
import requests

response = requests.get('http://lumtest.com/myip.json')

print(response)
```

이는 다음을 반환합니다:

```python
<Response [200]>
```

`response`는 몇 가지 유용한 메서드와 속성을 노출하는 `Response` 객체입니다. 다음 섹션에서 가장 중요한 항목을 살펴보겠습니다!

> **Warning**:
> `requests`는 항상 レスポンス를 반환하지는 않습니다. 오류(예: 잘못된 URL)의 경우 `RequestException`을 발생시킵니다. 아래 로직으로 이 예외를 방어하십시오:

```python
try:

response = requests.get('http://lumtest.com/myip.json')

# handle the response

except requests.exceptions.RequestException as e:

print('An error occurred during the request:', e)
```

### Status Codes

[レスポンス 상태 코드](https://brightdata.co.kr/blog/proxy-101/proxy-error-codes)는 リクエスト의 성공, 실패 또는 기타 상태를 나타내기 위해 서버가 반환하는 표준화된 값입니다.

이는 에러 처리에서 특히 유용하며, 클라이언트가 서로 다른 유형의 오류를 적절히 식별하고 처리할 수 있게 합니다. 예를 들어 `4xx` 상태 코드는 클라이언트 측 오류(예: 잘못된 リクエスト)를 나타내며, `5xx` 상태 코드는 서버 측 오류를 나타냅니다.

상태 코드를 확인하는 것은 일반적으로 `requests` 라이브러리를 사용해 Python에서 レスポンス를 처리할 때의 첫 단계입니다. リクエ스트를 수행한 후에는 항상 レスポンス의 상태 코드를 확인하여 リクエスト 성공 여부를 판단해야 합니다. 레スポンス 객체의 `status_code` 속성을 통해 상태 코드에 접근합니다:

```python
response.status_code # 200
```

수신한 상태 코드에 따라 조건문을 사용하여 다양한 시나리오를 적절히 처리해야 합니다:

```python
import requests

response = requests.get('http://lumtest.com/myip.json')

# check if the request was successful (status code 200)

if response.status_code == 200:

print('Successful request!')

# handle the response...

elif response.status_code == 404:

print('Resource not found!')

else:

print(f'Request failed with status code: {response.status_code}')
```

대부분의 시나리오에서는 성공 リクエ스트와 오류 レスポンス만 구분하면 됩니다. `requests`는 커스텀 [`__bool()__`](https://www.pythontutorial.net/python-oop/python-__bool__/) 오버로드 덕분에 그 과정을 단순화합니다. 구체적으로 `Response` 객체를 조건식에서 직접 사용할 수 있습니다. 그러면 상태 코드가 `200`과 `399` 사이면 `True`, 그렇지 않으면 `False`로 평가됩니다.

즉, 다음 로직으로 リクエ스트의 성공 여부를 확인할 수 있습니다:

```
if response:

print('Successful request!')

# handle the response...

else:

print(f'Request failed with status code: {response.status_code}')
```

### Response Headers

서버 レスポンス의 ヘッダー는 `headers` 속성을 통해 접근합니다:

```python
import requests

response = requests.get('http://lumtest.com/myip.json')

response_headers = response.headers

print(response_headers)
```

이는 다음을 출력합니다:

```
{'Server': 'nginx', 'Date': 'Thu, 09 May 2024 12:51:08 GMT', 'Content-Type': 'application/json; charset=utf-8', 'Content-Length': '279', 'Connection': 'keep-alive', 'Cache-Control': 'no-store', 'Access-Control-Allow-Origin': '*'}
```

보시는 바와 같이 `response.headers`는 딕셔너리처럼 동작하는 객체를 반환합니다. 즉 키로 ヘッダー 값을 접근할 수 있습니다. 예를 들어 レスポンス의 `Content-Type` ヘッダー에 접근하고 싶다고 가정해 보겠습니다. 아래와 같이 할 수 있습니다:

```python
response_headers['Content-Type'] # 'application/json; charset=utf-8'
```

HTTP 사양에서 ヘッダー는 대소문자를 구분하지 않으므로, `requests`는 대소문자 표기에 대해 걱정하지 않고 접근할 수 있게 합니다:

```python
response_headers['content-type'] # 'application/json; charset=utf-8'
```

### Response Content

`requests`는 レスポンス의 payload에 접근하기 위한 여러 속성과 메서드를 제공합니다:

- [`response.content`](https://requests.readthedocs.io/en/latest/api/#requests.Response.content): レスポンス 콘텐츠를 bytes로 반환합니다.
- [`response.text`](https://requests.readthedocs.io/en/latest/api/#requests.Response.text): レスポンス 콘텐츠를 Unicode 문자열로 반환합니다.
- [`response.json()`](https://requests.readthedocs.io/en/latest/api/#requests.Response.json): レスポンス의 JSON 인코딩 콘텐츠를 딕셔너리로 반환합니다.

다음 예제에서 동작을 확인해 보십시오:

```python
import requests

response = requests.get('http://lumtest.com/myip.json')

# access the response as bytes

response_bytes = response.content

print(type(response_bytes))

print(response_bytes)

print()

# retrieve the response as text

response_text = response.text

print(type(response_text))

print(response_text)

print()

# retrieve the response as a JSON-encoded dictionary

response_json = response.json()

print(type(response_json))

print(response_json)

print()
```

`http://lumtest.com/myip.json`은 호출자의 IP에 대한 정보를 반환하는 특별한 エンドポイント입니다. 위 스니펫의 결과는 다음과 비슷할 것입니다:

```json
<class 'bytes'>

b'{"ip":"45.85.135.110","country":"US","asn":{"asnum":62240,"org_name":"Clouvider Limited"},"geo":{"city":"Ashburn","region":"VA","region_name":"Virginia","postal_code":"20149","latitude":39.0469,"longitude":-77.4903,"tz":"America/New_York","lum_city":"ashburn","lum_region":"va"}}'

<class 'str'>

{"ip":"45.85.135.110","country":"US","asn":{"asnum":62240,"org_name":"Clouvider Limited"},"geo":{"city":"Ashburn","region":"VA","region_name":"Virginia","postal_code":"20149","latitude":39.0469,"longitude":-77.4903,"tz":"America/New_York","lum_city":"ashburn","lum_region":"va"}}

<class 'dict'>

{'ip': '45.85.135.110', 'country': 'US', 'asn': {'asnum': 62240, 'org_name': 'Clouvider Limited'}, 'geo': {'city': 'Ashburn', 'region': 'VA', 'region_name': 'Virginia', 'postal_code': '20149', 'latitude': 39.0469, 'longitude': -77.4903, 'tz': 'America/New_York', 'lum_city': 'ashburn', 'lum_region': 'va'}}
```

세 가지 서로 다른 レスポンス 형식을 확인하십시오. 딕셔너리로서 `response.json()`은 데이터 접근을 단순화하므로 특히 유용합니다:

```python
response_json['country'] # 'US'
```

자세한 내용은 [Python에서 JSON을 파싱하는 방법](/blog/how-tos/parse-json-data-with-python) 가이드를 확인하십시오.

### Response Cookies

[HTTP Cookie](/blog/web-data/http-cookies)는 ヘッダー로 정의되지만, `Response` 객체는 이를 다루기 위한 특별한 `cookies` 속성을 제공합니다. 이는 서버가 되돌려 보낸 Cookie를 포함하는 [http.cookiejar](https://docs.python.org/3/library/http.cookiejar.html) 객체를 반환합니다.

Python `requests` 라이브러리에서 レスポンス 객체로부터 Cookie에 접근하는 방법을 보여주는 예제를 확인해 보십시오:

```python
import requests

# define the login credentials

credentials = {

'username': 'example_user',

'password': 'example_password'

}

# send a POST request to the login endpoint

response = requests.post('https://www.example.com/login', data=credentials)

# access the cookies set by the server

cookies = response.cookies

# print the cookies received from the server

for cookie in cookies:

print(cookie.name, ':', cookie.value)
```

위 예시 스니펫은 다음과 같은 출력을 만들 수 있습니다:

```
session_id : be400765483cf840dfbbd39

user_id : 7164

expires : Sat, 01 Jan 2025 14:30:00 GMT
```

## Request Customization With the Python Requests Library

HTTP リクエ스트에는 종종 특별한 필터링 パラメータ와 커스텀 ヘッダー가 포함됩니다. `requests`에서 이를 지정하는 방법을 살펴보겠습니다.

### Query String Parameters

[쿼리 パラメータ](https://www.semrush.com/blog/url-parameters/)(URL パラメータ라고도 함)는 HTTP リクエ스트에서 URL 끝에 추가되는 추가 パラメータ입니다. 이는 보통 데이터를 필터링하고 レスポンス를 커스터마이징하는 방법 등, リクエ스트에 대한 추가 정보를 서버에 제공합니다.

다음 URL을 고려해 보십시오:

`https://api.example.com/data?key1=value1&key2=value2`

이 예제에서 `?key1=value1&key2=value2`는 쿼리 문자열이며 `key1`과 `key2`는 쿼리 パラメータ입니다.

쿼리 문자열은 `?`로 시작하며, 등호(`=`)로 구분된 키-값 쌍으로 구성되고 `&`로 연결됩니다. 특히 선택적 パラメータ를 다룰 때 Python 코드에서 이 쿼리 문자열을 프로그램적으로 지정하는 것은 항상 쉽지 않습니다. 그래서 `requests`는 `params` 옵션을 제공합니다:

```python
import requests

# define query parameters as a dictionary

params = {

'page': 1,

'limit': 10,

'category': 'electronics'

}

# send a GET request to the following URL:

# 'https://api.example.com/products?page=1&limit=10&category=electronics'

response = requests.get('https://api.example.com/products', params=params)
```

동일하게, 파라미터를 튜플 리스트로 `requests`에 전달할 수도 있습니다:

```python
import requests

# define query parameters as a list of tuples

params = [

('page', '1'),

('limit', '10'),

('category', 'electronics')

]

response = requests.get('https://api.example.com/products', params=params)
```

또는 `bytes` 문자열로도 전달할 수 있습니다:

```python
import requests

# define query parameters as a bytes string

params = b'page=1&limit=10&category=electronics'

response = requests.get('https://api.example.com/products', params=params)
```

### Request Headers

`requests`에서 HTTP リクエ스트의 ヘッダー를 커스터마이징하려면 `headers` 옵션에 딕셔너리로 전달하십시오. 예를 들어, 다음과 같이 `requests`에서 커스텀 `User-Agent` 문자열을 설정할 수 있습니다:

```python
import requests

# define custom headers

custom_headers = {

'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0.0.0 Safari/537.36',

# other headers...

}

# send a GET request with custom headers

response = requests.get('https://api.example.com/data', headers=custom_headers)
```

### Request Cookies

HTTP Cookie는 ヘッダー를 통해 서버로 전송되지만, `requests`는 이를 커스터마이징하기 위한 전용 `cookies` 옵션을 제공합니다. 다음 예제처럼 사용하십시오:

```python
# define custom cookies

custom_cookies = {

'session_id': 'be400765483cf840dfbbd39',

'user_id': '7164'

}

# send a GET request with custom cookies

response = requests.get('https://www.example.com', cookies=custom_cookies)
```

`cookies`는 딕셔너리 또는 `http.cookiejar` 객체를 받는다는 점에 유의하십시오.

## Other Configurations

`request`는 풍부한 API를 제공하며, 사용 가능한 고급 기법이 많습니다. 그중 가장 관련성이 높은 몇 가지를 살펴보겠습니다!

### Proxy Setup

`requests`에서 プロキシ를 통합하면 HTTP リクエ스트를 プロキシ 서버를 통해 라우팅할 수 있습니다. 이는 IPアドレス를 숨기고, レート制限 장치를 우회하거나, 지리적으로 제한된 콘텐츠에 접근할 수 있는 강력한 메커니즘입니다.

Python `requests` 라이브러리에서 `proxies` 옵션을 사용하여 プロキシ 서버를 통합할 수 있습니다:

```python
import requests

# define the proxy settings

proxy = {

'http': 'http://username:[email protected]:8080',

'https': 'https://username:[email protected]:8080'

}

# Make a request using the proxy

response = requests.get('https://www.example.com', proxies=proxy)
```

전체 튜토리얼은 [Python Requests에서 プロキシ 사용하기](/blog/proxy-101/proxy-with-python-requests) 가이드를 따르십시오.

### Basic Authentication

[HTTP 로그인 메커니즘](https://developer.mozilla.org/en-US/docs/Web/HTTP/Authentication)은 “basic login mechanisms”로 더 잘 알려져 있으며, HTTP 프로토콜에 내장된 간단한 로그인 메커니즘 스킴입니다. 이는 `Authorization` ヘッダー에 [Base64](https://developer.mozilla.org/en-US/docs/Glossary/Base64) 형식으로 인코딩된 사용자명과 비밀번호를 전송하는 방식입니다.

`Authorization` ヘッダー를 수동으로 설정하여 구현할 수도 있지만, `requests`는 이를 위한 전용 `auth` 옵션을 제공합니다. 이는 사용자명과 비밀번호의 튜플을 받습니다. `requests` Python 라이브러리에서 basic login mechanisms을 처리하려면 다음과 같이 사용하십시오:

```python
import requests

# define the username and password for basic login mechanisms

username = 'sample_username'

password = 'sample_password'

# send a GET request with basic login mechanisms

response = requests.get('https://api.example.com/private/users', auth=(username, password))
```

### SSL Certificate Verification

SSL 인증서 검증은 인터넷을 통해 클라이언트와 서버 간의 안전한 통신을 보장하는 데 매우 중요합니다. 동시에, 대상 서버를 신뢰하며 검증을 강제할 필요가 없는 상황도 있습니다.

특히 プロキシ 서버를 통해 HTTP 트래픽을 라우팅할 때 SSL 인증서와 관련된 오류를 만날 수 있습니다. 이 경우 SSL 인증서 검증을 비활성화해야 할 수 있습니다. `requests`에서는 [`verify`](https://requests.readthedocs.io/en/latest/user/advanced/#ssl-cert-verification) 옵션을 통해 이를 수행할 수 있습니다:

```python
import requests

# send a GET request to a website with SSL certificate verification disabled

response = requests.get('https://api.example.com/data', verify=False)
```

### Timeouts

기본적으로 requests는 서버가 응답할 때까지 무기한 대기합니다. 서버에 과부하가 걸렸거나 네트워크가 느려진 경우, 이러한 동작은 문제가 될 수 있습니다.

결코 도착하지 않을 수도 있는 レスポンス를 기다리느라 애플리케이션이 느려지는 것을 방지하기 위해 `requests`에는 [`timeout`](https://requests.readthedocs.io/en/latest/user/advanced/#timeouts) 옵션이 있습니다. 이는 レスポンス를 기다릴 초 수를 나타내는 정수 또는 부동소수 값을 받습니다:

```python
import requests

# timeout after 2 second

response1 = requests.get("https://api.example.com/data", timeout=2)
```

또는 `timeout`은 두 요소(연결 タイムアウト과 읽기 タイムアウト)를 가진 튜플도 받습니다. 아래 예제처럼 지정하십시오:

```python
import requests

# timeout after 2.5 seconds for connections and 4 seconds for reading response

response = requests.get("https://api.example.com/data", timeout=(2.5, 4))
```

리クエ스트가 지정된 연결 タイムアウト 내에 연결을 설정하고 읽기 タイムアウト 내에 데이터를 받으면, レスポンス는 평소처럼 반환됩니다. 그렇지 않고 リクエスト가 タイムアウト되면 `Timeout` 예외가 발생합니다:

```python
import requests

from requests.exceptions import Timeout

try:

response = requests.get("https://api.example.com/data", timeout=(2.5, 4))

except Timeout:

print("The request timed out")
```

## Conclusion

Python `requests` 모듈은 여러 사용 사례를 포괄하는 유용하고 인기 있는 HTTP 라이브러리입니다. 그러나 어떤 HTTP リクエ스트든 사용자의 공개 IP를 노출합니다. 이는 사용자가 누구인지, 어디에 사는지에 대한 정보를 제공하므로 프라이버시에 좋지 않습니다.

IPアドレス를 숨기는 방법은 여러 가지가 있으며, 더 높은 보안과 프라이버시를 달성하는 가장 효과적인 방법은 プロキシ 서버를 사용하는 것입니다. Bright Data는 전 세계 최고의 [プロキシ 서버](https://brightdata.co.kr/proxy-types)를 운영하며, Fortune 500 기업과 20,000명 이상의 고객에게 서비스를 제공합니다.

지금 등록하고 무료 체험을 시작해 보십시오!