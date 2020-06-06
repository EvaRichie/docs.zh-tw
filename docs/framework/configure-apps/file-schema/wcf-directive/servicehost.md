---
title: '@ServiceHost'
ms.date: 03/30/2017
ms.assetid: 96ba6967-00f2-422f-9aa7-15de4d33ebf3
ms.openlocfilehash: fdd6d83836c4ef31a4d7c8e68cb0cc050ac6bea4
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "76787793"
---
# <a name="servicehost"></a><span data-ttu-id="03fd2-101">\@ServiceHost</span><span class="sxs-lookup"><span data-stu-id="03fd2-101">\@ServiceHost</span></span>

<span data-ttu-id="03fd2-102">將用來產生服務主機的處理站，與要裝載的服務和存取或編譯 .svc 檔案中提供的程式碼所需的其他程式設計方面加以關聯。</span><span class="sxs-lookup"><span data-stu-id="03fd2-102">Associates the factory used to produce the service host with the service to be hosted and other programming aspects required to access or compile the hosting code provided in the .svc file.</span></span>

## <a name="syntax"></a><span data-ttu-id="03fd2-103">語法</span><span class="sxs-lookup"><span data-stu-id="03fd2-103">Syntax</span></span>

```xml
<% @ServiceHost
Service = "Service, ServiceNamespace"
Factory = "Factory, FactoryNamespace"
Debug = "Debug"
Language = "Language"
CodeBehind = "CodeBehind"
%>
```

## <a name="attributes"></a><span data-ttu-id="03fd2-104">屬性</span><span class="sxs-lookup"><span data-stu-id="03fd2-104">Attributes</span></span>

### <a name="service"></a><span data-ttu-id="03fd2-105">Service</span><span class="sxs-lookup"><span data-stu-id="03fd2-105">Service</span></span>

<span data-ttu-id="03fd2-106">所裝載之服務的 CLR 型別名稱。</span><span class="sxs-lookup"><span data-stu-id="03fd2-106">The CLR type name of the service hosted.</span></span> <span data-ttu-id="03fd2-107">這應該是實作一個以上的服務合約之型別的限定名稱。</span><span class="sxs-lookup"><span data-stu-id="03fd2-107">This should be a qualified name of a type that implements one or more of the service contacts.</span></span>

### <a name="factory"></a><span data-ttu-id="03fd2-108">Factory</span><span class="sxs-lookup"><span data-stu-id="03fd2-108">Factory</span></span>

<span data-ttu-id="03fd2-109">用來具現化服務主機的服務主機處理站之 CLR 型別名稱。</span><span class="sxs-lookup"><span data-stu-id="03fd2-109">The CLR type name of the service host factory used to instantiate the service host.</span></span> <span data-ttu-id="03fd2-110">這是一個選擇性的屬性。</span><span class="sxs-lookup"><span data-stu-id="03fd2-110">This attribute is optional.</span></span> <span data-ttu-id="03fd2-111">如果沒有指定，則使用預設的 <xref:System.ServiceModel.Activation.ServiceHostFactory>，它會傳回 <xref:System.ServiceModel.ServiceHost> 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="03fd2-111">If unspecified, the default <xref:System.ServiceModel.Activation.ServiceHostFactory> is used, which returns an instance of <xref:System.ServiceModel.ServiceHost>.</span></span>

### <a name="debug"></a><span data-ttu-id="03fd2-112">偵錯</span><span class="sxs-lookup"><span data-stu-id="03fd2-112">Debug</span></span>

<span data-ttu-id="03fd2-113">指出是否應該使用 debug 符號來編譯 Windows Communication Foundation （WCF）服務。</span><span class="sxs-lookup"><span data-stu-id="03fd2-113">Indicates whether the Windows Communication Foundation (WCF) service should be compiled with debug symbols.</span></span> <span data-ttu-id="03fd2-114">`true`如果 WCF 服務應使用 debug 符號進行編譯，則為，否則為 `false` 。</span><span class="sxs-lookup"><span data-stu-id="03fd2-114">`true` if the WCF service should be compiled with debug symbols; otherwise, `false`.</span></span>

### <a name="language"></a><span data-ttu-id="03fd2-115">Language</span><span class="sxs-lookup"><span data-stu-id="03fd2-115">Language</span></span>

<span data-ttu-id="03fd2-116">指定編譯檔案內 (.svc) 所有內嵌程式碼時使用的語言。</span><span class="sxs-lookup"><span data-stu-id="03fd2-116">Specifies the language used when compiling all the inline code within file (.svc).</span></span> <span data-ttu-id="03fd2-117">值可以代表任何。NET 支援的語言，包括 `C#` 、 `VB` 和 `JS` ，分別參考 c #、Visual Basic 和 JScript .net。</span><span class="sxs-lookup"><span data-stu-id="03fd2-117">The values can represent any .NET-supported language, including `C#`, `VB`, and `JS`, which refer to C#, Visual Basic, and JScript .NET, respectively.</span></span> <span data-ttu-id="03fd2-118">這是一個選擇性的屬性。</span><span class="sxs-lookup"><span data-stu-id="03fd2-118">This attribute is optional.</span></span>

