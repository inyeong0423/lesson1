# Lesson1_2022.06.06.Mon

## Python 개발환경 Setting 및 기초

### Install Visual Studio Code

- OS : Window 10
- "https://code.visualstudio.com/"
- 저장(ctl+s) 안 한 상태면 해당 탭명 옆에 하얀 동그라미 뜸

### Install Extensions

- Python
  
  - 코딩스타일 pep848 가이드 문서
  
     "https://ultrakain.gitbooks.io/python/content/chapter1/coding-style-pep8.html"

  - Python 확장자명 : ~.ipynb (IPython notebooks의 약자)
  - 마우스 프리 위한 단축키
    - enter/esc 로 code cell in/out
    - a : insert code cell Above (notebook cell>Insert cell>)
    - b : insert code cell Below (notebook cell>Insert cell>)
    - ctl + / : 여러줄주석  
    - shalt위아래화살표:줄복사 alt위아래화살표:줄이동 shctlK:줄삭제
    - ctlD : 같은 단어 찾아줌

- Jupyter
- Markdown All in one
  - Markdown 확장자명 : ~.md
  - Toc : Table of Content
  - 코드의 변경이력관리에 유용하며 상세한 작성이 추후 코드 관리 시 편리함
  - Markdown 작성 시 별도의 문법이 존재함. Editor도 사용가능하지만 problems 탭 읽으며 한줄 한줄 해결해나가기 추천함. 많이 작성해보고 Markdown 문법 자체에 어느 정도 익숙해지면 될 듯
  - Markdown rule 참고

    "https://github.com/DavidAnson/markdownlint/blob/main/doc/Rules.md"

  - 우측 상단 preview to the Side 활용

- Linter
  - 문법 체크해줌

### Connect with Github

- Github signup info
  - account name : inyeong0423
  - account id : clara9262@naver.com
  - "https://github.com/inyeong0423/lesson1"
- 명령어 사용 (Git Commands)
  - VS Code>Terminal>bash 에 입력
  - git status
  - git add README.md
  - git commit
  - git commit -m "~변경내용디테일하게~"
  - git config --global user.email "clara9262@naver.com"
  - git config --global user.name "inyeong0423"
  - git push
  - git pull
  - git commit -m "ex) readme.md file에 idea1_전역조건, 작업1, 작업2 상세내역 추가 " && git push

## idea1.주식

### 전역 조건

- 미국장 기준 (미국 UTC -5)
  - 프리장 시작부터 애프터장 종료 시점까지
  - 04:00 ~ 18:00 (UTC -5)
    - 프리장 : 04:00 ~ 09:30
    - 정규장 : 09:30 ~ 16:00
    - 애프터장 : 16:00 ~ 18:00
  - 써머타임 적용하기
    - 매년 3월 마지막 일요일 ~ 10월 마지막 일요일은 UTC -4 적용
- 주가 변동폭 n%은 현재 주가와 34분 전 주가의 차이를 기준으로 한다.
  - n% = (현재주가-과거주가)/현재주가*100
  - 단, n은 정수 (소수점 첫째자리에서 반올림)
- 당일 적용 환율(매매기준율) r은 전전날 프리장 시가와 전날 애프터장 종가 적용환율의 평균으로 한다.
  - 매수환율은 매매기준율+수수료 , 매도환율은 매매기준율-수수료

- 전체 보유금 중 현금(예수금) 보유 비중은 적어도 10% 이상을 유지해야 함
  - 즉 총매수금액 =< 전체보유금*0.9
- 총 매수액 중 10%를 나스닥 레버리지 etf인 QQQ로 유지한다
  - QQQ ETF 종목 리스트가 있다.
  - QQQ 배당금으로 매년 첫번째 영업일 시작에 인버스 ETF인 PSQ를 구매한다.

### 작업 1 : 매수

- 매수량만큼 주식 구매
- 금액
  - 매수량은 전날 애프터장 종료 시 총 매입금액의 8퍼센트
    - 부족한 금액은 반올림한다.
    - 단, r이 전날 r보다 11원 이상 크다면 8퍼센트가 아닌 5퍼센트 매수로 조정
  - 한 주당 2600달러 미만의 주식만 구매가능
- 구매조건
  - 전역 조건을 포함
  - QQQ ETF 중 하나인 종목이고 n이 -10 이하인 종목을 총 매수량 40%만큼 구매
  - QQQ ETF 중 하나인 종목이고 n이 -20 이하인 종목을 총 매수량 60%만큼 구매

### 작업 2 : 매도

- 매도량만큼 주식 구매
- 금액
  - 매도량은 전날 정규장 종료 시 총 매입금액의 9퍼센트
    - 부족한 금액은 반올림한다.
    - 단, r이 전날 r보다 11원 이상 작다면 8퍼센트가 아닌 5퍼센트 매수로 조정
- 판매 조건
  - 전역 조건을 포함
  - QQQ ETF 중 하나인 종목이고 n이 20 이상인 종목을 총 매도량의 40%만큼 판매
  - QQQ ETF 중 하나인 종목이고 n이 30 이하인 종목을 총 매도량의 60%만큼 판매

### 작업 3 : 예수금

- 당일 순이익 (매도량*r - 매수량*r*1.01 (원)) 은 자동으로 예수금에 더해짐
- 예수금이 10%를 초과하면 초과분만큼 다음 영업일에 Lit(QQQ 미포함) 구매
  