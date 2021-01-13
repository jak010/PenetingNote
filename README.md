# Method Thiking

### 워드프레스(WordPress)
> Enumeration 단계
 - TOOL : wpscan
   - Usage
     - Enum
       - wpscan --url http://{TARGET} -w {WORDLIST}
     - Password Brute forcing
       - wpscan --url http://{TARGET} -w {WORDLIST} --usernames a,b,c
> 체크 포인트
 - [x] wpscan을 이용해 나온 결과로 취약한 Plugin을 사용하는지 체크 
 - [x] exploit-db에서 해당 Plugin으로 사용가능한 취약점 체크
 - [x] wp-config.php의 내용을 읽어올 수 있는 체크
 - [x] wp-config.php을 통해 wp-admin에 로그인이 성공했다면 reverse-shell이 가능한 포인트 체크 (Appearance, Theme 같은 것)
 - [x] wordpress안에서 username에 guessing 할 수 있는 정보 체크
> TIP
 - [x] LFI가 가능할 때  php filter를 이용해 wp-config.php 파일을 읽을 수 있는지 시도
