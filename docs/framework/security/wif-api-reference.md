---
title: "WIF API 参考 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a027d902-9314-4bfd-b172-4e81847b1d68
caps.latest.revision: 4
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 4
---
# WIF API 参考
Windows Identity Foundation \(WIF\) classes are split across the following assemblies: `mscorlib` \(mscorlib.dll\), `System.IdentityModel` \(System.IdentityModel.dll\), `System.IdentityModel.Services` \(System.IdentityModel.Services.dll\), and `System.ServiceModel` \(System.ServiceModel.dll\).  This topic provides links to the WIF namespaces and brief explanations of the classes that each namespace contains.  
  
> [!IMPORTANT]
>  The following `System.IdentityModel` namespaces contain classes that implement the WCF claims\-based identity model: <xref:System.IdentityModel.Claims?displayProperty=fullName>, <xref:System.IdentityModel.Policy?displayProperty=fullName>, and <xref:System.IdentityModel.Selectors?displayProperty=fullName>.  Starting with .NET Framework 4.5, the WCF claims\-based identity model is superseded by WIF.  You should not use classes in these three namespaces when building solutions based on WIF.  
  
 <xref:System.IdentityModel?displayProperty=fullName>  
 Contains classes that represent cookie transforms, security token services, and specialized XML dictionary readers.  
  
 <xref:System.IdentityModel.Configuration?displayProperty=fullName>  
 Contains classes that provide configuration for applications and services built using the Windows Identity Foundation \(WIF\).  表示 [\<identityConfiguration\>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md) 元素下的设置的此命名空间的类。  
  
 <xref:System.IdentityModel.Metadata?displayProperty=fullName>  
 Contains classes that represent elements in a Federation Metadata document.  
  
 <xref:System.IdentityModel.Protocols.WSTrust?displayProperty=fullName>  
 Contains classes that represent WS\-Trust artifacts.  
  
 <xref:System.IdentityModel.Services?displayProperty=fullName>  
 Contains classes that are used in passive \(WS\-Federation\) scenarios.  Also contains some classes that represent settings under the [\<system.identityModel.services\>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/system-identitymodel-services.md) element.  Settings under this element configure WS\-Federation for applications.  The `System.IdentityModel.Services.Configuration` namespace contains most of the classes that are used to configure WS\-Federation.  
  
 <xref:System.IdentityModel.Services.Configuration?displayProperty=fullName>  
 Contains classes that provide configuration for WIF applications that use the WS\-Federation protocol.  表示 [\<system.identityModel.services\>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/system-identitymodel-services.md) 元素下的设置的此命名空间的类。  The `System.IdentityModel.Services` namespace also contains some classes that are used to configure WS\-Federation.  
  
 <xref:System.IdentityModel.Services.Tokens?displayProperty=fullName>  
 Contains specialized security token handlers for Web farm scenarios.  
  
 <xref:System.IdentityModel.Tokens?displayProperty=fullName>  
 Contains classes that represent security tokens, security token handlers, and other security token artifacts.  
  
 <xref:System.Security.Claims?displayProperty=fullName>  
 Contains classes that represent claims, claims\-based identities, claims\-based principals, and other claims\-based identity model artifacts.  
  
 <xref:System.ServiceModel.Security?displayProperty=fullName>  
 Contains classes that represent WCF contracts, channels, service hosts and other artifacts that are used in active \(WS\-Trust\) scenarios.  This namespace also contains classes that are specific to Windows Communication Foundation \(WCF\) and that are not used by WIF.  
  
## 请参阅  
 [WIF 配置参考](../../../docs/framework/security/wif-configuration-reference.md)   
 [WIF 3.5 和 WIF 4.5 之间的命名空间映射](../../../docs/framework/security/namespace-mapping-between-wif-3-5-and-wif-4-5.md)