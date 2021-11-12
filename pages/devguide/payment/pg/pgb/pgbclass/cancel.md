---
title: "PB 중계 시스템"
description: "문서 설명"
tags: [개발가이드, 템플릿 ]
---
# Cancel

## InterFace

- 부분 취소

```
public class PartialCancelParam
    {
        public string DbType { get; set; }
        public int OrderId { get; set; }
        public string PGType { get; set; }
        public string PayType { get; set; }
        public int CurrentTotalPrice { get; set; }
        public int ModifedTotalPrice { get; set; }
        public int RefundPrice { get; set; }
        public int JoinerId { get; set; }
        public string NationCode { get; set; }
    }
```

- 전체 취소

```
public class FullCancelParam
    {
        public string DbType { get; set; }
        public int OrderId { get; set; }
        public string PGType { get; set; }
        public string PayType { get; set; }
        public int CurrentTotalPrice { get; set; }
        public int JoinerId { get; set; }
        public string NationCode { get; set; }
    }
```

## Cancel Class

### [V2]MyPageOrderList.js

```
OrderAllCancel: function (intOrderNum) {
        return $http.postf("/Plugins/MyPageOrdersList/OrderCancel", {
            intOrderNum: intOrderNum,
            intOrderItemNum: 0
        });
	 },
 OrderCancel: function (intOrderNum, intOrderItemNum) {
        return $http.postf("/Plugins/MyPageOrdersList/OrderCancel", {
            intOrderNum: intOrderNum,
            intOrderItemNum: intOrderItemNum
        });
    },
```

### [Lib] PaymentGatewayService - PgCancel

- 부분취소/취소 PGB 서버에 전달

```
if (PGBService.IsPGBTarget(orderItem.PgType))
    {
         if (isAllCancel)
         {
            PGBService.FullCancel(PGTransformer.TransFullCancel(orderItem, joinerItem));
            return;
         }
          else
         {
             PGBService.PartialCancel(PGTransformer.TransPartialCancel(orderItem, refundPrice, joinerItem));
             return;
         }
    }
```

### [PGB] FullCancel, PartialCancel

 - 해당 PG사에서 결제 취소

```
 [HttpPost]
 [Route("FullCancel")]
 public IHttpActionResult FullCancel(PGBFullCancelParam cancelParam)
 {
     PGBServer.FullCancel(cancelParam);
     return Ok();
 }
[HttpPost]
 [Route("PartialCancel")]
 public IHttpActionResult PartialCancel(PGBPartialCancelParam cancelParam)
 {
     PGBServer.PartialCancel(cancelParam);
     return Ok();
 }
```