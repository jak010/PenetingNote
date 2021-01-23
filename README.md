# Pentesting Check Point

### Web App 테스팅 (Web App Testing)

#### Directory Brute Forcing
> Recon
 - TOOL
   - [Directory Brute Forcing] : gobuster, dirb, ffuf, wfuzz
   - [Custom List Generate TOOL] : cewl
 - 체크 포인트
   - [x] Web 사이트에서 공개된 접근 가능한 경로외에 접근할 수 있는 경로 체크
   - [x] Hidden Directory는 경로 추적을 여러번 해야될 수 있음 (sub-directory 존재)
     - [x] Brute Forcing으로 정보가 추출이 늦을 때 단순히 "1"에서부터 n까지 Guessing  
   - [x] WORD LIST를 하나만 쓰지 말고 여러번 시도해볼 것
   - [x] 파일 확장자로 접근 가능할 수도 있으니 각 툴에 맞게 확장자를 넣어서 시도해볼 것

### WordPress 테스팅 (WordPress)
> Recon
 - TOOL : wpscan
   - Usage
     - Enum
       - wpscan --url http://{TARGET} -w {WORDLIST}
     - Password Brute forcing
       - wpscan --url http://{TARGET} -w {WORDLIST} --usernames a,b,c
       - wpscan --url http://{TARGET} --passwords {WORDLIST_PAT} --usernames A,B,C
> 체크 포인트
 - [x] wpscan을 이용해 나온 결과로 취약한 Plugin을 사용하는지 체크 
 - [x] exploit-db에서 해당 Plugin으로 사용가능한 취약점 체크
 - [x] wp-config.php의 내용을 읽어올 수 있는 체크
 - [x] wp-config.php을 통해 wp-admin에 로그인이 성공했다면 reverse-shell이 가능한 포인트 체크 (Appearance, Theme 같은 것)
 - [x] wordpress안에서 username에 guessing 할 수 있는 정보 체크
> TIP
 - [x] LFI가 가능할 때  php filter를 이용해 wp-config.php 파일을 읽을 수 있는지 시도

### Gaining Access
> Desc
 - 목표 시스템에 대한 Shell을 얻었을 때 체크
> 체크 포인트
 - [x] /home/ 밑의 .ssh에서 ssh 공개키를 얻을 수 있는지 체크(id_rsa)
