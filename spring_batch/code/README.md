# Spring Batch 작성 Guide

## .yml
- Batch가 반복실행될 시간 주기 설정
- 초 분 시 일 월 년 순서.    
![photo_2022-06-01_19-13-32](https://user-images.githubusercontent.com/104426801/171381724-f4fa5773-bcd5-4da1-9d58-b7a3a7e0dc5c.jpg)

![image](https://user-images.githubusercontent.com/104426801/171381705-8454b9ba-2087-40c3-b7f9-6d0e8bd18781.png)


## Scheduler.java
![image](https://user-images.githubusercontent.com/104426801/171382472-239e8f31-aadb-430c-a8d0-fc3c915b1007.png)
![photo_2022-06-01_19-16-22](https://user-images.githubusercontent.com/104426801/171382514-f1edca4a-2245-4a5a-8019-845ed707086e.jpg)

- .yml에 등록한 시간파라미터를 사용
- 한 곳에서 시간을 관리하기 위함.

## JobsConfig.java
- job Bean 등록
![image](https://user-images.githubusercontent.com/104426801/171383401-b019f423-ebfa-4af4-86ba-091dc22ceb8a.png)



![image](https://user-images.githubusercontent.com/104426801/171385869-d93152aa-5f2f-474e-a0a2-a73bd7aeb48e.png)


* ChunkSize : 1000 일 경우, page도 1000개 권장.
* 1000건이 끝나고 commit 된다. 1000건 단위(bulk 단위)로 Rollback일어남.

* 세세한 구현체 설정
DB 하나당 sessionFactory, transactionManager 쌍으로 생성해야한다.
프로젝트 내 새로운 DB 추가시, yml추가, dataSource추가, myBatis 추가해야한다. (aspect는 api 프로젝트일때만)


(첨언)
* 보통은 Reader, Writer 만 사용할거임
* 만들어서 돌려보는게 좋다

