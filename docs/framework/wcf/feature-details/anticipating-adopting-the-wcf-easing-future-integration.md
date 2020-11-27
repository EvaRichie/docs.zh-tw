---
title: 預計採用 Windows Communication Foundation：簡化未來整合
ms.date: 03/30/2017
ms.assetid: 3028bba8-6355-4ee0-9ecd-c56e614cb474
ms.openlocfilehash: ead28354a3687bcca22a1a0eb5ccc9f15f0c69d2
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96266567"
---
# <a name="anticipating-adopting-the-windows-communication-foundation-easing-future-integration"></a><span data-ttu-id="7fc09-102">預計採用 Windows Communication Foundation：簡化未來整合</span><span class="sxs-lookup"><span data-stu-id="7fc09-102">Anticipating Adopting the Windows Communication Foundation: Easing Future Integration</span></span>

<span data-ttu-id="7fc09-103">如果您目前使用 ASP.NET，並預計在未來使用 WCF，本主題會提供指導方針，以確保新的 ASP.NET Web 服務能搭配 WCF 應用程式一起運作。</span><span class="sxs-lookup"><span data-stu-id="7fc09-103">If you use ASP.NET today, and anticipate using WCF in the future, this topic provides guidance to ensure that new ASP.NET Web services will work well together with WCF applications.</span></span>  
  
## <a name="general-recommendations"></a><span data-ttu-id="7fc09-104">一般建議</span><span class="sxs-lookup"><span data-stu-id="7fc09-104">General Recommendations</span></span>  

 <span data-ttu-id="7fc09-105">任何新服務都採用 ASP.NET 2.0。</span><span class="sxs-lookup"><span data-stu-id="7fc09-105">Adopt ASP.NET 2.0 for any new services.</span></span> <span data-ttu-id="7fc09-106">如此一來就能使用新版本的改進與增強功能。</span><span class="sxs-lookup"><span data-stu-id="7fc09-106">Doing so will provide access to the improvements and enhancements of the new version.</span></span> <span data-ttu-id="7fc09-107">不過，它也可讓您在相同應用程式中搭配使用 ASP.NET 2.0 元件和 WCF 元件。</span><span class="sxs-lookup"><span data-stu-id="7fc09-107">However, it will also allow for the possibility of using ASP.NET 2.0 components together with WCF components in the same application.</span></span>  
  
## <a name="protocols"></a><span data-ttu-id="7fc09-108">通訊協定</span><span class="sxs-lookup"><span data-stu-id="7fc09-108">Protocols</span></span>  

 <span data-ttu-id="7fc09-109">使用 ASP.NET 2.0 的新功能以驗證是否符合 WS-I Basic Profile 1.1：</span><span class="sxs-lookup"><span data-stu-id="7fc09-109">Use ASP.NET 2.0’s new facility for validating conformity to the WS-I Basic Profile 1.1:</span></span>  
  
```csharp  
[WebService(Namespace = "http://tempuri.org/")]  
[WebServiceBinding(  
     ConformsTo = WsiProfiles.BasicProfile1_1,  
     EmitConformanceClaims=true)]  
public interface IEcho  
```  
  
 <span data-ttu-id="7fc09-110">符合 WS-I Basic Profile 1.1 的 ASP.NET Web 服務將會使用 WCF 預先定義系結，與 WCF 用戶端互通 <xref:System.ServiceModel.BasicHttpBinding> 。</span><span class="sxs-lookup"><span data-stu-id="7fc09-110">ASP.NET Web services that conform to WS-I Basic Profile 1.1 will be interoperable with WCF clients by using WCF predefined binding, <xref:System.ServiceModel.BasicHttpBinding>.</span></span>  
  
## <a name="service-development"></a><span data-ttu-id="7fc09-111">服務開發</span><span class="sxs-lookup"><span data-stu-id="7fc09-111">Service Development</span></span>  

 <span data-ttu-id="7fc09-112">請避免使用 <xref:System.Web.Services.Protocols.SoapDocumentServiceAttribute> 屬性讓訊息不根據 SOAPAction HTTP 標頭而根據 SOAP 訊息的本文元素完整名稱傳送到方法。</span><span class="sxs-lookup"><span data-stu-id="7fc09-112">Avoid using the <xref:System.Web.Services.Protocols.SoapDocumentServiceAttribute> attribute to have messages routed to methods based on the fully-qualified name of the body element of the SOAP message rather than the SOAPAction HTTP header.</span></span> <span data-ttu-id="7fc09-113">WCF 會使用 SOAPAction HTTP 標頭來路由傳送訊息。</span><span class="sxs-lookup"><span data-stu-id="7fc09-113">WCF uses the SOAPAction HTTP header for routing messages.</span></span>  
  
