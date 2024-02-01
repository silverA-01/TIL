# 데이터 전처리(Data Preprocessing)
ML 알고리즘은 데이터에 기반하고 있기 때문에 어떤 데이터를 입력으로 가지느냐에 따라 결과도 크게 영향을 받는다. (Garbage In, Garbage Out)

데이터 전처리는 사이킷런 ML 알고리즘을 적용하기 전에 데이터에 미리 처리해야할 기본 사항이다.

- 데이터 클린징
- 결손값 처리(Null, NaN 처리)
  - ML 알고리즘은 결손값을 허용하지 않기 때문에 고정된 다른 값으로 변환 필요
  - Null값이 존재하는 피처 데이터의 중요도, Null 값이 해당 피처 데이터에서의 비율 등을 다양하게 고려해 변환된 Null값이 결과를 왜곡하지 않도록 처리해야 한다.
  - Null값이 대부분인 피처는 드롭하는 것이 더 좋을 수 있다.
- 데이터 인코딩
- 데이터 스케일링
- 이상치(Outlier) 제거
- Feature 선택, 추출 및 가공


## 데이터 인코딩(Data Encoding)
- ML 알고리즘은 문자열 데이터 속성을 입력받지 않는다.
- 그 중에서 문자형 카테고리형 속성, 즉 **명목형 문자형 피처는 모두 숫자값으로 변환/인코딩** 되어야 한다.
- 고유한 값을 가진 ID(Identification)로 사용되는 문자형 데이터는 인코딩하지 않고 삭제하는 것이 좋다.
  - 단순히 데이터 로우를 식별하는 용도로 사용되기 때문에 예측에 중요한 요소가 될 수 없다.
  - 오히려 ML 알고리즘을 복잡하게 만들고 예측 성능을 떨어뜨린다.
- Encoding : 코드화하는 것.
  - 코드란 컴퓨터가 알아들을 수 있는 정보를 의미한다. 즉, 인코딩이란 사람이 알아들을 수 있는 정보에서 컴퓨터가 알아들을 수 있는 정보로 바꾸는 것이다.

### 1. 레이블 인코딩(Lable Encoding)
카테고리(명목형) 피처를 코드형 숫자 값으로 변환하는 것
- 참고로 `01`, `02` 같은 코드 값 역시 문자열이므로 `1`, `2`와 같은 숫자형 값으로 변환돼야 함
- 사이킷런의 `LableEncoder` 클래스로 레이블 인코딩 구현
- `LableEncoder`의 객체를 생성한 후 `fit()`과 `transform()`을 호출해 레이블 인코딩을 수행

```python
items = ['TV','냉장고','전자렌지','컴퓨터','선풍기','선풍기','믹서','믹서']

from sklearn.preprocessing import LabelEncoder

# LabelEncoder 클래스 객체 생성
encoder = LabelEncoder()
# 인코딩 준비
encoder.fit(items)
# 인코딩 수행
labels = encoder.transform(items)
```
- `fit()`
  - `Transformer` 클래스를 `LabelEncoder` 클래스가 상속받아 `fit()` 메서드 사용 가능
  - `fit()`을 호출하면 데이터를 받아서 ML 알고리즘에 적용시킨다.
  - 여기서 `fit()`은 데이터 변환을 위해 내부적으로 Data를 ML 알고리즘에 적용시켜 이해하는 과정, 즉 데이터를 변환할 준비를 하는 것
- `transform()`
  - ML 알고리즘으로 이해한 변환된 데이터를 반환

```python
encoder.fit_transform(items)
```
- `fit_transform()` 로 `fit()`과 `transform()` 메서드의 기능을 동시에 수행할 수 도 있다.

```python
# 인코딩 변환값 확인
labels
```
```python
array([0, 1, 4, 5, 3, 3, 2, 2])
```
- 인코딩 변환값을 확인할 수 있다.

```python
# 인코딩 클래스 확인
encoder.classes_
```
```python
array(['TV', '냉장고', '믹서', '선풍기', '전자렌지', '컴퓨터'], dtype='<U4')
```
- 인코딩 값에 대응되는 문자열 형태의 원본 레이블 클래스가 저장된 것을 확인할 수 있다.

