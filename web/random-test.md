# B4 - random-test
https://dreamhack.io/wargame/challenges/931


## 문제
<img width="814" height="243" alt="image" src="https://github.com/user-attachments/assets/740aa628-f449-4434-9f51-3d8432b36ac8" />


## 풀이과정
사물함 번호와 비밀번호로 로그인에 성공하려면 조건문은 다음과 같다.
-> if locker_num != "" and rand_str[0:len(locker_num)] == locker_num:
     if locker_num == rand_str and password == str(rand_num):

"rand_str[0:len(locker_num)] == locker_num" 이 조건문에서 내가 작성한 사물함 번호의 길이만큼의 랜덤한 아이디가 생긴다.
그러므로 a ~ z, 0 ~ 9를 넣어보며 사물함 번호의 앞자리 순서대로 찾을 수 있다. 찾는 과정으로는 Burp suite의 Intruder를 사용하였다.

<img width="1710" height="478" alt="스크린샷 2026-10-03 오후 3 56 32" src="https://github.com/user-attachments/assets/850bd516-cbdb-4790-8718-556d4316298c" />
여기서 Start attack하면 다음과 같이 첫번째 자리의 문자를 넣었을 때 Good이 되는것을 알 수 있다.

<img width="1710" height="600" alt="image" src="https://github.com/user-attachments/assets/5307c117-6635-4fc9-9e63-ccc14ec047ef" />

다음과 같은 방법을 반복하여 사물함 번호의 4자리를 찾고 비밀번호도 100 ~ 200의 숫자를 반복하여 Flag를 찾을 수 있다.


## 취약점
1. 접두사 비교기반 논리 취약점
  - 문자열의 완전 일치를 검사하지 않고, 사용자가 입력한 값의 길이 만큼 정답의 앞부분과만 비교하도록 구현된 논리적 결함
  - Brute Force 공격으로 가능한 모든 문자열이나 비밀번호 조합을 하나씩 대입해 가며 올바른 값을 찾아낸다.

## 대응법
1. 전체 문자열이 모두 일치하는지 검사하면 이 취약점에 대응할 수 있다.
