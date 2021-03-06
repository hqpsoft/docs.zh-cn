---
title: "CLR ETW 关键字和级别 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "CLR ETW 关键字"
  - "CLR ETW 级别"
  - "ETW, CLR 关键字"
  - "ETW, CLR 级别"
ms.assetid: fdf5856d-516b-4042-849d-911c4518a6cb
caps.latest.revision: 15
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 15
---
# CLR ETW 关键字和级别
<a name="top"></a> Windows \(ETW\) 事件的事件跟踪可以按类别和级别进行筛选。 事件 [CLR ETW 关键字](#keywords) 启用按类别筛选事件；它们用于运行时提供程序和断开提供程序的组合。[事件级别](#levels)由标志来标识。  
  
<a name="keywords"></a>   
## CLR ETW 关键字  
 关键字是可以组合以生成值的标志。 在实践中，当调用命令行实用程序时，使用关键字的十六进制值而非关键字名称。  
  
 下表描述了这些关键字：  
  
-   [CLR ETW 运行时关键字](#runtime)  
  
-   [CLR ETW 断开关键字](#rundown)  
  
-   [用于运行时提供程序的符号解析的关键字组合](#runtime_combo)  
  
-   [用于断开提供程序的符号解析的关键字组合](#rundown_combo)  
  
<a name="runtime"></a>   
### CLR ETW 运行时关键字  
 下表列出了 CLR ETW 运行时关键字、它们的值以及它们的用途。  
  
|运行时关键字名称|值|目标|  
|--------------|-------|--------|  
|`GCKeyword`|0x00000001|启用[垃圾回收事件](../../../docs/framework/performance/garbage-collection-etw-events.md)的回收。|  
|`LoaderKeyword`|0x00000008|启用[加载程序事件](../../../docs/framework/performance/loader-etw-events.md)的回收。|  
|`JITKeyword`|0x00000010|启用[实时 \(JIT\) 事件](../../../docs/framework/performance/jit-tracing-etw-events.md)的回收。|  
|`NGenKeyword`|0x00000020|启用本机映像方法（由本机映像生成器 Ngen.exe 处理的方法）的事件的收集；与 `StartEnumerationKeyword` 和 `EndEnumerationKeyword` 一起使用。 此关键字具有高开销。 它将在每个加载的 NGen 模块内生成每个方法的事件。 只要有可能，我们建议使用由分析工具生成的程序数据库 \(PDB\) 从 NGen 模块检索有关方法的信息，而不是使用此关键字。 另请参阅此表后面的 `OverrideAndSuppressNGenEventsKeyword`。|  
|`StartEnumerationKeyword`|0x00000040|启用运行时中所有方法的枚举；与 `NGenKeyword` 配合使用。|  
|`EndEnumerationKeyword`|0x00000080|启用运行时中销毁的所有方法的枚举；与 `JITKeyword` 和 `NGenKeyword` 配合使用。|  
|`SecurityKeyword`|0x00000400|启用[安全事件](../../../docs/framework/performance/security-etw-events.md)的回收。|  
|`AppDomainResourceManagementKeyword`|0x00000800|启用应用程序域级别的资源监视事件的回收。|  
|`JITTracingKeyword`|0x00001000|启用 [JIT 跟踪事件](../../../docs/framework/performance/jit-tracing-etw-events.md)的回收。|  
|`InteropKeyword`|0x00002000|启用[互操作事件](../../../docs/framework/performance/interop-etw-events.md)的回收。|  
|`ContentionKeyword`|0x00004000|启用[争用事件](../../../docs/framework/performance/contention-etw-events.md)的回收。|  
|`ExceptionKeyword`|0x00008000|启用[异常事件](../../../docs/framework/performance/exception-thrown-v1-etw-event.md)的回收。|  
|`ThreadingKeyword`|0x00010000|启用[线程池事件](../../../docs/framework/performance/thread-pool-etw-events.md)的回收。|  
|`OverrideAndSuppressNGenEventsKeyword`|0x00040000|（[!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 及更高版本中可用。） 取消高开销 `NGenKeyword` 关键字，并防止生成 NGen 模块内方法的事件。 从 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 开始，分析工具应一并使用 `OverrideAndSuppressNGenEventsKeyword` 和 `NGenKeyword` 以取消生成 NGen 模块内方法的事件。 这使分析工具能够使用更高效的 NGen PDB 来获取 NGen 模块中方法的相关信息。 .NET Framework 4 及更早版本中的 CLR 不支持 NGen PDB 的创建。 在这些早期版本中，CLR 将不识别 `OverrideAndSuppressNGenEventsKeyword` 并将处理 `NGenKeyword` 以生成 NGen 模块内方法的事件。|  
|`PerfTrackKeyWord`|0x2000000|启用 `ModuleLoad` 和 `ModuleRange` 事件的回收。|  
|`StackKeyword`|0x40000000|启用 CLR [堆栈跟踪事件](../../../docs/framework/performance/stack-etw-event.md)的回收。|  
  
 [返回页首](#top)  
  
<a name="rundown"></a>   
### CLR ETW 断开关键字  
 下表列出了 CLR ETW 断开关键字、它们的值以及它们的用途。  
  
|断开关键字名称|值|目标|  
|-------------|-------|--------|  
|`LoaderRundownKeyword`|0x00000008|当与 `StartRundownKeyword` 和 `EndRundownKeyword` 一起使用时启用加载程序事件的回收。|  
|`JitRundownKeyword`|0x00000010|当与 `StartRundownKeyword` 和 `EndRundownKeyword` 一起使用时启用 JIT 编译的方法的方法 `DCStart` 和 `DCEnd` 事件的回收。|  
|`NGenRundownKeyword`|0x00000020|当与 `StartRundownKeyword` 和 `EndRundownKeyword` 一起使用时启用 NGen 本机映像方法的方法 `DCStart` 和 `DCEnd` 事件的回收。 此关键字具有高开销。 它将在每个加载的 NGen 模块内生成每个方法的事件。 只要有可能，我们建议使用由分析工具生成的程序数据库 \(PDB\) 从 NGen 模块检索有关方法的信息，而不是使用此关键字。 另请参阅此表后面的 `OverrideAndSuppressNGenEventsRundownKeyword`。|  
|`StartRundownKeyword`|0x00000040|在开始断开期间启用系统状态的枚举。|  
|`EndRundownKeyword`|0x00000100|在结束断开期间启用系统状态的枚举。|  
|`AppDomainResourceManagementRundownKeyword`|0x00000800|当与 `StartRundownKeyword` 或 `EndRundownKeyword` 一起使用时启用 <xref:System.AppDomain> 级别的资源监视的事件的回收。|  
|`ThreadingKeyword`|0x00010000|启用线程池事件的回收。|  
|`OverrideAndSuppressNGenEventsRundownKeyword`|0x00040000|（在 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 及更高版本中可用。） 取消高开销 `NGenRundownKeyword` 关键字，并防止生成 NGen 模块内方法的事件。 从 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 开始，分析工具应一并使用 `OverrideAndSuppressNGenEventsRundownKeyword` 和 `NGenRundownKeyword` 以取消生成 NGen 模块内方法的事件。 这使分析工具能够使用更高效的 NGen PDB 来获取 NGen 模块中方法的相关信息。 .NET Framework 4 及更早版本中的 CLR 不支持 NGen PDB 的创建。 在这些早期版本中，CLR 将不识别 `OverrideAndSuppressNGenEventsRundownKeyword` 并将处理 `NGenRundownKeyword` 以生成 NGen 模块内方法的事件。|  
|`PerfTrackKeyWord`|0x2000000|启用 `ModuleDCStart`、`ModuleDCEnd`、`ModuleRangeDCStart` 和 `ModuleRangeDCEnd` 事件的回收。|  
  
 [返回页首](#top)  
  
<a name="runtime_combo"></a>   
### 用于运行时提供程序的符号解析的关键字组合  
  
|关键字和标志|应用程序域、程序集、模块加载\/卸载事件|方法加载\/卸载事件（动态事件除外）|动态方法加载\/销毁事件|  
|------------|--------------------------|------------------------|------------------|  
|`LoaderKeyword`|加载和卸载事件。|无。|无。|  
|`JITKeyword`<br /><br /> （\+ `StartEnumerationKeyword` 不添加任何内容）|无。|加载事件。|加载和卸载事件。|  
|`JITKeyword` \+<br /><br /> `EndEnumerationKeyword`|无。|加载和卸载事件。|加载和卸载事件。|  
|`NGenKeyword`|无。|无。|不适用。|  
|`NGenKeyword` \+<br /><br /> `StartEnumerationKeyword`|无。|加载事件。|不适用。|  
|`NGenKeyword` \+<br /><br /> `EndEnumerationKeyword`|无。|卸载事件。|不适用。|  
  
 [返回页首](#top)  
  
<a name="rundown_combo"></a>   
### 用于断开提供程序的符号解析的关键字组合  
  
|关键字和标志|应用程序域、程序集、模块 DCStart\/DCEnd 事件|方法 DCStart\/DCEnd 事件（包括动态方法事件）|  
|------------|------------------------------------|------------------------------------|  
|`LoaderRundownKeyword` \+<br /><br /> `StartRundownKeyword`|`DCStart` 事件。|无。|  
|`LoaderRundownKeyword` \+<br /><br /> `EndRundownKeyword`|`DCEnd` 事件。|无。|  
|`JITKeyword` \+<br /><br /> `StartRundownKeyword`|无。|`DCStart` 事件。|  
|`JITKeyword` \+<br /><br /> `EndRundownKeyword`|无。|`DCEnd` 事件。|  
|`NGenKeyword` \+<br /><br /> `StartRundownKeyword`|无。|`DCStart` 事件。|  
|`NGenKeyword` \+<br /><br /> `EndRundownKeyword`|无。|`DCEnd` 事件。|  
  
 [返回页首](#top)  
  
<a name="levels"></a>   
## ETW 事件级别  
 ETW 事件还可按级别进行筛选。 如果级别设置为 0x5，则会引发包括 0x5 及以下级别的事件（这些事件属于通过关键字启用的类别）。 如果级别设置为 0x2，则只会引发 0x2 及以下级别的事件。  
  
 级别具有以下含义：  
  
 0x5 \- 详细  
  
 0x4 \- 信息性  
  
 0x3 \- 警告  
  
 0x2 \- 错误  
  
 0x1 \- 严重  
  
 0x0 \- LogAlways  
  
## 请参阅  
 [CLR ETW 提供程序](../../../docs/framework/performance/clr-etw-providers.md)   
 [CLR ETW 事件](../../../docs/framework/performance/clr-etw-events.md)   
 [公共语言运行时中的 ETW 事件](../../../docs/framework/performance/etw-events-in-the-common-language-runtime.md)