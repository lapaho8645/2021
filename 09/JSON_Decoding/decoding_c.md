## rest_json_parser.c
```c
#include <stdio.h>
#include <sys/types.h>
#include <netdb.h>
#include <stdlib.h>
#include <string.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <unistd.h>


#define MSGLEN 1024
#define READLEN 4072
#define DEFAULT_SIZE 512
#define COMM_MAX     5
#define MAX_CHARS (1024 * 8)

typedef struct Document_t {
    char        id                  [DEFAULT_SIZE]  ;
    char        place_name          [DEFAULT_SIZE]  ;
    char        category_group_code [DEFAULT_SIZE]  ;
    char        category_group_name [DEFAULT_SIZE]  ;
    char        category_name       [DEFAULT_SIZE]  ;
    char        phone               [DEFAULT_SIZE]  ;
    char        address_name        [DEFAULT_SIZE]  ;
    char        road_address_name   [DEFAULT_SIZE]  ;
    char        x                   [DEFAULT_SIZE]  ;
    char        y                   [DEFAULT_SIZE]  ;
    char        place_url           [DEFAULT_SIZE]  ;
    char        distance            [DEFAULT_SIZE]  ;
} Document ;

typedef struct Region_t {
    char        region              [DEFAULT_SIZE]  ;
} Region ;

typedef struct SameName_t {
    Region      regions             [COMM_MAX]      ;
    char        keyword             [DEFAULT_SIZE]  ;
    char        selected_region     [DEFAULT_SIZE]  ;
} SameName ;

typedef struct Meta_t {
    int         total_count                         ;
    int         pageable_count                      ;
    short       is_end                              ;
    SameName    same_name                           ;
} Meta ;

typedef struct DataSet_t {
    Document    documents           [COMM_MAX]      ;
    Meta        meta                                ;
} DataSet ;
/* forward refs */
void print_json(json_t *root);
void print_json_aux(json_t *element, int indent);
void print_json_indent(int indent);
const char *json_plural(size_t count);
void print_json_object(json_t *element, int indent);
void print_json_array(json_t *element, int indent);
void print_json_string(json_t *element, int indent);
void print_json_integer(json_t *element, int indent);
void print_json_real(json_t *element, int indent);
void print_json_true(json_t *element, int indent);
void print_json_false(json_t *element, int indent);
void print_json_null(json_t *element, int indent);

void print_json(json_t *root) { print_json_aux(root, 0); }

void print_json_aux(json_t *element, int indent) {
        switch (json_typeof(element)) {
                case JSON_OBJECT:
                        print_json_object(element, indent);
                        break;
                case JSON_ARRAY:
                        print_json_array(element, indent);
                        break;
                case JSON_STRING:
                        print_json_string(element, indent);
                        break;
                case JSON_INTEGER:
                        print_json_integer(element, indent);
                        break;
                case JSON_REAL:
                        print_json_real(element, indent);
                        break;
                case JSON_TRUE:
                        print_json_true(element, indent);
                        break;
                case JSON_FALSE:
                        print_json_false(element, indent);
                        break;
                case JSON_NULL:
                        print_json_null(element, indent);
                        break;
                default:
                        fprintf(stderr, "unrecognized JSON type %d\n", json_typeof(element));
        }
}

void print_json_indent(int indent) {
        int i;
        for (i = 0; i < indent; i++) {
                putchar(' ');
        }
}

const char *json_plural(size_t count) { return count == 1 ? "" : "s"; }

void print_json_object(json_t *element, int indent) {
        size_t size;
        const char *key;
        json_t *value;

        print_json_indent(indent);
        size = json_object_size(element);

        printf("JSON Object of %lld pair%s:\n", (long long)size, json_plural(size));
        json_object_foreach(element, key, value) {
                print_json_indent(indent + 2);
                printf("JSON Key: \"%s\"\n", key);
                print_json_aux(value, indent + 2);
        }
}

void print_json_array(json_t *element, int indent) {
        size_t i;
        size_t size = json_array_size(element);
        print_json_indent(indent);

        printf("JSON Array of %lld element%s:\n", (long long)size, json_plural(size));
        for (i = 0; i < size; i++) {
                print_json_aux(json_array_get(element, i), indent + 2);
        }
}

void print_json_string(json_t *element, int indent) {
        print_json_indent(indent);
        printf("JSON String: \"%s\"\n", json_string_value(element));
}

void print_json_integer(json_t *element, int indent) {
        print_json_indent(indent);
        printf("JSON Integer: \"%" JSON_INTEGER_FORMAT "\"\n", json_integer_value(element));
}

void print_json_real(json_t *element, int indent) {
        print_json_indent(indent);
        printf("JSON Real: %f\n", json_real_value(element));
}

void print_json_true(json_t *element, int indent) {
        (void)element;
        print_json_indent(indent);
        printf("JSON True\n");
}

void print_json_false(json_t *element, int indent) {
        (void)element;
        print_json_indent(indent);
        printf("JSON False\n");
}

void print_json_null(json_t *element, int indent) {
        (void)element;
        print_json_indent(indent);
        printf("JSON Null\n");
}

/*
 *  * Parse text into a JSON object. If text is valid JSON, returns a
 *   * json_t structure, otherwise prints and error and returns null.
 *    */
json_t *load_json(const char *text) {
        json_t *root;
        json_error_t error;

        root = json_loads(text, 0, &error);

        if (root) {
                return root;
        } else {
                fprintf(stderr, "json error on line %d: %s\n", error.line, error.text);
                return (json_t *)0;
        }
}

/*
 *  * Print a prompt and return (by reference) a null-terminated line of
 *   * text.  Returns NULL on eof or some error.
 *    */
char *read_line(char *line, int max_chars) {
        printf("Type some JSON > ");
        fflush(stdout);
        return fgets(line, max_chars, stdin);
}

int main(int argc, char *argv[])
{
        char *token;
        char message_fmt[] = "GET %s HTTP/1.1\r\nHost: %s\r\nAuthorization: KakaoAK %s\r\n\r\n";
        char buf[READLEN];
        char message[MSGLEN];
        char line[MAX_CHARS];
        int sock,left_len, sent_len;
        struct sockaddr_in server_addr;
        struct hostent *host;
        int bytes;
        if(argc < 4) {
                printf("usage : %s <Host> <Resource> <API_KEYS>\n", argv[0]);
                printf("ex) dapi.kakao.com /v2/local/search/keyword.json?query=<query> <API_KEYS>\n");
                return -1;
        }

        if((host=gethostbyname(argv[1]))== NULL){
                printf("gethostbyname error\n");
                exit(-1);
        }
        if((sock=socket(PF_INET, SOCK_STREAM, 0)) < 0) {
                printf("can not create socket\n");
                return -1;
        }

        sprintf(message, message_fmt,argv[2],argv[1], argv[3]);


        memset(&server_addr, 0, sizeof(server_addr));
        server_addr.sin_family=AF_INET;
        memcpy(&server_addr.sin_addr.s_addr, host->h_addr, host->h_length);
        server_addr.sin_port=htons(80);

        if(connect(sock, (struct sockaddr *) &server_addr, sizeof(server_addr)) < 0) {
                printf("can not connect");
                return -1;
        }
        left_len = strlen(message);
        sent_len = 0;
        do{
                bytes = write(sock, message+sent_len, left_len - sent_len);
                if(bytes < 0)
                        printf("write error\n");
                if(bytes == 0)
                        break;
                sent_len += bytes;
        }while(sent_len < left_len);

        memset(buf, 0, sizeof(buf));
        memset(line, 0, sizeof(line));

        do{
                memset(buf, 0, sizeof(buf));
                bytes = read(sock, buf, READLEN);
                printf("%s ",buf);
                //sprintf(line, "%s%s", line, buf);
                if(bytes  < 0)
                        printf("read error\n");
                if(bytes  == 0)
                        break;
        }while(1);

//      while(bytes = read(sock, buf, READLEN) > 0){
//                      sprintf(line, "%s%s", line, buf);
//                      printf("%d\n\n", bytes);
//                      memset(buf, 0, sizeof(buf));
//      }


// printf("%s ", line);
//json_t *root = load_json(line);
//if(root){
//      print_json(root);
//      json_decref(root);
//}
printf("\n");

close(sock);
}
```
