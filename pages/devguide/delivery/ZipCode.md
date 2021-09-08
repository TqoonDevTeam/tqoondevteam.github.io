---
title: "배송-우편코드"
description: ""
tags: [개발가이드, 우편코드]
history:
  - version: '1.0'
    date: '2021-09-07'
    user: '권예은'
    desc: '초안'
---

## Quick Start

1\. 티쿤 2.0 우편코드 검색 기능

2\. 우편코드 관리 테이블 tblzipCode

3\. 신규 우편 코드 등록 시 고려 사항

## 우편 코드 

우편 코드는 tblzipCode에서 관리되고 있으며, 테이블이 일본 국가 기준으로 구성 되있습니다.  tqoon2.0에서 우편 코드로 도, 시, 현 자동으로 찾을 수 있고, 도, 시 , 현 검색으로 우편코드를 찾을 수 있습니다.

<br/>

1\. 우편 코드를 직접 치는 경우, 도, 시, 현을 자동으로 찾아 도시 이름에 자동 추가

2\. 도, 시 , 현 검색으로 우편코드 찾기



## 우편 코드 테이블

\- 우편코드는 tblzipCode 테이블에서 관리되고 있고, 일본향 기준으로 구성돼있습니다..

\- 일본은 히나가라와, 가타카나를 사용하고 있어 strKata~, skrHan~으로 구성되어 있고, 검색은 strHan~ 컬럼을 사용합니다.

\- Tqoon2.0에서는 도 >시 > 현 (Ex 경기도 평택시 XX동) 으로 3가지 컬럼이 표시 가능합니다. 


<br/>

<table style="border-collapse: collapse; width: 100%; height: 349px;" data-ke-align="alignLeft" data-ke-style="style12">
    <tbody>
        <tr style="height: 19px;">
            <td style="width: 100%; height: 19px;" colspan="5">우편코드,(tblZipCode)</td>
        </tr>
        <tr style="height: 19px;">
            <td style="width: 18.4468%; height: 19px;">컬럼명</td>
            <td style="width: 23.801%; height: 19px;">속성명</td>
            <td style="width: 14.8806%; height: 19px;">데이터타입</td>
            <td style="width: 36.6507%; height: 19px;">비고</td>
            <td style="width: 6.22087%; height: 19px; text-align: center;">KEY</td>
        </tr>
        <tr style="height: 19px;">
            <td style="width: 18.4468%; height: 19px;">intZipCodeNum&nbsp;</td>
            <td style="width: 23.801%; height: 19px;"><span style="color: #676a6d;">id</span></td>
            <td style="width: 14.8806%; height: 19px;">&nbsp;</td>
            <td style="width: 36.6507%; height: 19px;">&nbsp;</td>
            <td style="width: 6.22087%; height: 19px; text-align: center;">PK</td>
        </tr>
        <tr style="height: 19px;">
            <td style="width: 18.4468%; height: 19px;">strPostCode1&nbsp;</td>
            <td style="width: 23.801%; height: 19px;">우편 코드</td>
            <td style="width: 14.8806%; height: 19px;">nvarchar(10)</td>
            <td style="width: 36.6507%; height: 19px;">우편 코드 앞자리</td>
            <td style="width: 6.22087%; height: 19px; text-align: center;">&nbsp;</td>
        </tr>
        <tr style="height: 19px;">
            <td style="width: 18.4468%; height: 19px;">strPostCode2&nbsp;</td>
            <td style="width: 23.801%; height: 19px;">우편 코드</td>
            <td style="width: 14.8806%; height: 19px;">nvarchar(10)</td>
            <td style="width: 36.6507%; height: 19px;">우편 코드 뒷자리(없으면 생략가능)</td>
            <td style="width: 6.22087%; height: 19px; text-align: center;">&nbsp;</td>
        </tr>
        <tr style="height: 19px;">
            <td style="width: 18.4468%; height: 19px;">strKataDo&nbsp;</td>
            <td style="width: 23.801%; height: 19px;">도</td>
            <td style="width: 14.8806%; height: 19px;">nvarchar(100)</td>
            <td style="width: 36.6507%; height: 19px;">일본 지역 구분(도&gt;시&gt;현)</td>
            <td style="width: 6.22087%; height: 19px; text-align: center;">&nbsp;</td>
        </tr>
        <tr style="height: 19px;">
            <td style="width: 18.4468%; height: 19px;">strKataSi&nbsp;</td>
            <td style="width: 23.801%; height: 19px;">시</td>
            <td style="width: 14.8806%; height: 19px;">nvarchar(300)</td>
            <td style="width: 36.6507%; height: 19px;">&nbsp;</td>
            <td style="width: 6.22087%; height: 19px; text-align: center;">&nbsp;</td>
        </tr>
        <tr style="height: 25px;">
            <td style="width: 18.4468%; height: 25px;">strKataHyun&nbsp;</td>
            <td style="width: 23.801%; height: 25px;">현</td>
            <td style="width: 14.8806%; height: 25px;">nvarchar(500)</td>
            <td style="width: 36.6507%; height: 25px;">&nbsp;</td>
            <td style="width: 6.22087%; height: 25px; text-align: center;">&nbsp;</td>
        </tr>
        <tr style="height: 19px;">
            <td style="width: 18.4468%; height: 19px;">strHanDo&nbsp;</td>
            <td style="width: 23.801%; height: 19px;">도</td>
            <td style="width: 14.8806%; height: 19px;">nvarchar(100)</td>
            <td style="width: 36.6507%; height: 19px;">일본 지역 구분(가타카나)</td>
            <td style="width: 6.22087%; height: 19px; text-align: center;">&nbsp;</td>
        </tr>
        <tr style="height: 19px;">
            <td style="width: 18.4468%; height: 19px;">strHanSi&nbsp;</td>
            <td style="width: 23.801%; height: 19px;">시</td>
            <td style="width: 14.8806%; height: 19px;">nvarchar(300)</td>
            <td style="width: 36.6507%; height: 19px;">&nbsp;</td>
            <td style="width: 6.22087%; height: 19px; text-align: center;">&nbsp;</td>
        </tr>
        <tr style="height: 19px;">
            <td style="width: 18.4468%; height: 19px;">strHanHyun&nbsp;</td>
            <td style="width: 23.801%; height: 19px;">현</td>
            <td style="width: 14.8806%; height: 19px;">nvarchar(500)</td>
            <td style="width: 36.6507%; height: 19px;">&nbsp;</td>
            <td style="width: 6.22087%; height: 19px; text-align: center;">&nbsp;</td>
        </tr>
        <tr style="height: 19px;">
            <td style="width: 18.4468%; height: 19px;">intManPaymentBan&nbsp;</td>
            <td style="width: 23.801%; height: 19px;">대인가능여부</td>
            <td style="width: 14.8806%; height: 19px;">int</td>
            <td style="width: 36.6507%; height: 19px;">&nbsp;</td>
            <td style="width: 6.22087%; height: 19px; text-align: center;">&nbsp;</td>
        </tr>
        <tr style="height: 19px;">
            <td style="width: 18.4468%; height: 19px;">intDeliveryTimeBan&nbsp;</td>
            <td style="width: 23.801%; height: 19px;">시간지정여부</td>
            <td style="width: 14.8806%; height: 19px;">int</td>
            <td style="width: 36.6507%; height: 19px;">&nbsp;</td>
            <td style="width: 6.22087%; height: 19px; text-align: center;">&nbsp;</td>
        </tr>
        <tr style="height: 19px;">
            <td style="width: 18.4468%; height: 19px;">intDeliveryAmtAdd&nbsp;</td>
            <td style="width: 23.801%; height: 19px;">배송추가금액</td>
            <td style="width: 14.8806%; height: 19px;">int</td>
            <td style="width: 36.6507%; height: 19px;">&nbsp;</td>
            <td style="width: 6.22087%; height: 19px; text-align: center;">&nbsp;</td>
        </tr>
        <tr style="height: 19px;">
            <td style="width: 18.4468%; height: 19px;">intZipCodeArea&nbsp;</td>
            <td style="width: 23.801%; height: 19px;">지역구분코드</td>
            <td style="width: 14.8806%; height: 19px;">int</td>
            <td style="width: 36.6507%; height: 19px;">지역별 요금 구간을 다르게 설정하기 위함</td>
            <td style="width: 6.22087%; height: 19px; text-align: center;">FK</td>
        </tr>
        <tr style="height: 39px;">
            <td style="width: 18.4468%; height: 39px;">strZipcodeSpecificAreaCode&nbsp;</td>
            <td style="width: 23.801%; height: 39px;">지역구분코드정보</td>
            <td style="width: 14.8806%; height: 39px;">varchar(50)</td>
            <td style="width: 36.6507%; height: 39px;">&nbsp;</td>
            <td style="width: 6.22087%; height: 39px; text-align: center;">FK</td>
        </tr>
        <tr style="height: 19px;">
            <td style="width: 18.4468%; height: 19px;">lastMileDeliveryPriceId</td>
            <td style="width: 23.801%; height: 19px;">&nbsp;</td>
            <td style="width: 14.8806%; height: 19px;">int</td>
            <td style="width: 36.6507%; height: 19px;">&nbsp;</td>
            <td style="width: 6.22087%; height: 19px; text-align: center;">&nbsp;</td>
        </tr>
    </tbody>
