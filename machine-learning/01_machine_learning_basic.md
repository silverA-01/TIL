# 머신러닝의 개념

## 머신러닝이란?
- 데이터로 기계 학습
- **데이터로부터 학습**하도록 컴퓨터를 프로그래밍하는 과학
- **명시적인 프로그래밍 없이** 컴퓨터가 학습하는 능력을 갖추게 하는 연구 분야
- 애플리케이션을 수정하지 않고도 데이터를 기반으로 **패턴을 학습**하는 알고리즘

## 머신러닝의 필요성
- **현실 세계의 매우 복잡한 조건들**로 인해 기존의 소프트웨어 코드만으로 해결하기 어려웠던 문제점들을 머신러닝을 이용해 해결
- 데이터 마이닝, 영상인식, 음성인식, 자연어 처리 등 여러 분야에서 사용

## 기존 컴퓨터사이언스와 머신러닝의 차이점
1. **기존 컴퓨터 사이언스**
    - 기존 개발자들이 알고리즘을 풀기 위해 함수 등을 정의하고 매개변수(parameter)를 받아 결과값(return value)를 확인할 수 있는 코딩(coding)을 의미
    - 즉, 로직을 미리 만들어서 데이터를 받아 결과를 확인하는 방식
2. **머신러닝**
   - **특성 데이터와 결과를 넣어 로직을 머신이 학습하는 방식**
   - 문제와 답에 대한 로직을 모르지만 문제 데이터와 정답 데이터를 반복적으로 넣어주면 알고리즘에 의해 입력된 데이터의 패턴을 파악하여 어떤 로직(연산)이 이루어 질지를 학습하게 된다.

## 머신러닝의 유형
### 1. 지도학습(Supervised Learning)
- 머신러닝 모델에게 문제(Feature)와 답(Lable)을 모두 제공
  - Feature : 타겟(Target)의 특징적인 데이터
- 모델에 대해 정량적인 수치로 평가할 수 있다.
- 분류, 회귀, 추천 시스템, 시각 및 음성 감지 인지 등

### 2. 비지도학습(Un-Supervised Learning)
- 머신러닝 모델에게 문제(Feature)만 제공
- 머신러닝 모델에 대한 최종적인 평가는 사람이 해야 한다.
  - 머신러닝 모델 자체의 성능을 평가하는 방법이 따로 있기는 하지만, 기본적으로 사람이 머신러닝 모델의 성능을 파악해야 한다.
- 군집화(클러스터링), 차원 축소, 토픽 모델링, 문서 군집 등

## 지도학습의 대표적인 알고리즘
- 데이터의 종류에 따라 분류와 회귀로 나눌 수 있다.

### 1. 분류(Classfication)
Discreate(Categorical) Valued Output을 예측하는 문제
- 예측해야할 데이터가 범주형 변수일 때 분류라고 함
- Discreate : 이산
- Caregorical : 범주형
- 데이터의 종류(범주)가 정해져있어 데이터의 개수를 셀 수 있는(count) 문제
- ex. 스펨 메일 판단하기, 코로나 검사, 신용카드 부정사례 검출하기

1. 이진 분류 (Binary Classfication)
   - Yes/No로 대답할 수 있는 문제
   - 음성(Negative), 양성(Positive)를 예측한다.
     - 음성은 `0`, 양성은 `1`로 return value를 갖는다.
     - 음성은 부정적인 의미가 아니라 문제에 대한 답이 No라는 의미이다.
   - ex. 당신은 비만인가요? 이 사진은 고양이인가요? 
  
2. Multi-Class Classfication
   - 다지선다형 문제
   - 여러 카테고리 중 하나를 예측한다. 
   - ex. 이 사진은 고양이, 강아지, 말 중 어떤 동물의 사진인가요?
   - 여러 번의 이진 분류를 통해 다중 분류를 구분하게 된다.
   - 다중 분류에 대한 해석은 확률로 분석한다.
   - 확률이 높은 카테고리를 return value로 선택한다.
   - ex. 이 사진은 고양이, 강아지, 말 중 어떤 동물의 사진인가요?
       - 이 사진은 고양이일 확률이 80%, 강아지일 확률 20% 이기 때문에 이 사진은 고양이이다.
   - ex. 10시간 동안 공부를 했을 때 시험점수의 등급이 무엇인가?
     - 정답 데이터를 A부터 F 등급으로 카테고리를 나눌 수 있다.


### 2. 회귀(Regression)
Countinous Valued Output 예측하기
- 예측해야할 데이터가 연속적인 값일 때 회귀라고 함
- 데이터의 개수를 셀 수 없다.
- ex. 공부시간으로 시험점수 예측하기, 집값 예측하기
- ex. 10시간 동안 공부를 했을 때 시험 점수가 몇 점인가?
  - 정답 데이터가 시험 점수라는 수치로 나온다. 
  
