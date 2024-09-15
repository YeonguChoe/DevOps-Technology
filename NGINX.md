# NGINX
## 명령어

### 심볼릭 링크 만들기
- `sites-available`에 만든 NGINX 설정파일을 활성화 한다.

```bash
sudo ln -s /etc/nginx/sites-available/파일이름 /etc/nginx/sites-enabled/
```

### NGINX 설정 파일을 테스트한다
```bash
sudo nginx -t
```
### NGINX 웹서버를 재시작한다
```bash
sudo systemctl restart nginx
```

## NGINX 설정 파일

```conf
server {  # 새로운 서버 블록의 시작
    listen 80;  # HTTP 요청을 포트 80에서 수신
    server_name naver.com;  # 도메인 이름 설정

    location / {  # 루트 경로에 대한 설정
        return 301 https://$host$request_uri;  # HTTP 요청을 HTTPS로 리다이렉트
    }
}

server {  # 또 다른 서버 블록의 시작
    listen 443 ssl;  # HTTPS 요청을 포트 443에서 수신
    server_name naver.com;  # 도메인 이름 설정

    ssl_certificate /etc/nginx/ssl/certs/파일.crt;  # SSL 인증서 파일 경로
    ssl_certificate_key /etc/nginx/ssl/private/server.key;  # SSL 인증서 개인 키 파일 경로

    ssl_protocols TLSv1.2 TLSv1.3;  # 사용할 SSL/TLS 프로토콜 버전
    ssl_ciphers HIGH:!aNULL:!MD5;  # 사용할 암호화 알고리즘
    ssl_prefer_server_ciphers on;  # 서버 쪽 암호화 알고리즘 우선 순위 설정

    location / {  # 루트 경로에 대한 설정
        root /var/www/html;  # 웹 콘텐츠의 루트 디렉터리 설정
        try_files $uri /index.html;  # 요청된 파일이 존재하면 제공, 없으면 index.html 제공
    }

    location /api/ {  # /api/ 경로에 대한 프록시 설정
        proxy_pass http://localhost:8080;  # 내부 서버로 요청을 프록시
        proxy_set_header Host $host;  # 원본 호스트 헤더를 프록시 요청에 포함
        proxy_set_header X-Real-IP $remote_addr;  # 클라이언트의 실제 IP 주소를 프록시 요청에 포함
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;  # 원본 IP 주소를 X-Forwarded-For 헤더에 추가
        proxy_set_header X-Forwarded-Proto $scheme;  # 요청의 프로토콜 (HTTP/HTTPS)을 X-Forwarded-Proto 헤더에 포함
    }

    location /news {  # /news 경로에 대한 프록시 설정
        proxy_pass http://localhost:8080;  # 내부 서버로 요청을 프록시
        proxy_set_header Host $host;  # 원본 호스트 헤더를 프록시 요청에 포함
        proxy_set_header X-Real-IP $remote_addr;  # 클라이언트의 실제 IP 주소를 프록시 요청에 포함
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;  # 원본 IP 주소를 X-Forwarded-For 헤더에 추가
        proxy_set_header X-Forwarded-Proto $scheme;  # 요청의 프로토콜 (HTTP/HTTPS)을 X-Forwarded-Proto 헤더에 포함
        proxy_http_version 1.1;  # HTTP/1.1을 사용하여 프록시 요청 수행
        proxy_set_header Upgrade $http_upgrade;  # WebSocket 업그레이드 요청을 처리하기 위한 헤더 설정
        proxy_set_header Connection 'upgrade';  # WebSocket 업그레이드 요청을 처리하기 위한 헤더 설정
    }
}
```
