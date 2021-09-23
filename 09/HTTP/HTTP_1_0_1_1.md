## HTTP 1.0 vs HTTP 1.1
#### Persistent Connection(Keep alive)
HTTP 1.0(Multiple Connections)은 요청 컨텐츠마다 TCP 세션을 맺어야 하지만 HTTP 1.1(Persistent Connection)은 Persistent 기능을 이용하여 한 개의 TCP 세션을 통해 여러 개의 컨텐츠 요청이 가능하다.
> Keep-alive에서는 서버들이 설정한 시간이 지나면 타임 아웃되어 연결이 끊긴다.
>
> 데이터를 빈번하게 주고 받아야할 때 유용한 기능이다. 그렇지 않은 경우 오히려 성능을 하락시킬 수 있다.

![image](https://user-images.githubusercontent.com/64197428/134464765-9516edb7-a69f-437a-9e8e-d7860287ed0e.png)

#### Pipelining
HTTP 1.0에서는 첫번째 요청을 보내고 첫번째 요청에 대한 응답을 받아야 두번째 요청을 보내는 반면, HTTP 1.1에서는 여러 요청을 보내고 이에 대한 각각의 응답을 받아 처리한다.

![image](https://user-images.githubusercontent.com/64197428/134465275-99afadb7-23c2-480d-a6bb-45659013b629.png)

#### Host Header
HTTP 1.0에서는 하나의 IP에 여러 개의 도메인을 운영할 수 없어 도메인만큼 서버의 개수가 늘어날 수 밖에 없다.

HTTP 1.1에서는 Host 헤더를 추가하여 버츄얼 호스팅이 가능해졌다.

## 예제
#### HTTP 1.0으로 요청했을 때
HTTP 1.0의 Connection 기본 값이 Close이기 때문에 바로 연결을 닫음
```c
//Request문
GET dapi.kakao.com HTTP/1.0
Host: /v2/local/research/keyword.json?query=eluon
Authorization: KakaoAK <API 키>
```
![image](https://user-images.githubusercontent.com/64197428/134467737-320a2871-91f5-400a-901d-72034f68bb99.png)

#### HTTP 1.1로 요청했을 때
HTTP 1.1의 Connection 기본 값이 keep-alive이기 때문에 타임 아웃되어 연결이 끊기기 전까지 지연 발생 
```c
//Request문
GET dapi.kakao.com HTTP/1.1
Host: /v2/local/research/keyword.json?query=eluon
Authorization: KakaoAK <API 키>
```
![image](https://user-images.githubusercontent.com/64197428/134467871-4f56097f-7ef2-457d-aca7-8b04a1713fb9.png)
> HTTP 1.1로 요청하면서 지연을 발생시키지 않기 위해 헤더에 Connection을 Close로 설정할 수 있다.
> ```c
> //Request문
> GET dapi.kakao.com HTTP/1.1
> Host: /v2/local/research/keyword.json?query=eluon
> Connection: close
> Authorization: KakaoAK <API 키>
> ```
