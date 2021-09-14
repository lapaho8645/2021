## 도메인을 IP로 바꿔주는 함수
#### gethostbyname
> struct hostent *를 반환
```c
#include <netdb.h>
struct hostent *gethostbyname(const char *name);
```
* struct hostent
```c
struct hostent {
  char  *h_name;         
  char  **h_aliases;
  int   h_addrtype;       //AF_INET 또는 AF_INET6
  int   h_length;
  char  **h_addr_list;
}
```
#### getaddrinfo
```c
#include <sys/types.h>
#include <sys/socket.h>
#include <netdb.h>

int getaddrinfo(const char *host, const char *service, const struct addriinfo *hints, struct addrinfo **result);
//host : 도메인 이름이거나 ip주소
//service : 포트 번호
//hints : result에 해당하는 주소 구조체 안에 정보 입력
//result : addrinfo를 사용하는 링크 리스트
```
* struct addrinfo
```c
struct addrinfo { 
  int               ai_flags;       //AI_PASSIVE를 넣으면 localhost에 대한 정보를 얻을 수 있다.
  int               ai_family;      //IPv4를 이용하면 AF_INET, IPv6을 이용하면 AF_INET6
  int               ai_socktype;    //스트림 소켓이면 SOCK_STREAM, 데이터그램 소켓이면 SOCK_DGRAM
  int               ai_protocol;    //특정 프로토콜 지정
  char              *ai_canonname;  //host의 별칭  
  size_t             ai_addrlen;    //ai_addr의 길이
  struct sockaddr   *ai_addr;       //소켓 주소 구조체를 가르키는 포인터
  struct addrinfo   *ai_next;       //다음 데이터 포인터
}
```
## 빅 엔디안 & 리틀 엔디안
#### 빅 엔디안
큰 단위부터 메모리에 적는 방식으로 부호비트 확인이 빠름

네트워크 통신에서는 빅엔디안 방식을 사용
#### 리틀 엔디안
작은 단위부터 메모리에 적는 방식으로 연산이 빠름

일반 PC는 보통 리틀 엔디안 방식으로 구현

#### 빅 엔디안 <-> 리틀 엔디안
* htons() - "Host to Network Short"  : 리틀 엔디안에서 빅 엔디안으로 short만큼
* htonl() - "Host to Network Long"   : 리틀 엔디안에서 빅 엔디안으로 long만큼
* ntohs() - "Network to Host Short"  : 빅 엔디안에서 리틀 엔디안으로 short만큼
* ntohl() - "Network to Host Long"   : 빅 엔디안에서 리틀 엔디안으로 long만큼
## 문자열 자르기 함수 strtok
```c
char* strtok(char* str, char* delimiters);
//delimiters를 기준으로 문자열을 자름
```
* 예시
```c
int main(){
  char * token;
  char buf[1024] = "HTTP/1.1 101 Switching Protocols\r\nConnection: Upgrade\r\nUpgrade: h2c";
  token = strtok(buf, " ");
  while(token != NULL){
    printf("%s\n", token);
    if(!strcmp(token, "101"))
       break;
    token = strtok(NULL, " ");      //strtok 함수는 방금 전에 분리한 문자열의 분리 지점 바로 다음 값을 기억하고 있기 때문에 NULL을 첫번째 인자를 주면 기억한 곳으로 부터 분리를 시도한다.
  }
  return 0;
}
```
