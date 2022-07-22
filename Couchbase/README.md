# Couchbase

## RDBMS_Normal SQL
* DB1
  - schema1 
    + table1 
      + data1
      + data2  
    + table2 
  - schema2 
    + table3 
    + table4 
* DB2
  - schema1
    + table1
    + table2
  - schema2
    + table3
    + table4
    

## Couchbase_NoSQL
* Couchbase1
  - bucket1
    + document1
    + document2
  - bucket2
    + document1
    + document2

* Couchbase2
  - bucket1
    + document1
    + document2
  - bucket2
    + document1
    + document2

쉽게 이해하자면
DB schema == Couchbase bukcet
DB data == Couchbase document

DB data 저장소. 
Couchbase 적재적소하게 필요한 data 저장소.

(ex1)
DB
local DB - assets Schema - **asset Table** - asset data

Couchbase
local Couchbase - **local-asset Bucket** - asset document

(ex2)
DB
local DB - coin Schema - **market_list Table** - market_list data
local DB - coin Schema - **market Table** - market data
local DB - coin Schema - **coin Table** - coin data
local DB - wallet Schema - **coin_detail Table** - coin_detail data
![image](https://user-images.githubusercontent.com/104426801/180435566-5d1c5f59-29aa-40a6-8f70-55a05461bf0c.png)



Couchbase
local Couchbase - **local-market-coin Bucket** - asset document



1. ConnectionPool DB보다 훨씬 큼.
2. 데이터 무결성을 지킬 수 있음.
  - 특히 asset. couchbase에서 먼저 변경. 매도, 매수가 일어나는 중 매도, 매수가 일어나는 것을 방지할 수 있음.(더 큰 에러 방지)
