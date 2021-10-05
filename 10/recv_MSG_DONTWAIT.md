## MSG_DONTWAIT
Enables nonblocking operation

만약 operation이 block이면 EAGAIN 또는 EWOULDBLOCK을 반환
```c
n = recv(s, buf, READLEN, MSG_DONTWAIT);
//n에 -1이 넣어진다.
```
> ![image](https://user-images.githubusercontent.com/64197428/135991322-7c6aa6b0-48c0-4eb4-b505-b91ad19c6549.png)
> 
> EAGAIN 오류 반환
