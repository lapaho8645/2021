## JSON(JavaScript Object Notation)
* 네트워크를 통해 데이터를 주고 받는 데 자주 사용되는 경량의 데이터 형식
* 속성-값 쌍으로 이루어져 있으며 데이터를 저장하거나 전송할 때 사용

#### JSON 형식
1. name-value 형식의 쌍
```
{ String key : String value }
```
2. 값들의 순서화된 리스트 형식
```
{ String key : [value1, value2, ...] }
```
* 형식 예
```
{
  "name" : "jspark",
  "age" : "23",
  "interests" : ["C", "Java", "Python"]
}
```
## JSON 파싱
JSON 형식의 문자열을 객체로 변환하는 것
#### C에서 JSON 파싱
* jansson 라이브러리 사용
```c
#include <jansson>
```
* 컴파일 옵션
> -ljansson 추가
```
gcc sample.c -o sample -ljansson
```
