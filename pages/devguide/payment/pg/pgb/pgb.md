---
title: "PB 중계 시스템"
description: "문서 설명"
tags: [개발가이드, 템플릿 ]
---

# Payment Gateway Bridge(PGB)
PG 사가 추가될 때마다 복잡해지는 라이브러리 해결 및 참조 충돌 해결을 위해 티쿤 시스템과 분리된 별도 API 서버에서 PG와 통신할 수 있도로 구성된 시스템입니다.

PGB 서버는 티쿤 시스템과 분리되서 공통 모듈 사용을 위해 티쿤 라이브러리를 참조 하지만 직접 서비스 로직을 호출 하지 않습니다.
별도 PGB용 데이터베이스로 결제 상태를 관리하고, 결제를 처리합니다.



## PGB 시스템 구성도
![image](https://user-images.githubusercontent.com/12683073/103264460-11867280-49ee-11eb-88af-ec4ed2804d1b.png)


1. \[결제 시작\] 티쿤 시스템 → PGB 결제 시작 요청,  응답 데이터로 페이지 이동

2. PGB 페이지, 혹은 PG 페이지에서 결제 완료

3. \[결제 완료\] PGB에서 PG사의 결제 상태 확인
- PGB Server → PG Server 입금 완료 단계 이동 처리 요청 
- PG Server에서 입금 완료 상태로 단계 이동

4. \[결제 취소\] 티쿤 시스템에서 PGB에 취소 요청
- PGB→  PG로 취소 요청, 취소 단계 이동

## PGB Interface
- /PGB/PayStart (결제 시작)
- /PGB/PartialCancel (부분 취소)
- /PGB/FullCancel (전체 취소)



### [POST] /PGB/PayStart (결제 시작)

    public class PGBPayStartParam
        {
           //Request
            public string DBType { get; set; }
            public int OrderId { get; set; }
            public string PayType { get; set; }
            public string TotalPrice { get; set; }
            public int JoinerId { get; set; }
            public string OrderDescription { get; set; }
            public string RedirectUrl { get; set; }
            public string NationCode { get; set; }
        }
    
  
    public class PGBPayStartResult
        {
          //Response
            public PGBPayStartResult();
    
            public string ErrorCode { get; set; }
            public string ErrorMessage { get; set; }
            public bool IsSuccess { get; set; }
            public string RedirectUrl { get; set; }
            public string Type { get; set; }
        }
    
    
### [POST] /PGB/PartialCancel (부분 취소)

    
    public class PGBPartialCancelParam
        {
            public string DBType { get; set; }
            public int OrderId { get; set; }
            public string RefundPrice { get; set; }
            public string CurrentTotalPrice { get; set; }
            public string ModifedTotalPrice { get; set; }
            public int JoinerId { get; set; }
            public string NationCode { get; set; }
        }
    
    
### [POST] /PGB/FullCancel (전체 취소)
    
    
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
    
    

---
## PGB 입금 Complete

- 결제 완료 후, 결제 처리가 정상적인지 PG사에 결괏값 요청 후, TqoonPGServer을 통해 결제 완료 처리를 합니다.
- [ex. STRIPE] [POST] /PGBReturn/WebHook (결제 완료 처리 - PGB에서 구현)
   

          [HttpPost]
            [Route("WebHook")]
            public void WebHook()
            {
    
                var json = new StreamReader(this.HttpContext.Request.InputStream).ReadToEnd();
                    var stripeEvent = EventUtility.ParseEvent(json);
                    if (stripeEvent.Type == Events.CheckoutSessionCompleted) //결제 성공
                    {
                        var stripeResponse = ((Stripe.Checkout.Session)stripeEvent.Data.Object);
                        PGBPayService.PayComplete(stripeResponse);
                    }
    
            }
   