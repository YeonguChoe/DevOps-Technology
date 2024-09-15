# NGINX
## 명령어

### 심볼릭 링크 만들기
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

### HTTPS 인증을 위한 CSR 얻는 방법
```bash
sudo mkdir -p /etc/nginx/ssl/certs /etc/nginx/ssl/private
sudo openssl req -newkey rsa:2048 -nodes -keyout /etc/nginx/ssl/private/server.key -out /etc/nginx/ssl/certs/server.csr
```

### Key 파일의 암호화를 풀는 방법
```bash

````
