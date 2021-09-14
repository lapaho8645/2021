## pthread_join && pthread_detach
pthread_create 후 반드시 pthread_detach 또는 pthread_join을 사용해주어야 한다.
#### pthread_join
보조 스레드의 종료까지 대기해주는 함수

non-detached로 thread를 생성했을 때 pthread_join을 호출하지 않으면 메모리 누수 발생
```c
int pthread_join(pthread_t th, void **thread_return);
//th는 종료를 기다릴 스레드, trhead_return은 스레드의 리턴 값에 접근할 수 있는 2차원 포인터
```
#### pthread_detach
생성된 스레드를 메인 스레드에서 분리

detached로 thread를 생성하며 pthread_join을 호출하지 않아도 thread 종료 시 자원이 자동으로 반납됨
```c
int pthread_detach(pthead_t thread)
```
두 함수 모두 스레드가 종료하면 사용된 자원에 대해서 free를 한다.
#### pthread_attr_setdetachstate
스레드 속성 값으 주어 생성될 때 detach 속성으로 생성되게 할 수 있다.
```c
int pthread_attr_setdetachstate(pthread_attr_t *attr, int detachstate);
```
```c
pthread_attr_t attr;

phtread_attr_init(&attr);         //초기화
pthread_attr_setdetachstate(&attr, PTHREAD_CREATE_JOINABLE);
pthread_attr_setdetachstate(&attr, PTHREAD_CREATE_DETACHED);
```


#### 차이점
* pthread_join은 스레드가 종료될 때까지 기다리는 함수로 독립적이지 않다. pthread_detach는 기다리지 않고 알아서 끝내도록 하는 방식으로 독립적으로 동작할 수 있다.
* pthread_detach는 독립적으로 동작하는 대신 반드시 자원을 반환해야 한다.
