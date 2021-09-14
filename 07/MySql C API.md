## MySql C API 작성

#### 데이터 베이스 접속
```c
   conn = mysql_init(NULL);

    if(!mysql_real_connect(conn, "127.0.0.1", "사용자", "비밀번호", NULL, 0, NULL, 0)){
        printf("cannot connect");
        exit(1);
    }
    else{
        if(mysql_select_db(conn, "데이터베이스 이름")){
            printf("cannot use databases");
            exit(1);
        }
    }
```

#### void query(MYSQL *conn, const char *query_buffer)
mysql구조체와 query_buffer을 받아 쿼리를 수행하고 결과를 출력해주는 함수


```c 
  int i;
        MYSQL_ROW row;
        MYSQL_FIELD * field;
        if(mysql_query(conn, query_buffer)){        //쿼리 수행
            printf("query failed : %s\n", query_buffer);
            printf("errMsg : %s\n", mysql_error(conn));

        }
        result = mysql_use_result(conn);      //수행 결과를 한 개의 ROW씩 받아온다.
        while((row = mysql_fetch_row(result)) != NULL){     //데이터를 0으로 시작하는 숫자형 인텍스 배열로 반환
            for(i = 0; i < mysql_num_fields(result);i++){          //결과값의 필드 개수를 반환
                if(i == 0){
                    while(field = mysql_fetch_field(result))      //필드에 대한 정보를 출력
                        printf("%-25s|", field->name);
                    printf("\n");
                }
                printf("%-25s|", row[i]? row[i] : "NULL");      //데이터 출력
            }
            printf("\n");
        }

        mysql_free_result(result);      //메모리 해제
}
```

#### 1. 테이블 조회
* 코드
```c
  sprintf(query_buffer, "%s", "show tables");
  query(conn, query_buffer);
```
* 쿼리문
```c
   show tables
 ```
* 결과

