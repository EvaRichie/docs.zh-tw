---
title: ServiceModel 交易組態
ms.date: 03/30/2017
helpviewer_keywords:
- transactions [WCF], ServiceModel configuration
ms.assetid: 5636067a-7fbd-4485-aaa2-8141c502acf3
ms.openlocfilehash: 1d04a7bb756cccb33b436c1f57decc0249764828
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84600331"
---
# <a name="servicemodel-transaction-configuration"></a><span data-ttu-id="8f475-102">ServiceModel 交易組態</span><span class="sxs-lookup"><span data-stu-id="8f475-102">ServiceModel Transaction Configuration</span></span>
<span data-ttu-id="8f475-103">Windows Communication Foundation （WCF）提供三個屬性來設定服務的交易： `transactionFlow` 、 `transactionProtocol` 和 `transactionTimeout` 。</span><span class="sxs-lookup"><span data-stu-id="8f475-103">Windows Communication Foundation (WCF) provides three attributes for configuring transactions for a service: `transactionFlow`, `transactionProtocol`, and `transactionTimeout`.</span></span>  
  
## <a name="configuring-transactionflow"></a><span data-ttu-id="8f475-104">設定 transactionFlow</span><span class="sxs-lookup"><span data-stu-id="8f475-104">Configuring transactionFlow</span></span>  
 <span data-ttu-id="8f475-105">WCF 提供的大部分預先定義系結都包含 `transactionFlow` 和 `transactionProtocol` 屬性，因此您可以使用特定的交易流程通訊協定，將系結設定為接受特定端點的傳入交易。</span><span class="sxs-lookup"><span data-stu-id="8f475-105">Most of the predefined bindings WCF provides contain the `transactionFlow` and `transactionProtocol` attributes, so that you can configure the binding to accept incoming transactions for a specific endpoint using a specific transaction flow protocol.</span></span> <span data-ttu-id="8f475-106">此外，您可以使用 `transactionFlow` 元素及其 `transactionProtocol` 屬性來建置您自訂的繫結。</span><span class="sxs-lookup"><span data-stu-id="8f475-106">In addition, you can use the `transactionFlow` element and its `transactionProtocol` attribute to build your own custom binding.</span></span> <span data-ttu-id="8f475-107">如需設定 configuration 元素的詳細資訊，請參閱 [\<binding>](../../configure-apps/file-schema/wcf/bindings.md) 和[WCF 設定架構](../../configure-apps/file-schema/wcf/index.md)。</span><span class="sxs-lookup"><span data-stu-id="8f475-107">For more information about setting the configuration elements, see [\<binding>](../../configure-apps/file-schema/wcf/bindings.md) and [WCF Configuration Schema](../../configure-apps/file-schema/wcf/index.md).</span></span>  
  
 <span data-ttu-id="8f475-108">`transactionFlow` 屬性會指定是否要為使用繫結的服務端點啟用交易流程。</span><span class="sxs-lookup"><span data-stu-id="8f475-108">The `transactionFlow` attribute specifies whether transaction flow is enabled for service endpoints that use the binding.</span></span>  
  
## <a name="configuring-transactionprotocol"></a><span data-ttu-id="8f475-109">設定 transactionProtocol</span><span class="sxs-lookup"><span data-stu-id="8f475-109">Configuring transactionProtocol</span></span>  
 <span data-ttu-id="8f475-110">`transactionProtocol` 屬性會指定交易通訊協定與使用繫結的服務端點一起使用。</span><span class="sxs-lookup"><span data-stu-id="8f475-110">The `transactionProtocol` attribute specifies the transaction protocol to use with service endpoints that use the binding.</span></span>  
  
 <span data-ttu-id="8f475-111">以下是組態區段的範例，其中設定了支援異動流程的指定繫結程序，以及使用 WS-AtomicTransaction 通訊協定的範例。</span><span class="sxs-lookup"><span data-stu-id="8f475-111">The following is an example of a configuration section that configures the specified binding to support transaction flow, as well as a use the WS-AtomicTransaction protocol.</span></span>  
  
