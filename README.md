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
  -  Column 구성
        - 1.Country : 국가 193개
        - 2.Year : 연도 2000-2015
        - 3.Status : Developing(83%), Developed(17%)
        - 4.Life expentancy : 기대수명
        - 5.Adult Mortality : 성인남녀사망률(인구 1000명당 15-60세 사망률)
        - 6.Infant deaths : 인구 1000명당 유아사망률
        - 7.Alchol : 1인당 소비(15+)로 기록된 알코올(순수 알코올 리터 단위)
        - 8.Percentage expenditure : 1인당 GDP 대비 건강에 대한 지출(%)
        - 9.Hepatitis B : (1세 아동) 예방 접종 보장(%)
        - 10.Meales : 인구 1000명당 홍역으로 보고된 사례 수
        - 11.BMI 지수
        - 12.Under – five deaths : 1000명당 5세 미만 사망
        - 13.Polio : 1세 아동 소아마비 예방 접종 보장(%)
        - 14.Total expenditure : 총 정부 지원금 지출 대비 건강에 대한 정부 지원금 지출 (%)
        - 15.Diphtheria : 1세 아동 파상풍 톡소이드 및 백일해 예방 접종 보장(%)
        - 16.HIV/AIDS : 1000명당 사망(0-4세)
        - 17.GDP : 1인당 국내 총생산
        - 18.Population : 인구
        - 19.thinness1-19years : 유병률(%)
        - 20.thinness5-9years : 유병률(%)
        - 21.Income composition of resources : 자원소득구성 중 인적자원
        - 22.Schooling : 교육 정도

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
- GDP per capita 컬럼 4구간으로 나누어 원핫 인코딩
- 전체 정부 지출 대비 건강에 관한 정부 지출(%), 교육 정도 평균값으로 결측치 처리
- 그 외 19개 컬럼 중위값으로 결측치 처리
<img width="403" alt="스크린샷 2021-03-26 오후 2 58 02" src="https://user-images.githubusercontent.com/78460413/112589053-c987b800-8e43-11eb-81da-d91f2a595b6c.png">

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
