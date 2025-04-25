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
