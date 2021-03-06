# Weak File Permission

## File Permission
```
Linux를 공부하다 보면 파일의 권한에 대해 알게된다. 단순히 a,g,o의 개념으로 
누가 읽을 수 있고 누가 편집할 수 있구나 정도로만 이해했던 기억이 있다.
권한상승 파트를 보면서 File Permission이 어떻게 이용될 수 있는지 생각해보자
```

### 1.Readable /etc/shadow 
```
/etc/shadow 파일은 /etc/passwd의 패스워드를 암호화해 저장 시키는 파일이다.
```
#### Think
 - 그렇다면 shadow 파일의 권한 설정이 Other 그룹이 읽을 수 있게 될 때 어떤 일이 일어날까?

#### Method 
 - /etc/shadow
 > -rw-r--r-- 1 root shadow 837 Jan 15 12:21 /etc/shadow
 ```
 위의 권한을 통해 /etc/shadow 파일이 Other 그룹이 읽을 수 있다는 것을 알 수 있다. 파일의 내용을
 읽었을 떄 다음과 같은 내용이 기재되있다고 가정해보자
 ```
 ```
 root:$6$Tb/euwmK$OXA.dwMeOAcopwBl68boTG5zi65wIHsc84OWAIye5VITLLtVlaXvRDJXET..it8r.jbrlpfZeMdwD3B0fGxJI0:17298:0:99999:7:::
 ```
 ```
 두 번째 필드에 패스워드가 암호화되어 저장되있는데 복호화를 어떻게 시킬 수 있을까? 현실 세계
 에서의 패스워드는 더 복잡한 설정으로 되어있겠지만 공격자는 패스워드 사전을 입수해 그 해쉬값
 을 대조해봄으로써 패스워드를 알아낼 수 있다. 보다 복잡한 이론과 배경지식을 습득하면 좋겠지만 
 이 과정을 단순히 해보자 어짜피 이 과정의 목적은 원래 패스워드가 무엇이었는지 알아내는 것일 뿐이다.
 즉, 필요한 건 다음 두 가지 뿐이다.
 ```
 - [x] 패스워드 사전 파일 (구글링을 통해서 많이 얻을 수 있음) 
 - [x] John the ripper (Kali linux)
 ```
 즉 패스워드 크랙 툴을 이용하여 미리 모아놓은 패스워드 사전에서 일치하는 값이 있나 대조해보는 것이다.
 ```
 ```
 # John the ripper 사용법 (단순예시)
 john --wordlist=rockyou.txt shadow
 ```

#### Result
```
지금까지 했던 작업 목록을 요약해 to do를 생각해보자
```
 - [x] /etc/shadow File Permissong의 other의 권한에 r이 포함 되어있는지 체크
 - [x] 공격에 사용될 패스워드 사전 파일 입수 (구글링)
 - [x] 패스워드 크랙 도구를 이용한 패스워드 크랙

### 2.Writeable /etc/shadow
```
위의 예제에서는 단순히 /etc/shadow 파일을 "읽을 수" 있을 떄 이다. 그렇다면 "쓸 수" 있을 떄
즉, "편집"할 수 있을 때는 무슨 액션을 취할 수 있을까?
```

#### Think
```
Readable일 떄는 그 내용을 읽어 패스워드를 크랙해보는 것이 목표였다. 그렇다면 편집할 때는 이 파일에
적어진 패스워드 부분을 덮어 씀으로 패스워드를 변경할 수 있지 않을까? 만약 그렇다면 어떻게?
```

#### Method 
 - /etc/shadow
 > -rw-r--rw- 1 root shadow 837 Jan 15 12:21 /etc/shadow
 ```
 파일의 권한이 변경됬다. `Think`에서 언급했듯 파일을 덮어쓰려면 무엇이 필요할까? 
 ```
 ```
 가설을 세워보자면 /etc/shadow의 패스워드 필드에 맞는 형식으로 변경한 다음에 덮어 씌우면 
 될 것이다. 그러기 위해선 무엇이 필요할까?
 ```
 ```
 whois 패키지에서 제공하는 mkpasswd를 이용하여 내가 원하는 문자열을 /etc/shadow의 패스워드 필드에
 맞는 형식으로 바꿔보자
 ```
 ```
 mkpasswd -m sha-512 INPUT_PASSSWORD_HERE
 ```
 ```
 위의 결과로 나온 문자열을 /etc/shadow의 패스워드 필드에 덮어 씌움으로써 기존 패스워드 설정을 덮어버리자.
 ```
#### Result
```
하지만 결과적으로 빠진 것이 있다. 여기서 나는 "패스워드 필드에 맞는 형식"이라고 언급했다. 
이 부분은 시스템별로 패스워드 해쉬 알고리즘이 다를 수 있다. 이 부분은 주의하고 
만약 /etc/shadow 파일에 Writeable한 설정이 적용되어있을 때 다음과 같은 부분을 생각
```
 - [x] /etc/shadow 파일의 패스워드 필드가 어떤 암호화 알고리즘으로 형식 체크
 - [x] mkpasswd를 이용해서 패스워드를 생성한 뒤 내용을 덮어씌움으로서 내가 지정한 패스워드로 로그인이 가능한지 시도