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
