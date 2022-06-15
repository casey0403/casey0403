# SELECT 함수

## JOIN ( SELECT _____   )

1) JOIN할 테이블의 전체 데이터를 조회하는 경우 
JOIN table_name ON ~~
2) JOIN할 테이블 중 원하는 테이터를 테이블로 만들어서 조회하는 경우
JOIN ( 
  SELECT column_name
  FROM table_name
  WHERE 조건
) ON ~~~

## group by

## having


## ROW_NUMBER() 랭킹 매기기 

ROW_NUMBER() OVER( 


)


## datediff( date1, date2)
date1, date2 차이값
(ex) 2022-06-01, 2022-05-28 => -3

