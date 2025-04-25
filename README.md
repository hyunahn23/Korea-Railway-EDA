# **국내 철도 운행 현황 분석**

## 1. 프로젝트 개요

이 프로젝트는 2019년부터 2021년까지의 **국내 철도 운행 데이터**를 통합·정제하고, 이를 바탕으로 **기초 분석(EDA), 시각화, 향후 예측 모델링 기반 마련**을 목표로 합니다.

---

## 2. 프로젝트 목표

- 연도별 원시 데이터를 통합한 **신뢰성 있는 분석용 데이터셋 구축**
- 철도 운행량, 시간대, 요일 등 주요 변수 기반 **탐색적 시각화**
- 결측치/이상치 정제 및 **데이터 품질 향상**
- 향후 수요 예측, 지연 패턴 분석 등 **ML 적용 기반 마련**

---

## 3. 데이터 처리 로직

### 데이터 병합
```python
dfs = [pd.read_csv(file) for file in file_paths]
merged_df = pd.concat(dfs, ignore_index=True)
```

### 결측치 및 이상치 처리
```python
# 결측치 확인
merged_df.isnull().sum()

# 예시: 운행시간이 0 이하인 경우 제거
merged_df = merged_df[merged_df['운행시간'] > 0]
```

### 날짜 파싱 및 파생 변수 생성
```python
merged_df['운행일'] = pd.to_datetime(merged_df['운행일'])
merged_df['연도'] = merged_df['운행일'].dt.year
merged_df['월'] = merged_df['운행일'].dt.month
merged_df['요일'] = merged_df['운행일'].dt.day_name()
```

---

## 4. 탐색적 시각화 예시

### 연도별 총 운행 건수
```python
sns.countplot(data=merged_df, x='연도')
plt.title('연도별 운행 건수')
```

### 월별 운행 추이
```python
monthly_counts = merged_df.groupby(['연도', '월']).size().unstack(0)
monthly_counts.plot(figsize=(10, 5), marker='o')
plt.title('월별 운행 추이')
```

### 요일별 운행 패턴
```python
sns.countplot(data=merged_df, x='요일', order=['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday', 'Sunday'])
plt.title('요일별 운행 패턴')
```
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

| ![output_army1](https://github.com/user-attachments/assets/a5627568-ad30-456c-8f1f-994511370d70) | ![output_army2](https://github.com/user-attachments/assets/2c42631a-7e6f-466f-b719-5b3626a1fc84) |
|--------|--------

---

### 관광 및 수학여행 열차의 종착역 분석

![output8](https://github.com/user-attachments/assets/f4adc2b2-c933-4356-943d-5c09abb0de20)

<a href= "https://namu.wiki/w/%EA%B4%80%EA%B4%91%EC%97%B4%EC%B0%A8/%EB%8C%80%ED%95%9C%EB%AF%BC%EA%B5%AD#s-3.1">관광열차종류
- 출발역 / 도착역 기준으로 결과를 산출하다 보니 바다열차, 동해산타열차가 출도착 하는 강릉역이 상위 순위로 출력됨.
  
  | 동해산타열차 노선표 |
  |--------|
  | ![DgiDlfaSOG6g](https://github.com/user-attachments/assets/af9ae053-8d60-454d-8ed3-bd7afdef0495) |

---

## 5. 파일 구조

```
📁 train_data/
 └── data_v2/
     ├── 2019.csv
     ├── 2020.csv
     ├── 2021.csv
     └── 19_21.csv        ← 병합된 최종 데이터셋

📄 train_v2.ipynb         ← 데이터 병합, 전처리 및 시각화 코드 포함 노트북
```

---

## 6. 실행 방법

```bash
git clone https://github.com/yourname/korea-railway-eda.git
cd korea-railway-eda
jupyter notebook train_v2.ipynb
```

※ `train_data/data_v2` 폴더에 연도별 데이터를 미리 준비해야 합니다.

---

## 7. 향후 계획

- 시간대별 철도 수요 분석 (출퇴근 피크 등)
- 지역별 운행 트렌드 시각화
- 운행 지연 원인 분류 및 예측 모델 설계
- Streamlit을 활용한 대시보드 구축

---

## 8. 사용 기술

- Python 3.8+
- pandas / numpy
- matplotlib / seaborn
- Jupyter Notebook

---
