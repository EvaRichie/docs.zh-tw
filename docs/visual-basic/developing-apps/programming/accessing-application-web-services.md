---
title: 存取應用程式 Web 服務
ms.date: 07/20/2015
helpviewer_keywords:
- Web services [Visual Basic], My.WebServices object
- My.WebServices object
- applications [Visual Basic], Web services
ms.assetid: 8ad5405b-e771-42b1-82d3-ce97af2cea9e
ms.openlocfilehash: cf9a0c9840b9228b59af9959cf3a4efb9a1d1ea0
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410188"
---
# <a name="accessing-application-web-services-visual-basic"></a><span data-ttu-id="c6687-102">存取應用程式 Web 服務 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="c6687-102">Accessing Application Web Services (Visual Basic)</span></span>

<span data-ttu-id="c6687-103">`My.WebServices` 物件會提供目前專案所參考之每個 Web 服務的執行個體。</span><span class="sxs-lookup"><span data-stu-id="c6687-103">The `My.WebServices` object provides an instance of each Web service referenced by the current project.</span></span> <span data-ttu-id="c6687-104">每個執行個體都是依需要具現化。</span><span class="sxs-lookup"><span data-stu-id="c6687-104">Each instance is instantiated on demand.</span></span> <span data-ttu-id="c6687-105">您可以透過 `My.WebServices` 物件的屬性來存取這些 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="c6687-105">You can access these Web services through the properties of the `My.WebServices` object.</span></span> <span data-ttu-id="c6687-106">屬性名稱和屬性存取的 Web 服務名稱相同。</span><span class="sxs-lookup"><span data-stu-id="c6687-106">The name of the property is the same as the name of the Web service that the property accesses.</span></span> <span data-ttu-id="c6687-107">任何繼承自 <xref:System.Web.Services.Protocols.SoapHttpClientProtocol> 的類別都是 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="c6687-107">Any class that inherits from <xref:System.Web.Services.Protocols.SoapHttpClientProtocol> is a Web service.</span></span>

## <a name="tasks"></a><span data-ttu-id="c6687-108">工作</span><span class="sxs-lookup"><span data-stu-id="c6687-108">Tasks</span></span>

<span data-ttu-id="c6687-109">下表列出存取應用程式所參考之 Web 服務的可能方式。</span><span class="sxs-lookup"><span data-stu-id="c6687-109">The following table lists possible ways to access Web services referenced by an application.</span></span>

|<span data-ttu-id="c6687-110">至</span><span class="sxs-lookup"><span data-stu-id="c6687-110">To</span></span>|<span data-ttu-id="c6687-111">請參閱</span><span class="sxs-lookup"><span data-stu-id="c6687-111">See</span></span>|
|---|---|
|<span data-ttu-id="c6687-112">呼叫 Web 服務</span><span class="sxs-lookup"><span data-stu-id="c6687-112">Call a Web service</span></span>|[<span data-ttu-id="c6687-113">My.WebServices 物件</span><span class="sxs-lookup"><span data-stu-id="c6687-113">My.WebServices Object</span></span>](../../language-reference/objects/my-webservices-object.md)|
|<span data-ttu-id="c6687-114">以非同步方式呼叫 Web 服務並於完成時處理事件</span><span class="sxs-lookup"><span data-stu-id="c6687-114">Call a Web service asynchronously and handle an event when it completes</span></span>|[<span data-ttu-id="c6687-115">作法：非同步呼叫 Web 服務</span><span class="sxs-lookup"><span data-stu-id="c6687-115">How to: Call a Web Service Asynchronously</span></span>](how-to-call-a-web-service-asynchronously.md)|

## <a name="see-also"></a><span data-ttu-id="c6687-116">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c6687-116">See also</span></span>

- [<span data-ttu-id="c6687-117">My.WebServices 物件</span><span class="sxs-lookup"><span data-stu-id="c6687-117">My.WebServices Object</span></span>](../../language-reference/objects/my-webservices-object.md)
