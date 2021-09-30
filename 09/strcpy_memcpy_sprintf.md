## memcpy
```c
void *memcpy(void *dest, const void *src, size_t byte);
```
문자열의 종료 문자인 NULL 여부를 확인하지 않고 byte 수만큼 복사

자료형에 상관 없이 지정한 byte 수만큼 복사 (문자 배열, 구조체,,,)

문자열 끝의 NULL을 복사해주지 않기 때문에 
## strcpy
```c
char *strcpy(char *dest, const char *src);
```
바이트 수를 입력하지 않기 때문에 src 문자열이 반드시 '\0'로 끝나야 한다.

## sprintf
```c
int sprintf(char *dest, const char *format-string, argument-list);
```
사용자가 원하는 대로 문자열 형식을 지정하여 복사

마지막 NULL 문자를 계산하지 않고 dest에 작성된 바이트 수를 반환

## memcpy vs strcpy
strcpy는 매번 해당 문자가 '\0'인지 확인하는 과정이 있고 memcpy는 메모리 관점에서의 복사이기 때문에 대체로 memcpy()가 더 빠르다.
