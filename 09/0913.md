## HTTP/2 checker
http에서 HTTP/2를 지원하는 지를 알아보기 위한 코드

> 요청 예시
> 
> ![image](https://user-images.githubusercontent.com/64197428/133040720-f774e275-e486-47a4-8d85-b896d8e22ee2.png)

```c

#include <stdio.h>
#include <sys/types.h>
#include <netdb.h>
#include <stdlib.h>
#include <string.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <unistd.h>

int main(int argc, char *argv[])
{
        int s, n, len_in, len_out;
        struct sockaddr_in server_addr;
        struct hostent *host;
        struct sockaddr_in addr;
        char buf[BUFSIZ+1];
        int port;
        int i= 0;
        if(argc!=2) {
                printf("usage : webClient server_addr");
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

        memset(&server_addr, 0, sizeof(server_addr));
        server_addr.sin_family=AF_INET;
        server_addr.sin_addr.s_addr=*((unsigned long *)host->h_addr);
        server_addr.sin_port=htons(80);

        if(connect(s, (struct sockaddr *) &server_addr, sizeof(server_addr)) < 0) {
                printf("can not connect");
                return -1;
        }

        sprintf(buf, "GET / HTTP/1.1\r\nHost: %s\r\nConnection: %s\r\nUpgrade: %s\r\nHTTP2-Settings: %s\r\n\r\n", argv[1], "Upgrade, HTTP2-Settings", "h2c", "<base64url encoding of HTTP/2 SETTINGS payload>");
     
        write(s, buf, strlen(buf));

        memset(buf, 0, sizeof(buf));
        n = read(s, buf, 12);
        printf("%s\n", buf);
        if(strstr(buf, "101"))
                printf("HTTP/2 is supported\n");
        else
                printf("HTTP/2 is not supported\n");
                
         memset(buf, 0, sizeof(buf));
         close(s);
}
```

> 응답 예시
>
> nghttp2.org 입력
> 
> ![image](https://user-images.githubusercontent.com/64197428/133040922-0b494725-1880-47b0-8b6d-65f6cdd88279.png)
>
> '200 OK'라고 응답한 서버는 HTTP/1.1만 지원하는 서버이고 '101'로 응답한 서버는 HTTP/2를 지원하는 서버이다.
