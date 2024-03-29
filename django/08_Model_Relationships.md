# Model Relationships
RDBMS(관계형 데이터베이스)는 테이블 상호간의 관계를 설정한다는 것이 특징이자 강점이다. 장고에서는 모델과 매핑된 데이터베이스의 관계를 크게 세 가지로 분류한다.

## FK(Foreign Key)
- 외래키로서 FK를 설정해야 한다.
- 다른 모델 클래스와의 관계 설정을 위해 필요
- FK는 `on_delete` 인자를 필수적으로 받는다.
  - 만약 FK로 사용하는 데이터의 레코드가 삭제되었을 때 FK를 사용하고 있는 모델은 어떻게 할지 정해주는 것
  - 데이터베이스가 데이터의 무결성을 지켜야하기 때문에 필요함

### 데이터의 무결성
데이터의 정확성, 일관성, 유효성이 유지되는 것

#### 1. 개체 무결성(Entity integrity)
- 개체는 하나의 row의 데이터 레코드를 의미
- Primary Key로 선택된 필드는 고유한 값을 가져야 하며, 빈 값은 허용하지 않는다.

### 2. 참조 무결성
참조 관계에 있는 두 테이블의 데이터가 항상 일관된 값을 갖도록 유지하는 것
- 참조되는 테이블의 특정 레코드가 지워졌을 때, 해당 테이블을 참조하는 다른 테이블에 무결성이 발생한다.
- 데이터베이스에서는 참조 무결성을 위해 참조 대상이 존재하지 않는 FK를 허용하지 않는다.
- 따라서 FK는 `on_delete` 인자를 필수적으로 받는다.

데이터의 참조 무결성을 지키기위해 FK의 `on_delete`인자에 대해 아래 기능을 지원한다.
- `RESTRICTED` : 레코드를 변경 또는 삭제하고자 할 때, 레코드를 참조하고 있는 개체가 있다면 변경 또는 삭제 연산을 취소한다.
- `CASCADE` : 레코드를 변경 또는 삭제하면, 해당 레코드를 참조하고 있는 개체도 변경 또는 삭제된다.
- `SET_NULL` : 레코드를 변경 또는 삭제하면, 해당 레코드를 참조하고 있는 개체의 값을 NULL로 설정한다.

## 1. `Many-to-one-relationships` - 1:N 관계
- 하나의 테이블의 레코드가 다른 테이블의 여러 레코드와 관련있을 때 1:N 관계를 갖는다.
- 1에 해당하는 모델 클래스를 먼저 정의하고 N에 해당하는 모델 클래스를 정의해야 한다.

## 2. `Many-to-Many-relationships` - M:N 관계

## 3. `One-to-one-relationships` - 1:1 관계