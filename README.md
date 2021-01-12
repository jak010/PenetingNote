# Method Thiking

### 워드프레스(WordPress)
> Enumeration 단계
 - TOOL : wpscan
   - Usage
     - wpscan --url http://{TARGET} -eu
> 정찰 포인트
 - [x] wpscan을 이용해 나온 결과로 취약한 Plugin을 사용하는지 체크 
 - [x] exploit-db에서 해당 Plugin으로 사용가능한 취약점 체크
 - [x] wp-config.php의 내용을 읽어올 수 있는 체크
 - [x] wp-config.php을 통해 wp-admin에 로그인이 성공했다면 reverse-shell이 가능한 포인트 체크 (Appearance, Theme 같은 것)
> TIP
 - [x] php filter를 이용해 bypass 되는지 시도
