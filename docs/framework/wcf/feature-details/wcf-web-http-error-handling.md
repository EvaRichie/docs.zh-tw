---
title: WCF Web HTTP 錯誤處理
ms.date: 03/30/2017
ms.assetid: 02891563-0fce-4c32-84dc-d794b1a5c040
ms.openlocfilehash: cfbf98c69370764a9526c32459d43521177476e3
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96239025"
---
# <a name="wcf-web-http-error-handling"></a><span data-ttu-id="624d7-102">WCF Web HTTP 錯誤處理</span><span class="sxs-lookup"><span data-stu-id="624d7-102">WCF Web HTTP Error Handling</span></span>

<span data-ttu-id="624d7-103">Windows Communication Foundation (WCF) Web HTTP 錯誤處理可讓您從 WCF Web HTTP 服務傳回錯誤，這些服務會指定 HTTP 狀態碼，並使用與作業相同的格式傳回錯誤詳細資料 (例如 XML 或 JSON) 。</span><span class="sxs-lookup"><span data-stu-id="624d7-103">Windows Communication Foundation (WCF) Web HTTP error handling enables you to return errors from WCF Web HTTP services that specify an HTTP status code and return error details using the same format as the operation (for example, XML or JSON).</span></span>  
  
## <a name="wcf-web-http-error-handling"></a><span data-ttu-id="624d7-104">WCF Web HTTP 錯誤處理</span><span class="sxs-lookup"><span data-stu-id="624d7-104">WCF Web HTTP Error Handling</span></span>  

 <span data-ttu-id="624d7-105"><xref:System.ServiceModel.Web.WebFaultException> 類別會定義一個建構函式，供您指定 HTTP 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="624d7-105">The <xref:System.ServiceModel.Web.WebFaultException> class defines a constructor that allows you to specify an HTTP status code.</span></span> <span data-ttu-id="624d7-106">然後，這個狀態碼會傳回用戶端。</span><span class="sxs-lookup"><span data-stu-id="624d7-106">This status code is then returned to the client.</span></span> <span data-ttu-id="624d7-107"><xref:System.ServiceModel.Web.WebFaultException> 類別的泛型版本 <xref:System.ServiceModel.Web.WebFaultException%601> 可讓您傳回使用者定義的型別，其中包含已發生錯誤的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="624d7-107">A generic version of the <xref:System.ServiceModel.Web.WebFaultException> class, <xref:System.ServiceModel.Web.WebFaultException%601> enables you to return a user-defined type that contains information about the error that occurred.</span></span> <span data-ttu-id="624d7-108">此自訂物件會使用作業指定的格式序列化，然後傳回用戶端。</span><span class="sxs-lookup"><span data-stu-id="624d7-108">This custom object is serialized using the format specified by the operation and returned to the client.</span></span> <span data-ttu-id="624d7-109">下列範例示範如何傳回 HTTP 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="624d7-109">The following example shows how to return an HTTP status code.</span></span>  
  
```csharp
public string Operation1()
{
    // Operation logic  
   // ...
   throw new WebFaultException(HttpStatusCode.Forbidden);
}  
```  
  
 <span data-ttu-id="624d7-110">下列範例示範如何傳回 HTTP 狀態碼，以及使用者定義型別中的額外資訊。</span><span class="sxs-lookup"><span data-stu-id="624d7-110">The following example shows how to return an HTTP status code and extra information in a user-defined type.</span></span> <span data-ttu-id="624d7-111">`MyErrorDetail` 是使用者定義的型別，其中包含有關已發生之錯誤的額外資訊。</span><span class="sxs-lookup"><span data-stu-id="624d7-111">`MyErrorDetail` is a user-defined type that contains extra information about the error that occurred.</span></span>  
  
