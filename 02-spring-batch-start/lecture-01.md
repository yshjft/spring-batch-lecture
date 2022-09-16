# 스프링 배치 시작 - 프로젝트 구성 및 의존성 설정

## @EnableBatchProcessing
스프링 배치가 작동하기 위해 선언해야 하는 어노테이션

* 총 4개의 설정 클래스를 실행
* 빈으로 등록된 모든 Job을 검색해서 초기화와 동시에 Job을 수행하도록 구성


## 스프링 배치 초기화 설정 클래스
앞에서 언급한 ```총 4개의 설정 클래스```이다.

* **BatchAutoConfiguration**   
  * 스프링 배치가 초기화 될 때 장도으로 실행되는 설정 클래스
  * Job을 수행하는 ```JobLauncherApplicationRunner``` 빈을 생성
    * spring boot 초기화 이후 ```ApplicationRunner``` 구현체들을 실행한다,
    * ```JobLauncherApplicationRunner```가 ```ApplicationRunner```의 구현체이다.

* **SimpleBatchConfiguration**
  * ```JobBuilderFactory```와 ```StepBuilderFactory``` 생성
    * batch job 생성시 ```JobBuilderFactory```와 ```StepBuilderFactory``` 사용
  * 스프릥 배치의 주요 구성 요소를 생성한다.(프록시 객체로 생성)

* **BatchConfigurerConfiguration**
  * **BasicBatchConfigurer**
    * ```SimpleBatchConfiguration```에서 생성한 프록시 객체의 실제 대상 객체를 생성하는 클래스
    * 빈으로 의존성 주입 받아서 주입 받아서 주요 객체들을 참조해서 사용할 수 있다.
  * **JpaBatchConfigurer**
    * ```BasicBatchConfigurer```를 상속
    * JPA 관련 객체를 생성하는 설정 클래스


### 설정 클래스 순서
> @EnableBatchProcessing → SimpleBatchConfiguration → BatchConfigurerConfiguration → BatchAutoConfiguration