</table>

## 신규 우편 코드 등록 시 고려 사항
​
### 1\. 티쿤 2.0 우편 코드 포맷 수정
​
\- 각 국가별로 우편 코드 포맷이 다릅니다. 국가별에 맞는 우편 코드 포맷으로 수정해야합니다.
​
```
InputFormat.js
ZipCodeSearch-locale.js
OrderShippingAddress-locale.js
```
​
### 2\. Libraries 주소 표기 형식 검색
​
\- 국가마다 주소 표기 형식이 다릅니다. (Ex) strPostCod1만 쓰는 경우, strPostCode1, strPostCode 둘다 쓰는 경우)
​
#### 2\. 1 ZipcodeSearchService
​
```
 public IEnumerable<string> FindSpecificAreaZipcodeListByHyun(string postCode, string siteNationCode = "")
   {
            if (siteNationCode.ToUpper() == "US") return CODJ.Query(ZipCodeQuery.SearchListByPostCode1(postCode)).Select(t => t.USAFullAddress);
            if (siteNationCode.ToUpper() == "ID" || siteNationCode.ToUpper() == "BR") return CODJ.Query(ZipCodeQuery.SearchListByPostCode1(postCode)).Select(t => t.FullAddress);
            return CODJ.Query(ZipCodeQuery.SearchListByPostCode(postCode)).Select(t => t.FullAddress);
    }
```
​
### 3\. 지역 구분 코드 정보
​
\- 우편코드 등록시 intZipCodeArea 컬럼을 확인하셔야 합니다.
​
\- 해당 컬럼은 지역별 요금 구간을 다르게 설정하기 위한 컬럼으로, 배송 요금표에 사용됩니다.

\- 자세한 내용은 배송 요금표 가이드에서 확인 가능합니다.

​
### 비고

- 일본향의 경우 224 CCNET에서 우편 코드가 자동 수집됩니다. ZipCodeCrawlerSet을 확인해주세요
- 한국향의 경우 API를 사용하고 있습니다.
- 다국향은 보통 우편 코드를 사서 수동으로 등록합니다.