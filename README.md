# Lesson1_2022.06.06.Mon

## Python 개발환경 Setting

### Install Visual Studio Code

- OS : Window 10
- "https://code.visualstudio.com/"

### Install Extensions

- Python
  
  - 코딩스타일 pep848 가이드 문서
  
     "https://ultrakain.gitbooks.io/python/content/chapter1/coding-style-pep8.html"

  - Python 확장자명 : ~.ipynb (IPython notebooks의 약자)

- Jupyter
- Markdown All in one
  - Markdown 확장자명 : ~.md
  - 코드의 변경이력관리에 유용하며 상세한 작성이 추후 코드 관리 시 편리함
  - Markdown 작성 시 별도의 문법이 존재함. Editor도 사용가능하지만 problems 탭 읽으며 한줄 한줄 해결해나가기 추천함. 많이 작성해보고 Markdown 문법 자체에 어느 정도 익숙해지면 될 듯
  - Markdown rule 참고

    "https://github.com/DavidAnson/markdownlint/blob/main/doc/Rules.md"

  - 우측 상단 preview to the Side 활용

- Linter

### Connect with Github

- Github signup info
  - account name : inyeong0423
  - account id : clara9262@naver.com
  - account pw : love2022!!
  - "https://github.com/inyeong0423/lesson1"
- 명령어 사용 (Git Commands)
  - VS Code>Terminal>bash 에 입력
  - 

## idea1.주식

### 전역 조건

- 미국장 기준  
- 장 시작 1시간 이후와 장 종료 전 1시간을 제외한다
- 가격 확인은 1시간 전 가격을 기준으로 한다.
- 변동폭이 n% 이하로 급락하고 (n: 정수. 반올림. 지정 하락 변동폭)
- 환율이 작일 대비

### 작업 1 : 구매

- 매수 금액만큼 주식 구매
- 금액
  - 매수 금액은 현재 유동 자산의 5퍼센트
    - 부족한 금액은 반올림한다.
  - 한 주당 20,000원 미만의 주식만 구매가능
- 구매조건
  - 전역 조건을 포함
  - 한 시간 전 매수가보다 30퍼센트 큰 경우.

### 작업 2 : 판매

- 판매 금액만큼 주식 구매
- 금액
  - 매도 금액은 현재 보유량의 10퍼센트
    - 부족한 금액은 반올림한다.
- 판매 조건
  - 전역 조건을 포함
  - 한 시간 전 매도가보다 30퍼센트 큰 경우.
