# HTTPS 인증 받는법

## 1단계: 개인(private)키 만들기

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

# NGINX에서 저장위치

|파일 이름|위치|
|---|---|
|개인키|/etc/nginx/ssl/private/|
|csr파일|/etc/nginx/ssl/certs/|
|crt파일|/etc/nginx/ssl/certs/|


### HTTPS 인증을 위한 CSR 얻는 방법
```bash
sudo mkdir -p /etc/nginx/ssl/certs /etc/nginx/ssl/private
sudo openssl req -newkey rsa -nodes -keyout /etc/nginx/ssl/private/server.key -out /etc/nginx/ssl/certs/server.csr
```

### Key 파일의 암호화를 풀는 방법
#### 암호화된 key파일 복호화
```bash
openssl rsa -in server.key -out server.key
```

#### 암호화된 pem파일 복호화
```bash
openssl rsa -in server.pem -out server.pem
```

## CSR(Certificate signing request) 파일 생성 방법
### key파일을 이용해서 CSR파일 생성 방법
```bash
openssl req -new -key server.key -out server.csr
```

### pem파일을 이용해서 CSR파일 생성 방법
```bash
openssl req -new -key server.pem -out server.csr
```
