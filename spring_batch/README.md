# Spring Batch


## batch 란?
업무 혹은 IT에서 배치라함은 우리말로 일괄 처리(batch processing)의 batch를 말합니다. 배치는 사용자의 개입 없이 실행을 스케줄링할 수 있는 작업(job)을 의미하며. 컴퓨터 프로그램 흐름에 따라 순차적으로 자료를 처리하는 방식입니다.


'배치' 이용의 장점
1. 배치 프로그램을 이용하면 사용자가 적을때 컴퓨터 자원을 이용할 수 있습니다.  
2. 배치 실행 시간을 지정할 수 있어 컴퓨터 리소스가 덜 사용되는 시간대에 동작하게 함으로써 전체적으로 리소스의 유휴를 피할수 있습니다.  
3. 결과적으로 컴퓨터 자원 이용률과 효율을 높여 비용 낭비를 줄여줍니다.
 

## Spring Batch란?
- Spring Batch는 로깅/추적, 트랜잭션 관리, 작업 처리 통계, 작업 재시작, 건너뛰기, 리소스 관리 등 대용량 레코드 처리에 필수적인 기능을 제공합니다. 또한 최적화 및 파티셔닝 기술을 통해 대용량 및 고성능 배치 작업을 가능하게 하는 고급 기술 서비스 및 기능을 제공합니다.

- Spring Batch에서 배치가 실패하여 작업 재시작을 하게 된다면 처음부터가 아닌 실패한 지점부터 실행을 하게 됩니다.

-또한 중복 실행을 막기 위해 성공한 이력이 있는 Batch는 동일한 Parameters로 실행 시 Exception이 발생하게 됩니다.

## 그래서 언제사용하는데?
예를 들어, 전체 금액이 10000원 이상인 회원들에게 1,000원씩 캐시백을 줄 때 

*****

## Spring Batch 용어
### Job
- *최상단*
- Job은 배치처리 과정을 하나의 단위로 만들어 놓은 객체입니다. 또한 배치처리 과정에 있어 전체 계층 최상단에 위치하고 있습니다.

### JobInstance
- *실행단위*
- JobInstance는 Job의 실행의 단위를 나타냅니다. 
- Job을 실행시키게 되면 하나의 JobInstance가 생성되게 됩니다. 예를들어 1월 1일 실행, 1월 2일 실행을 하게 되면 각각의 JobInstance가 생성되며 1월 1일 실행한 JobInstance가 실패하여 다시 실행을 시키더라도 이 JobInstance는 1월 1일에 대한 데이터만 처리하게 됩니다.

### JobParameters
- *구분자*
- JobInstance는 Job의 실행 단위라고 했습니다. 그렇다면 JonInstance는 어떻게구별 할까요? 이는 바로 JobParameters 객체로 구분하게 됩니다. JobParameters는 JobInstance 구별 외에도 개발자 JobInstacne에 전달되는 매개변수 역할도 하고 있습니다.

- 또한 JobParameters는 String, Double, Long, Date 4가지 형식만을 지원하고 있습니다.

### JobExecution
- *실행시도*
- JobExecution은 JobInstance에 대한 실행 시도에 대한 객체입니다. 1월 1일에 실행한 JobInstacne가 실패하여 재실행을 하여도 동일한 JobInstance를 실행시키지만 이 2번에 실행에 대한 JobExecution은 개별로 생기게 됩니다. JobExecution는 이러한 JobInstance 실행에 대한 상태,시작시간, 종료시간, 생성시간 등의 정보를 담고 있습니다.

### Step
- Job 1 : Step *
- Step은 Job의 배치처리를 정의하고 순차적인 단계를 캡슐화 합니다. Job은 최소한 1개 이상의 Step을 가져야 하며 Job의 실제 일괄 처리를 제어하는 모든 정보가 들어있습니다.

### StepExecution
- StepExecution은 JobExecution과 동일하게 Step 실행 시도에 대한 객체를 나타냅니다. 하지만 Job이 여러개의 Step으로 구성되어 있을 경우 이전 단계의 Step이 실패하게 되면 다음 단계가 실행되지 않음으로 실패 이후 StepExecution은 생성되지 않습니다. StepExecution 또한 JobExecution과 동일하게 실제 시작이 될 때만 생성됩니다. StepExecution에는 JobExecution에 저장되는 정보 외에 read 수, write 수, commit 수, skip 수 등의 정보들도 저장이 됩니다.

### ExecutionContext
- *데이터 저장소*
- ExecutionContext란 Job에서 데이터를 공유 할 수 있는 데이터 저장소입니다. 
- Spring Batch에서 제공하느 ExecutionContext는 JobExecutionContext, StepExecutionContext 2가지 종류가 있으나 이 두가지는 지정되는 범위가 다릅니다. JobExecutionContext의 경우 Commit 시점에 저장되는 반면 StepExecutionContext는 실행 사이에 저장이 되게 됩니다. ExecutionContext를 통해 Step간 Data 공유가 가능하며 Job 실패시 ExecutionContext를 통한 마지막 실행 값을 재구성 할 수 있습니다.

### JobRepository
- JobRepository는 위에서 말한 모든 배치 처리 정보를 담고있는 매커니즘입니다. Job이 실행되게 되면 JobRepository에 JobExecution과 StepExecution을 생성하게 되며 JobRepository에서 Execution 정보들을 저장하고 조회하며 사용하게 됩니다.