```python
# 인코딩 변환값을 활용해 디코딩 함수 호출
encoder.inverse_transform([0, 1, 4, 5, 3, 3, 2, 2])
```
```python
array(['TV', '냉장고', '전자렌지', '컴퓨터', '선풍기', '선풍기', '믹서', '믹서'], dtype='<U4')
```
- `inverse_transform()` : 인코딩된 값을 디코딩하여 원본 데이터로 되돌려주는 함수
  - 디코딩은 인코딩의 반대말로, 컴퓨터가 알아볼 수 있는 정보에서 사람이 알아볼 수 잇는 정보로 변환하는 과정

### 2. 원-핫 인코딩(One-Hot Encoding)
- One-Hot : 오직 하나의 피처만 의미있게 사용하는 것을 의미
- 피처의 유형에 따라 **새로운 피처를 추가해 고유값에 해당하는 컬럼에만 1을 표시하고, 나머지 컬럼에는 0을 표시**한다.
- 행 형태로 되어 있는 피처의 고유 값을 열 형태로 차원을 변환한 뒤, 고유값에 해당하는 컬럼에만 1을 표시하고 나머지 컬럼에는 0을 표시
- 새로 만들어진 컬럼을 **더미(dummy) 컬럼** 혹은 더미 특성이라고 하고 더미 컬럼 전체를 묶어서 **희소행렬**이라고 부른다.
  - 데이터의 값이 0인 것은 수치로서 의미가 없고 필요없는 데이터라는 의미이다.
  - 즉, 희소행렬은 0이 많은 의미없는 데이터가 많다.
- 이 방식은 더미 컬럼이 너무 많아질 수 있기 때문에, 데이터의 양에 비해 의미없는 데이터가 너무 많아질 수 있다는 점이다.
- 이를 방지하기 위해 사이킷런의 `OneHotEncoder` 클래스는 Compressed Sqaure Row Format을 지원하여 희소행렬을 압축해 1이 있는 위치(행번호, 열번호)로 체크해준다.

```python
## 원-핫 인코딩(One-Hot Encoding)
from sklearn.preprocessing import OneHotEncoder
import numpy as np

# 넘파이 2차원 ndarray로 변환
items_arr = np.array(items).reshape(-1, 1)
items_arr
```
```python
array([['TV'],
       ['냉장고'],
       ['전자렌지'],
       ['컴퓨터'],
       ['선풍기'],
       ['선풍기'],
       ['믹서'],
       ['믹서']], dtype='<U4')
```
- `OneHotEncoder` 클래스는 2차원 배열의 데이터만 사용할 수 있기 때문에 데이터를 배열로 만들어준 후,  `reshape` 사용해서 배열의 모양과 차원을 변경해준다.
- `reshape(-1, 1)`
  - `-1` 자리는 배열의 행의 개수를 의미하는 정수
  - `1` 자리는 배열의 열의 개수를 의미하는 정수
  - `-1`은 열의 값이 지정되었을 때 남은 배열의 길이와 남은 차원을 추정해 알아서 지정하라는 의미. 여기서는 2차원 배열을 만들어주기 위해 사용되었다.

```python
# OneHotEncoder 객체 생성
encoder = OneHotEncoder()

# 데이터 인코딩 수행
ohe_labels = encoder.fit_transform(items_arr)
ohe_labels
```
```python
<8x6 sparse matrix of type '<class 'numpy.float64'>'
	with 8 stored elements in Compressed Sparse Row format>
```
- `OneHotEncoder`는 Compressed Square Row Format을 통해 1의 위치를 압축된 형식의 데이터로 변환한다.

```python
print(ohe_labels)
```
```python
  (0, 0)	1.0
  (1, 1)	1.0
  (2, 4)	1.0
  (3, 5)	1.0
  (4, 3)	1.0
  (5, 3)	1.0
  (6, 2)	1.0
  (7, 2)	1.0
```
- 출력해보면 압축된 형식의 데이터를 확인할 수 있다.

```python
ohe_labels.toarray()
```
```python
array([[1., 0., 0., 0., 0., 0.],
       [0., 1., 0., 0., 0., 0.],
       [0., 0., 0., 0., 1., 0.],
       [0., 0., 0., 0., 0., 1.],
       [0., 0., 0., 1., 0., 0.],
       [0., 0., 0., 1., 0., 0.],
       [0., 0., 1., 0., 0., 0.],
       [0., 0., 1., 0., 0., 0.]])
```
- `toarray()`를 활용하여 압축된 형식의 데이터를 풀어서 새로 추가된 더미 컬럼을 확인할 수 잇다.