```csharp
public string Operation2()
{
   // Operation logic  
   // ...
   MyErrorDetail detail = new MyErrorDetail()
   {  
      Message = "Error Message",  
      ErrorCode = 123,  
   }  
   throw new WebFaultException<MyErrorDetail>(detail, HttpStatusCode.Forbidden);  
}  
```  
  
 <span data-ttu-id="624d7-112">前一個程式碼會傳回 HTTP 回應，附上禁止狀態碼與本文，而本文中會包含 `MyErrorDetails` 物件的執行個體。</span><span class="sxs-lookup"><span data-stu-id="624d7-112">The preceding code returns an HTTP response with the forbidden status code and a body that contains an instance of the `MyErrorDetails` object.</span></span> <span data-ttu-id="624d7-113">`MyErrorDetails` 物件的格式取決於：</span><span class="sxs-lookup"><span data-stu-id="624d7-113">The format of the `MyErrorDetails` object is determined by:</span></span>  
  
- <span data-ttu-id="624d7-114">服務作業所指定 `ResponseFormat` 或 <xref:System.ServiceModel.Web.WebGetAttribute> 屬性之 <xref:System.ServiceModel.Web.WebInvokeAttribute> 參數的值。</span><span class="sxs-lookup"><span data-stu-id="624d7-114">The value of the `ResponseFormat` parameter of the <xref:System.ServiceModel.Web.WebGetAttribute> or <xref:System.ServiceModel.Web.WebInvokeAttribute> attribute specified on the service operation.</span></span>  
  
- <span data-ttu-id="624d7-115"><xref:System.ServiceModel.Description.WebHttpBehavior.AutomaticFormatSelectionEnabled%2A> 的值。</span><span class="sxs-lookup"><span data-stu-id="624d7-115">The value of <xref:System.ServiceModel.Description.WebHttpBehavior.AutomaticFormatSelectionEnabled%2A>.</span></span>  
  
- <span data-ttu-id="624d7-116">透過存取 <xref:System.ServiceModel.Web.OutgoingWebResponseContext.Format%2A> 之 <xref:System.ServiceModel.Web.OutgoingWebResponseContext> 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="624d7-116">The value of the <xref:System.ServiceModel.Web.OutgoingWebResponseContext.Format%2A> property by accessing the <xref:System.ServiceModel.Web.OutgoingWebResponseContext>.</span></span>  
  
 <span data-ttu-id="624d7-117">如需這些值如何影響作業格式的詳細資訊，請參閱 [WCF WEB HTTP 格式](wcf-web-http-formatting.md)。</span><span class="sxs-lookup"><span data-stu-id="624d7-117">For more information about how these values affect the formatting of the operation, see [WCF Web HTTP Formatting](wcf-web-http-formatting.md).</span></span>  
  
 <span data-ttu-id="624d7-118"><xref:System.ServiceModel.Web.WebFaultException> 是一個 <xref:System.ServiceModel.FaultException>，因此可以針對公開 SOAP 端點以及 Web HTTP 端點的服務，用來當做服務的錯誤例外狀況程式撰寫模型。</span><span class="sxs-lookup"><span data-stu-id="624d7-118"><xref:System.ServiceModel.Web.WebFaultException> is a <xref:System.ServiceModel.FaultException> and therefore can be used as the fault exception programming model for services that expose SOAP endpoints as well as web HTTP endpoints.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="624d7-119">另請參閱</span><span class="sxs-lookup"><span data-stu-id="624d7-119">See also</span></span>

- [<span data-ttu-id="624d7-120">WCF Web HTTP 程式設計模型</span><span class="sxs-lookup"><span data-stu-id="624d7-120">WCF Web HTTP Programming Model</span></span>](wcf-web-http-programming-model.md)
- [<span data-ttu-id="624d7-121">WCF Web HTTP 格式化</span><span class="sxs-lookup"><span data-stu-id="624d7-121">WCF Web HTTP Formatting</span></span>](wcf-web-http-formatting.md)
- [<span data-ttu-id="624d7-122">定義並指定錯誤</span><span class="sxs-lookup"><span data-stu-id="624d7-122">Defining and Specifying Faults</span></span>](../defining-and-specifying-faults.md)
- [<span data-ttu-id="624d7-123">處理例外狀況和錯誤</span><span class="sxs-lookup"><span data-stu-id="624d7-123">Handling Exceptions and Faults</span></span>](../extending/handling-exceptions-and-faults.md)
- [<span data-ttu-id="624d7-124">傳送和接收錯誤</span><span class="sxs-lookup"><span data-stu-id="624d7-124">Sending and Receiving Faults</span></span>](../sending-and-receiving-faults.md)
