## HTTP 요청과 응답
![image](https://user-images.githubusercontent.com/64197428/132800202-3630e421-0c56-4863-81de-884ba83b512e.png)

### HTTP 요청
#### Start Line
공백으로 구분지어 진다.
* 첫 번째로 GET, PUT, POST 또는 HEAD, OPTIONS과 같은 HTTP 메서드로 서버가 수행해야 할 동작을 나타낸다.
* 두 번째로 주로 URL, 또는 프로토콜, 포트, 도메인의 절대 경로 등을 나타낸다.
* 세 번째로 hTTP 버전을 나타낸다.
#### Header
요청이 들어가는 HTTP 헤더는 대소문자 구별 없이 문자열 다음에 콜론이 붙으며, 그 뒤에 오는 값은 헤더에 따라 달라진다.
* General 헤더
* Request 헤더
* Entity 헤더 
![image](https://user-images.githubusercontent.com/64197428/132800928-8f8f8d40-828f-4b5b-be75-6dc3a2d056d9.png)
#### Body
GET, HEAD, DELETE, OPTIONS처럼 리소스를 가져오는 요청은 본문이 필요 없다. POST 요청인 경우 업데이트를 하기 위해 서버에 데이터를 전송하는데 이때 사용된다.

### HTTP 응답
#### Status Line
* 첫 번째로 프로토콜의 버전을 나타낸다.
* 두 번째로 요청의 성공 여부를 나타낸다.
* 세 번째로 짧고 간결하게 상태 코드에 대한 설명을 나타낸 상태 텍스트를 나타낸다.
#### Headers
요청이 들어가는 HTTP 헤더는 대소문자 구별 없이 문자열 다음에 콜론이 붙으며, 그 뒤에 오는 값은 헤더에 따라 달라진다.
* General 헤더
* Request 헤더
* Entity 헤더 
![image](https://user-images.githubusercontent.com/64197428/132801309-ffaeb46e-30e4-44ac-92f3-43303b38214d.png)
#### Body
