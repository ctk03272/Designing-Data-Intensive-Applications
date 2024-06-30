# Chapter1
## 넷플릭스의 카오스 몽키
- https://github.com/netflix/chaosmonkey
- 카오스 몽키는 임의로 버츄얼 머신을 종료시켜, 결함이 일어나게 하고 그 상태에서 복구를 하도록함
- 카오스 엔지니어링(https://principlesofchaos.org/)
  - 인위적으로 문제를 발생시켜 미리미리 준비한다
- 여러 장애를 일으키는 몽키들이 있다
  - 레이턴시 몽키(API 인위적 지연)
  - 순응 몽키(인스턴스 종료시킴)
  - 의사 몽키(인스턴스 상태를 점검하여 불안정 인스턴스 탐지) 등등
- 실제로 회사에서 어떻게들 이런 테스트를 하는지 궁금
  - 우리 회사의 경우 AWS의 AZ일부 존을 shutdown하는 방식의 테스트를 진행

## 2012년 6월 30일 윤초
- https://blog-tech.tadatada.com/2016-12-28-struggling-with-the-leap-second

## 비 프로덕션 샌드박스
- 회사에는 이런 환경이 없다. 이런 환경을 만들 필요성이 있을것 같긴함.....


## 부하에 관한 트위터의 예시
- 라인에서는 어떻게 처리했을 까? (https://d2.naver.com/helloworld/809802)


# Chapter2
## noSQL의 쓰기 처리량이 더 높은 이유
- 수평적 확장성 ( 샤딩 및 분산 아키텍처 )
- 단순한 일관성 모델 (데이터 쓰기가 즉시 모든 노드에 반영되지 않아도 된다.)
- 복잡한 트랜잭션 관리의 부재

## 데이터베이스에서 지역성이란?
- 데이터베이스 액세스 패턴이 물리적 저장 구조와 잘 맞아 떨어져서 데이터 접근이 효율적이고 빠르게 이루어 진다는 것을 의미한다.

## 오라클의 다중 테이블 색인 클러스터 테이블이란
- 여러 테이블의 데이터를 물리적으로 인접하게 저장하여 조인 성능을 향상시키는 데이터 저장 구조
예시
```SQL
CREATE CLUSTER employee_department_cluster (
    department_id NUMBER
)
INDEX BY department_id;

CREATE TABLE employees (
    employee_id NUMBER,
    employee_name VARCHAR2(50),
    department_id NUMBER
)
CLUSTER employee_department_cluster (department_id);

CREATE TABLE departments (
    department_id NUMBER,
    department_name VARCHAR2(50)
)
CLUSTER employee_department_cluster (department_id);

```