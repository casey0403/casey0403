## Kafka란? 
카프카는 대용량의 실시간 로그처리에 특화되어 있는 솔루션이며, 데이터 유실없이 안정적으로 메세지를 전달할 수 있다. 
분산환경에 특화되어 설계되어 있다는 특징이 있으며 다른 메세지 큐(ex.RabbitMQ)보다 성능적으로 뛰어나다고 한다.

### Publisher-Subscriber 모델
발행과 구독 모델을 사용한다(일명 pub-sub모델). 발행과 구독이란 메세지를 특정 수신자에게 다이렉트로 전달하는 시스템이 아니다.  
Publisher는 메세지를 topic을 통해서 카테고리화하고 Subscriber는 그 topic을 구독함으로써 메세지를 읽어올 수 있다.  
Publisher는 topic에 대한 정보만 알고있고, Subscriber도 topic만 바라보기 때문에 발행자와 구독자는 서로 모르는 상태다.   


![image](https://user-images.githubusercontent.com/104426801/179468767-ff96d370-8357-45ff-ae5c-32f1e8b6934f.png)


### topic과 partition
메세지는 topic으로 분류되며, topic은 여러개의 파티션으로 나눠질 수 있다.   
파티션의 자리를 차지하는 한칸은 로그라고 불리고 메세지는 로그에 순차적으로 들어가게 된다. 메세지의 상대적인 위치를 나타내는 것을 offset이라고 한다.


![image](https://user-images.githubusercontent.com/104426801/179468952-8a1d472a-5e94-4e13-8bca-b36d46ec8729.png)

하나의 토픽에 여러개의 파티션을 나눠서 메세지를 쓰는 이유는 대량의 메세지가 같은 토픽으로 쓰여질 때, 파티션이 하나면 순차적으로 append되므로 처리하는데 버거울 수 있다.   
하지만 여러 개의 파티션을 사용 할 경우 메세지나 분산되어 쓰여지기 때문에 처리하는데 있어서 훨씬 빠를 수 있다.   
다만 파티션을 늘릴 경우 메세지가 쓰여지는게 순차적이지 않기 때문에 순서가 중요한 모델에선 적합하지 않을 수 있다.  


### consumer
컨슈머는 영어단어 뜻처럼 소비자의 기능을 한다. 즉 메세지를 소비한다. producer의 존재를 모르지만 특정 토픽을 구독함으로써 스스로 상황에 맞게 메세지를 소비한다.   
소비를 한 표시는 offset의 위치를 통해 기억하고 consumer 서버의 메모리가 부족하다거나 서버가 죽는 등의 일이 발생해도 이전에 소비했던 offset의 위치를 통해 다시 읽어드릴 수 있다. 
그렇기 때문에 매우 안정적이다.  


![image](https://user-images.githubusercontent.com/104426801/179470160-c0b2e932-ab08-4c9d-b32a-f4f7169b5983.png)

(출처)
https://devcheon.tistory.com/73 
https://galid1.tistory.com/793 





