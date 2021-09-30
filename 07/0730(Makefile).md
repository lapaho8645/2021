## Makefile
* target: 명령어가 수행되어 나온 결과 파일 이름
* dependency
* command : dependency에 정의된 파일의 내용이 바뀌거나 target이 없을 때 명령어가 실행됨
* 입력파일을 변경했을 때 자동으로 결과 파일을 변경하고 싶을 때 사용한다.
* 컴파일 양이 많을 때 나누어 컴파일을 시도할 수 있어 프로그램 개발 및 유지에 용이하다.
* 명령어 부분은 반드시 Tab으로 시작해야 한다.

#### 매크로
* $@ : 현재 taget의 이름
* $* : 확장자를 제외한 현재 target의 이름
* $< : 현재 dependency 중 첫 번째 파일 이름
* $^ : 현재 target의 종속 항목 리스트

```c
TARGET=test
OBJ=test.o test1.o test2.o
CC=gcc
CFLAGS=-c

all: $(TARGET)

$(TARGET):$(OBJ) $(TARGET)
    $(CC) -o $(TARGET) $(OBJ)

test.o : test.c
    $(CC) $(CFLAGS) $<

test1.o : test1.c
    $(CC) $(CFLAGS) $<
    
test2.o : test2.c
    $(CC) $(CFLAGS) $<
clean :
    rm -rf $(TARGET) $(OBJ)

```
#### 패턴 규칙
```c
test.o : test.c
    $(CC) $(CFLAGS) $<

test1.o : test1.c
    $(CC) $(CFLAGS) $<
    
test2.o : test2.c
    $(CC) $(CFLAGS) $<
/********************************************/
.c.o :  
  $(CC) $(CFLAGS) $<          //패턴 규칙을 통해 한문장으로 변경 
```

#### 리눅스 디렉토리 구조
* / : 가장 중요한 최상위 디렉토리
* /bin : 기본 명령어들이 들어있는 디렉토리
* /sbin : 시스템 관리에 관련된 실행 명령어들이 들어있는 디렉토리
* /etc : 시스템 환경 설정이 있는 디렉토리
* /var : 자료 데이터가 변경될 때 변경된 자료들이 저장되는 곳으로 로그들을 저장하는 디렉토리
* /boot : 부팅에 핵심적인 커널 이미지와 부팅 정보 파일을 담고 있는 디렉토리
* /home : 일반 사용자의 홈 디렉토리
* /lib : 프로그램들이 의존하고 있는 라이브러리 파일이 있는 디렉토리
* /dev : 물리적인 장치들이 파일화되어 있는 디렉토리
* /opt

![image](https://user-images.githubusercontent.com/64197428/127618638-99c2b032-56ba-47b0-a033-96f80b673191.png)

#### grep
원하는 문자열이 들어간 행을 찾아 출력하는 명령어
* grep [문자열][파일명]
* grep [^문자열] : 문자열로 행이 시작되는 경우 출력 
* grep [문자열&] : 문자열로 행이 끝나는 경우 출력
* grep [문자1\|문자2] : 여러 문자열을 한번에 검색
* grep -A2 [문자열] : 해당 문자열이 들어강 행을 포함해 아래 2행 출력
* grep -v [문자열] : 해당 문자를 제외한 행 출력
* grep [문자열]* : 현재 위치의 모든파일 (*)에서 특정 문자열 출력

![image](https://user-images.githubusercontent.com/64197428/127617826-20f47c47-8818-4970-b620-8ef8c4664baa.png)