### <a name="codebehind"></a><span data-ttu-id="03fd2-119">CodeBehind</span><span class="sxs-lookup"><span data-stu-id="03fd2-119">CodeBehind</span></span>

<span data-ttu-id="03fd2-120">當實 XML Web Service 的類別不存在於相同的檔案中，而且尚未編譯成元件並放在*\bin*目錄中時，指定用來執行 XML Web Service 的原始程式檔。</span><span class="sxs-lookup"><span data-stu-id="03fd2-120">Specifies the source file that implements the XML Web service, when the class that implements the XML Web service does not reside in the same file and has not been compiled into an assembly and placed in the *\Bin* directory.</span></span>

## <a name="remarks"></a><span data-ttu-id="03fd2-121">備註</span><span class="sxs-lookup"><span data-stu-id="03fd2-121">Remarks</span></span>

<span data-ttu-id="03fd2-122"><xref:System.ServiceModel.ServiceHost>用來裝載服務的是 Windows Communication Foundation （WCF）程式設計模型內的擴充性點。</span><span class="sxs-lookup"><span data-stu-id="03fd2-122">The <xref:System.ServiceModel.ServiceHost> used to host the service is a point of extensibility within the Windows Communication Foundation (WCF) programming model.</span></span> <span data-ttu-id="03fd2-123">因為 <xref:System.ServiceModel.ServiceHost> 是潛在的多型型別，而裝載環境不應直接具現化多型型別，所以使用處理站模式加以具現化。</span><span class="sxs-lookup"><span data-stu-id="03fd2-123">A factory pattern is used to instantiate the <xref:System.ServiceModel.ServiceHost> because it is, potentially, a polymorphic type that the hosting environment should not instantiate directly.</span></span>

<span data-ttu-id="03fd2-124">預設實作會使用 <xref:System.ServiceModel.Activation.ServiceHostFactory> 來建立 <xref:System.ServiceModel.ServiceHost> 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="03fd2-124">The default implementation uses <xref:System.ServiceModel.Activation.ServiceHostFactory> to create an instance of <xref:System.ServiceModel.ServiceHost>.</span></span> <span data-ttu-id="03fd2-125">但是，您可以藉由在指示詞中指定 factory 的 CLR 型別名稱，來提供您自己的處理站（一個傳回您的衍生主機） `@ServiceHost` 。</span><span class="sxs-lookup"><span data-stu-id="03fd2-125">But you can provide your own factory (one that returns your derived host) by specifying the CLR type name of your factory implementation in the `@ServiceHost` directive.</span></span>

<span data-ttu-id="03fd2-126">若要使用您自己的自訂服務主機 factory，而不是預設的 factory，只要在指示詞中提供型別名稱，如下所示 `@ServiceHost` 。</span><span class="sxs-lookup"><span data-stu-id="03fd2-126">To use you own custom service host factory instead of the default factory, just provide the type name in the `@ServiceHost` directive as follows.</span></span>

```xml
<% @ServiceHost Factory="DerivedFactory" Service="MyService" %>
```

<span data-ttu-id="03fd2-127">盡可能保持處理站實作的簡便。</span><span class="sxs-lookup"><span data-stu-id="03fd2-127">Keep the factory implementations as light as possible.</span></span> <span data-ttu-id="03fd2-128">假設您有許多自訂邏輯，那麼若您將邏輯放在主機而非處理站內，則這些程式碼就更能重複使用。</span><span class="sxs-lookup"><span data-stu-id="03fd2-128">If you have lots of custom logic, your code is more reusable if you put that logic inside your host instead of inside the factory.</span></span>

<span data-ttu-id="03fd2-129">例如，若要啟用已啟用 AJAX 的端點 `MyService` ，請 <xref:System.ServiceModel.Activation.WebScriptServiceHostFactory> 在指示詞中指定屬性值的， `Factory` 而不是預設的（ <xref:System.ServiceModel.Activation.ServiceHostFactory> `@ServiceHost` 如下列範例所示）：</span><span class="sxs-lookup"><span data-stu-id="03fd2-129">For example, to enable an AJAX-enabled endpoint for `MyService`, specify the <xref:System.ServiceModel.Activation.WebScriptServiceHostFactory> for the value of the `Factory` attribute, instead of the default <xref:System.ServiceModel.Activation.ServiceHostFactory>, in the `@ServiceHost` directive as shown in the following example:</span></span>

```xml
<% @ServiceHost
Service="MyService"
Language="C#"
Debug="true"
Factory="WebScriptServiceHostFactory"
%>
```

## <a name="see-also"></a><span data-ttu-id="03fd2-130">另請參閱</span><span class="sxs-lookup"><span data-stu-id="03fd2-130">See also</span></span>

- [<span data-ttu-id="03fd2-131">自訂服務裝載</span><span class="sxs-lookup"><span data-stu-id="03fd2-131">Custom Service Host</span></span>](../../../wcf/samples/custom-service-host.md)