### JobLauncher
- JobLauncher는 Job과 JobParameters를 사용하여 Job을 실행하는 객체입니다.

### ItemReader
- ItemReader는 Step에서 Item을 읽어오는 인터페이스입니다. ItemReader에 대한 다양한 인터페이스가 존재하며 다양한 방법으로 Item을 읽어 올 수 있습니다.

### ItemWriter
- ItemWriter는 처리 된 Data를 Writer 할 때 사용한다. Writer는 처리 결과물에 따라 Insert가 될 수도 Update가 될 수도 Queue를 사용한다면 Send가 될 수도 있다. Writer 또한 Read와 동일하게 다양한 인터페이스가 존재한다. Writer는 기본적으로 Item을 Chunk로 묶어 처리하고 있습니다.

### ItemProcessor
- Item Processor는 Reader에서 읽어온 Item을 데이터를 처리하는 역할을 하고 있다. Processor는 배치를 처리하는데 필수 요소는 아니며 Reader, Writer, Processor 처리를 분리하여 각각의 역할을 명확하게 구분하고 있습니다.

*****

## Spring Batch 사용하기
Spring Batch에서의 Job은 여러가지 Step의 모음으로 구성되어 있으며 Job은 순차적인 Step을 수행하며 Batch를 수행하게 됩니다. Step은 Tasklet 처리 방식과 Chunk 지향 처리 방식을 지원하고 있습니다.

![img](https://user-images.githubusercontent.com/104426801/171368436-16b3e992-64b3-4cee-a51c-f41b6cc64ccc.png)

## STEP을 구성하는 Tasklet과 Chunk 지향 처리
### Tasklet
- Tasklet은 하나의 메서드로 구성 되어있는 간단한 인터페이스입니다. 이 메서드 는 실패를 알리기 위해 예외를 반환 하거나 throw할 때까지 execute를 반복적으로 호출하게 됩니다 .

![img (1)](https://user-images.githubusercontent.com/104426801/171368767-6cd1f5f1-7264-4ded-b0bf-0f47cc4280ae.png)


- Taslket에서는 @BeforeStep, @AfterStep을 통해 execute 배치 실행 전 후에 Event를 등록하여 실행 시킬 수 있습니다.


### Chunk
- Spring Batch에서의 Chunk란 처리 되는 커밋 row 수를 의미합니다. Batch 처리에서 커밋 되는 row 수라는건 chunk 단위로 Transaction을 수행하기 때문에 실패시 Chunk 단위 만큼 rollback이 되게 됩니다.

- Chunk 지향 처리에서는 다음과 같은 3가지 시나리오로 실행 됩니다

읽기(Read) — Database에서 배치처리를 할 Data를 읽어온다
처리(Processing) — 읽어온 Data를 가공,처리를 한다 (필수사항X)
쓰기(Write) — 가공,처리한 데이터를 Database에 저장한다.

![다운로드](https://user-images.githubusercontent.com/104426801/171369300-1ced0f0a-aca1-4253-8bcc-e8bc9f98598f.png)

cf)
1. Spring Batch에는 다양한 ItemReader와 ItemWriter가 존재합니다. 대용량 배치 처리를 하게 되면 Item을 읽어 올 때 Paging 처리를 하는게 효과적입니다. Spring Batch Reader에서는 이러한 Paging 처리를 지원하고 있습니다. 또한 적절한 Paging처리와 Chunk Size(한번에 처리 될 트랜잭션)를 설정하여 더욱 효과적인 배치 처리를 할 수 있습니다.

한번의 Read 쿼리 수행시 1번의 Transaction을 위해 두 설정의 값을 일치를 시키는게 가장 좋은 성능 향상 방법이며 특별한 이유가 없는 한 Paging Size 와 Chunk Size를 동일하게 설정하는 것을 추천합니다.

2. 페이징 처리 시 각 쿼리에 Offset 과 , Limit를 지정해 주어야 하는데 이는 PageSize를 지정하면 Batch에서 Offset과 Limit를 지정해줍니다. 하지만 페이징 처리를 할 때 마다 새로운 쿼리를 실행하기 때문에 데이터 순서가 보장 될 수 있도록 반드시 Order By를 사용하여야 합니다.

### @JobScope, @StepScope?
Chunk 지향 처리 Example을 확인하면 @JobScope와 @StepScope Annotation을 확인할 수 있습니다.

@JobScope는 Step 선언문에 사용 가능하며 @StepScope는 Step을 구성하는 ItemReader, ItemProcessor, ItemWriter에 사용이 가능합니다.

@JobScope와 @StepScope는 Singleton 패턴이 아닌 Annotation이 명시된 메소드의 실행 시점에 Bean이 생성되게 됩니다. 또한 @JobScope와 @StepScope Bean이 생성 될 때 JobParameter가 생성되기 때문에 JobParameter 사용하기 위해선 반드시 Scope를 지정해주어야 합니다. 이는 LateBinding을 하여 JobParameter를 비즈니스 로직 단계에서 할당하여 보다 유연한 설계를 가능하게 하고 서로 다른 Step이 서로를 침범하지 않고 병렬로 실행되게 하기 위함입니다.


