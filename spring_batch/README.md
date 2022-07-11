# Spring Batch


[스프링 배치 ]
![spring-batch-architecture](https://user-images.githubusercontent.com/104426801/171371382-0232069a-76e0-4c79-a742-34c0df1a0140.jpg)
- 노란색은 스케줄러 또는 데이터베이스와 같은 외부 애플리케이션을 나타냅니다. 스케줄링이라는 점은 스프링 배치와 별도로 고려되어야한다는 점에 유의하는 것이 중요합니다.
- 빨간색으로 표시한 요소들은 어플리케이션 서비스를 나타냅니다. 대부분의 서비스들은 스프링 배치에서 제공하고 있지만, 원하는 구조가 있다면 입맛에 맞게 디자인 할 수 있습니다.
- 초록색으로 표시된 요소들은 개발자가 구성해야하는 것들을 나타냅니다. 예를 들어 일정한 주기대로 작업이 시작되도록 설정하거나, 작업을 실행하는 방법 등을 구현해야합니다.

1. Run Tier: 어플리케이션의 예약 및 시작과 관련이 있는 계층입니다. 배치 작업의 시간 기반 및 상호 의존적인 스케줄링을 제공할뿐만 아니라 병렬 처리 기능을 제공합니다.
2. Job Tier: 배치 작업의 전체 실행을 담당합니다. 배치 단계를 순차적으로 실행하여 모든 단계가 올바른 상태에 있고 모든 적절한 정책이 시행 되도록합니다.
3. Application Tier: 프로그램을 실행하는 데 필요한 구성 요소가 포함되어 있습니다. 이 계층에는 요구된 배치의 기능을 처리하고 Tasklet 실행에 대한 정책을 시행하는 특별한 Tasklet이 포함됩니다.
4. Data Tier: 데이터베이스, 파일 또는 대기열을 포함 할 수있는 물리적 데이터 소스와의 연결을 제공합니다.

## Batch 란?
업무 혹은 IT에서 배치라함은 우리말로 일괄 처리(batch processing)의 batch를 말합니다. 배치는 사용자의 개입 없이 실행을 스케줄링할 수 있는 작업(job)을 의미하며. 컴퓨터 프로그램 흐름에 따라 순차적으로 자료를 처리하는 방식입니다.


'배치' 이용의 장점
1. 배치 프로그램을 이용하면 사용자가 적을때 컴퓨터 자원을 이용할 수 있습니다.  
2. 배치 실행 시간을 지정할 수 있어 컴퓨터 리소스가 덜 사용되는 시간대에 동작하게 함으로써 전체적으로 리소스의 유휴를 피할수 있습니다.  
3. 결과적으로 컴퓨터 자원 이용률과 효율을 높여 비용 낭비를 줄여줍니다.
 

## Spring Batch란?
- Spring Batch는 로깅/추적, 트랜잭션 관리, 작업 처리 통계, 작업 재시작, 건너뛰기, 리소스 관리 등 대용량 레코드 처리에 필수적인 기능을 제공합니다. 또한 최적화 및 파티셔닝 기술을 통해 대용량 및 고성능 배치 작업을 가능하게 하는 고급 기술 서비스 및 기능을 제공합니다.

- Spring Batch에서 배치가 실패하여 작업 재시작을 하게 된다면 처음부터가 아닌 실패한 지점부터 실행을 하게 됩니다.

-또한 중복 실행을 막기 위해 성공한 이력이 있는 Batch는 동일한 Parameters로 실행 시 Exception이 발생하게 됩니다.

## 이런 일괄처리는 어떠한 경우에 필요할까요?
배치 프로세싱은 일괄처리라는 뜻을 가지고 있습니다. 일괄처리의 의미는 일련의 작업을 정해진 로직으로 수행하는 것이라고 할 수 있습니다.

1. 대용량의 비즈니스 데이터를 복잡한 작업으로 처리해야하는 경우
2. 특정한 시점에 스케쥴러를 통해 자동화된 작업이 필요한 경우 (ex. 푸시알림, 월 별 리포트)
3. 대용량 데이터의 포맷을 변경, 유효성 검사 등의 작업을 트랜잭션 안에서 처리 후 기록해야하는 경우

예를 들어, 전체 금액이 10000원 이상인 회원들에게 1,000원씩 캐시백을 줄 때 

위와 같은 경우에 배치 어플리케이션을 작성하여 처리하게됩니다. 실제로 엔터프라이즈 환경에서는 정말 다양 종류의 작업들을 배치를 이용하여 처리하고 있습니다.
스프링 팀은 위와 같은 요구사항을 처리해줄 수 있는 배치와 관련된 어플리케이션 제작의 편의를 위해서 스프링 배치 프레임워크를 만들어 표준화하게 되었습니다.

*****

## Spring Batch 용어
### Job
- *최상단*
- Job은 배치처리 과정을 하나의 단위로 만들어 놓은 객체입니다. 또한 배치처리 과정에 있어 전체 계층 최상단에 위치하고 있습니다.
- 스프링 배치의 Job은 단순하게 표현하면 Step 인스턴스의 컨테이너입니다. 비즈니스로직을 가지고 있는 여러 Step을 결합하고 재시작 가능성과 같이 모든 Step에 전역 속성을 설정할 수 있습니다.
- 
### JobRunner
외부 요청에 의해 작업 실행을 담당하는 클래스입니다. 예를 들어, 쉘 스크립트와 같은 다양한 외부 트리거로 메소드 호출을 할 수 있는 등의 여러 구현 방법들이 있습니다. JobLauncher의 인스턴스화를 수행합니다.

### JobLocator
파라미터로 전달된 작업에 대한 구현 계획(작업 스크립트)과 같은 설정 정보를 가져 오는 책임이 있는 클래스입니다. JobRunner와 함께 작동합니다.

### JobLauncher
- JobLauncher는 Job과 JobParameters를 사용하여 Job을 실행하는 객체입니다.
- 작업의 시작과 실제 실행을 관리하는 인터페이스로 JobRunner에 의해 인스턴스화되고, JobParameters와 함께 배치를 실행하는 주체입니다.

### JobInstance
- *실행단위*
- JobInstance는 Job의 실행의 단위를 나타냅니다. 
- Job을 실행시키게 되면 하나의 JobInstance가 생성되게 됩니다. 예를들어 1월 1일 실행, 1월 2일 실행을 하게 되면 각각의 JobInstance가 생성되며 1월 1일 실행한 JobInstance가 실패하여 다시 실행을 시키더라도 이 JobInstance는 1월 1일에 대한 데이터만 처리하게 됩니다.

![job-instance](https://user-images.githubusercontent.com/104426801/171372151-01d3a596-30f1-4821-8406-69f4edc5b2d4.jpg)


### JobParameters
- *구분자*
- JobInstance는 Job의 실행 단위라고 했습니다. 그렇다면 JonInstance는 어떻게구별 할까요? 이는 바로 JobParameters 객체로 구분하게 됩니다. JobParameters는 JobInstance 구별 외에도 개발자 JobInstacne에 전달되는 매개변수 역할도 하고 있습니다.
- 스프링 배치에서 JobParameters를 정상적으로 사용하기 위해서 JobScope나 StepScope를 함께 사용해주셔야 합니다. 그 이유는 JobParameters는 Scope Bean의 생성 시점에만 함께 생성될 수 있기 때문입니다.
- JobParameters는 배치 Job이 실행될 때 필요한 파라미터 셋을 가지고 있는 객체입니다. 또 JobParameters와 JobInstance는 1:1 관계이기 때문에 JobParameters는 JobInstance를 구분하는 기준이 되기도 합니다.

- 또한 JobParameters는 String, Double, Long, Date 4가지 형식만을 지원하고 있습니다.

### JobExecution
- *실행시도*
- JobExecution은 JobInstance에 대한 실행 시도에 대한 객체입니다. 1월 1일에 실행한 JobInstacne가 실패하여 재실행을 하여도 동일한 JobInstance를 실행시키지만 이 2번에 실행에 대한 JobExecution은 개별로 생기게 됩니다. JobExecution는 이러한 JobInstance 실행에 대한 상태,시작시간, 종료시간, 생성시간 등의 정보를 담고 있습니다.

### Step
- Job 1 : Step *
- Step은 Job의 배치처리를 정의하고 순차적인 단계를 캡슐화 합니다. Job은 최소한 1개 이상의 Step을 가져야 하며 Job의 실제 일괄 처리를 제어하는 모든 정보가 들어있습니다.

### StepExecution
- StepExecution은 JobExecution과 동일하게 Step 실행 시도에 대한 객체를 나타냅니다. 하지만 Job이 여러개의 Step으로 구성되어 있을 경우 이전 단계의 Step이 실패하게 되면 다음 단계가 실행되지 않음으로 실패 이후 StepExecution은 생성되지 않습니다. StepExecution 또한 JobExecution과 동일하게 실제 시작이 될 때만 생성됩니다. StepExecution에는 JobExecution에 저장되는 정보 외에 read 수, write 수, commit 수, skip 수, 각 Step에 대해서 개발자가 지정한 데이터 등의 정보들도 저장이 됩니다.


### ExecutionContext
- *데이터 저장소*
- ExecutionContext란 Job에서 데이터를 공유 할 수 있는 데이터 저장소입니다. 
- Spring Batch에서 제공하느 ExecutionContext는 JobExecutionContext, StepExecutionContext 2가지 종류가 있으나 이 두가지는 지정되는 범위가 다릅니다. JobExecutionContext의 경우 Commit 시점에 저장되는 반면 StepExecutionContext는 실행 사이에 저장이 되게 됩니다. ExecutionContext를 통해 Step간 Data 공유가 가능하며 Job 실패시 ExecutionContext를 통한 마지막 실행 값을 재구성 할 수 있습니다.

### JobRepository
- 배치 처리 과정 중 프레임워크에서 사용하는 메타데이터 정보를 액세스하는 Facade 클래스입니다.
- JobRepository는 위에서 말한 모든 배치 처리 정보를 담고있는 매커니즘입니다. Job이 실행되게 되면 JobRepository에 JobExecution과 StepExecution을 생성하게 되며 JobRepository에서 Execution 정보들을 저장하고 조회하며 사용하게 됩니다.
- 테이블의 정보들을 저장하고 관리합니다.

### ItemReader
- ItemReader는 Step에서 Item을 읽어오는 인터페이스입니다. ItemReader에 대한 다양한 인터페이스가 존재하며 다양한 방법으로 Item을 읽어 올 수 있습니다.
- 일반적으로 청크 구조에서 사용되는 컴포넌트로 배치 작업에서 모든 데이터에 대한 처리가 될 때까지 DB, File 등의 소스에서 반복적으로 읽는데 사용하는 인터페이스입니다. 프레임워크에서 Reader 셋을 제공하지만 필요한 경우 개발자가 직접 개발할 수도 있습니다.

### ItemWriter
- ItemWriter는 처리 된 Data를 Writer 할 때 사용한다. Writer는 처리 결과물에 따라 Insert가 될 수도 Update가 될 수도 Queue를 사용한다면 Send가 될 수도 있다. Writer 또한 Read와 동일하게 다양한 인터페이스가 존재한다. Writer는 기본적으로 Item을 Chunk로 묶어 처리하고 있습니다.
- Writer 또한 청크 구조에서 사용되는 컴포넌트로 배치에서 데이터를 DB, File 등에 저장하기 위한 인터페이스입니다. 동일하게 프레임워크에서 기본적으로 제공하지만 개발자가 직접 개발할 수도 있습니다.

### ItemProcessor
- Item Processor는 Reader에서 읽어온 Item을 데이터를 처리하는 역할을 하고 있다. Processor는 배치를 처리하는데 필수 요소는 아니며 Reader, Writer, Processor 처리를 분리하여 각각의 역할을 명확하게 구분하고 있습니다.

Reader, Processor, Writer로 분리된 구조는 비즈니스 로직을 분리하기에 용이하고, Reader와 Writer 데이터 타입이 다른 경우 어뎁터의 역할을 할 수도 있습니다.

*****

## Spring Batch 사용하기
Spring Batch에서의 Job은 여러가지 Step의 모음으로 구성되어 있으며 Job은 순차적인 Step을 수행하며 Batch를 수행하게 됩니다. Step은 Tasklet 처리 방식과 Chunk 지향 처리 방식을 지원하고 있습니다.

![img](https://user-images.githubusercontent.com/104426801/171368436-16b3e992-64b3-4cee-a51c-f41b6cc64ccc.png)

## STEP을 구성하는 Tasklet과 Chunk 지향 처리
### Tasklet
- Tasklet은 하나의 메서드로 구성 되어있는 간단한 인터페이스입니다. 이 메서드 는 실패를 알리기 위해 예외를 반환 하거나 throw할 때까지 execute를 반복적으로 호출하게 됩니다 .
- 배치의 특정 작업을 개발하기 위해 Step의 기본 단위를 만들 수 있는 클래스입니다.

![img (1)](https://user-images.githubusercontent.com/104426801/171368767-6cd1f5f1-7264-4ded-b0bf-0f47cc4280ae.png)


- Taslket에서는 @BeforeStep, @AfterStep을 통해 execute 배치 실행 전 후에 Event를 등록하여 실행 시킬 수 있습니다.


### Chunk
- Spring Batch에서의 Chunk란 처리 되는 커밋 row 수를 의미합니다. Batch 처리에서 커밋 되는 row 수라는건 chunk 단위로 Transaction을 수행하기 때문에 실패시 Chunk 단위 만큼 rollback이 되게 됩니다.

- Chunk 지향 처리에서는 다음과 같은 3가지 시나리오로 실행 됩니다

읽기(Read) — Database에서 배치처리를 할 Data를 읽어온다
처리(Processing) — 읽어온 Data를 가공,처리를 한다 (필수사항X)
쓰기(Write) — 가공,처리한 데이터를 Database에 저장한다.

![다운로드](https://user-images.githubusercontent.com/104426801/171369300-1ced0f0a-aca1-4253-8bcc-e8bc9f98598f.png)

- 일반적으로 스프링 배치는 대용량 데이터를 다루는 경우가 많기 때문에 Tasklet보다 상대적으로 트랜잭션의 단위를 짧게 하여 처리할 수 있는 Reader, Proccessor, Writer를 이용한 Chunk 지향 프로세싱을 이용합니다.

### Job, Step, Tasklet 정리
![spring-batch-job](https://user-images.githubusercontent.com/104426801/171375330-5fc8a769-d6d0-495c-999a-b284e70c30cc.jpg)
- Job: 배치 처리 과정을 하나의 단위로 만들어 표현한 객체이고 여러 Step 인스턴스를 포함하는 컨테이너
- Step: Step은 실직적인 배치 처리를 정의하고 제어 하는데 필요한 모든 정보가 있는 도메인 객체
- Tasklet: Step안에서 수행될 비즈니스 로직 전략의 인터페이스


cf)
1. Spring Batch에는 다양한 ItemReader와 ItemWriter가 존재합니다. 대용량 배치 처리를 하게 되면 Item을 읽어 올 때 Paging 처리를 하는게 효과적입니다. Spring Batch Reader에서는 이러한 Paging 처리를 지원하고 있습니다. 또한 적절한 Paging처리와 Chunk Size(한번에 처리 될 트랜잭션)를 설정하여 더욱 효과적인 배치 처리를 할 수 있습니다.

한번의 Read 쿼리 수행시 1번의 Transaction을 위해 두 설정의 값을 일치를 시키는게 가장 좋은 성능 향상 방법이며 특별한 이유가 없는 한 Paging Size 와 Chunk Size를 동일하게 설정하는 것을 추천합니다.

2. 페이징 처리 시 각 쿼리에 Offset 과 , Limit를 지정해 주어야 하는데 이는 PageSize를 지정하면 Batch에서 Offset과 Limit를 지정해줍니다. 하지만 페이징 처리를 할 때 마다 새로운 쿼리를 실행하기 때문에 데이터 순서가 보장 될 수 있도록 반드시 Order By를 사용하여야 합니다.

3. @JobScope, @StepScope?
Chunk 지향 처리 Example을 확인하면 @JobScope와 @StepScope Annotation을 확인할 수 있습니다.

@JobScope는 Step 선언문에 사용 가능하며 @StepScope는 Step을 구성하는 ItemReader, ItemProcessor, ItemWriter에 사용이 가능합니다.

@JobScope와 @StepScope는 Singleton 패턴이 아닌 Annotation이 명시된 메소드의 실행 시점에 Bean이 생성되게 됩니다. 또한 @JobScope와 @StepScope Bean이 생성 될 때 JobParameter가 생성되기 때문에 JobParameter 사용하기 위해선 반드시 Scope를 지정해주어야 합니다. 이는 LateBinding을 하여 JobParameter를 비즈니스 로직 단계에서 할당하여 보다 유연한 설계를 가능하게 하고 서로 다른 Step이 서로를 침범하지 않고 병렬로 실행되게 하기 위함입니다.

*****
## Spring Meta Table
Spring Batch에는 6개의 Meta Table과 3개의 Sequence Table이 존재합니다. 이는 Spring BatchJob이 실행 될 때마다 실행된 Job에 대한 다양한 정보들이 저장되게 됩니다.

일반적으로는 해당 Meta Table이 없이는 Spring Batch Framework를 실행시킬 수 없으나 이는 필요에 따라 커스터마이징을 통해 Meta Table이 없이도 실행되게 만들 수 있습니다
(하지만 Spirng Batch에서 해당 Table이 없이 실행되지 않게 했다는 건 그만큼 중요한 정보들이 저장 된다는 것이겠죠?)

[스프링 배치 메타 테이블 이미지1]
![image](https://user-images.githubusercontent.com/104426801/171370699-ccb0fec0-9c9f-452f-84b7-ca8eceae8564.png)

[스프링 배치 메타 테이블 이미지2]
![spring-batch-meta-tables](https://user-images.githubusercontent.com/104426801/171374925-30616f26-6894-4f51-bc9f-cfc96cc87fbb.jpg)


### SEQUENCE
BATCH_JOB_INSTANCE, BATCH_JOB_EXECUTION및 BATCH_STEP_EXECUTION의 Primary Key는 시퀀스에 의해 생성됩니다.

*****

### 스프링 배치 탄생 배경
웹 기반의 MSA에 집중을 하고 있던 Spring source(현 Pivotal)은 Java 기반의 일괄처리 프레임워크 제작에는 집중하지 못하였습니다. 그래서 많은 기업들이 일괄처리를 하기 위해 자체 사내 솔루션을 개발하는 경우가 많았습니다.

하지만 점차 일괄처리에 대한 표준 프레임워크를 만들어달라는 요구가 많아지면서 Pivotal은 독점적으로 일괄처리 프레임워크를 가지고 있던 기업인 Accenture와 협력하여 Spring Batch 프로젝트를 시작하게 되었습니다.

### 배치의 일반적인 사용 시나리오
![job-instance](https://user-images.githubusercontent.com/104426801/171374223-5627d5d0-2188-49dd-91b4-30583ed9ed0b.jpg)
- 데이터베이스, 파일 또는 큐에서 데이터 읽기
- 데이터를 정의한 방식으로 처리
- 처리된 데이터를 데이터 쓰기  
스프링 배치는 위와 같은 방식으로 사용자와의 상호작용 없이 반복적으로 데이터를 트랜잭션 단위로 처리할 수 있도록 구현되어 있고, 개발자는 데이터 처리에 대한 비즈니스 로직에만 집중하여 배치 프로세스를 작성할 수 있습니다.

#### 스프링 배치가 제공할 수 있는 비즈니스 시나리오
1. 주기적인 배치 프로세스
2. 동시적인 배치 프로세스: 작업의 병렬 처리
3. 단계별 엔터프라이즈 메시지 기반 처리
4. 대규모 작업에 대한 병렬 배치 프로세스
5. 실패 후 수동 또는 예약 된 재시작
6. 단계별 순차 처리
7. 부분 처리: 레코드 건너 뛰기 (예: 롤백 시)
8. 배치 작업 처리의 단위가 작은 경우, 기존 저장 프로시저/스크립트가 있는 경우 전체 배치에 대한 트랜잭션 처리
스프링 배치 프레임워크는 위와 같이 다양한 비즈니스 시나리오를 처리할 수 있도록 설계되어 있습니다.

### 스프링 배치 계층 구조
[spring batch structure]
![spring-batch-structure](https://user-images.githubusercontent.com/104426801/171374712-832b5bd0-5aa6-4759-a4cc-7c9704413ba7.jpg)

스프링 배치 프레임워크는 확장성과 최종사용자를 염두해두고 설계되었기 때문에 위와 같이 Application, Batch Core 그리고 Batch Infrastructure로 설계되었습니다.

- Application: 개발자가 작성한 모든 배치 작업과 사용자 정의 코드 포함
- Batch Core: 배치 작업을 시작하고 제어하는데 필요한 핵심 런타임 클래스 포함 (JobLauncher, Job, Step)
- Batch Infrastructure: 개발자와 어플리케이션에서 사용하는 일반적인 Reader와 Writer 그리고 RetryTemplate과 같은 서비스를 포함
스프링 배치는 계층 구조가 위와 같이 설계되어 있기 때문에 개발자는 Application 계층의 비즈니스 로직에 집중할 수 있고, 배치의 동작과 관려된 것은 Batch Core에 있는 클래스들을 이용하여 제어할 수 있습니다.




*출처 및 참고*
https://khj93.tistory.com/entry/Spring-Batch%EB%9E%80-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B3%A0-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0
https://deeplify.dev/back-end/spring/batch-architecture-and-components


   
https://jojoldu.tistory.com/328?category=902551

