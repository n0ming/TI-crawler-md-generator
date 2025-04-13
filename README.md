# TI-crawler-md-generator
인턴십 자동화 도구 개발

## 자동화 Twitter&ChatGPT v.1
트위터 계정에서 최신 트윗 URL를 획득하고 ChatGPT을 정리하는 버전

### Twitter 접속을 통한 데이터 수집
- Twitter Following URL 접속
- Following 계정들 확인 후 순차적으로 접속
- 접속한 계정에서의 특정 날짜 이후에 게시된 경우 최신 트윗으로 판단하여 해당 트윗 게시글 URL 수집
- 수집된 데이터를 AttackCheck, Profile, URL, Date, Origin_Content, ImageUrl, AttackTweet, AttackUrl순으로 csv 재정렬
  ![image](https://github.com/user-attachments/assets/78ab2bb7-7856-4fd4-828f-275a290923ee)
- 재정렬된 csv 데이터를 마크 다운으로 재구성
  ChatGPT를 통한 Origin_Content의 적절한 제목과 번역된 내용을 획득
  획득한 추가 데이터를 포함하여 정해진 DOCS의 형식으로 재구성
  사이트상으로 내용을 보여주기 위한 작업
- http://127.0.0.1:5000와 같은 로컬 URL을 통해 결과 확인

## 패치 v.2
- 필요한 정보를 가진 게시글을 필터링 하는 1차적인 수작업이 존재하기 때문에 Outlook 메일을 통해 전달되는 단계를 지금 당장 해결하기 어려움
- ChatGPT의 지속적인 자동화 방해 작업 존재
- ChatGPT의 페이지 형식을 지속적으로 변경하기 때문에 유지보수를 하지 않을 경우 셀레니움을 통한 데이터 수집이 어려움

### Outlook으로 획득한 Tweet Url을 통한 데이터 수집
1. Outlook DDW로 전송된 메일들에서 TweetUrl 수집
2. 수집된 TwwetUrls에 접속하여 데이터 수집
3. 수집된 데이터를 AttackCheck, Profile, URL, Date, Origin_Content, ImageUrl, AttackTweet, AttackUrl순으로 csv 재정렬
4. 재정렬된 csv데이터를 마크다운으로 재구성 -> 정해진 DOCS의 형식으로 재구성
   ![image](https://github.com/user-attachments/assets/6b7bf7e2-8496-4554-b112-110884c8b870)
5. http://127.0.0.1:5000와 같은 로컬 URL을 통해 결과 확인 -> 트윗 게시글의 원본 내용 버전의 사이트와 번역된 내용과 DOCS 형식을 갖춘 버전의 사이트 두개가 구동됨
6. 트윗 게시글의 원본 내용 버전의 사이트: http://127.0.0.1:5000/K
7. DOCS형식을 갖춘 버전의 사이트: http://127.0.0.1:5000/E
   ![image](https://github.com/user-attachments/assets/df79532a-b44b-4677-a193-bc493411cfd4)

## 사용 예시
intel_scraper.py 실행 >> ti_report_maker.py 실행 >> 웹사이트 2개 구동 >> DOCS로 옮기는 작업 실행
![image](https://github.com/user-attachments/assets/92958dbe-ab53-4874-8cc3-d518aeba6d8b)

-----

## 사용 기술
### 1. Selenum
데이터 수집의 핵심 도구로 Selenium을 사용함
Selenium으로 동적 트위터 사이트내 게시글에 대한 데이터를 수집함
이때 webdriver를 chrome으로 사용했기 때문에 Chrome 버전과 chromedriver 버전확인 필요함

#### Chrome의 버전 확인하는 법
1. 오른쪽 상단에 있는 3개의 점 모양의 바 클릭
2. 도움말 클릭
3. Chrome 정보 클릭

#### ChromeDriver 다운받기
1. https://googlechromelabs.github.io/chrome-for-testing/ 에서 자신의 버전(ex 116.0.5845.xxx)에 해당하는 드라이버를 설치합니다.
  ![image](https://github.com/user-attachments/assets/b223192d-a8f3-4a6c-8eb0-bef542d2b9f2)
2. zip을 풀은 뒤 드라이버를 원하는 지정 파일에 넣어주고 해당 경로를 복사합니다.
3. 설치한 드라이버의 파일 경로를 executable_path에 넣습니다.
   ![image](https://github.com/user-attachments/assets/ba992f5b-dd4b-4d72-8afb-eacd544b8163)
   ![image](https://github.com/user-attachments/assets/27a56ba0-c569-4a75-b3df-6c20da8be760)

#### 2. Pandas
게시글로부터 수집한 데이터를 csv형태로 저장했고 csv내 필요한 데이터를 가져와 마크다운 형식의 코드로 재구성해야하기 때문에 Pandas를 사용했음

#### 3. Markdown
텍스트 기반의 문서를 구조화하고 서식을 지정하는데 사용되는 텍스트 포캣임
HTML보다 더 간결하고 읽기 쉬운 문법을 가지기 때문에 Markdown을 사용했음

| 년월일 | [tag]제목 | 본문 | 첨부추가트윗 |
|--------|-----------|------|---------------|
| ![image](https://github.com/user-attachments/assets/d60ca371-0f36-4755-a28e-19a8c1c493a3) | ![image](https://github.com/user-attachments/assets/9341b134-55b5-469c-b640-4c8f3c007a01) | ![image](https://github.com/user-attachments/assets/15eb1f6a-8cbb-430e-9e98-8b144da589fd) | ![image](https://github.com/user-attachments/assets/fdef9d5e-4fff-4957-90a3-9e58f8851dbd) |

#### 4. requirements.txt
![image](https://github.com/user-attachments/assets/e4adfda2-bd6e-429a-9dcf-95dd71201a1e)






