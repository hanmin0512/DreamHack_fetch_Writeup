# DreamHack patch Writeup
워게임 주소: https://dreamhack.io/wargame/challenges/49/

## 동적 분석

윈도우를 하나 띄우고 안에 flag를 그리고 보이지 않게 직선으로 그은 그림인 것 같다.

<img width="607" alt="스크린샷 2024-08-27 오후 10 41 00" src="https://github.com/user-attachments/assets/9eeb6374-9e55-4593-9cf0-a36f01b4940d">

## 정적 분석

### main 함수 분석

sub_1400032F0함수는 콜백 함수인 것을 볼 수 있다.

<img width="653" alt="스크린샷 2024-08-27 오후 10 54 10" src="https://github.com/user-attachments/assets/b2600647-ad6a-49d0-9481-bb0325a19e11">

### sub_1400032F0 함수 분석

아래 그림과 같이 switch-case문을 보면 0xf 값일 때 특정 그림을 그리는 것을 볼 수 있다. 또한 sub_140002C40

<img width="650" alt="스크린샷 2024-08-27 오후 10 55 57" src="https://github.com/user-attachments/assets/9cc92d75-092f-4e1f-ad85-952b1c8ec5b9">

### sub_140002C40 함수 분석

sub_14000EB80 함수가 특정 축을 기준으로 반복 호출 되는 것으로 보아 flag를 가리는 직선임을 유추 할 수 있다.

<img width="441" alt="스크린샷 2024-08-27 오후 10 57 10" src="https://github.com/user-attachments/assets/df88c212-4726-4200-a1be-30ed186a922b">

### sub_140002B80 함수 분석

그림을 그릴 팬을 준비하고 간단하게 그림을 그리는 것으로 보아 flag를 가리는 직선임을 더욱더 확신을 가질 수 있다.

<img width="804" alt="스크린샷 2024-08-27 오후 10 58 04" src="https://github.com/user-attachments/assets/78f674b6-2500-4b4d-ae7f-5cf06793b730">

그림을 그리는 곳에 f2를 눌러 break point를 설정 하고 f9를 눌러 디버깅을 시작한다.

<img width="543" alt="스크린샷 2024-08-27 오후 10 59 42" src="https://github.com/user-attachments/assets/c9505508-74e2-4578-8b6d-db15796c2432">

### debugging

f8을 눌러 breakpoint에 걸릴 때 까지 한 단계 한단 계 진행한다. 예상에 맞게 직선을 긋는 함수였다.

<img width="849" alt="스크린샷 2024-08-28 오전 12 06 19" src="https://github.com/user-attachments/assets/436ad42e-912a-4442-8e6f-24596d8be446">

이제 이 함수가 실행되면 바로 ret을 호출하여 그림을 그리지 못하도록 해준다.

디버깅을 멈추고 다시 f9를 누른다.
이유는 모르겠지만 멈추고 한번더 디버깅을 실행해야 아래와 같이 어셈블리 코드로 나온다.

<img width="609" alt="스크린샷 2024-08-28 오전 12 10 52" src="https://github.com/user-attachments/assets/3725225e-59e9-4826-9b09-379da6f86e58">

sub_7FF6EDC72B80 함수를 더블 클릭 한다. 
이후 edit -> Patch Program -> assemble를 이용해 mov ~~ 명령어를 ret으로 변경한다.
그렇게 되면 그림을 그리는 로직이 실행 되기 전에 ret이 실행되어 그림을 그리지 않게 된다.

<img width="835" alt="스크린샷 2024-08-28 오전 12 11 11" src="https://github.com/user-attachments/assets/085f6118-35f7-4f5e-8ea4-d5b7d7fdfca4">

변경 이후 f9를 눌러 쭉 실행 하면 아래와 같이 flag를 얻을 수 있다.

<img width="614" alt="스크린샷 2024-08-28 오전 12 11 31" src="https://github.com/user-attachments/assets/f1556642-7aee-4b10-af0c-df8a884fc64f">

## 결론

<img width="808" alt="스크린샷 2024-08-28 오전 12 16 30" src="https://github.com/user-attachments/assets/f901579d-c902-4355-a053-170893cecf16">

<img width="817" alt="스크린샷 2024-08-28 오전 12 16 44" src="https://github.com/user-attachments/assets/d7edc681-348c-4be3-8460-0e8a8db1bf5c">







