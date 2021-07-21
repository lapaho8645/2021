## 목록

> ## [ㄴㄴㄴ](#vi-시작-명령어)
> ## [vi 커서 ](#vi-커서-명령어)

프로토콜
======

## 프로토콜
* 컴퓨터나 통신 장비 사이에서 메시지를 주고 받기 위해 설계된 일련의 규칙 체계
* Syntax, Semantic, Actions
* 프로토콜들의 역할을 분담하여 특정 서비스를 제공하기 위한 Protocol의 계층별 집합 
* Protocol Data Unit : 발송지/목적지 주소, 사용자 정보, 오류 검출 정보, 흐름 제어 정보
![image](https://user-images.githubusercontent.com/64197428/126431981-3f6acb48-fee7-4f79-9bd8-8dcfd17e4e43.png)
## vi 시작 명령어

## OSI 7 Layer Architecture
데이터를 전송할 때 각각의 층에서 헤더를 붙이는 과정을 캡슐화라고 하고, 전송된 데이터의 헤더를 벗기는 과정을 디캡슐레이션이라고 한다. 각각의 층마다 요청과 응답을 하면서 상호작용하기 떄문에 서버와 클라이언트 관계라고 할 수 있다. 
#### 1. Physical Layer
* **비트** 단위의 정보를 물리적 매체를 통해 전자기적 신호나 광 신호로 전달
> 장비 : 허브, 리피터
#### 2. Data Link Layer
* 하나의 **프레임**을 오류없이 안전하게 전송하는 것이 목적
> 장비 : 브리지, 스위치
#### 3. Network Layer
* **패킷**을 발신지로부터 목적지로 전달하는 Packet Path 제공
* Routing, Flow Control, Error Control 수행
> 장비 : 라우터
> 
> 프로토콜 : IP, ICMP, IGMP
#### 4. Transport Layer
* 메시지를 **Segmentation/Reassembly**
* 정보 전송, Flow Control, Checksum 방식으로 전송에러 검출
> 장비 : 게이트웨이
> 
> 프로토콜 : TCP, UDP, ARP
#### 5. Session Layer
* 응용 간의 질서 제어
#### 6. Presentation Layer
* 이해할 수 있는 포멧 변환
#### 7. Application Layer
* 사용자가 네트워크에 접급할 수 있게 해주며 사용자 응용프로그램간에 정보교환을 담당
> 프로토콜 : DHCP, DNS, FTP, HTTP
## TCP/IP Architecture
#### 1. Network Interface Layer
* 노드간의 신뢰성 있는 데이터 전송을 담당
> MAC 주소
>
> 프로토콜 : Ethernet, TokenRing
#### 2. Internet Layer
* 데이터를 정의하고 데이터의 경로를 배정하는 라우팅을 담당
> IP 주소
#### 3. Transport Layer
* 목적지까지 오류 없이 데이터를 전송
> 포트 번호
#### 4. Application Layer
* 전송 계층을 기반으로 한 다수의 프로토콜과 응용 프로그램을 포괄
> 소켓
## vi 커서 명령어 
## 포트와 소켓
#### 포트
포트는 네트워크를 통해 데이터를 주고 받는 프로세스를 식별하기 위해 호스트 내부적으로 프로세스가 할당받는 고유한 값이다. 메시지가 목적지 호스트에 도착하면 호스트 내에서 특정 포트번호를 할당받은 프로세스를 찾아 데이터를 전달하게 된다. 데이터를 보내는 프로세스, 데이터를 받는 프로세스 둘 다 포트 번호를 할당받아야 한다.
#### 소켓
프로세스가 네트워크를 통해서 데이터를 주고 받기 위해 열어야 하는 것으로 소켓을 열기 위해서는 호스트에 할당된 IP주소, 포트 넘버, 프로토콜 등이 필요하다. 

Internetworking Device
=====================
#### Repeater
* 거리가 증가할수록 감쇄되는 신호를 증폭하여 연결된 네트워크로 전송
* 신호를 재생하여 전달되는 거리를 증가
#### Bridges
* 
