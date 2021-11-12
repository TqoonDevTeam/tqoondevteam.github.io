---
title: "PB 중계 시스템"
description: "문서 설명"
tags: [개발가이드, 템플릿 ]
---

#  PGB DataBase
## TqoonPGB
-   **Payment Gateway Bridge(PGB)를 사용 PG와, 결제 상태를 관리하기 위한 별도 데이터베이스 입니다.**
-   PGB를 사용하는 전 국가 PG 정보와, 결제 상태를 관리합니다.

## PGBPgInfo

-   PGB를 사용하는 모든 국가의 PG사 정보 테이블입니다.

| Column | DataType | description  |
| --- | --- | --- |
| id | int | PK |
| nationCode | varchar(10) | 국가 |
| dbType | varchar(10) | AD/OM |
| joinerId | int | 사용 이용사 |
| key | varchar(max) | PG key |
| pgType | varchar(100) |   |
| currency | varchar(10) |   |
| state | varchar(10) |   |

## PGBTransaction

-   결제 요청 : STANDBY
-   결제 성공 : PAID
-   결제 취소 : CANCEL

-   PG사와의 결제 상태 정보를 관리하는 테이블입니다.

| Column | DataType | description  |
| --- | --- | --- |
| id | int |   |
| orderId | int |   |
| pgbPGInfoId | int | PGBPGinfo Id |
| pgbTransactionId | varchar(100) |   |
| state | int |   |
| writeDate | datetime |   |
| lasModifedDate | datetime |   |

-   pgTransactionId는 지불이 완료되면 Insert 되며, pgTransactionId로 결제 취소를 시도합니다.