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
        - Country : 국가 193개
        - Year : 연도 2000-2015
        - Status : Developing(83%), Developed(17%)
        - Life expentancy : 기대수명
        - Adult Mortality : 성인남녀사망률(인구 1000명당 15-60세 사망률)
        - Infant deaths : 인구 1000명당 유아사망률
        - Alchol : 1인당 소비(15+)로 기록된 알코올(순수 알코올 리터 단위)
        - Percentage expenditure : 1인당 GDP 대비 건강에 대한 지출(%)
        - Hepatitis B : (1세 아동) 예방 접종 보장(%)
        - Meales : 인구 1000명당 홍역으로 보고된 사례 수
        - BMI 지수
        - Under – five deaths : 1000명당 5세 미만 사망
        - Polio : 1세 아동 소아마비 예방 접종 보장(%)
        - Total expenditure : 총 정부 지원금 지출 대비 건강에 대한 정부 지원금 지출 (%)
        - Diphtheria : 1세 아동 파상풍 톡소이드 및 백일해 예방 접종 보장(%)
        - HIV/AIDS : 1000명당 사망(0-4세)
        - GDP : 1인당 국내 총생산
        - Population : 인구
        - thinness1-19years : 유병률(%)
        - thinness5-9years : 유병률(%)
        - Income composition of resources : 자원소득구성 중 인적자원
        - Schooling : 교육 정도

### 1-3 팀원 / 역할
- [이지홍]
  - https://github.com/jihong7107
  - raw data 정제와 결측치 처리, 프레젠테이션 자료 작성, 리드미 작성
- [이주영]
  - https://github.com/leekj3133
  -  데이터 전처리, 데이터 시각화, 데이터 스케일링, K-Fold 모델 검증, 모델 학습 평가, GridSearchCV, 모델 성능 

*****

## 2. PROCESS

데이터 전처리 -> 상관관계 시각화 -> 피쳐와 타겟 전처리 -> 모델학습과 예측 평가 -> 모델 검증 
 

### 2-1. 데이터 전처리
- GDP per capita 컬럼 4구간으로 나누어 원핫 인코딩
- 전체 정부 지출 대비 건강에 관한 정부 지출(%), 교육 정도 평균값으로 결측치 처리
  - 히스토그램 상에서 편측 되지 않게 나타나기 때문에 평균값으로 대치
- 그 외 19개 컬럼 중위값으로 결측치 처리
  - 히스토그램 상에서 편측 되게 나타났기 때문에 중위값으로 대치 
<img width="403" alt="스크린샷 2021-03-26 오후 2 58 02" src="https://user-images.githubusercontent.com/78460413/112589053-c987b800-8e43-11eb-81da-d91f2a595b6c.png">

### 2-2. 상관관계 시각화
- 기대 수명과 각 요소간의 상관관계 히트맵 작성

#### 1. 데이터 전처리 전 상관관계
<img width="547" alt="스크린샷 2021-03-26 오후 2 58 02" src="https://user-images.githubusercontent.com/75352728/117157546-a284b480-adf9-11eb-82cc-afcdf01da8c7.png">


#### 2. 데이터 전처리 후 상관관계
<img width="547" alt="스크린샷 2021-03-26 오후 3 28 06" src="https://user-images.githubusercontent.com/78460413/112591711-1e2d3200-8e48-11eb-8a9e-06e8b20814cf.png">

- 전처리 전과 전처리 후 상관관계 차이 없음.

#### 3. 기대수명과 다른 요소 간의 상관관계

<img width="447" alt="스크린샷 2021-05-05 오후 11 55 37" src="https://user-images.githubusercontent.com/75352728/117162229-8f73e380-adfd-11eb-9d5b-ee033d5332f0.png">


#### 3.1 교육수준 , 인적자원 비율, BMI 지수는 양의 상관관계를 보임
  - 교육수준, 자원소득구성 중 인적자원 비율, BMI 지수가 높을 수록 기대수명이 늘어난다.
  - 자원소득구성 중 인적자원은 한 나라의 경제발전과 한 기업의 생존과 경쟁력을 결정하는 중요요소이며 높을수록 나라의 경제 발전의 이득이 된다.
    - 선진국일수록 자원소득구성 중 인적자원이 높음 
  - BMI지수가 높은 경우 : 개방도상국에 비해 선진국에서 BMI 지수가 높다 -> 선진국의 기대수명은 높다.
  
  
#### 3.2 HIV/AIDS, 성인남녀사망률에서는 음의 상관관계를 보였다.
  - 인간면역결핍바이러스 걸린 사람이 많을 수록 기대수명은 떨어진다. 
    - 치료제가 있더라도 면역관련 질환이고 치명적이기 때문에 GDP 관련 없이 기대수명에 영향을 준다.
  - 성인 남녀 사망률이 늘어나면 기대수명이 떨어진다.
    - 당연히 성인 사망률이 늘어나므로 기대수명이 떨어질 수밖에 없다.    
 






<br/><br/>
## GDP 구간에 따라 기대수명에 차이가 있는 거 같다! 알아보자!







- GDP 구간 별 기대수명과의 관계를 요소마다 시각화하여 확인
<img width="508" alt="스크린샷 2021-03-26 오후 3 29 34" src="https://user-images.githubusercontent.com/78460413/112591718-208f8c00-8e48-11eb-94cc-789e6c0d5c23.png">


### 2-3. 피쳐와 타겟 전처리

### 2-4. 모델 학습과 예측 평가

### 2-5. 모델 검증
- 사용한 모델에 대한 K-Fold 수치
<img width="890" alt="스크린샷 2021-03-26 오후 5 26 13" src="https://user-images.githubusercontent.com/78460413/112603568-897f0000-8e58-11eb-9352-426231c3dc30.png">

- 회귀 평가 지표
<img width="727" alt="스크린샷 2021-03-26 오후 5 32 01" src="https://user-images.githubusercontent.com/78460413/112604249-42ddd580-8e59-11eb-9daf-e099496fa7e0.png">

- GridSearch
<img width="987" alt="스크린샷 2021-03-26 오후 5 26 42" src="https://user-images.githubusercontent.com/78460413/112603573-8b48c380-8e58-11eb-846f-cf862380ecf8.png">


## 3. CONCLUSION
- 진행 사항
  - Scaler 성능 비교를 통해 스케일링 StandScaler 선정하여 사용하였습니다.
  - RMSE가 가장 작은 최적의 모델로 판단된 RandomForest 선정하여 사용하였습니다
- 한계점
  - 사용되는 모델에 대한 더 많은 분석과 공부가 필요함을 인지했습니다.
  - 다중공산성에 대한 심도깊은 연구가 필요함을 인지했습니다.
