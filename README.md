## **국내 철도 운행 현황 분석**
### 개요: 
- 코레일의 열차 운행 통계 데이터를 활용하여 열차 운행 패턴을 분석 후 시기별, 노선별 운행 현황을 파악하며 운행 트렌드를 한눈에 이해할 수 있도록 돕고, 향후 운영 전략 수립 및 정책 결정에 유용한 인사이트를 제공하는 데 기여하고자 함.

## 목표 : 
- 열차 운행 데이터의 구조를 파악하고, 분석에 적합한 형태로 가공
결측값 처리 및 데이터의 일관성 확보
탐색적 데이터 분석(EDA)

- 연도별·노선별 열차 운행량 및 변화 추이를 분석

 - 지역별·노선별 운행 데이터를 차트, 그래프, 지도 등을 활용해 시각적으로 표현
직관적인 인사이트 도출을 위한 대시보드 구성
데이터 기반 인사이트 도출


 - 분석 결과를 바탕으로 코레일 열차 운행 트렌드에 대한 해석 제공
운영 효율성 개선 및 서비스 향상을 위한 시사점 도출

## 데이터 전처리 과정
### 1. 데이터 병합
![image](https://github.com/user-attachments/assets/b97c94f6-cd1a-47b6-b501-b403d7880102)
- 2019, 2020, 2021년도 철도 운행 데이터를 컬럼명에 맞게 병합하여 산출

### 2. 컬럼명 변경
![image](https://github.com/user-attachments/assets/a652f53c-75bf-4767-9bd4-1c8aa7f562da)
- SQL 물리설계 컬럼명으로 되어있던 컬럼명을 보다 직관적인 문자로 변경하고 저장

### 3. 결측값 확인 및 제거, 필요 데이터로만 분류
![image](https://github.com/user-attachments/assets/2d92c993-9c5e-4013-968b-ad49845d0c77)
![image](https://github.com/user-attachments/assets/4e302ee3-d15a-486a-b982-f2271b2a769f)
- 결측치를 너무 많이 가지고 있어 데이터로서의 의미가 없는 컬럼 삭제 및 필요가 없는 컬럼 삭제

### 4. 코드 정의서를 참고하여 단축어나 기호가 아닌 직관적인 레이블 명으로 변경
![image](https://github.com/user-attachments/assets/0d9e4c51-02c9-4ba2-9fb3-8e81598912da)
- 레이블명을 코드 정의서를 확인하여 직관적으로 바꾸고, 단순 문자열 값으로 되어있던 날짜 데이터를 datetime으로 알맞게 형변환

### 5. 데이터 셋의 최종 결측치 확인과 이상치 확인
![image](https://github.com/user-attachments/assets/4f628fb3-47ca-4f94-badf-b02b27601d34)
- 결측치가 정리 되었는지 최종적으로 확인하고, 레이블명 변경 및 형 변환 후 나타난 이상치 삭제

### 6. 데이터 분석을 위한 컬럼 추가
![image](https://github.com/user-attachments/assets/95270062-4718-4b16-af67-da79d96f7247)
- 원할한 데이터 분석을 위해 운행일자 컬럼 datetime 값을 기반으로 요일을 산출 데이터의 컬럼으로 추가
---
## 데이터 분석
---
### 열차 종류별 운행 횟수 통계 시각화

![output](https://github.com/user-attachments/assets/aeaa986e-3bad-4f9f-8204-c31b85e4c367)

---
### 출발 시간대별 운행 통계
 ![output2](https://github.com/user-attachments/assets/d175af62-84c6-41d6-81eb-0246b1479174)

---

### 시간대별 상행 / 하행 운행 횟수 분석 

 ![output3](https://github.com/user-attachments/assets/0befbaa9-6690-4406-9b0b-1907d28a11ce) 

---

### 요일별 기차 운행 횟수 분석

 ![output4](https://github.com/user-attachments/assets/c1be661c-b1cd-4990-9e03-c2075628eaa9) 

---

### 연도별 / 월별 기차 운행 횟수 분석 

 ![output7](https://github.com/user-attachments/assets/9033971f-2bb2-448e-aefa-c5511f568302)

---

### 무궁화호 감축 뉴스

<a href= "https://www.idomin.com/news/articleView.html?idxno=770462">|뉴스1|

<a href= "https://www.ohmynews.com/NWS_Web/View/at_pg.aspx?CNTN_CD=A0002758695&CMPT_CD=P0010&utm_source=naver&utm_medium=newsearch&utm_campaign=naver_news">|뉴스2|

<a href= "https://imnews.imbc.com/replay/2022/nwdesk/article/6396256_35744.html">|뉴스3|

---

### 기차가 많이 출발하는 역 순위

![output9](https://github.com/user-attachments/assets/31c91d50-d138-4299-b45f-dab5f3ee831c)


---

### 열차가 많이 종착하는 역 순위

![output10](https://github.com/user-attachments/assets/05203c0d-55ec-4508-aa75-5eade7a73b5c)


---

### 가장 많이 운행되는 노선

![output11](https://github.com/user-attachments/assets/0c5dae12-57d6-4234-952f-f73502e107f4)

---

### '공항' 키워드 필터링으로 도출한 운행 분석
| ![output5](https://github.com/user-attachments/assets/d4801ec8-c9fc-4bce-9f77-c802d446ce4b) | ![output6](https://github.com/user-attachments/assets/c2594b5e-7c68-45df-905a-553739a9ac3e) |
|--------|--------|

- 2019년 7월 9일 ~ 7월 29일까지 2019 광주 세계수영선수권대회의 영향으로 KTX 임시 열차를 운행하였으며, 하루 7회(인천공항2터미널 → 광주 1일 4회, 광주 → 인천공항2터미널 1일 3회) 운행하였다.
<a href= "https://www.yna.co.kr/view/AKR20190523102200054?input=1195m">관련기사
---

### 매주 1회 운행하는 장병열차 데이터 도출
![army](https://github.com/user-attachments/assets/520ac3e2-f87d-4c81-a497-1aff7e4079e7)
- '연무'역 키워드를 통한 필터링

| ![output_army1](https://github.com/user-attachments/assets/a5627568-ad30-456c-8f1f-994511370d70) | ![output_army2](https://github.com/user-attachments/assets/2c42631a-7e6f-466f-b719-5b3626a1fc84) |
|--------|--------|

---

### 관광 및 수학여행 열차의 종착역 분석

![output8](https://github.com/user-attachments/assets/f4adc2b2-c933-4356-943d-5c09abb0de20)

<a href= "https://namu.wiki/w/%EA%B4%80%EA%B4%91%EC%97%B4%EC%B0%A8/%EB%8C%80%ED%95%9C%EB%AF%BC%EA%B5%AD#s-3.1">관광열차종류
- 출발역 / 도착역 기준으로 결과를 산출하다 보니 바다열차, 동해산타열차가 출도착 하는 강릉역이 상위 순위로 출력됨.
  
  | 동해산타열차 노선표 |
  |--------|
  | ![DgiDlfaSOG6g](https://github.com/user-attachments/assets/af9ae053-8d60-454d-8ed3-bd7afdef0495) |

---





