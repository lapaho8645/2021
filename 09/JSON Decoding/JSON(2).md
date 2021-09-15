## JSON 함수
#### json_t
jasson API에서 JSON 전체적인 값을 나타내기 위한 변수로 항상 포인터를 통해 사용된다.
#### json_typeof
JSON 값의 유형을 반환
```c
int json_typeof(const json_t *json);
```
> |index|enum json_type|
> |------|------|
> |0|JSON_OBJECT|
> |1|JSON_ARRAY|
> |2|JSON_STRING|
> |3|JSON_INTEGER|
> |4|JSON_REAL|
> |5|JSON_TRUE|
> |6|JSON_FALSE|
> |7|JSON_NULL|
#### json_loads
JSON 문자열 입력에 대해 디코딩 후 포함된 배열이나 개체를 반환, 오류가 발생하면 NULL을 반환
```c
json_t *json_loads(const char *input, size_t flags, json_error_t *error);
//flags는 데이터 인코딩 방식을 제어하는 변수로 기본값은 0
```
#### json_object_size
object의 요소 개수를 반환, JSON object가 아니면 0을 반환
```c
size_t json_object_size(const json_t *object);

```
#### json_object_foreach
object에 포함된 모든 key와 value 항목들을 확인
```c
const char *key;
json_t *value;

json_object_foreach(obj, key, value) {
    /* block of code that uses key and value */
}
```
#### json_array_get
배열에서 해당 index 위치에 있는 요소 반환
```c
json_t *json_array_get(const json_t *array, size_t index);
```
#### json_array
새로운 빈 JSON 배열을 반환
```c
json_t *json_array(void)
```
#### json_array_append
array의 마지막에 value값을 추가
```c
int json_array_append(json_t *array, json_t *value);
```
#### json_string
value값이 들어있는 새로운 JSON string 반환
```c
json_t json_string(const char*value);
```
#### json_dumps
json의 내용을 문자열로 반환
```c
char *json_dumps(const json_t *json, size_t flags);
//flags에 JSON_ENCODE_ANY를 입력하면 모든 값을 인코딩할 수 있다.
```
#### json_dump_file
json의 내용을 path 경로에 작성
```c
int json_dump_file(const json_t *json, const char *path, size_t flags);
//flags에 JSON_ENCODE_ANY를 입력하면 모든 값을 인코딩할 수 있다.
```

