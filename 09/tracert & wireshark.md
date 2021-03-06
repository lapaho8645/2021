## write/read 함수와 send/recv 함수
* recv와 send, read와 write는 대체로 비슷하지만 recv/send에서는 플래그 등 다른 옵션을 사용할 수 있기 떄문에 더욱 전문적이다.
* send/recv는 소켓에서만 작동하고 write/read 함수는 모든 디스크립터에서 작동한다.
## Tracert를 이용한 ip 경로 추적
목적지까지의 경로를 모두 모니터링할 수 있어 ping명령보다 세부적으로 네트워크 문제를 파악할 수 있다.

```
tracert 목적지ip
```
![image](https://user-images.githubusercontent.com/64197428/132463591-5f1e7204-ff8e-4b53-94d6-68e030b8d1a0.png)
## wireshark
오픈 소스 패킷 분석 프로그램으로 네트워크 패킷을 캡쳐하고 분석한다.
#### 실행 화면
![image](https://user-images.githubusercontent.com/64197428/132464822-3f88db3e-5943-4c31-8d98-957cbd197d7d.png)

![image](https://user-images.githubusercontent.com/64197428/132466522-403155c2-f376-4103-9330-baf1151238df.png)

#### 필터링
수 많은 패킷 중에서 원하는 패킷을 찾기 위해 사용

* ex) http를 검색했을 때 프로토콜이 http인 패킷들만 검색
*    tcp.dst port != 80를 검색했을 때 목적지가 tcp포트 80인 패킷을 제외하고 출력
![image](https://user-images.githubusercontent.com/64197428/132467922-a49624a6-82ec-494d-8fe2-cb7ece98f3a7.png)
#### 패킷
![image](https://user-images.githubusercontent.com/64197428/132470422-524582e5-17bf-472f-8e75-4c75c624b014.png)
**1. Packet List**
* No. : 패킷을 수집한 순서
* Time : 패킷이 수집된 시간
* Source : 패킷을 보낸 주소
* Destination : 패킷 도착 주소
* Protocol : 프로토콜 정보
* Length : 패킷의 길이
* Info : 패킷 정보

**2. Packet Details**
* Packet List에서 선택한 패킷에 대한 상세한 정보를 알려준다.

**3. packet Bytes**
* 왼쪽에는 패킷 데이터 오프셋을 나타내고 중간 부분에는 패킷데이터의 16진수로 나타내고 오른쪽에는 아스키 형식으로 값을 나타냄
