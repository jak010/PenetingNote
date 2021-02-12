#### Pentesting Methodology : Web

#### Local File Inclusion
> 공격 파일이 공격 대상 서버에 있을 때 읽어올 수 있는 취약점
  - Point
    - Reconissance 단계에서 얻은 엔드 포인트가 다음과 같을 때
      ```
      http://{URL}/config.php
      ```
    - 웹에 표출되지 않는 주석 또는 Request&Response로만 얻을 수 없는 내용을 읽어오는 것에도 이용할 수 있음
- Tech
  > LFI 는 기본적으로 "../../../etc/passwd"를 통해 파일을 읽어 올 수 있지만 상황에 따라 다음과 같은 테크닉이 필요할 수 있음
  - php filter
    - Resource
      - https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/File%20Inclusion
  - User Agent Injection
    - Resource
      - https://www.hackingarticles.in/apache-log-poisoning-through-lfi/
