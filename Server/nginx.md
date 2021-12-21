## **Nginx**
---
러시아 개발자 Igor Sysoev 가 만든 동시접속에 특화된 웹서버 프로그램, 세계적으로 가장많이 사용했던 Apache를 제낄정도로 비등비등하게 사용되고 있음

Apache보다 동작이 단순하고,전달자 역할만 하기 때문에 동시접속에 특화 되어있음

동시접속자가 700명 이상일 경우 서버를 증설하거나 Nginx 환경을 권장 

서버가 기존 하드웨어에서 클라우드로 많이 넘어가고 있는 환경에서 더 빛을 바라보고 있음 

가장 많이 사용하는 aws 에서는 시장 점유율 44%정도 가볍고 성능이 좋기 때문에 많이들 사용하는 사용중

[Nginx 공식문서](https://docs.nginx.com/nginx/admin-guide/web-server/web-server/)

## **Apache와 Nginx 다른점**
---

#### **Apache** : 쓰레드/프로세스키반 구조로 요청 하나당 쓰레드 하나가 처리하는구조
사용자가 많으면 많은 쓰레드 생성,메모리 및 CPU낭비가 심함
하나의 쓰레 - 하나의 클라이언트 구조

#### **Nginx** : 비동기 Event-Driven 기반구조
다수의 연결을 효과적으로 처리가능,대부분의 코어모듈이 Apache보다 적은 리소스를 더 빠르게 동작가능




## **Nginx 다운로드 및 Window 서비스 올리기**
---
Nginx는 공식 사이트를 방문하여 다운로드 할수 있는데 dnflsms Window 버전이 필요하기 떄문에 윈도우 버전을 받아준다.
![Nginx](/image/nginx1.png)

버전을 다운로드 받고 압축을 풀어주면 밑에와 같은 폴더로 구조가 되어있다 . **nginx.exe**로 실행 할수 있다. 
![nginx2](/image/nginx2.png)


## **NSSM**
---
Non-Sucking Service Manager의 약자 Microsoft Window용 서비스 관리 프로그램. 백그라운드 및 그라운드 서비스, 프로세스를 관리하는 무료 유틸
[NSSM](https://nssm.cc/download) 을 다운후 해당위치로 이동

```
C:\nssm-2.24\win64
```
명령어를 통해 서비스 등록을 실행 할수 있음

```
nssm.exe install nginx //등록
nssm.exe edit nginx //수정
nssm.exe remove nginx //삭제
```

등록이 끝난다면

![nginx3](/image/nginx3.png)   
이렇게 서비스에 등록된것을 볼수 있다.

## Nginx conf 설정
---
nginx의 설정은 nginx.conf 파일로 간단하게 설정이 가능하다.
```

#user  nobody;

#엔진엑스의 워커수, 최소4가 좋은 셋팅 기본 1
#Cpu 코어가 여러개 있을때 2~4개의 워커를 찾고 코어당 기본적으로 하나씩 할당됨
worker_processes  1;

#error_log  logs/error.log;
#error_log  logs/error.log  notice;
#error_log  logs/error.log  info;


#엔진엑스 마스터 프로세스 pid
#pid        logs/nginx.pid;

#워커 작업 연결수 8192가 좋은 설정
events {
    worker_connections  1024; 	# 1024 Default
    #use epoll; # 리눅스에서만 사용가능
}


http {
    #mime.types을 이용해 파일 확장명과 목록을 커스텀 할수 있음 mine.type은 같은 폴더에 존재하고 있음 조건을 세부적으로 포함시키면  조금더 깨끗해짐
    include       mime.types;

    # 자주 일어나지 않은 상황에 대한 기본대응을 설정 할수 있음 위에서 지정한 mine.type에 포함되지 않는 설정들을 이야기 할수 있음
    default_type  application/octet-stream;
	
    #로그는 awstats 와 같은 로그 포맷과 호환가능함 표준 아파치 로그구문을 분석 할수 있음
    #log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
    #                  '$status $body_bytes_sent "$http_referer" '
    #                  '"$http_user_agent" "$http_x_forwarded_for"';
	
    
    #access_log  logs/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    #keepalive_timeout  0;
    keepalive_timeout  65;

    #gzip  on;

    server {
        listen       80; //80으로 들어옴
        server_name  localhost;

        #charset koi8-r;

        #access_log  logs/host.access.log  main;

        location / {
            proxy_set_header Host $host; 
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_pass http://127.0.0.1:8080;
        }

        #error_page  404              /404.html;

        # redirect server error pages to the static page /50x.html
        #
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }

        # proxy the PHP scripts to Apache listening on 127.0.0.1:80
        #
        #location ~ \.php$ {
        #    proxy_pass   http://127.0.0.1;
        #}

        # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
        #
        #location ~ \.php$ {
        #    root           html;
        #    fastcgi_pass   127.0.0.1:9000;
        #    fastcgi_index  index.php;
        #    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
        #    include        fastcgi_params;
        #}

        # deny access to .htaccess files, if Apache's document root
        # concurs with nginx's one
        #
        #location ~ /\.ht {
        #    deny  all;
        #}
    }


    # another virtual host using mix of IP-, name-, and port-based configuration
    #
    #server {
    #    listen       8000;
    #    listen       somename:8080;
    #    server_name  somename  alias  another.alias;

    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}


    # HTTPS server
    #
    #server { // Nginx SSL(HTTPS) 보안서버 설정
    #    listen       443 ssl;
    #    server_name  localhost;

    #    ssl_certificate      cert.pem; //SSL 인증서가 있는 파일 경로
    #    ssl_certificate_key  cert.key; //Private Key 파일 경로

    #    ssl_session_cache    shared:SSL:1m;
    #    ssl_session_timeout  5m;

    #    ssl_ciphers  HIGH:!aNULL:!MD5;
    #    ssl_prefer_server_ciphers  on;

        location / { //프록시 설정 하는 부분 
            proxy_redirect off;
        	proxy_pass_header Server;
        	proxy_set_header Host $http_host;
        	proxy_set_header X-Real-IP $remote_addr;
        	proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        	proxy_set_header X-Forwarded-Proto $scheme;
        	proxy_http_version 1.1;
            proxy_pass http://127.0.0.1:8080;
        }
    #}

}

```