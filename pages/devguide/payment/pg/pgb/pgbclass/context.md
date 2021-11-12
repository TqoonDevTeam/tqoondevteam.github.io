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

## PGB - appContext.xml

- TqoonPG 서버 정보

```jsx
<?xml version="1.0" encoding="utf-8"?>
<objects xmlns="http://www.springframework.net" xmlns:db="http://www.springframework.net/database" xmlns:tx="http://www.springframework.net/tx">
  <db:provider id="DbProvider" provider="System.Data.SqlClient" connectionString="SERVER=172.168.2.12\TQOONPGB,2900 ;DATABASE=TqoonPGB;USER ID=web; PASSWORD=xlzns!@#0" />  
  <object id="AdoTemplate" type="Spring.Data.Generic.AdoTemplate, Spring.Data">
    <property name="DbProvider" ref="DbProvider" />
    <property name="DataReaderWrapperType" value="Spring.Data.Support.NullMappingDataReader, Spring.Data" />
    <property name="CommandTimeout" value="60" />
  </object>
  <object id="transactionManager" type="Spring.Data.Core.AdoPlatformTransactionManager, Spring.Data">
    <property name="DbProvider" ref="DbProvider" />
  </object>
 <object id="PGBServerAllowedIp" type="System.Collections.Generic.List&lt;string>">
    <constructor-arg>
      <list>
        <value>222.122.209.240</value>
      </list>
    </constructor-arg>
  </object>
  <object id="PGBServerIp" type="System.Collections.Generic.List&lt;string>">
    <constructor-arg>
      <list>
        <value>222.122.209.240</value>
      </list>
    </constructor-arg>
  </object>
  <object id="TqoonPGServerInfoRepo" type="PGBridge_Stripe.Service.TqoonPG.Model.TqoonPGServerInfoRepo">
    <property name="TqoonPGServerInfos" ref="TqoonPGServerInfos" />
  </object>
  <object id="TqoonPGServerInfoJP" type="PGBridge_Stripe.Service.TqoonPG.Model.TqoonPGServerInfo">
    <property name="NationCode" value="JP" />
    <property name="Url" value="https://pg.tqoon.com" />
  </object>
  <object id="TqoonPGServerInfoKR" type="PGBridge_Stripe.Service.TqoonPG.Model.TqoonPGServerInfo">
    <property name="NationCode" value="KR" />
    <property name="Url" value="https://pg.tqoon.kr" />
  </object>
  <object id="TqoonPGServerInfoMY" type="PGBridge_Stripe.Service.TqoonPG.Model.TqoonPGServerInfo">
    <property name="NationCode" value="MY" />
    <property name="Url" value="https://pg.tqoon.my" />
  </object>
 <object id="TqoonPGServerInfoID" type="PGBridge_Stripe.Service.TqoonPG.Model.TqoonPGServerInfo">
    <property name="NationCode" value="ID" />
    <property name="Url" value="http://pg.tqoon.id" />
  </object>
  <object id="TqoonPGServerInfoAU" type="PGBridge_Stripe.Service.TqoonPG.Model.TqoonPGServerInfo">
    <property name="NationCode" value="AU" />
    <property name="Url" value="https://pg.tqoon.com.au" />
  </object>
  <object id="TqoonPGServerInfoAU" type="PGBridge_Stripe.Service.TqoonPG.Model.TqoonPGServerInfo">
    <property name="NationCode" value="AU" />
    <property name="Url" value="https://pg.tqoon.com.au" />
  </object>
  <object id="TqoonPGServerInfoMX" type="PGBridge_Stripe.Service.TqoonPG.Model.TqoonPGServerInfo">
    <property name="NationCode" value="MX" />
    <property name="Url" value="https://pg.tqoon.com.au" />
  </object>
  <object id="TqoonPGServerInfoBR" type="PGBridge_Stripe.Service.TqoonPG.Model.TqoonPGServerInfo">
    <property name="NationCode" value="BR" />
    <property name="Url" value="https://pg.tqoonbr.com" />
  </object>
  <object id="TqoonPGServerInfoCN" type="PGBridge_Stripe.Service.TqoonPG.Model.TqoonPGServerInfo">
    <property name="NationCode" value="CN" />
    <property name="Url" value="http://pg.tqoon.cn" />
  </object>
  <object id="TqoonPGServerInfos" type="System.Collections.Generic.List&lt;PGBridge_Stripe.Service.TqoonPG.Model.TqoonPGServerInfo>">
    <constructor-arg>
      <list>   
		<ref object="TqoonPGServerInfoJP"/>
		<ref object="TqoonPGServerInfoKR"/>
		<ref object="TqoonPGServerInfoMY"/>
		<ref object="TqoonPGServerInfoID"/>
		<ref object="TqoonPGServerInfoAU"/>
		<ref object="TqoonPGServerInfoMX"/>
		<ref object="TqoonPGServerInfoBR"/>
		<ref object="TqoonPGServerInfoCN"/>
      </list>
    </constructor-arg>
  </object>
  <tx:attribute-driven />
</objects>
```