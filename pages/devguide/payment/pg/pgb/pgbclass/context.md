---
title: "PB 중계 시스템"
description: "문서 설명"
tags: [개발가이드, 템플릿 ]
---
## V2- maintContext.xml

- PGB 서버 정보

```jsx
<?xml version="1.0" encoding="utf-8" ?>
<objects xmlns="http://www.springframework.net" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <import resource="~/App_Config/Provider/AppContext.xml"></import>
  <object id="PaygentAuthorize" type="TqoonV2.Models.PaygentAuthorize, TqoonV2"></object>
  <object id="PGBServerInfoRepo" type="Adprint.Service.PGIntegration.Module.PGB.Model.PGBServerInfoRepo, AdprintLib">
    <property name="PGBServerInfos" ref="PGBServerInfos" />
  </object>
  <object id="ElavonPGBServerInfo" type="Adprint.Service.PGIntegration.Module.PGB.Model.PGBServerInfo, AdprintLib">
    <property name="PGName" value="ELAVON" />
    <property name="PGBUrl" value="http://elavon.pgb.tqoon.com" />
    <property name="Token" value="" />
  </object>
  <object id="StripePGBServerInfo" type="Adprint.Service.PGIntegration.Module.PGB.Model.PGBServerInfo, AdprintLib">
    <property name="PGName" value="STRIPE" />
    <property name="PGBUrl" value="https://stripe.pgb.tqoon.com" />
    <property name="Token" value="" />
  </object>
  <object id="PGBServerInfos" type="System.Collections.Generic.List&lt;Adprint.Service.PGIntegration.Module.PGB.Model.PGBServerInfo>">
    <constructor-arg>
      <list>
        <ref object="ElavonPGBServerInfo"/>
		<ref object="StripePGBServerInfo"/>
      </list>
    </constructor-arg>
  </object>
</objects>
```
