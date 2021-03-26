# 회귀 분석을 이용한 기대수명 예측

![life_expectancy](https://user-images.githubusercontent.com/78460413/112588440-bfb18500-8e42-11eb-8319-1b456b7592c9.png)
*그림 출처 : BBC News

***
## 1. INTRO
### 1-1 개요
- WTO가 제공한 국가별 15개년(2000 ~ 2015) 데이터를 활용한 회귀 분석 프로젝트 입니다.
- 본 프로젝트에서는 기대수명과 그 외 타 요소들과의 상관관계를 분석하였습니다.
- 본 프로젝트의 목적은 EDA를 통한 전처리와 스케일링을 통하여 정제된 데이터를 가지고 분석 모델의 성능을 비교하며 최적의 모델을 찾음에 있습니다.


### 1-2 수집 데이터
- 출처 
  -  Kaggle : Statistical Analysis on factors influencing Life Expectancy(WTO)
  -  링크 : https://www.kaggle.com/augustus0498/life-expectancy-who 

### 1-3 팀원 / 역할
- [이지홍]
  - https://github.com/jihong7107
  - raw data 정제와 결측치 처리, 프레젠테이션 자료 작성, 리드미 작성
- [이주영]
  - https://github.com/***
  -  데이터 스케일링, K-Fold 모델 검증, 모델 학습 평가, GridSearch 

## 2. PROCESS

데이터 전처리 -> 상관관계 시각화 -> 피쳐와 타겟 전처리 -> 모델학습과 예측 평가 -> 모델 검증 
 

### 2-1. 데이터 전처리

### 2-2. 상관관계 시각화

### 2-3. 피쳐와 타겟 전처리

### 2-4. 모델 학습과 예측 평가

### 2-5. 모델 검증


## 3. CONCLUSION
- 진행 사항
  - Scaler 성능 비교를 통해 스케일링 StandScaler 선정하여 사용하였습니다.
  - RMSE가 가장 작은 최적의 모델로 판단된 RandomForest 선정하여 사용하였습니다
- 한계점
  - 사용되는 모델에 대한 더 많은 분석과 공부가 필요함을 인지했습니다.
  - 다중공산성에 대한 심도깊은 연구가 필요함을 인지했습니다.
