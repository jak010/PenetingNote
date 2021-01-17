# Netcat File Transfer
```
[Server] : 파일 송신
nc IP PORT < send.file

[Client] : 파일 수신 
nc -l -p PORT > recv.file
```

### Case By Case
```
[pop3] on port 110 : nc IP PORT
[samba] on port 445 : enum4linux
```

### John the Ripper
```
ssh    : ssh2john
*.asc  : gpg2john

```


### FTP Check List
- [x] 파일 사이즈가 다른 디렉토리 체크
- [x] 확장자명을 보고 복호화하는데 사용할 수 있는 파일인지 체크
- [x] 디렉토리명을 보고 정보를 얻을 수 있는 지 체크
- [x] 리눅스 파일 트리 구조를 저장한 경우 /home/ 밑에 유저명으로 생성된 디렉토리 체크

### John the Ripper
 - [x] 형식에 맞춰 제대로 크랙했을 경우에도 결과가 없다면 "--show" 옵션을 줘서 결과 체크