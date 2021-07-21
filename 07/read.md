0720
======
## 자료형
![image](https://user-images.githubusercontent.com/64197428/126418632-88350812-1730-4a05-b11b-126ae2b94878.png)
## 구조체
* 1개 이상의 다른 데이터형을 갖는 변수들을 모아둔 집합체로 사용자가 새롭게 정의할 수 있는 사용자 정의 타입
* 구조체가 포함하고 있는 요소들 중 가장 큰 값을 기준으로 그 값의 배수만큼의 크기를 가지기 때문에 여분의 바이트를 붙여 계산
```c
typedef struct{
  char name[10];
  int age;          //해당 구조체의 크기는 12 + 4 + 12 = 28byte
  char phone[10];
  }header
```
```c
typedef struct{
  char name[10];
  char phone[10];     //해당 구조체의 크기는 20 + 4 = 24byte
  int age;
  }header;
```
* 메모리에 패딩이 생기는 이유는 CPU가 메모리에 접근하는 것을 최소화하여 동작속도를 빠르게 하기 위해서이다.  
## 리눅스 명령어
* pwd : 현재 작업중인 디렉토리 정보 출력
* cd : 디렉토리를 이동하는 명령어
* ls : 현재 위치 파일 목록 조회하는 명령어
* touch : 파일의 용량이 0인 파일 생성, 날짜 변경하는 명령어
* mkdir : 디렉토리 생성
* cp : 파일 복사
* mv : 파일 이동
* rm : 파일 제거
* cat : 파일의 내용을 화면에 출력하거나 파일을 만듦
* redirection : 화면에 출력되는 결과를 파일로 저장
  - 명령 > 파일 : 명령의 결과를 파일로 저장
    + cat fname1 fname2 > fname3 : fname1, fname2를 출력하고 fname3이라는 파일에 저장
  - 명령 >>  파일 : 명령의 결과를 파일에 추가
    + cat fname4 >> fname3 : fname3에 fname4의 내용을 추가
  - 명령 < 파일 : 파일의 데이터를 명령에 입력
    + cat < fname1 : fname1의 내용을 출력
* alias : 자주 수행하는 명령어를 쉽게 사용할 수 있도록 설정
## 이동 통신 개요
### 1. 이동 통신의 발달
* 1G: 음성 통화만 가능한 아날로그 통신 방식
* 2G: 음성과 간단한 인터넷 메일을 주고 받을 수 있는 방식 - CDMA
* 3G: 음성 문자 전송 속도 향상, 인터넷, 동영상, 멀티미디어 통신
* 4G: 음성 데이터 멀티미디어 인터넷 연결의 고속/고품질/대용량/보안/저비용
* 5G: 초고화질 실시간 영상/자율주행 드론 서비스/IoT/VR/AR, 초고속/대용량/초저지연/초연결
### 2. 네트워크 구조
* MS(Mobile Station)
  - 가입자 식별/인증을 위한 IMSI값이 들어가 있음
* eNB(Evolved Node B)
  - LTE 기지국이라고 불리며 UE와 LTE 네트워크 간에 무선 연결을 제공하는 장비
  - MS와 eNB는 무선 연결
* MME(Mobility Management Entity)
  - eNB와 MME는 유선 연결
  - LTE 망의 두뇌 역할을 하는 장비로 HSS로부터 MS를 인증하기 위한 Key 정보를 받아 MS를 인증
  - 가입자의 Mobility 상태를 관리
* HSS(Home Subscriber Server)
  - MME와 HSS는 유선 연결
  - MS 별로 인증하기 위한 Key 정보와 가입자의 프로파일을 가지고 있는 LTE망의 중앙 DB
  - IMSI(이동 국가 코드 + 이동 네트워크 코드 + 이동 가입자 식별 번호)와 MSISDN(일상 생활에서 사람들이 발신과 착신에 사용하는 번호 정보)가 있음


