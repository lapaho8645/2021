## telnet 사용
* 별도의 클라이언트 프로그램을 구현하지 않고도 텔넷으로 이미 컴퓨터에서 운용 중인 서비스에 연결해 볼 수 있다.
* 해당 서비스를 운용 중인 컴퓨터의 IP 주소와 포트 번호를 알고 있어야 한다는 전체가 따른다.
#### 설치
```
$ yum install telnet -y
```
#### 설치 확인
```
$ rpm -qa|grep telnet
```
![image](https://user-images.githubusercontent.com/64197428/132288175-4c98678c-37ba-4e48-bc38-3bc5505806e7.png)
#### 아파치 서버 시작
```
systemctl start httpd
```
#### 아파치 서버 상태 확인
```
systemctl status httpd
```
![image](https://user-images.githubusercontent.com/64197428/132288247-dd45ee95-9934-43a5-b250-5a0ca70278c7.png)
#### 서버 루트 디렉토리 확인
1. httpd.conf 파일 확인 (설치된 컴퓨터마다 httpd.conf 파일 위치가 다름)
 
![image](https://user-images.githubusercontent.com/64197428/132311740-07a66ce1-0313-489f-b1a2-57e644f72e78.png)

2. ServerRoot 확인

![image](https://user-images.githubusercontent.com/64197428/132312594-5d88ab35-3fbe-47ad-a1c1-c37a98677790.png)

#### 문서 홈 디렉토리 확인
1. httpd.conf 파일 확인 (설치된 컴퓨터마다 httpd.conf 파일 위치가 다름)

![image](https://user-images.githubusercontent.com/64197428/132311740-07a66ce1-0313-489f-b1a2-57e644f72e78.png)

2. DocumentRoot 확인

![image](https://user-images.githubusercontent.com/64197428/132312717-85193a0d-6496-4258-b026-72990da862b9.png)

#### 서비스 연결
```
$ telnet 호스트_IP_주소 포트_번호
```
DocumentRoot 폴더에 있는 index.html파일을 요청
![image](https://user-images.githubusercontent.com/64197428/132311404-8cef9997-5bd9-4ed8-9174-0aac93f1c941.png)

