## Ingress_Egress
#### Ingress 
외부로부터 서버 내부로 유입되는 네티워크 트래픽
#### Egress
서버 내부에서 외부로 나가는 트래픽 
## 조건부 컴파일
```c
#if 1    //조건이 항상 참
    printf("1\n");
#endif

#if 0    // 조건이 항상 거짓이므로 주석과 같은 효과
    printf("0\n");
#endif
```