## 머신러닝을 사용할 때 주의사항
- 머신러닝은 **데이터에 너무 의존적**이다.
  - Garbage In, Garbage Out : 쓰레기를 넣으면 쓰레기가 나온다.
  - 즉 문제로 주는 입력 데이터가 매우 중요하고, 좋은 머신러닝 모델을 만들기 위해 입력 데이터를 EDA 해야한다.
    - EDA : 분석 및 시각화 작업
    - 즉, 가지고 있는 입력 데이터를 파악하는 과정이 필요
    - ex. 선형독립인 입력 데이터를 사용할 수 있게 데이터를 필터링
    - 딥러닝에서는 데이터에 대한 EDA의 중요성이 낮아진 편
- 학습시에 최적의 결과를 도출하기 위해 수립된 머신러닝 모델은 **실제 환경 데이터에 적용시 과적합되기 쉽다.**
  - 데이터의 양이 부족하면 실제 환경(필드)에서는 데이터의 예측 성능이 떨어지게 된다.
  - ex. 교과서에 나온 문제만 완벽하게 풀이(학습)하여 수능(실제 환경)을 잘 볼 수 있을까?
    - 실제 환경에 맞춰 학습할 데이터를 교과서 외에 다른 응용 문제도 완벽하게 풀이할 수 있도록 해야 한다.
  - 즉, 데이터는 많으면 많을 수록 좋다.
- 한 번 머신러닝 모델을 만드는 것에 그치지 않고 지속적인 관리가 필요하다.
  - 끊임없이 모델을 개선하기 위한 노력이 필요하다.
  - 데이터의 특성을 파악하고, 최적의 알고리즘과 파라미터를 구성할 수 있는 고급 능력이 필요하다.
  - 서비스가 운용되면 데이터는 계속해서 생성되기 때문에, 모델에 새로운 데이터를 업데이트 하여, 새로운 데이터의 패턴을 파악하도록 훈련시켜줘야 한다.

## 머신러닝 용어 정리
### 1. Feature ($X$)
- 머신러닝 알고리즘이 학습해야 할 데이터
- 데이터 세트의 일반 속성
- 머신러닝은 2차원 이상의 다차원 데이터에서도 많이 사용되므로, 타겟값을 제외한 나머지 속성을 모두 Feature로 지칭한다.
- 사이킷런에서는 무조건 Feature를 2차원 데이터로 사용한다.($X \in \mathbf{R}^{N \times M}$
)
- 딥러닝 프레임워크에서는 다차원 데이터 사용 가능하다.

## 2. Target / Lable ($y$)
- 타겟 혹은 레이블은 **지도 학습 시 데이터의 학습을 위해 주어지는 정답 데이터**
- 보통 지도 학습 중 **회귀 문제의 경우 타겟이라고 지칭**하고,  **분류 문제의 경우 이러한 정답 데이터를 레이블(Lable)로 지칭**한다.
- 반드시 벡터의 형태 혹은 1열의 행렬로 이루어진다.($y \in \mathbf{R}^{N \times 1}$)

## 3. Class
- 분류 문제에서 레이블의 종류를 의미하고 집합(Set)으로 표현된다.

## 사이킷런(Scikit-Learn)
파이썬의 대표적인 머신러닝 라이브러리/패키지
- 가장 쉽고 파이썬다운 API 제공
- 머신러닝을 위한 매우 다양한 알고리즘, 개발을 위한 편리한 프레임워크, API를 제공
- 오랜 기간 실전 환경에서 검증돼었으며, 매우 많은 환경에서 사용되는 성숙한 라이브러리
  - 머신러닝 시장에서 90%는 사이킷런을 사용
- 주로 Numpy와 Scipy 기반 위에서 구축된 라이브러리

## 사이킷런의 클래스 구조도
### `Estimator`
- 'Estimator'는 '추정기'라는 뜻으로, 추정을 하기 위한 지도 학습에 대한 클래스
- **지도학습의 모든 알고리즘을 구현한 클래스**를 통칭
- 학습을 위한 `fit()`과 예측을 위한 `predict()` 메서드가 정의되어 있다.
  - `fit(X, y)` : 학습을 위한 메서드
    - `X` : feature 데이터 중 학습을 위한 훈련 데이터
    - `y` : target 데이터
  - `predict(X)` : 예측을 위한 메서드
    - `X` : feature 데이터 중 학습된 머신러닝 모델의 성능을 평가하기 위한 테스트 데이터
