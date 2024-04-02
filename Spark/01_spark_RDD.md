# Spark RDD

## Spark Context 구성
가장 먼저 Spark Context를 사용할 수 있는 환경 설정을 해야 한다.
- Spark Context를 이용해 Driver Program 개발
- Driver Program을 클라이언트는 Spark Master에게 제출
- Spark Master는 Spark Worker에게 Task를 전달


```python
from pyspark import SparkConf, SparkContext

conf = SparkConf().setMaster("local").setAppName("country-student-count")

sc = SparkContext(conf=conf)
sc
```
- 한 번만 실행해야 한다. 
  - 만약 여러번 실행하여 에러가 날 경우 `sc.stop()`으로 종료 후 다시 실행
- `SparkConf` : 스파크 실행 환경 설정 클래스
  - `setMaster()` : Master 위치 지정
    - 현재 `SparkConf`가 실행되는 위치인 local의 Disk로 설정한 것
    - HDFS 연동시, `"yarn"`으로 설정하여 하둡과 연결할 수 있다.
  - `setAppName()` : Job 이름(작업명) 지정
- `SparkContext` : Driver Program 실행 환경 구성을 위한 클래스
  - `SparkContext`의 변수명은 웬만하면 `sc`로 만드는 것을 권장
- Spark Jobs web ui에서 Job이 연결된 것을 확인할 수 있다.
  - `localhost:4040/`

## Data Load
- Spark는 데이터를 로드할 때 **RDD로 데이터를 추상화**시킨다.
- **데이터 추상화** : 하나의 파일이 여러 개의 블록으로 여러 DataNode에 저장될 수 있다. Spark에서는 하나의 파일을 이루는 블록들을 세부적으로 지칭하지 않고 이 블록 전체를 대략적으로 RDD라고 지칭하는데 이를 데이터 추상화라고 볼 수 있다. 
- Spark에서는 하나의 파일을 RDD로 데이터를 모아서 가져온다.

```python
# 파일 경로 지정
filepath = "/home/ubuntu/working/spark/data/xAPI-Edu-Data.csv"

# 파일 경로에서 csv 파일 가져오기
lines = sc.textFile(f"file:///{filepath}")
lines
```
- `textFile` : 데이터의 형식을 textFile로 지정
- `file://<파일경로>` : 파일 경로로 `/{filepath}` 지정
- `lines` 변수명으로 Data Load에 대한 하나의 RDD가 만들어지게 된다.
  - **Transformations**
  - RDD의 특징은 게으른 연산이기 때문에, 데이터 로드도 연산으로서 실제로 데이터를 가져오는 것이 아니라 해당 연산을 기록하고 추후 Action을 수행했을 때 실제로 데이터가 로드된다.

## `filter()`
```python
RDD.filter(<task>)
```
- SQL의 WHERE절과 같은 역할로 **특정 조건(Task)의 데이터만 조회**하는 함수
  - Task는 `lambda`식 혹은 `def`로 함수를 정의하여 사용
- **Transformation 함수**로 반드시 return이 있어야 하고 실행시 RDD를 반환

## `map()`
```python
RDD.map(<task>)
```
- 각 row에 대해 Task를 적용하여 원하는 데이터로 변형시킬 수 있는 함수
- **Transformation 함수**


## 데이터 확인 - Action
- **결과물(Output)의 확인하는 것은 Action**
- Action 함수 실행시 **Stage 생성**
    - Stage는 첫 번째 Transformation부터 Action까지의 연산 기록을 모두 수행하는 과정
    - Spark web ui Stages에서 작업 수행 내용을 해당 Stage에서 확인 가능
    - DAG Visualization에서 연산 기록을 확인할 수 있다.
  
### `first()`
- 데이터의 첫 번째 줄 확인하는 Action 함수

## `countByValue()`
- Pandas DataFrame의 `value_counts()`와 비슷한 역할로 unique값들의 갯수를 집계해주는 Action 함수

### `collect()`
- 모든 연산 수행에 대한 결과물을 모두 가져오는 Action 함수

## Spark Context 종료 - `stop()`
```python
# 위에서 Spark Context를 sc 변수명으로 지정함
sc.stop()
```
- 하나의 작업이 끝나면 반드시 해당하는 작업의 Spark Context를 종료해주어야 한다.
- 종료하지 않을 경우 계속해서 메모리를 차지한다.