## 데이터 스케일링(Feature Scaling)
서로 다른 피처 데이터값의 범위를 일정한 수준으로 맞추는 작업
- 대표적인 방법으로 표준화, 정규화가 있다.

### 1. `StandardScaler` - 표준화
- 표준화는 모든 피처 데이터가 평균이 0이고 분산이 1(표준편차가 1)인 가우시안 정규 분포를 가진 값으로 변환하는 것
- Zero-Centered : 모든 피처 데이터가 0을 중심으로 분포하도록 변환하여 데이터를 동일선상에 놓고 본다.
- 모든 피처 데이터의 분포 및 스케일이 다른 경우 사용한다. 대부분의 피처 데이터는 표준화를 사용한다.
- 음수가 존재할 수 있다.
- 2차원 배열만 데이터로 사용할 수 있다.

```python
import numpy as np

data1 = np.array([100, 110, 120, 130, 140])
data2 = np.array([0, 1, 2, 3, 4])

data1_mvs = data1.mean(), data1.var(), data1.std()
data2_mvs = data2.mean(), data2.var(), data2.std()

data1_mvs, data2_mvs
```
```python
((120.0, 200.0, 14.142135623730951), (2.0, 2.0, 1.4142135623730951))
```
- data 1, data2의 평균, 분포, 표준편차가 다르고 동일 선상에 있지 않은 것을 확인할 수 있다.

```python
from sklearn.preprocessing import StandardScaler

# StandardScaler 객체 생성
std_scaler = StandardScaler()

# 표준화할 데이터를 넘파이 2차원 배열로 만들어준다.
data1 = data1.reshape(-1, 1)
data2 = data2.reshape(-1, 1)

# 표준화 데이터 변환
data1_scaled = std_scaler.fit_transform(data1)
data2_scaled = std_scaler.fit_transform(data2)

data1_scaled, data2_scaled
```
```python
(array([[-1.41421356],
        [-0.70710678],
        [ 0.        ],
        [ 0.70710678],
        [ 1.41421356]]),
 array([[-1.41421356],
        [-0.70710678],
        [ 0.        ],
        [ 0.70710678],
        [ 1.41421356]]))
```
- 0점 기준으로 data 1, data2가 동일 선상에 놓아진 것을 확인할 수 있다.

### 2. `MinMaxScaler` - 정규화
- `MinMaxScaler`를 이용하는 정규화는 피처 데이터의 최소값을 0으로, 최대값을 1로 변환하는 것
- 즉, 모든 피처 데이터의 분포는 그대로 유지하되, 데이터의 크기를 0에서 1사이로 변환하여 데이터를 공평하게 놓고 본다.
  - 따라서 음수가 존재하지 않는다.
- 데이터의 최솟값, 최대값이 정해져 있을 경우 사용하기 좋다. 
  - ex. 별점
- Min-Max Scaling으로 정규화하는 데이터는 Standard Scaling으로 표준화해도 무방하다. 데이터 분석을 통해 더 유리한 쪽으로 데이터 스케일링을 하면 된다.
- 2차원 배열만 데이터로 사용한다.

```python
# 네이버와 넷플릭스 영화 평점이 담긴 데이터프레임 생성
import pandas as pd
movie_score = pd.DataFrame({
    "naver":[0, 2, 4, 6, 8],
    "netflix":[1, 2, 3, 4, 5]
})

# MinMaxScaler를 이용해서 naver와 netflix 의 데이터를 동일하게 볼 수 있게 정규화
from sklearn.preprocessing import MinMaxScaler

# MinMaxScaler 객체 생성
mm_scaler = MinMaxScaler()

# 데이터프레임을 인자로 넣어준다.
movie_score_scaled = mm_scaler.fit_transform(movie_score)

movie_score_scaled
```
```python
array([[0.  , 0.  ],
       [0.25, 0.25],
       [0.5 , 0.5 ],
       [0.75, 0.75],
       [1.  , 1.  ]])
```