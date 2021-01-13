# ffuf 
> ffuf : A faster web fuzze written in Go
> ffuf는 속도가 빠른 웹 퍼징 툴

###  OS
 - Kali linux 20.03

### installation
 - sudo apt-get install ffuf

### Usage
- Basic

```
ffuf -w {WORDLIST_PATH} -u http://{TARGET}/FUZZ

> FUZZ는 디렉터리를 "fuzzing"
``` 

- GET Parameter fuzzing
```
ffuf -w {WORDLIST_PATH} -u https://{TARGET}/script.php?FUZZ=test_value -fs 4242

> This also assumes an response size of 4242 bytes for invalid
```

- POST data fuzzing
```
ffuf -w {WORDLIST_PATH} -X POST -d "username=admin\&password=FUZZ" -u https://target/login.php -fc 401
```

- 그 외 자세한 사항은 https://github.com/ffuf/ffuf 참조
