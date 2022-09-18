# 스프링 배치 시작 - Hello Spring Batch 시작하기

## 스프링 배치 흐름
> Job → Step → Tasklet
* ```Job```이 구동되면 ```Step```을 실행
* ```Step```이 구동되면 ```Tasklet```을 실행
* 기본적으로 ```Step```에서 ```Tasklet```을 무한 반복한다.
  * 한번만 작동하고 종료하기 위해서는 ```RepeatStatus.FINISHED```를 사용해야 한다.
  ```
  @Bean
    public Step helloStep1() {
        return stepBuilderFactory.get("helloStep1")
                .tasklet((contribution, chunkContext) -> {
                    System.out.println("=====================");
                    System.out.println(">> Hello Spring Batch");
                    System.out.println("=====================");
                    return RepeatStatus.FINISHED;
                })
                .build();
    }
  ```


## 예제 코드
[예제 코드](https://github.com/yshjft/spring-batch-practice/tree/Part2)

