
# 회귀 분석을 이용한 기대수명 예측

![life_expectancy](https://user-images.githubusercontent.com/78460413/112588440-bfb18500-8e42-11eb-8319-1b456b7592c9.png)

*그림 출처 : BBC News

***

## 1. INTRO

## 1-1. 목적
- WTO가 제공한 국가별 15개년(2000 ~ 2015) 데이터를 활용한 회귀 분석 프로젝트 입니다.
- 본 프로젝트에서는 기대수명과 그 외 타 요소들과의 상관관계를 분석하였습니다.
- 본 프로젝트의 목적은 EDA를 통한 전처리와 스케일링을 통하여 정제된 데이터를 가지고 분석 모델의 성능을 비교하며 최적의 모델을 찾음에 있습니다.

## 1-2. CONCLUSION
- Conclusion
  - Scaler 성능 비교를 통해 스케일링 StandScaler 선정하여 사용하였습니다.
  - RMSE가 가장 작은 최적의 모델로 판단된 RandomForest 선정하여 사용하였습니다
  -  StandScaler와 RandomForest가 가장 최적화된 성능의 모델이었습니다
 
  교육수준, 자원소득구성 중 인적자원 비율, BMI 지수가 높을 수록 기대수명이 늘어난다.
  - 자원소득구성 중 인적자원은 한 나라의 경제발전과 한 기업의 생존과 경쟁력을 결정하는 중요요소이며 높을수록 나라의 경제 발전의 이득이 된다.
    - 선진국일수록 자원소득구성 중 인적자원이 높음 
  - BMI지수가 높은 경우 : 개방도상국에 비해 선진국에서 BMI 지수가 높다 -> 선진국의 기대수명은 높다.
  <br/>


- Limitation & 하고 싶은 것
  - 사용되는 모델에 대한 더 많은 분석과 공부가 필요함을 인지했으며, 추후 파라미터 변경으로 더 다양한 모델을 사용하고 싶습니다.
  - 다중공산성에 대한 심도깊은 연구가 필요함을 인지했습니다.
  
## 1-3. 수집 데이터
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


### 1-4. 팀원 / 역할
- [이지홍]
  - https://github.com/jihong7107
  - raw data 정제와 결측치 처리, 프레젠테이션 자료 작성, 리드미 작성
- [이주영]
  - https://github.com/leekj3133
  -  데이터 전처리, 데이터 시각화, 데이터 스케일링, 모델링, 모델 학습 평가, 모델 성능, K-Fold 모델 검증,  GridSearchCV, READ_ME 작성 

*****

<br/>

## 2. PROCESS

<br/>

<img width="157" alt="스크린샷 2021-06-07 오전 12 37 16" src="https://user-images.githubusercontent.com/75352728/120930518-8477e000-c728-11eb-840a-ce6b4eda0b36.png">
 
<br/>

### 2-1. 데이터 전처리
- GDP per capita 컬럼 4구간으로 나누어 원핫 인코딩
  - low, low_middle, high_middle, high로 구분
  
<img width="450" alt="스크린샷 2021-05-06 오전 1 03 06" src="https://user-images.githubusercontent.com/75352728/117172480-d1edee00-ae06-11eb-8ad1-78d386ed11ef.png">
<img width="450" alt="스크린샷 2021-03-26 오후 2 58 02" src="https://user-images.githubusercontent.com/78460413/112589053-c987b800-8e43-11eb-81da-d91f2a595b6c.png">

<br/>
<br/>

- 결측치 유형에 따른 처리 방법 선택

|결측치 비율|처리방법|
|:---:|:---:|
|10% 미만|제거 또는 치환|
|10% 이상 20% 미만|모델 기반 처리|
|20% 이상|모델 기반 처리|

<br/>

`led.isnull().sum()`

<img width="300" alt="스크린샷 2021-05-12 오후 1 35 07" src="https://user-images.githubusercontent.com/75352728/117918861-df373b00-b326-11eb-998d-052cec4a135f.png">

<br/>

## 간염 B형의 결측값은 왜 많을까? 

<br/>

`led[led['HepatitisB'].isnull()]["Country"].unique()`

<img width="450" alt="스크린샷 2021-05-12 오후 1 38 04" src="https://user-images.githubusercontent.com/75352728/117919045-48b74980-b327-11eb-9ee4-558bf8a06835.png">

<br/>

## 접종률이 낮은 나라 중에 선진국, 개발도상국 다양하다.

<br/><br/>

- 간염 B형의 결측값은 0 또는 중위수로 변환
  - 호주 접종률 94.6% -> 중위수로 결정
- 전체 정부 지출 대비 건강에 관한 정부 지출(%), 교육 정도 평균값으로 결측치 처리
  - 히스토그램 상에서 편측 되지 않게 나타나기 때문에 평균값으로 대치
- 그 외 19개 컬럼 중위값으로 결측치 처리
  - 히스토그램 상에서 편측 되게 나타났기 때문에 중위값으로 대치
  
<br/>

<img width="450" alt="스크린샷 2021-05-12 오후 1 38 04" src="https://user-images.githubusercontent.com/75352728/117919303-b82d3900-b327-11eb-90bc-5e2d3a119569.png">

<br/><br/>

### 2-2. 상관관계 시각화
- 기대 수명과 각 요소간의 상관관계 히트맵 작성

#### 1. 데이터 전처리 전 상관관계
<img width="450" alt="스크린샷 2021-03-26 오후 2 58 02" src="https://user-images.githubusercontent.com/75352728/117157546-a284b480-adf9-11eb-82cc-afcdf01da8c7.png">

- 전체 정부 지출 대비 건강에 관한 정부 지출(%), 교육 정도 => 평균값으로 결측치 처리
- 나머지 => 중위값으로 결측치 처리
  
  <br/>
  
#### 2. 데이터 전처리 후 상관관계
<img width="450" alt="스크린샷 2021-03-26 오후 3 28 06" src="https://user-images.githubusercontent.com/78460413/112591711-1e2d3200-8e48-11eb-8a9e-06e8b20814cf.png">

=> 전처리 전과 전처리 후 상관관계 차이 없음.

<br/>

#### 3. 기대수명과 다른 요소 간의 상관관계

<img width="447" alt="스크린샷 2021-05-05 오후 11 55 37" src="https://user-images.githubusercontent.com/75352728/117162229-8f73e380-adfd-11eb-9d5b-ee033d5332f0.png">

- 교육수준 , 인적자원 비율, BMI 지수 : 양의 상관관계
- HIV/AIDS, 성인남녀사망률 : 음의 상관관계

<br/>

## GDP 구간에 따라 기대수명에 차이가 있는 거 같다! 알아보자!

<br/><br/>

### 2-3. GDP에 따른 시각화

<br/>

#### 2-3.1. 개발도상국과 선진국 기대수명 비교

<img width="450" alt="스크린샷 2021-05-06 오전 1 14 33" src="https://user-images.githubusercontent.com/75352728/117174191-6c026600-ae08-11eb-9dbd-b08b8d0f9be3.png">

- 선진국의 기대수명이 현저히 높음.

<br/>

#### 2-3.2. GDP 구간 별 기대수명과의 관계를 요소마다 시각화하여 확인

 <img width="700" src="https://user-images.githubusercontent.com/75352728/117923047-6340f100-b32e-11eb-8ea5-1813456cec0e.png">

<br/>

<img width="700" src="https://user-images.githubusercontent.com/75352728/117920970-e06a6700-b32a-11eb-832b-beb163c6b8aa.png">

<br/>

#### 2.3.2-1 교육수준 , 인적자원 비율, BMI 지수는 양의 상관관계를 보임
  - 교육수준, 자원소득구성 중 인적자원 비율, BMI 지수가 높을 수록 기대수명이 늘어난다.
  - 자원소득구성 중 인적자원은 한 나라의 경제발전과 한 기업의 생존과 경쟁력을 결정하는 중요요소이며 높을수록 나라의 경제 발전의 이득이 된다.
    - 선진국일수록 자원소득구성 중 인적자원이 높음 
  - BMI지수가 높은 경우 : 개방도상국에 비해 선진국에서 BMI 지수가 높다 -> 선진국의 기대수명은 높다.
  
 <br/>
 
 
#### 2.3.2-2 HIV/AIDS, 성인남녀사망률에서는 음의 상관관계를 보였다.
  - 인간면역결핍바이러스 걸린 사람이 많을 수록 기대수명은 떨어진다. 
    - 치료제가 있더라도 면역관련 질환이고 치명적이기 때문에 GDP 관련 없이 기대수명에 영향을 준다.
  - 성인 남녀 사망률이 늘어나면 기대수명이 떨어진다.
    - 당연히 성인 사망률이 늘어나므로 기대수명이 떨어질 수밖에 없다.    
    
   <br/>
   
### 2-4. 피쳐와 타겟 전처리

<br/>

#### 2-4.1 사용하지 않는 데이터 제거

`led.drop(columns=['Country','Status'], inplace=True)`


`led.drop(columns='GDP_Bins', inplace=True)`

- 원핫인코딩한 GDP 사용 예정
- Country, GDP_BINS, Status 컬럼 제거

<br/>

#### 2-4.2 컬럼 타입 전처리

`led = led.astype('float')`

- 타입을 실수로 통일

<br/>

#### 2-4.3 데이터 니누기

`from sklearn.model_selection import train_test_split`


`X = led.drop('Lifeexpectancy', axis=1)`


`y = led['Lifeexpectancy']`


`X_train, X_test, y_train, y_test = train_test_split(X, y, 
                                                   test_size = 0.3,
                                                   random_state=13)`

- train 70%
- test 30%                                               

<br/>

#### 2-4.4 선형회귀모델 만들기

`import statsmodels.api as sm`


`lm = sm.OLS(y_train, X_train).fit()`


`lm.summary()`


<img width="450" alt="스크린샷 2021-05-12 오후 3 01 06" src="https://user-images.githubusercontent.com/75352728/117925919-e19f9200-b332-11eb-8f96-3fda92fb9e83.png">

- R-squared:0.997 -> 좋은 모델
  - R-squared이 높을 수록 좋은 모델이지만 컬럼이 많을 수록 R-squared가 높아질수밖에 없다고 한다.
-  The condition number is large, 5.38e+09. This might indicate that there are
strong multicollinearity or other numerical problems.
      - 조건수가 너무 큼, 강한 다중공선성이 있을 수 있음. -> 스케일링 필요(더미변수 제외)

<br/>

#### 2-4.4 다중공산성 변수를 찾기 위한 VIF 계산

`from statsmodels.stats.outliers_influence import variance_inflation_factor
sm.OLS(y_train, X_train).exog_names
pd.DataFrame({'컬럼': column, 'VIF': variance_inflation_factor(sm.OLS(y_train, X_train).exog, i)} 
             for i, column in enumerate(sm.OLS(y_train, X_train).exog_names)
             if column != 'Intercept')`
             
             
<img width="350" alt="스크린샷 2021-05-12 오후 3 06 03" src="https://user-images.githubusercontent.com/75352728/117926335-933ec300-b333-11eb-9de3-487a196f26ca.png">

- 높게 나타나면 상관성이 높은것..(10보다 크면 크다고 할 수 있음)
- 계수가 통계적으로 유의미하지 않다면 대처
- 계수가 통계적으로 유의미하다면 VIF 크더라도 괜찮음
- 변수를 더하거나 빼서 새로운 변수 만들기(두 예측변수를 빼거나 더해도 문제 없을 경우)
- 더하거나 빼기 어려운 경우 변수 모형에서 제거

<br/>

## 다중공산성이 변수 간에 영향을 미치지만 변수들의 관계도 의미가 있으므로 제거는 하지않는다!

<br/>

### 2-5. 모델 학습과 예측 평가

<br/>

#### 2-5.1 예측

`predictions = lm.predict(X_test)
predictions, y_test`

<img width="450" src="https://user-images.githubusercontent.com/75352728/117927246-e5ccaf00-b334-11eb-9ece-0e419432cf5d.png">

#### 2-5.2 참값과 예측값의 직관적 비교

`sns.scatterplot(y_test, predictions);
plt.plot([50,90],[50,90], 'r',ls='dashed',lw=3);`

<img width="300" src="https://user-images.githubusercontent.com/75352728/117927306-fd0b9c80-b334-11eb-8e59-ef21cb2bd979.png">

<br/>

#### 2-5.3 모델학습

`from sklearn.linear_model import LinearRegression
reg = LinearRegression()
reg.fit(X_train, y_train)`

<br/>

#### 2-5.4 모델평가

`pred_tr = reg.predict(X_train)
pred_test = reg.predict(X_test)`

<img width="450" alt="스크린샷 2021-05-12 오후 3 18 58" src="https://user-images.githubusercontent.com/75352728/117927594-612e6080-b335-11eb-9114-cd3091c49dc2.png">

<br/>

#### 2-5.5 모델성능

#### 1. Linear Regression & scaling

<img width="550" alt="스크린샷 2021-05-12 오후 3 18 58" src="https://user-images.githubusercontent.com/75352728/117936405-c6874f00-b33f-11eb-948b-656123f75d66.png">


#### 2. Ridge & scaling

<img width="550" alt="스크린샷 2021-05-12 오후 3 18 58" src="https://user-images.githubusercontent.com/75352728/117937299-c89ddd80-b340-11eb-8188-f69f4676b8a8.png">

#### 3. Lasso & scaling

<img width="550" alt="스크린샷 2021-05-12 오후 3 18 58" src="https://user-images.githubusercontent.com/75352728/117937556-1b779500-b341-11eb-9d35-08c5923bee38.png">

#### 4. ElasticNet & scaling

<img width="550" alt="스크린샷 2021-05-12 오후 3 18 58" src="https://user-images.githubusercontent.com/75352728/117937968-80cb8600-b341-11eb-96ec-7902ee02fa09.png">

#### 5. RandomForestRegressor & scaling

<img width="550" alt="스크린샷 2021-05-12 오후 3 18 58" src="https://user-images.githubusercontent.com/75352728/117938212-c12b0400-b341-11eb-8d93-482d3b1cebec.png">

<br/>

### 2-6. 모델 검증

<br/>

## MSE 와 RMSE는 수치가 작을 수록 좋은 성능을 가진 모델로 볼 수 있다.

- 사용한 모델에 대한 K-Fold 수치
<img width="430" alt="스크린샷 2021-03-26 오후 5 26 13" src="https://user-images.githubusercontent.com/78460413/112603568-897f0000-8e58-11eb-9352-426231c3dc30.png">

- 회귀 평가 지표
<img width="450" alt="스크린샷 2021-03-26 오후 5 32 01" src="https://user-images.githubusercontent.com/78460413/112604249-42ddd580-8e59-11eb-9daf-e099496fa7e0.png">

- GridSearch
<img width="450" alt="스크린샷 2021-03-26 오후 5 26 42" src="https://user-images.githubusercontent.com/78460413/112603573-8b48c380-8e58-11eb-846f-cf862380ecf8.png">

## 최적의 모델 & Scaling : RMSE가 제일 적은 Standard Scaler, RandomForest 