- `Classifier`(분류) 클래스와 `Regressor`(회귀) 클래스는 `Estimator` 클래스를 상속받은 클래스로 `fit()`과 `predict()` 메서드를 사용할 수 있다.
- `Classifier`(분류) 클래스와 `Regressor`(회귀) 클래스를 합쳐서 `Estimator` 클래스라고도 한다.
- evaluation(평가) 함수, 하이퍼 파라미터 튜닝을 지원하는 클래스의 경우 `Estimator`를 인자로 받아 함수내에서 `Extimator`의  `fit()`과 `predict()` 메서드를 호출해서 평가 혹은 하이퍼 파라미터 튜닝을 수행
  - ex. `cross_val_score()` : evaluation 함수
  - ex. `GridSearchCV` : 하이퍼 파라미터 튜닝을 지원

### `Classifier`
- 지도 학습 중 **분류 알고리즘을 구현한 클래스**
- `Classifier`를 상속받은 분류 구현 클래스
  - DecisionTreeClassfier
  - RandomGorestClassfier
  - GradientBoostingClassifer
  - LogisticRegression
    - Linear Regression(선형 회귀)에 Logistic 함수가 합쳐져서 만들어진 것
    - 많이 사용되고 딥러닝의 기초로 사용되는 클래스
  - SCV 등

### `Regressor`
- 지도학습 중 **회귀 알고리즘을 구현한 클래스**
- `Regressor`를 상속받은 회귀 구현 클래스
  - DecisionTreeRegressor
  - RandomForestRegressor
  - GradientBoostingRegressor
  - LinearRegression
  - Ridge, Lasso 등

## 사이킷런 주요 모듈
### 예제 데이터
- `sklearn.datasets` : 사이킷런에 내장되어 예제로 제공하는 데이터 세트
  - `load_iris`

### 데이터 분리, 검증, 파라미터 튜닝
- `sklearn.model_selection` : 교차 검증을 위한 학습용/테스트용 데이터 세트로 분리, 그리드 서치(Grid Search)로 최적 파라미터 추출 등의 API 제공
  - `train_test_split`
  - `KFold`
  - `StratifiedKFold`
  - `cross_val_score`
  - `GridSearchCV`

### 피처 처리
- `sklearn.preprocessing` : 데이터 전처리에 필요한 다양한 가공 기능 제공(인코딩, 정규화, 스케일링 등)
- `skelarn.feature_selection` : 알고리즘에 큰 영향을 미치는 피처를 우선순위 대로 셀렉션 작업을 수행하는 다양한 기능을 제공
- `sklearn.feature_extraction`
  - 텍스트 데이터나 이미지 데이터의 벡터화된 피처를 추출하는데 사용
  - `sklearn_feature_selection.text` : 텍스트 데이터 피처 추출
  - `sklearn_feature_selection.image` : 이미지 데이터 피처 추출

### 피처 처리 및 차원 축소
- `sklearn.decompositon` 
  - 차원 축소와 관련한 알고리즘을 지원하는 모듈
  - PCA, NMF, Truncated SVD 등을 통한 차원 축소 기능 수행

### 평가
- `sklearn.metrics` : 분류, 회귀, 클러스터링 등에 대한 다양한 **성능측정 방법** 제공
  - Accuracy, Precision, Recall, ROC-AUC, RMSE 등 제공

### 머신러닝 알고리즘
- `sklearn.encemble` : 앙상블 알고리즘 제공
  - RandomForest, AdaBoost, GradientBoosting emd
- `sklearn.linear_model` : 회귀 관련, SGD(Stochastic Gradient Descent) 관련 알고리즘 지원
  - Linear Regression(선형 회귀), Ridge, Lasso, LogisticRegression(회귀 관련 알고리즘이지만 분류 모델에 해당) 등
- `sklearn.naive_bayes` : 나이브 베이즈 알고리즘 제공
  - 가우시안 NB, 다항 분포 NB 등 지원
- `sklearn.neighbors` : 최근접 이웃 알고리즘 제공
  - KNN 등
- `sklearn.svm` : 서포트 벡터 머신(SVM; Support vector Machine) 알고리즘 제공
- `sklearn.tree` : 의사 결정 트리 알고리즘 제공
- `sklearn.cluster` : 비지도 클러스터링 알고리즘 제공
  - K-Mean, 계층형, DBSCAN 등

### 유틸리티
- `sklearn.pipeline` : 피처 처리 등의 변환과 ML 알고리즘 학습, 예측 등을 함께 묶어서 실행할 수 있는 유틸리티 제공

## 머신러닝 모델링 프로세스
1. **데이터 분할** : 데이터를 학습 데이터 세트, 테스트 데이터 세트로 분리
2. **모델 학습(fit)** : 학습 데이터를 기반으로 머신러닝 알고리즘을 적용해 모델을 학습
3. **예측 수행(predict)** : 학습된 머신러닝 모델을 이용해 테스트 데이터로 예측
4. **평가(evaluate**) : 예측된 결과값과 테스트 데이터의 실제 결과값을 비교해 머신러닝 모델 예측 성능을 평가
  