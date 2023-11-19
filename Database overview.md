# DB

- 전자적으로 저장되고 사용되는 관련있는 데이터들의 조직화된 집합(organized collection)
- 관련있는: 같은 출처, 목적 등
- 이 관련있는 데이터를 조직화된 집합으로 묶어야 함

# DBMS

- 사용자에게 DB를 정의하고 만들고 관리하는 기능을 제공하는 소프트웨어 시스템

# Metadata

- database를 정의하거나 기술하는(descriptive) data
- catalog라고도 부름(메타데이터가 저장되는 곳을 catalog라고도 함)
- 데이터 유형, 구조, 제약조건, 보안, 저장, 인덱스 ,사용자 그룹 등등
- metadata 또한 DBMS로 저장, 관리 됨

# Database system

- database+DBMS+연관된 applications
- 줄여서 database라고도 부름 (문맥에 따라 잘 구별해야함)
- 사용자, 프로그래머->어플리케이션 프로그램(여기엔 데이터베이스에 접근하는 쿼리가 있음)->DBMS가 쿼리 분석하고 이것을 파악하면, 처리 (부가적인 메타데이터를 바탕으로)->이후 처리한 내용을 어플리케이션에 돌려줌

# Data models

- DB의 구조를 기술하는데 사용될 수 있는 개념들이 모인 집합
- DB 구조(데이터 유형, 데이터 관계, 제약사항 등)를 추상화해서 표현할 수 있는 수단을 제공
- data model은 여러 종류가 있으며 추상화 수준과 DB 구조화 방식이 조금씩 다름
- DB에서 읽고 쓰기 위한 기본적 동작(operation)도 포함됨

## data models 분류

- conceptual (or high-level) data models
  - 일반 사용자들이 쉽게 이해할 수 있는 개념들로 이뤄짐
  - 추상화 수준이 가장 높음
  - 비즈니스 요구사항을 추상화하여 기술할 때 사용
    - entity-relationship model
    - ER diagram 등이 있음

- logical (or representational) data models
  - 이해하기 어렵지 않으면서 디테일하게 DB를 구조화 할 수 잇는 개념들을 제공
  - 데이터가 컴퓨터에 저장될 때의 구조와 크게 다르지 않게 DB 구조화를 가능하게 함
  - 특정 DBMS나 storage에 종속되지 않는 수준에서 DB를 구조화 할 수 있는 모델
    - relational data model
      - 표가 있다고 보면 됨 (pandas처럼)
    - object data model
    - object-relational data model
  - 유명한 DMBS는 거의 relational data model이다.
 
  
- physical (or low-level) data models
  - 컴퓨터가 데이터에 어떻게 파일 형태로 저장되는지를 기술할 수 있는 수단을 제공
  - data format, data orderings, access path 등
  - access path: 데이터 검색을 빠르게 하기 위한 구조체, e.g.)index

# schema and state

## database schema
- data model 바탕으로 database 구조를 기술한 것
- schema는 database 설계할 때 정해지며 한번 정해지면 자주 바뀌지 않음
- pandas의 표와 같이 구조를 보면 알 수 있는 형태와 비슷

   
## database state
- database에 있는 실제 데이터는 꽤 자주 바뀔 수 있다.
- 특정 시점에 database에 있는 데이터를 database state 혹은 snapshot이라고한다.
- database에 있는 현재 instances의 집합이라고도 한다.
  - 시간축에 따라 나온 그 상태

## three-schema architecture
- database system을 구축하는 architecture 중의 하나
- user application으로 부터 물리적(physical) database를 분리시키는 목적
- 세 가지 level 존재하고 각각의 level 마다 schema가 정의되어 있음

  - external schema (user view) at external (or view) level
    - 실제 사용자가 보는 schema (external views, user views)
    - 특정 유저들이 필요로 하는 데이터만 표현
    - 그 외 알려 줄 필요가 없는 데이터는 숨김
    - logical data model을 통해 표기
  
  - conceptual schema at conceptual level
    - 전체 database에 대한 구조를 기술
    - internal schema를 한번 추상화 시켜서 표현
    - 물리적 저장 구조에 관한 내용은 숨김
    - entities, data types, relationships, user operations, constraints에 focus
    - logic data model을 통해 기술

  - internal schema at internal level
    - 물리적인 저장장치에 가장 붙어있음
    - 물리적으로 데이터가 어떻게 저장되는지 physucak data model을 통해 표현
    - data storage, data structrure, access path 등등 실체가 있는 내용을 기술
   
- 결국 이 three schema architecture는 각 레벨을 독립시켜서 어느 레벨에서의 변화가 상위 레벨에 영향을 주지 않기 위함
  - 대부분의 DBMS가 three level을 어느 정도 따르긴 하나 완벽하게 혹은 명시적으로 나누지는 않고, 데이터가 존재하는 곳은 internal level

# Database language 종류
## data definition language (DDL)
- conceptual schema를 정의하기 위해 사용되는 언어
  - internal schema 까지 정의할 수 있는 경우도 있다.

## storage definition language (SDL)
- internal schema를 정의하는 용도로 사용되는 언어
- 요즘은 특히 relational DBMS에서는 SDL 거의 없고 파라미터 등의 설정으로 대체됨

## view definition language (VDL)
- external schemas를 정의하기 위해 사용되는 언어
- 대부분의 DBMS에서는 DDL이 VDL 역할까지 수행

## data manipulation language (DML)
- database에 있는 data를 활용하기 위한 언어
- data 추가,삭제,수정,검색 등등의 기능을 제공하는 언어

- 요즘엔 통합된 언어로 존재 대표적인 예가 relational database language: SQL
