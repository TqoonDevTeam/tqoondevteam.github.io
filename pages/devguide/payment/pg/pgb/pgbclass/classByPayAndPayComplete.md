---
title: "PB 중계 시스템"
description: "문서 설명"
tags: [개발가이드, 템플릿 ]
---
# PayStart
- /PGB/PayStart
    - 결제 세션 생성
    - 결제 세션, 결제 완료 → success or cancelUrl return
    - 결제 단계 STANDBY
    
## INTERFACE
- request

```
    public class PGBPayStartParam
        {
            //reqeust
            public string DBType { get; set; }
            public int OrderId { get; set; }
            public string PayType { get; set; }
            public string TotalPrice { get; set; }
            public int JoinerId { get; set; }
            public string OrderDescription { get; set; }
            public string RedirectUrl { get; set; }
            public string NationCode { get; set; }
        }

 ```

- response

```  
    public class PGBPayStartResult
        {
            public PGBPayStartResult();
    
            public string ErrorCode { get; set; }
            public string ErrorMessage { get; set; }
            public bool IsSuccess { get; set; }
            public string RedirectUrl { get; set; }
            public string Type { get; set; }
        }
```    
    
## CLASS
    
### [Client] PgController.OrderStart
- PGB RedirectUrl
```    
    if (PGIntegrationService.IsIntegrationTarget(orderItem.PgType, orderItem.PayType))
        {
             var result = PGIntegrationService.PayStart(id, CurrentUser.UserId, CurrentSite.JoinerId);
             return Redirect(result.RedirectUrl);
                                  
        }
```   
    
### [Lib Server] PGBService.PayStart
- PGB로 결제 시작 요청
```    
    //PGB 서버 정보를 가져온다.
    var server = GetPGBServerInfo(param.PGType);
    
    //PGB서버에 보내기 위한 PGBPayStartParam create & PGB 서버에 Post 
    var result = PGBClient.PayStart(server, PGBTransformer.Trans(param));
    
    //PGB 응답 PGBPayStartResult Return
    return PGBTransformer.Trans(result);
```    
    
### [PGB Server] PGBServer.PayStart
- 해당 PG사에 결제 시도
```    
    public IHttpActionResult PayStart(PGBPayStartParam payStartParam)
            {
    
                var result = PGBServer.PayStart(payStartParam);
                return Ok(result);
            }
```   

### 결제 완료(PayComplete)
- 결제 완료 후, 정상적으로 결제 처리가 됐는지 재확인
- 결제가 정상적으로 처리됬다면, TqoonPG로 입금 완료 단계 이동 요청
```    
    [ex. Stripe PGB]
    
    - /PGBReturn/Webhook
        - (Webhook) - checkout.session.completed 전달 받으면
            - 검증을 위해 지불 상태 확인
            - payState →  succeeded
                - 결제 상태 paid 상태로 update
                - PG API 전달 → 결제 완료 단계 이동
```                