# HTTPS 인증 받는법

## 개인키 만들기

### key 파일로 만들기
#### 키를 생성하면서 AES로 암호화
```bash
openssl genpkey -algorithm RSA -out server.key -aes256
```

#### 암호화 없이 키 생성
```bash
openssl genpkey -algorithm RSA -out server.key -nodes
```

### pem 파일로 만들기
#### 키를 생성하면서 AES로 암호화
```bash
openssl genpkey -algorithm RSA -out server.pem -aes256
```

#### 암호화 없이 키 생성
```bash
openssl genpkey -algorithm RSA -out server.pem -nodes

```

### HTTPS 인증을 위한 CSR 얻는 방법
```bash
sudo mkdir -p /etc/nginx/ssl/certs /etc/nginx/ssl/private
sudo openssl req -newkey rsa -nodes -keyout /etc/nginx/ssl/private/server.key -out /etc/nginx/ssl/certs/server.csr
```

### Key 파일의 암호화를 풀는 방법
```bash

````
