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

| 파일 이름 | 위치                    |
| --------- | ----------------------- |
| 개인키    | /etc/nginx/ssl/private/ |
| csr파일   | /etc/nginx/ssl/certs/   |
| crt파일   | /etc/nginx/ssl/certs/   |

## 2단계: CSR(Certificate signing request) 파일 생성하기
### key파일을 이용해서 CSR파일 생성 방법
```bash
openssl req -new -key server.key -out server.csr
```

### pem파일을 이용해서 CSR파일 생성 방법
```bash
openssl req -new -key server.pem -out server.csr
```

## 1-2단계 한번에 하는 방법
```bash
sudo mkdir -p /etc/nginx/ssl/private /etc/nginx/ssl/certs
sudo openssl req -newkey rsa -nodes -keyout /etc/nginx/ssl/private/server.key -out /etc/nginx/ssl/certs/server.csr
```

## 3단계: 인증서(CRT파일) 발급

## 4단계: 웹서버 설정하기

### Key 파일의 암호화를 풀는 방법
- crt파일은 개인키와 같이 사용되어야 한다.
- crt파일과 개인키를 같이 사용하려면, 개인키가 복호화 되어 있어야 한다.
#### 암호화된 key파일 복호화
```bash
openssl rsa -in server.key -out server.key
```

#### 암호화된 pem파일 복호화
```bash
openssl rsa -in server.pem -out server.pem
```

## 도메인 설정 방법

| 종류         | 호스트 | 값           | 하는일                                     |
| ------------ | ------ | ------------ | ------------------------------------------ |
| A record     | @      | 서버 IP 주소 | domain 이름을 서버의 IP 주소에 연결한다.   |
| CNAME record | www    | domain 주소  | domain 주소를 다른 domain 주소로 연결한다. |
