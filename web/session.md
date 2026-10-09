# B4 - session
https://dreamhack.io/wargame/challenges/266

## 문제
<img width="1218" height="221" alt="image" src="https://github.com/user-attachments/assets/87af87a8-47d4-4f27-a5f8-df7134f3b3a1" />

 쿠키로 인증 상태를 관리하는 로그인 서비스에서 admin 계정으로 로그인 성공해야 한다.
 
## 풀이과정
쿠키로 인증 상태를 관리하는 프로그램이고, 문제 파일을 확인해봤을때 각 유저의 세션 id를 쿠키값으로 인증한다는 것을 알 수 있다.

```python
session_id = request.cookies.get('sessionid', None)
    try:
        username = session_storage[session_id]
```

가져온 session_id를 키로 사용하여, 서버의 session_storage 딕셔너리에서 이에 대응하는 값인 사용자 이름을 찾아 username 변수에 할당합니다.

```python
session_storage[os.urandom(1).hex()] = 'admin'
```

그리고 admin의 쿠키값은 1byte의 Hex값으로 생성된다. 따라서 00부터 ff 사이의 값이 admin의 쿠키 값이 될 수 있다.

<img width="502" height="434" alt="image" src="https://github.com/user-attachments/assets/78f0c0cf-300e-49bc-982f-cbaefa815fac" />

Burp suite의 Intruder로 00 ~ ff 까지 값을 "Cookie: sessionid=" 에 대입해서 admin의 쿠키 값을 찾아주면 된다

## 취약점 정리
1. 미흡한 세션 ID 엔트로피 (예측 가능한 세션 ID): 세션 ID 생성 시 복잡도(엔트로피)가 매우 낮아 경우의 수가 256개에 불과하므로, 공격자가 짧은 시간 안에 전수 조사를 통해 세션을 탈취할 수 있다.

## 대응법
1. 안전한 난수 생성기 사용 및 엔트로피 확보
2. 안전한 쿠키 속성 설정 - 쿠키의 Secure와 같은 보안 설정이 필요함
