# B4 - cookie
https://dreamhack.io/wargame/challenges/6


## 문제
<img width="1233" height="621" alt="스크린샷 2026-10-01 오후 2 46 56" src="https://github.com/user-attachments/assets/9bf4bf77-1f3f-4990-8ee0-f4266e81115f" />
 
 쿠키로 인증 상태를 관리하는 로그인 서비스에서 admin 계정으로 로그인 성공해야한다.

 
## 풀이과정
1. 풀이 방향성
 
 쿠키로 인증 상태를 관리하기때문에 패킷을 분석한 후 쿠키를 확인해봐야겠다고 생각했다.


<img width="985" height="529" alt="스크린샷 2026-10-01 오후 3 26 16" src="https://github.com/user-attachments/assets/066d0513-68b0-44df-b543-9edec88d0f25" />
 
 문제 파일을 봤을 때 다음과 같았는데 users에 guest의 아이디, 비밀번호와 admin 아이디와 FLAG인 비밀번호가 있음을 확인할 수 있다. 따라서 문제의 VM에 접속하여 guest로 로그인 후 쿠키를 확인하면된다.


<img width="1328" height="618" alt="image" src="https://github.com/user-attachments/assets/830c3d5a-0288-49fa-975c-2d03155055bf" />
 
 guest로 로그인한 패킷을 확인해봤을때 cookie가 단순히 guest로만 되어있는것을 확인할 수 있다.


<img width="599" height="528" alt="image" src="https://github.com/user-attachments/assets/fb1cd08b-f1c4-44ea-8716-b5b4829727bf" />
 
 따라서 Repeater를 통해 cookie값을 admin으로 바꿔주면 FLAG를 알 수 있다. 


## 취약점 정리
 *
