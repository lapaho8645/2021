## 카카오 API 사용하기
#### Rest API Key 발급
> https://developers.kakao.com/ 접속 후 "내 애플리케이션" 클릭
>
>![image](https://user-images.githubusercontent.com/64197428/133574414-f6efdf9d-6136-4767-bb76-078cc83e8306.png)

> "애플리케이션 추가하기" 클릭 후 앱 아이콘, 앱 이름, 사업자 명 입력
>
> ![image](https://user-images.githubusercontent.com/64197428/133574687-dc576233-5098-4c31-b4a4-0933ef2f13f2.png)

> 내 애플리케이션 > 앱 설정 > 요약 정보 > 앱 키에서 REST API 키 확인
>
> ![image](https://user-images.githubusercontent.com/64197428/133575157-8f338518-a0f1-44e3-b3da-d5a2e8a1f9e3.png)

#### 카카오 API 중 "키워드로 장소 검색" 활용하기
https://developers.kakao.com/docs/latest/ko/local/dev-guide#search-by-keyword
* 요청 예시

![image](https://user-images.githubusercontent.com/64197428/133575849-400240d9-c543-4dda-8658-0defe92cc5ec.png)

* 키워드로 장소 검색 예제
```c

#include <stdio.h>
#include <sys/types.h>
#include <netdb.h>
#include <stdlib.h>
#include <string.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <unistd.h>

#define MSGLEN 1024
#define READLEN 4072
int main(int argc, char *argv[])
{
        char message_fmt[] = "GET %s HTTP/1.1\r\nHost: %s\r\nAuthorization: KakaoAK %s\r\n\r\n";
        char buf[READLEN];
        char message[MSGLEN];
        int s, n, left_len, sent_len, recv_len;
        struct sockaddr_in server_addr;
        struct hostent *host;
        int port;
        int byte;
        int i= 0;
        char *token;
        if(argc < 4) {
                printf("usage : %s <Host> <Resource> <API_KEYS>\n", argv[0]);
                printf("ex) dapi.kakao.com /v2/local/search/keyword.json?query=<query> <API_KEYS>\n");
                return -1;
        }

        if((host=gethostbyname(argv[1]))== NULL){
                printf("gethostbyname error\n");
                exit(-1);
        }
        if((s=socket(PF_INET, SOCK_STREAM, 0)) < 0) {
                printf("can not create socket\n");
                return -1;
        }

        sprintf(message, message_fmt,argv[2],argv[1], argv[3]);


        memset(&server_addr, 0, sizeof(server_addr));
        server_addr.sin_family=AF_INET;
        memcpy(&server_addr.sin_addr.s_addr, host->h_addr, host->h_length);
        server_addr.sin_port=htons(80);

        if(connect(s, (struct sockaddr *) &server_addr, sizeof(server_addr)) < 0) {
                printf("can not connect");
                return -1;
        }
        left_len = strlen(message);
        sent_len = 0;
        do{
                byte = write(s, message+sent_len, left_len - sent_len);
                if(byte < 0)
                        printf("write error\n");
                if(byte == 0)
                        break;
                sent_len += byte;
        }while(sent_len < left_len);

        memset(buf, 0, sizeof(buf));
        left_len = sizeof(buf) - 1;
        recv_len = 0;

        do{
                memset(buf, 0, sizeof(buf));
                n = read(s, buf, READLEN);
                printf("%s ", buf);
                if(n < 0)
                        printf("read error\n");
                if(n == 0)
                        break;
        }while(1);

        printf("\n");

        close(s);
}
```
#### 검색 결과
![image](https://user-images.githubusercontent.com/64197428/133579499-ce40cccf-3f02-4514-9e54-76c1ac6304c8.png)
