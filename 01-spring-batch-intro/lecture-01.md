# 스프링 배치 소개

## 스프링 배치 탄생 배경
* 자바 기반 표준 배치 기술 부재
  * 배치 처리에서 요구하는 재사용 가능한 자바 기반 배치 아키텍처 표준의 필요성이 대두


## 배치 핵심 패턴
### Read
데이터 소스(데이터베이스, 파일)에서 다량의 데이터를 조회한다.

### Process
특정 바법으로 데이터를 가공한다.

### Write
데이터를 수정된 양식으로 다시 저장한다.

### Read Process Write = Extract Transform Load
* Read Process Write
  * 스프링 배치에서 사용하는 개념
* Extract Transform Load(ETL)
  * 데이터를 추출, 데이터 변형, 데이터 적재
  * DB에서 사용하는 개념
 

## 배치 시나리오
* 배치 프로세스를 주기적으로 커밋
  * 대용량의 데이터를 쪼개서 커밋
* 동시 다발적인 Job의 배치처리, 대용량 병렬 처리
  * 병렬 처리 = 멀티 스레드 처리
* 실패 후 수동 또는 스케줄링에 의한 재시작
* 의존관계가 있는 step 여러개를 순차적으로 처리
  * >step1 → step2 → step3
* 조건적 Flow 구성을 통한 체계적이고 유연한 배치 모델 구성
  * > step1 → step3
  * 조건에 따라 ```step2```를 거치지 않고 다음 단계를 실행
* 반복, 재시도, skip 처리
  * 반복적으로 배치 실행
  * 재시도를 장애가 복구 되면 Job이 이루어질 수 있게 해야한다 .
  * 특정한 예외는 skip하여 Job이 지속될 수 있도록 한다.


## 아키텍처
![img.png](https://docs.spring.io/spring-batch/docs/current/reference/html/images/spring-batch-layers.png)

### Application
* 스프링 배치 프레임워크를 통해 개발자가 만든 모든 배치 job과 커스텀 코드를 포함
* 개발자는 비즈니스 로직 구현에만 집중, 공통적인 기반기술은 프레임웍이 담당

### Batch core
* Job을 실행, 모니터링, 관리하는 API로 구성
* JobLauncher, Job, Step, Flow 등이 속한다.

### Batch Infrastructure
* Application, Batch core 모두 공통 Infrastructure 위에서 빌드한다.
* Job 실행의 흐름과 처리르 위한 틀을 제공
  * 어떻게 데이터를 처리할지와 관련된 클래스들이 속한다.
* Reader, Processor Writer, Skip, Retry 등이 속한다.