![image](https://user-images.githubusercontent.com/64197428/127121647-30b7adce-6c02-4e34-b609-f9e233fe7662.png)


#### 2. 테이블 구조 확인
* 코드
```c
  printf("table name: ");
  scanf("%[^\n]s",&table_name);
  getchar();
  sprintf(query_buffer, "desc %s",  table_name);
  query(conn, query_buffer);

```
* 쿼리문
```c
   desc topic
```

* 결과

![image](https://user-images.githubusercontent.com/64197428/127121711-3bd432e7-385b-4703-afb3-c8e88aba62c2.png)

#### 3. 데이터 조회
* 코드
```c
   printf("table name: ");
   scanf("%[^\n]s",&table_name);
   getchar();
   printf("columns name('*' means all data): ");
   scanf("%[^\n]s", &column_name);
   getchar();
   sprintf(query_buffer, "select %s from %s", column_name, table_name);
   query(conn, query_buffer);

```

* 쿼리문
```c
   select * from topic
```

* 결과

![image](https://user-images.githubusercontent.com/64197428/127121787-e7ec2ca9-9280-42c1-a913-f61a3dfb5d3f.png)

#### 4. 데이터 추가
* 코드
```c
   printf("table name: ");
   scanf("%[^\n]s",&table_name);
   getchar();
   printf("columns name: ");
   scanf("%[^\n]s", &column_name);
   getchar();
   printf("data values : ");
   scanf("%[^\n]s", &data);
   getchar();
   sprintf(query_buffer, "insert into %s (%s) values (%s) ", table_name, column_name, data);
   query(conn, query_buffer);

```

* 쿼리문
```c
   insert into topic (id, title, created) values (8, 'DB', NOW())
```


* 결과


![image](https://user-images.githubusercontent.com/64197428/127121930-0b67bcd1-475d-4e33-a22f-671176c65390.png)

#### 5. 데이터 변경
* 코드
```c
  printf("table name: ");
  scanf("%[^\n]s",&table_name);
  getchar();
  printf("Number of columns to update : ");
  scanf("%d", &column_num);
  getchar();
  for(i = 0; i < column_num;i++){
      printf("columns %d : ", i);
      scanf("%[^\n]s", &column_name);
      getchar();
      printf("data %d: ", i);
      scanf("%[^\n]s", &data);
      getchar();
      sprintf(setData,"%s %s = %s",setData, column_name, data);
      if(i != column_num -1)
      sprintf(setData,"%s, ",setData);
  }
  printf("input column name for update : ");
  scanf("%[^\n]s", &column_name);
  getchar();
  printf("input data : ");
  scanf("%[^\n]s", &data);
  getchar();
  sprintf (query_buffer, "update %s set %s where %s=%s", table_name, setData, column_name,data);
  query(conn, query_buffer);
  sprintf(setData, "%s", "");

```
* 쿼리문
```c
   update topic set title='SQL', author_id=3 where id=7   
```

* 결과


![image](https://user-images.githubusercontent.com/64197428/127122147-597a4002-177d-45e6-adab-f99ee31e0f08.png)

#### 6. 데이터 삭제
* 코드
```c
   printf("table name: ");
   scanf("%[^\n]s",&table_name);
   getchar();
   printf("column name : ");
   scanf("%[^\n]s", &column_name);
   getchar();
   printf("data : ");
   scanf("%[^\n]s", &data);
   getchar();
   sprintf(query_buffer, "delete from %s where %s=%s", table_name, column_name, data);
   query(conn, query_buffer );

```
* 쿼리문
```c
   delete from topic where id=8
```

* 결과


![image](https://user-images.githubusercontent.com/64197428/127122257-127482ef-6c73-481b-ab9c-6835d3b69519.png)


## Code

```c
#include <stdio.h>
#include <mysql.h>
#include <errno.h>
#include <stdlib.h>

void query(MYSQL *conn, const char *query_buffer );
void printMenu();
int main (int argc, char **argv){
    MYSQL *conn;
    char query_buffer[2048];
    char column_name[100];
    char data[1000];
    char table_name[100];
    char setData[100];
    int menuNum;
    int column_num;
    int i;
    conn = mysql_init(NULL);

    if(!mysql_real_connect(conn, "127.0.0.1", "사용자", "비밀번호", NULL, 0, NULL, 0)){
        printf("cannot connect");
        exit(1);
    }
    else{
        if(mysql_select_db(conn, "데이터베이스 이름")){
            printf("cannot use databases");
            exit(1);
        }
    }
    while(1){
        printMenu();
        printf("menu : ");
        scanf("%d", &menuNum);
        getchar();
        switch(menuNum){
            case 1:
                sprintf(query_buffer, "%s", "show tables");
                query(conn, query_buffer);
                break;
            case 2:
                printf("table name: ");
                scanf("%[^\n]s",&table_name);
                getchar();
                sprintf(query_buffer, "desc %s",  table_name);
                query(conn, query_buffer);
                break;
            case 3:
                printf("table name: ");
                scanf("%[^\n]s",&table_name);
                getchar();
                printf("columns name('*' means all data): ");
                scanf("%[^\n]s", &column_name);
                getchar();
                sprintf(query_buffer, "select %s from %s", column_name, table_name);
                query(conn, query_buffer);
                break;
            case 4:
                printf("table name: ");
                scanf("%[^\n]s",&table_name);
                getchar();
                printf("columns name: ");
                scanf("%[^\n]s", &column_name);
                getchar();
                printf("data values : ");
                scanf("%[^\n]s", &data);
                getchar();
                sprintf(query_buffer, "insert into %s (%s) values (%s) ", table_name, column_name, data);
                query(conn, query_buffer);
                break;
            case 5:     //update
                printf("table name: ");
                scanf("%[^\n]s",&table_name);
                getchar();
                printf("Number of columns to update : ");
                scanf("%d", &column_num);
                getchar();
                for(i = 0; i < column_num;i++){
                    printf("columns %d : ", i);
                    scanf("%[^\n]s", &column_name);
                    getchar();
                    printf("data %d: ", i);
                    scanf("%[^\n]s", &data);
                    getchar();
                    sprintf(setData,"%s %s = %s",setData, column_name, data);
                    if(i != column_num -1)
                        sprintf(setData,"%s, ",setData);
                }

                printf("input column name for update : ");
                scanf("%[^\n]s", &column_name);
                getchar();
                printf("input data : ");
                scanf("%[^\n]s", &data);
                getchar();
                sprintf (query_buffer, "update %s set %s where %s=%s", table_name, setData, column_name,data);
                query(conn, query_buffer);
                sprintf(setData, "%s", "");
                break;
            case 6:         //delete
                printf("table name: ");
                scanf("%[^\n]s",&table_name);
                getchar();
                printf("column name : ");
                scanf("%[^\n]s", &column_name);
                getchar();
                printf("data : ");
                scanf("%[^\n]s", &data);
                getchar();
                sprintf(query_buffer, "delete from %s where %s=%s", table_name, column_name, data);
                query(conn, query_buffer );

                break;
            case 7:
                exit(1);
                break;
            default:
                printf("다시 입력하세요.\n");

        }
    }
        mysql_close(conn);
}

void query(MYSQL *conn, const char *query_buffer ){
        int i;
        MYSQL_ROW row;
        MYSQL_FIELD * field;
        MYSQL_RES *result;
        if(mysql_query(conn, query_buffer)){
            printf("query failed : %s\n", query_buffer);
            printf("errMsg : %s\n", mysql_error(conn));

        }
        result = mysql_use_result(conn);
        while((row = mysql_fetch_row(result)) != NULL){
            for(i = 0; i < mysql_num_fields(result);i++){
                if(i == 0){
                    while(field = mysql_fetch_field(result))
                        printf("%-25s|", field->name);
                    printf("\n");
                }
                printf("%-25s|", row[i]? row[i] : "NULL");
            }
            printf("\n");
        }

        mysql_free_result(result);
}

void printMenu(){
        printf("---------------------------\n");
        printf("1. 테이블 조회\n");
        printf("2. 테이블 구조 확인\n");
        printf("3. 데이터 조회\n");
        printf("4. 테이터 추가\n");
        printf("5. 데이터 변경\n");
        printf("6. 데이터 삭제\n");
        printf("7. 종료\n");
        printf("---------------------------\n");
}




## 용어

#### pgw(패킷 데이터 네트워크 게이트웨이)
단말에 IP주소를 부여하기 때문에 트래픽은 PGW를 거쳐야 한다.
사용자 트래픽 정보를 이용하여 해당 사용자에게 과금처리르 수행
#### PCRF (Policy and Charging Rules Function)
서비스 및 가입자 프로파일 기반으로 동적으로 Policy 및 과금 정책을 제공하는 시스템
