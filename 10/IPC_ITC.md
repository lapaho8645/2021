## IPC (Inter Process Communications)
프로세스들 사이에 서로 데이터를 주고 받는 방식
- PIPE

![image](https://user-images.githubusercontent.com/64197428/139030930-e95130fd-3dc5-4277-a71f-197e64875272.png)

부모와 자식 프로세스 간에서만 단방향의 데이터 통신용

하나의 프로세스는 데이터를 쓰기만 하고, 다른 하나는 데이터를 읽기만 한다. 한쪽 방향으로만 통신이 가능하기 때문에 Half-Duplex 통신이라고 한다.

- named PIPE

프로세스 통신을 위해 이름이 있는 파일을 사용하기 때문에 부모 프로세스와 무관하게 외부 다른 프로세스들 사이에서 통신이 가능하다. 
- Message Queue

FIFO 자료구조를 가지는 메모리 공간으로 커널에서 관리한다.

- Shared Memory

빠르고 효율적이지만 공간에 대한 접근 제어가 필요

공유 메모리 생성 -> 메모리가 필요한 프로세스는 필요할 때마다 자신의 프로세스에 첨부한 후 사용

- Semaphore

공유 자원에 대한 접속을 제어하여 프로세스 간 데이터를 동기화하고 보호한다.

## ITC (Inter Thread Communications)
메시지 큐를 사용하여 스레드 사이에 서로 데이터를 주고 받는 방식

