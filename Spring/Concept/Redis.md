# 레디스(Redis)란 무엇인가?
## 1. NOSQL 이란?
RDBMS는 보통 "관계형 데이터베이스"라고 하며 반면 **NOSQL은 "비관계형 데이터 베이스"** 이다.  
보통 NOSQL은 키-밸류나 컬럼, 문서 형식의 데이터 모델을 이용한다.

### **NOSQL: Not Only SQL, 비관계형 데이터베이스**
왜 NOSQL을 쓰는 걸까? 아주 많은 양의 데이터를 효율적으로 처리가 필요할 때, 데이터의 분산처리, 빠른 쓰기 및 데이터의 안정성이 필요할 때 사용한다.  
특정 서버에 장애가 발생했을 때에도 데이터 유실이나 서비스 중지가 없는 형태의 구조이기 때문에, NOSQL을 사용한다.

## 1-1 NOSQL 의 종류
1) 키-밸류 스토리지형 키-밸류형: Redis, memcached, Oracle, Coherence
2) 열 지향 와이드 칼럼 스토어: Cassandra, HBASE, Cloud Database
3) 문서형: MongoDB, Couchbase, MarkLogic, PostgreSQL, MySQL, DynamicDB MS-DocumentDB
4) 그래프형: Neo4j

<br>

> ### MongoDB 란?  
> - 몽고DB는 도큐먼트 지향 데이터 베이스이다.  
> - bson 데이터 구조로 저장한다.  
> - 문서를 기본 저장 단위로 이용하면서 내장 문서와 배열을 이용해서 복잡한 계층구조를 하나의 레코드(열)로 표현한다.  
> - 스키마가 없다.  
> - 필드 추가 제거는 자유로우며 필요할 때 마다 자유자재로 변경 가능하다.  
> - RDBMS 보다 몇십, 몇백배 빠른 고성능이다.  
> - 조인과 트랜잭션을 지원하지 않으며 여러 제약조건에 대한 처리도 없다.(버전에 따라 상이함)

## 2. 레디스(Redis)란?
REDIS(REmote Dictionary Server)는 메모리 기반의 "키-값" 구조 데이터 관리 시스템이며, 모든 데이터를 메모리에 저장하고 조회하기에 빠른 Read, Write 속도를 보장하는 **비 관계형 데이터베이스**이다.

레디스는 크게 5가지 ```<String, Set, Sorted Set, Hash, List>```의 데이터 형식을 지원한다.

Redis는 빠른 오픈 소스 인 메모리 키-값 데이터 구조 스토어이며, 다양한 인 메모리 데이터 구조 집합을 제공하므로 사용자 정의 애플리케이션을 손쉽게 생성할 수 있다.

<img src="https://miro.medium.com/max/1280/1*K8URxSP-CISf4_HkuXkPcA.jpeg">

## 3. 레디스(Redis)특징
* 영속성을 지원하는 인메모리 데이터 저장소.
* 읽기 성능 증대를 위한 서버 측 복제를 지원한다.

>(Redis가 실행중인 서버가 충돌하는 경우 장애 조치 처리와 함께 더 높은 읽기 성능을 지원하기 위해 슬레이브가 마스터에 연결하고 전체 데이터베이스의 초기 복사본을 받는 마스터 / 슬레이브 복제를 지원한다. 마스터에서 쓰기가 수행되면 슬레이브 데이터 세트를 실시간으로 업데이트하기 위해 연결된 모든 슬레이브로 전송된다.)

**쓰기 성능 증대를 위한 클라이언트 측 샤딩(Sharding)을 지원한다.**

> 샤딩(Sharding)이란??? 파티셔닝(Partitionong)과 동일하다. 같은 테이블 스키마를 가진 데이터를 다수의 데이터베이스에 분산하여 저장하는 방법을 의미한다.

**문자열, 리스트, 해시, 셋, 정렬된 셋과 같은 다양한 데이터형을 지원한다.**


## 4. 레디스(Redis)의 장점

* 리스트, 배열과 같은 데이터를 처리하는데 유용하다.

> value 값으로 문자열, 리스트, Set, Sorted set, Hash 등 여러 데이터 형식을 지원하기에, 다양한 방식으로 데이터를 활용할 수 있다.

* 리스트형 데이터 입력과 삭제가 MySQL에 배해서 10배정도 빠르다.

> 여러 프로세스에서 동시에 같은 key에 대한 갱신을 요청할 경우, Atomic 처리로 데이터 부정합 방지 Atomic처리 함수를 제공한다.(원자성을 잘 지킨다) 

* 메모리를 활용하면서 영속적인 데이터 보존

> 명령어로 명시적으로 삭제, expires를 설정하지 않으면 데이터가 삭제되지 않는다.스냅샷(기억장치) 기능을 제공하여 메모리의 내용을 *.rdb 파일로 저장하여 해당 시점으로 복구할 수 있다.

* Redis Server는 1개의 싱글 쓰레드로 수행되며, 따라서 서버 하나에 여러개의 서버를 띄우는 것이 가능하다.

> Master — Slave 형식으로 구성이 가능함, 데이터 분실 위험을 없애주는 것이 바로 Master — Slave 방식이다.

<img src="https://miro.medium.com/max/2648/1*z2wKmVgW6GZclPE2wpRadg.jpeg">