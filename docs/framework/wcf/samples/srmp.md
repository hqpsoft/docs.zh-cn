---
title: "SRMP | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: cf37078c-dcb4-45e0-acaf-2f196521b226
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# SRMP
本示例演示如何使用 HTTP 上的消息队列 \(MSMQ\) 来执行事务处理排队通信。  
  
 在排队通信中，客户端使用队列与服务进行通信。  更确切地说，客户端向队列发送消息。  服务从队列接收消息。  因此不必同时运行服务和客户端便可使用队列进行通信。  
  
 MSMQ 启用 HTTP（包括启用 HTTPS）来向队列发送消息。  在本示例中，我们演示如何使用 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 排队通信和如何通过 HTTP 发送消息。  MSMQ 使用一种称为 SRMP 的协议，此协议是一种用于通过 HTTP 进行通信的基于 SOAP 的协议。  
  
### 设置、生成和运行示例  
  
1.  确保已经执行了[Windows Communication Foundation 示例的一次性安装过程](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)。  
  
2.  若要生成 C\# 或 Visual Basic .NET 版本的解决方案，请按照[生成 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/building-the-samples.md)中的说明进行操作。  
  
3.  若要用单机配置或跨计算机配置来运行示例，请按照[运行 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/running-the-samples.md)中的说明进行操作。  
  
4.  在**“添加\/删除 Windows 组件”**中运行示例之前，确保安装了 MSMQ 和 HTTP 支持。  安装 HTTP 支持时，会自动安装 Internet 信息服务 \(IIS\)，并会在 IIS 中添加对 MSMQ 的协议支持。  
  
5.  如果想要确保使用 HTTP 进行通信，则可以启用 MSMQ 以便在加强模式中运行。  这可确保任何消息都不能使用任何非 HTTP 传输到达计算机上承载的任何队列。  
  
6.  选择 MSMQ 以在加强模式中运行后，如果系统为 [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)]，计算机需要重新启动。  
  
7.  运行服务。  
  
8.  运行客户端。  确保将终结点地址更改为指向计算机名或 IP 地址而不是 localhost。  客户端将发送消息并退出。  
  
## 要求  
 若要运行此示例，服务计算机和客户端计算机上除了 MSMQ 外，还必须安装 IIS。  
  
## 演示  
 示例演示如何通过 HTTP 使用 MSMQ 来发送 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 排队消息。  这也称为 SRMP 消息传递。  发送排队消息时，发送方计算机上的 MSMQ 通过 TCP 或 HTTP 传输将消息传送到接收队列管理器。  通过选择 SRMP，用户可以指示选择 HTTP 作为队列传送的传输协议。  SRMP 安全启用 HTTPS。  
  
## 示例  
 示例代码基于事务处理示例。  使用 SRMP 将消息发送到队列和从队列中接收消息的方式与使用本机协议发送和接收消息的方式相同。  
  
 客户端的配置将会发生更改以指示选择队列传输协议。  队列传输协议可以是本机、SRMP 或 SrmpSecure 之一。  默认情况下，传输协议为“本机”。  在此示例中，客户端和服务在配置中指定使用 SRMP。  
  
 SRMP 存在与传输安全相关的限制。  默认 MSMQ 传输安全需要使用 Active Directory，而 Active Directory 要求发送队列管理器和接收队列管理器位于同一个 Windows 域中。  这在通过 HTTP 边界发送消息时是不可能的。  因此，无法使用默认传输安全。  如果需要传输安全，则传输安全必须设置为“证书”。  消息安全也可用于保护消息。  在本示例中，为说明 SRMP 消息传递，关闭了传输和消息安全。  
  
```  
<?xml version="1.0" encoding="utf-8" ?>  
<configuration>  
  
  <system.serviceModel>  
  
    <client>  
      <!-- Define NetMsmqEndpoint -->  
      <endpoint name="OrderProcessorEndpoint"  
           address=  
          "net.msmq://localhost/private/ServiceModelSamplesSrmp"   
           bindingConfiguration="srmpBinding"   
           binding="netMsmqBinding"   
           contract="IOrderProcessor" />  
    </client>  
    <bindings>  
      <netMsmqBinding>  
        <binding name="srmpBinding"  
                 queueTransferProtocol="Srmp">  
          <security mode="None"></security>  
        </binding>  
      </netMsmqBinding>  
    </bindings>  
  </system.serviceModel>  
  
</configuration>  
```  
  
 运行此示例可生成下面的输出。  
  
```  
Processing Purchase Order: 556b70be-31ee-4a3b-8df4-ed5e538015a4   
Customer: somecustomer.com   
OrderDetails   
    Order LineItem: 54 of Blue Widget @unit price: $29.99   
    Order LineItem: 890 of Red Widget @unit price: $45.89   
    Total cost of this order: $42461.56   
    Order status: Pending  
```  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。  在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。  此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WCF\Basic\Binding\Net\MSMQ\SRMP`  
  
## 请参阅