```xml  
<netNamedPipeBinding>  
   <binding name="test"  
      closeTimeout="00:00:10"  
      openTimeout="00:00:20"
      receiveTimeout="00:00:30"  
      sendTimeout="00:00:40"  
      transactionFlow="true"  
      transactionProtocol="WSAtomicTransactionOctober2004"  
      hostNameComparisonMode="WeakWildcard"  
      maxBufferSize="1001"  
      maxConnections="123"
      maxReceivedMessageSize="1000">  
   </binding>  
</netNamedPipeBinding>  
```  
  
## <a name="configuring-transactiontimeout"></a><span data-ttu-id="8f475-112">設定 transactionTimeout</span><span class="sxs-lookup"><span data-stu-id="8f475-112">Configuring transactionTimeout</span></span>  
 <span data-ttu-id="8f475-113">您可以 `transactionTimeout` 在設定檔的元素中設定 WCF 服務的屬性 `behavior` 。</span><span class="sxs-lookup"><span data-stu-id="8f475-113">You can configure the `transactionTimeout` attribute for your WCF service in the `behavior` element of the configuration file.</span></span> <span data-ttu-id="8f475-114">下列程式碼會示範如何執行此項作業。</span><span class="sxs-lookup"><span data-stu-id="8f475-114">The following code demonstrates how to do this.</span></span>  
  
```xml  
<configuration>  
   <system.serviceModel>  
      <behaviors>  
         <behavior name="NewBehavior" transactionTimeout="00:01:00" /> <!-- 1 minute timeout -->  
      </behaviors>  
   </system.serviceModel>  
</configuration>  
```  
  
 <span data-ttu-id="8f475-115">`transactionTimeout` 屬性會指定在服務所建立之新交易必須完成的時間週期。</span><span class="sxs-lookup"><span data-stu-id="8f475-115">The `transactionTimeout` attribute specifies the time period within which a new transaction created at the service must complete.</span></span> <span data-ttu-id="8f475-116">這個屬性可當做任何建立新異動之作業的 <xref:System.Transactions.TransactionScope> 逾時使用，若套用了 <xref:System.ServiceModel.OperationBehaviorAttribute>，則 <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionScopeRequired%2A> 屬性會設為 `true`。</span><span class="sxs-lookup"><span data-stu-id="8f475-116">It is used as the <xref:System.Transactions.TransactionScope> time-out for any operation that establishes a new transaction, and if <xref:System.ServiceModel.OperationBehaviorAttribute> is applied, the <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionScopeRequired%2A> property is set to `true`.</span></span>  
  
 <span data-ttu-id="8f475-117">逾時會指定從建立異動到完成兩階段異動認可通訊協定中的階段 1 的時間範圍。</span><span class="sxs-lookup"><span data-stu-id="8f475-117">The time-out specifies the duration of time from the creation of the transaction to the completion of phase 1 in the two-phase commit protocol.</span></span>  
  
 <span data-ttu-id="8f475-118">如果在 `service` 組態區段中設定這個屬性，您至少應該以 <xref:System.ServiceModel.OperationBehaviorAttribute> 套用一個對應服務的方法，其中 <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionScopeRequired%2A> 屬性設定為 `true`。</span><span class="sxs-lookup"><span data-stu-id="8f475-118">If this attribute is set within a `service` configuration section, you should apply at least one method of the corresponding service with <xref:System.ServiceModel.OperationBehaviorAttribute>, in which the <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionScopeRequired%2A> property is set to `true`.</span></span>  
  
 <span data-ttu-id="8f475-119">請注意，所使用的逾時值會是這個 `transactionTimeout` 組態設定和任何 <xref:System.ServiceModel.ServiceBehaviorAttribute.TransactionTimeout%2A> 屬性間的較小值。</span><span class="sxs-lookup"><span data-stu-id="8f475-119">Note that the time-out value used is the smaller value between this `transactionTimeout` configuration setting and any <xref:System.ServiceModel.ServiceBehaviorAttribute.TransactionTimeout%2A> property.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="8f475-120">請參閱</span><span class="sxs-lookup"><span data-stu-id="8f475-120">See also</span></span>

- [\<binding>](../../configure-apps/file-schema/wcf/bindings.md)
- [<span data-ttu-id="8f475-121">WCF 組態結構描述</span><span class="sxs-lookup"><span data-stu-id="8f475-121">WCF Configuration Schema</span></span>](../../configure-apps/file-schema/wcf/index.md)
