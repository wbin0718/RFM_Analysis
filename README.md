# RFM 분석 프로젝트

![image](https://github.com/wbin0718/RFM_Analysis/assets/104637982/4ae36a2f-7bc4-4721-b5a6-fe6be0d685f3)

* 분석 목적: RFM 고객 세분화를 적용하여 고객을 4개의 등급으로 나누고 각 등급이 매출 기여비율 확인
* 분석 데이터: [캐글US E-Commerce Records 2020 데이터](https://www.kaggle.com/datasets/ammaraahmad/us-ecommerce-record-2020)

## Recency Score

* 2020-01-01 ~ 2020-12-30 기간의 데이터
* 기준을 2020-01-01 및 2020-12-30으로 정할 수 있지만 Frequency_Score, Monetary_Score와 높을 수록 높은 값을 갖게 하기 위해서 2020-01-01 기준
* 빅쿼리를 통해 각 고객의 최근 일자를 구하고 기준 날짜와 day를 기준으로 차이를 계산
* 4분위수를 활용하여 구분을 하고 4개의 등급으로 나눔

## Frequency Score

* Customer_ID와 Order_ID를 활용해서 고객마다 구매 빈도 계산
* Recency_Score, Monetary_Score와 달리 discrete 특징을 가짐. 4분위수를 활용할 때 같은 score를 가지지만 다른 등급값을 갖는 문제점 발생
* Unique한 값은 1~8까지 있어 (1,2), (3,4), (5,6), (7,8)로 기준을 정하고 차례대로 (4,3,2,1) 등급 부여

## Monetary Score
* Customer_ID와 Sales를 활용해서 고객이 구매한 총 금액을 계산
* 4분위수를 통해 기준을 정하고 4개의 등급으로 나눔

## Weight 계산

* 단순히 각 지표의 등급을 활용하는 것이 아닌 가중치의 합을 통해 고객의 등급을 결정함.
* R, F, M 모두 0부터 1사이의 값을 전체 탐색하여 분산이 가장 큰 가중치 선택
* 따라서 R=0.2, F=0, M=0.8
* 가중치를 적용하고 고객의 등급을 결정

## 각 등급별 매출 비교

* 아래 표를 살펴보면 1등급의 고객이 전체 매출의 80%를 책임지는 결과가 도출됨.
![image](https://github.com/wbin0718/RFM_Analysis/assets/104637982/10d5168b-1098-4dc6-9ee0-0a13a6dfef4f)
* 파레토 법칙이 맞는건가?
