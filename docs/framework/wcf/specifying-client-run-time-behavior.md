---
title: 指定用戶端執行階段行為
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- behaviors [WCF], system-provided client
ms.assetid: d16d3405-be70-4edb-8f62-b5f614ddeca5
ms.openlocfilehash: 17031f2100c6760cd14aae57cd4efab7428eb362
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96235892"
---
# <a name="specifying-client-run-time-behavior"></a><span data-ttu-id="afad4-102">指定用戶端執行階段行為</span><span class="sxs-lookup"><span data-stu-id="afad4-102">Specifying Client Run-Time Behavior</span></span>

<span data-ttu-id="afad4-103">Windows Communication Foundation (WCF) 用戶端（例如 Windows Communication Foundation (WCF) services）可以設定為符合用戶端應用程式的執行時間行為。</span><span class="sxs-lookup"><span data-stu-id="afad4-103">Windows Communication Foundation (WCF) clients, like Windows Communication Foundation (WCF) services, can be configured to modify the run-time behavior to suit the client application.</span></span> <span data-ttu-id="afad4-104">指定用戶端執行階段行為時有三個屬性可供使用。</span><span class="sxs-lookup"><span data-stu-id="afad4-104">Three attributes are available for specifying client run-time behavior.</span></span> <span data-ttu-id="afad4-105">雙工用戶端回呼物件可以使用 <xref:System.ServiceModel.CallbackBehaviorAttribute> 和 <xref:System.ServiceModel.Description.CallbackDebugBehavior> 屬性來修改其執行階段行為。</span><span class="sxs-lookup"><span data-stu-id="afad4-105">Duplex client callback objects can use the <xref:System.ServiceModel.CallbackBehaviorAttribute> and <xref:System.ServiceModel.Description.CallbackDebugBehavior> attributes to modify their run-time behavior.</span></span> <span data-ttu-id="afad4-106">而另一個屬性 <xref:System.ServiceModel.Description.ClientViaBehavior> 則可用來區隔邏輯目的和立即網路目的。</span><span class="sxs-lookup"><span data-stu-id="afad4-106">The other attribute, <xref:System.ServiceModel.Description.ClientViaBehavior>, can be used to separate the logical destination from the immediate network destination.</span></span> <span data-ttu-id="afad4-107">此外，雙工用戶端回呼類型也可使用一些服務端的行為。</span><span class="sxs-lookup"><span data-stu-id="afad4-107">In addition, duplex client callback types can use some of the service-side behaviors.</span></span> <span data-ttu-id="afad4-108">如需詳細資訊，請參閱 [指定服務 Run-Time 行為](specifying-service-run-time-behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="afad4-108">For more information, see [Specifying Service Run-Time Behavior](specifying-service-run-time-behavior.md).</span></span>  
  
## <a name="using-the-callbackbehaviorattribute"></a><span data-ttu-id="afad4-109">使用 CallbackBehaviorAttribute</span><span class="sxs-lookup"><span data-stu-id="afad4-109">Using the CallbackBehaviorAttribute</span></span>  

 <span data-ttu-id="afad4-110">您可以使用 <xref:System.ServiceModel.CallbackBehaviorAttribute> 類別，即可設定或擴充用戶端應用程式中回呼合約實作的執行行為。</span><span class="sxs-lookup"><span data-stu-id="afad4-110">You can configure or extend the execution behavior of a callback contract implementation in a client application by using the <xref:System.ServiceModel.CallbackBehaviorAttribute> class.</span></span> <span data-ttu-id="afad4-111">這個屬性對回呼類別執行的函式類似於 <xref:System.ServiceModel.ServiceBehaviorAttribute> 類別，而執行個體化行為和交易設定則為其例外。</span><span class="sxs-lookup"><span data-stu-id="afad4-111">This attribute performs a similar function for the callback class as the <xref:System.ServiceModel.ServiceBehaviorAttribute> class, with the exception of instancing behavior and transaction settings.</span></span>  
  
 <span data-ttu-id="afad4-112"><xref:System.ServiceModel.CallbackBehaviorAttribute> 類別必須套用至實作回呼合約的類別。</span><span class="sxs-lookup"><span data-stu-id="afad4-112">The <xref:System.ServiceModel.CallbackBehaviorAttribute> class must be applied to the class that implements the callback contract.</span></span> <span data-ttu-id="afad4-113">如果套用至非雙工合約實作，便會在執行階段擲回 <xref:System.InvalidOperationException> 例外狀況 (Exception)。</span><span class="sxs-lookup"><span data-stu-id="afad4-113">If applied to a nonduplex contract implementation, an <xref:System.InvalidOperationException> exception is thrown at run time.</span></span> <span data-ttu-id="afad4-114">下列程式碼範例會顯示回呼物件上的 <xref:System.ServiceModel.CallbackBehaviorAttribute> 類別，這個類別會使用 <xref:System.Threading.SynchronizationContext> 物件來判斷要封送處理的執行緒、使用 <xref:System.ServiceModel.CallbackBehaviorAttribute.ValidateMustUnderstand%2A> 屬性以強制執行訊息驗證，並使用 <xref:System.ServiceModel.CallbackBehaviorAttribute.IncludeExceptionDetailInFaults%2A> 屬性將例外狀況當做 <xref:System.ServiceModel.FaultException> 物件傳回服務以進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="afad4-114">The following code example shows a <xref:System.ServiceModel.CallbackBehaviorAttribute> class on a callback object that uses the <xref:System.Threading.SynchronizationContext> object to determine the thread to marshal to, the <xref:System.ServiceModel.CallbackBehaviorAttribute.ValidateMustUnderstand%2A> property to enforce message validation, and the <xref:System.ServiceModel.CallbackBehaviorAttribute.IncludeExceptionDetailInFaults%2A> property to return exceptions as <xref:System.ServiceModel.FaultException> objects to the service for debugging purposes.</span></span>  
  
 [!code-csharp[CallbackBehaviorAttribute#3](../../../samples/snippets/csharp/VS_Snippets_CFX/callbackbehaviorattribute/cs/client.cs#3)]
 [!code-vb[CallbackBehaviorAttribute#3](../../../samples/snippets/visualbasic/VS_Snippets_CFX/callbackbehaviorattribute/vb/client.vb#3)]  
  
## <a name="using-callbackdebugbehavior-to-enable-the-flow-of-managed-exception-information"></a><span data-ttu-id="afad4-115">使用 CallbackDebugBehavior 啟用 Managed 例外狀況資訊的流動</span><span class="sxs-lookup"><span data-stu-id="afad4-115">Using CallbackDebugBehavior to Enable the Flow of Managed Exception Information</span></span>  

 <span data-ttu-id="afad4-116">如果您以程式設計方式或從應用程式組態檔將 <xref:System.ServiceModel.Description.CallbackDebugBehavior.IncludeExceptionDetailInFaults%2A> 屬性設定為 `true`，則可以讓用戶端回呼物件中的 Managed 例外狀況資訊的流動回到服務，以達偵錯的目的。</span><span class="sxs-lookup"><span data-stu-id="afad4-116">You can enable the flow of managed exception information in a client callback object back to the service for debugging purposes by setting the <xref:System.ServiceModel.Description.CallbackDebugBehavior.IncludeExceptionDetailInFaults%2A> property to `true` either programmatically or from an application configuration file.</span></span>  
  
 <span data-ttu-id="afad4-117">將 Managed 例外狀況資訊傳回服務可能導致安全性風險，因為例外狀況詳細資料會公開未授權的服務可使用的內部用戶端實作相關資訊。</span><span class="sxs-lookup"><span data-stu-id="afad4-117">Returning managed exception information to services can be a security risk because exception details expose information about the internal client implementation that  unauthorized services could use.</span></span> <span data-ttu-id="afad4-118">此外，雖然也能以程式設計方式設定 <xref:System.ServiceModel.Description.CallbackDebugBehavior> 屬性，不過在部署時很容易會忘記停用 <xref:System.ServiceModel.Description.CallbackDebugBehavior.IncludeExceptionDetailInFaults%2A>。</span><span class="sxs-lookup"><span data-stu-id="afad4-118">In addition, although the <xref:System.ServiceModel.Description.CallbackDebugBehavior> properties can also be set programmatically, it can be easy to forget to disable <xref:System.ServiceModel.Description.CallbackDebugBehavior.IncludeExceptionDetailInFaults%2A> when deploying.</span></span>  
  
 <span data-ttu-id="afad4-119">由於牽涉到安全性議題，我們強烈建議您：</span><span class="sxs-lookup"><span data-stu-id="afad4-119">Because of the security issues involved, it is strongly recommended that:</span></span>  
  
- <span data-ttu-id="afad4-120">使用應用程式的組態檔將 <xref:System.ServiceModel.Description.CallbackDebugBehavior.IncludeExceptionDetailInFaults%2A> 屬性的值設定為 `true`。</span><span class="sxs-lookup"><span data-stu-id="afad4-120">You use an application configuration file to set the value of the <xref:System.ServiceModel.Description.CallbackDebugBehavior.IncludeExceptionDetailInFaults%2A> property to `true`.</span></span>  
  
- <span data-ttu-id="afad4-121">您只能在受控制的偵錯狀況下這樣做。</span><span class="sxs-lookup"><span data-stu-id="afad4-121">You do so only in controlled debugging scenarios.</span></span>  
  
 <span data-ttu-id="afad4-122">下列程式碼範例示範的用戶端設定檔，會指示 WCF 從 SOAP 訊息中的用戶端回呼物件傳回 managed 例外狀況資訊。</span><span class="sxs-lookup"><span data-stu-id="afad4-122">The following code example shows a client configuration file that instructs WCF to return managed exception information from a client callback object in SOAP messages.</span></span>  
  
 [!code-xml[SCA.CallbackContract#4](../../../samples/snippets/csharp/VS_Snippets_CFX/sca.callbackcontract/cs/client.exe.config#4)]  

## <a name="using-the-clientviabehavior-behavior"></a><span data-ttu-id="afad4-123">使用 ClientViaBehavior 行為</span><span class="sxs-lookup"><span data-stu-id="afad4-123">Using the ClientViaBehavior Behavior</span></span>  

 <span data-ttu-id="afad4-124">您可以使用 <xref:System.ServiceModel.Description.ClientViaBehavior> 行為，對應該建立的傳輸通道指定統一資源識別項。</span><span class="sxs-lookup"><span data-stu-id="afad4-124">You can use the <xref:System.ServiceModel.Description.ClientViaBehavior> behavior to specify the Uniform Resource Identifier for which the transport channel should be created.</span></span> <span data-ttu-id="afad4-125">當立即網路目的不是訊息的預期處理器時，請使用這個行為。</span><span class="sxs-lookup"><span data-stu-id="afad4-125">Use this behavior when the immediate network destination is not the intended processor of the message.</span></span> <span data-ttu-id="afad4-126">當呼叫應用程式不需要知道最終目的，或者目的 `Via` 標頭不是位址時，這個行為可啟用多重躍點交談。</span><span class="sxs-lookup"><span data-stu-id="afad4-126">This enables multiple-hop conversations when the calling application does not necessarily know the ultimate destination or when the destination `Via` header is not an address.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="afad4-127">另請參閱</span><span class="sxs-lookup"><span data-stu-id="afad4-127">See also</span></span>

- [<span data-ttu-id="afad4-128">指定服務執行階段行為</span><span class="sxs-lookup"><span data-stu-id="afad4-128">Specifying Service Run-Time Behavior</span></span>](specifying-service-run-time-behavior.md)