## <a name="data-representation"></a><span data-ttu-id="7fc09-114">資料表示</span><span class="sxs-lookup"><span data-stu-id="7fc09-114">Data Representation</span></span>  

 <span data-ttu-id="7fc09-115">根據預設，<xref:System.Xml.Serialization.XmlSerializer> 序列化型別的目標 XML 在語意上與 <xref:System.Runtime.Serialization.DataContractSerializer> 序列化型別的目標 XML 是一樣的 (前提是 XML 的命名空間已明確定義)。</span><span class="sxs-lookup"><span data-stu-id="7fc09-115">The XML into which <xref:System.Xml.Serialization.XmlSerializer> serializes a type by default is semantically identical to the XML into which the <xref:System.Runtime.Serialization.DataContractSerializer> serializes a type, provided the namespace for the XML is explicitly defined.</span></span> <span data-ttu-id="7fc09-116">當您定義資料類型以便與 ASP.NET Web 服務搭配使用，以預期未來採用 WCF 時，請執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="7fc09-116">When defining a data type for use with ASP.NET Web services in anticipation of adopting WCF in the future, do the following:</span></span>  
  
1. <span data-ttu-id="7fc09-117">使用 .NET Framework 類別，而不是 XML 結構描述來定義型別。</span><span class="sxs-lookup"><span data-stu-id="7fc09-117">Define the type using .NET Framework classes rather than XML Schema.</span></span>  
  
2. <span data-ttu-id="7fc09-118">僅將 <xref:System.SerializableAttribute> 和 <xref:System.Xml.Serialization.XmlRootAttribute> 新增至類別，並使用後者明確定義該型別的命名空間。</span><span class="sxs-lookup"><span data-stu-id="7fc09-118">Add only the <xref:System.SerializableAttribute> and the <xref:System.Xml.Serialization.XmlRootAttribute> to the class, using the latter to explicitly define the namespace for the type.</span></span> <span data-ttu-id="7fc09-119">請勿從 <xref:System.Xml.Serialization> 命名空間新增其他屬性，以控制 .NET Framework 類別轉譯成 XML 的方式。</span><span class="sxs-lookup"><span data-stu-id="7fc09-119">Do no add additional attributes from the <xref:System.Xml.Serialization> namespace to control how the .NET Framework class is to be translated into XML.</span></span>  
  
 <span data-ttu-id="7fc09-120">採用這個方法之後，您稍後應該可以藉由新增 <xref:System.Runtime.Serialization.DataContractAttribute> 和 <xref:System.Runtime.Serialization.DataMemberAttribute>，將 .NET 類別納入資料合約中，而不用特別提醒針對傳輸需要而序列化類別的目標 XML。</span><span class="sxs-lookup"><span data-stu-id="7fc09-120">By adopting this approach, you should be able to later make the .NET classes into data contracts with the addition of the <xref:System.Runtime.Serialization.DataContractAttribute> and <xref:System.Runtime.Serialization.DataMemberAttribute> without significantly altering the XML into which the classes are serialized for transmission.</span></span> <span data-ttu-id="7fc09-121">ASP.NET Web 服務在訊息中使用的型別，可以由 WCF 應用程式當做資料合約來處理，並在其他優點與 WCF 應用程式中更佳的效能之間進行處理。</span><span class="sxs-lookup"><span data-stu-id="7fc09-121">The types used in messages by ASP.NET Web services will be able to be processed as data contracts by WCF applications, yielding, amongst other benefits, better performance in WCF applications.</span></span>  
  
## <a name="security"></a><span data-ttu-id="7fc09-122">安全性</span><span class="sxs-lookup"><span data-stu-id="7fc09-122">Security</span></span>  

 <span data-ttu-id="7fc09-123">請避免使用 Internet Information Services (IIS) 提供的驗證選項。</span><span class="sxs-lookup"><span data-stu-id="7fc09-123">Avoid using the authentication options provided by Internet Information Services (IIS).</span></span> <span data-ttu-id="7fc09-124">WCF 用戶端不支援它們。</span><span class="sxs-lookup"><span data-stu-id="7fc09-124">WCF clients do not support them.</span></span> <span data-ttu-id="7fc09-125">如果需要保護服務，請使用 WCF 提供的選項，因為這些選項更豐富且以標準通訊協定為基礎。</span><span class="sxs-lookup"><span data-stu-id="7fc09-125">If a service needs to be secured, use the options provided by WCF, because these options are richer and are based on standard protocols.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="7fc09-126">另請參閱</span><span class="sxs-lookup"><span data-stu-id="7fc09-126">See also</span></span>

- [<span data-ttu-id="7fc09-127">預計採用 Windows Communication Foundation：簡化未來移轉</span><span class="sxs-lookup"><span data-stu-id="7fc09-127">Anticipating Adopting the Windows Communication Foundation: Easing Future Migration</span></span>](anticipating-adopting-wcf-migration.md)
