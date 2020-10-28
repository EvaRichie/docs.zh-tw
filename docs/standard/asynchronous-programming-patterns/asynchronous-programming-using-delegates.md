---
title: 使用委派非同步設計程式
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- BeginInvoke method
- asynchronous programming, delegates
- asynchronous delegates
- calling synchronous methods in asynchronous manner
- EndInvoke method
- calling asynchronous methods
- delegates [.NET], asynchronous
- synchronous calling in asynchronous manner
ms.assetid: 38a345ca-6963-4436-9608-5c9defef9c64
ms.openlocfilehash: 05e574536abe4eac823b7b74369f5b191724e5b5
ms.sourcegitcommit: 4a938327bad8b2e20cabd0f46a9dc50882596f13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/28/2020
ms.locfileid: "92889253"
---
# <a name="asynchronous-programming-using-delegates"></a><span data-ttu-id="5741c-102">使用委派非同步設計程式</span><span class="sxs-lookup"><span data-stu-id="5741c-102">Asynchronous Programming Using Delegates</span></span>

<span data-ttu-id="5741c-103">委派可讓您以非同步方式呼叫同步方法。</span><span class="sxs-lookup"><span data-stu-id="5741c-103">Delegates enable you to call a synchronous method in an asynchronous manner.</span></span> <span data-ttu-id="5741c-104">當您同步呼叫委派時，`Invoke` 方法會在目前的執行緒上直接呼叫目標方法。</span><span class="sxs-lookup"><span data-stu-id="5741c-104">When you call a delegate synchronously, the `Invoke` method calls the target method directly on the current thread.</span></span> <span data-ttu-id="5741c-105">如果呼叫 `BeginInvoke` 方法，通用語言執行平台 (CLR) 會將要求排入佇列，並立即返回呼叫端。</span><span class="sxs-lookup"><span data-stu-id="5741c-105">If the `BeginInvoke` method is called, the common language runtime (CLR) queues the request and returns immediately to the caller.</span></span> <span data-ttu-id="5741c-106">在執行緒集區中的執行緒上會非同步呼叫目標方法。</span><span class="sxs-lookup"><span data-stu-id="5741c-106">The target method is called asynchronously on a thread from the thread pool.</span></span> <span data-ttu-id="5741c-107">送出要求的原始執行緒不被佔用，可以繼續與目標方法平行執行。</span><span class="sxs-lookup"><span data-stu-id="5741c-107">The original thread, which submitted the request, is free to continue executing in parallel with the target method.</span></span> <span data-ttu-id="5741c-108">如果已在 `BeginInvoke` 方法呼叫中指定回撥方法，目標方法結束時會呼叫回撥方法。</span><span class="sxs-lookup"><span data-stu-id="5741c-108">If a callback method has been specified in the call to the `BeginInvoke` method, the callback method is called when the target method ends.</span></span> <span data-ttu-id="5741c-109">在回撥方法中，`EndInvoke` 方法會取得傳回值和任何輸入/輸出或僅輸出參數。</span><span class="sxs-lookup"><span data-stu-id="5741c-109">In the callback method, the `EndInvoke` method obtains the return value and any input/output or output-only parameters.</span></span> <span data-ttu-id="5741c-110">如果呼叫 `BeginInvoke` 時未指定回撥方法，則可以從呼叫 `BeginInvoke` 的執行緒呼叫 `EndInvoke`。</span><span class="sxs-lookup"><span data-stu-id="5741c-110">If no callback method is specified when calling `BeginInvoke`, `EndInvoke` can be called from the thread that called `BeginInvoke`.</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="5741c-111">編譯器應該利用由使用者指定的委派簽章，使用 `Invoke`、`BeginInvoke` 和 `EndInvoke` 方法發出委派類別。</span><span class="sxs-lookup"><span data-stu-id="5741c-111">Compilers should emit delegate classes with `Invoke`, `BeginInvoke`, and `EndInvoke` methods using the delegate signature specified by the user.</span></span> <span data-ttu-id="5741c-112">`BeginInvoke` 和 `EndInvoke` 方法應該裝飾為原生。</span><span class="sxs-lookup"><span data-stu-id="5741c-112">The `BeginInvoke` and `EndInvoke` methods should be decorated as native.</span></span> <span data-ttu-id="5741c-113">因為這些方法標示為原生，CLR 會在類別載入時自動提供實作。</span><span class="sxs-lookup"><span data-stu-id="5741c-113">Because these methods are marked as native, the CLR automatically provides the implementation at class load time.</span></span> <span data-ttu-id="5741c-114">載入器可確保不覆寫它們。</span><span class="sxs-lookup"><span data-stu-id="5741c-114">The loader ensures that they are not overridden.</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="5741c-115">本節內容</span><span class="sxs-lookup"><span data-stu-id="5741c-115">In This Section</span></span>  
 [<span data-ttu-id="5741c-116">以非同步的方式呼叫同步方法</span><span class="sxs-lookup"><span data-stu-id="5741c-116">Calling Synchronous Methods Asynchronously</span></span>](calling-synchronous-methods-asynchronously.md)  
 <span data-ttu-id="5741c-117">討論使用委派對一般方法進行非同步呼叫，並提供簡單的程式碼範例，示範等待非同步呼叫返回的四種方式。</span><span class="sxs-lookup"><span data-stu-id="5741c-117">Discusses the use of delegates to make asynchronous calls to ordinary methods, and provides simple code examples that show the four ways to wait for an asynchronous call to return.</span></span>  
  
## <a name="related-sections"></a><span data-ttu-id="5741c-118">相關章節</span><span class="sxs-lookup"><span data-stu-id="5741c-118">Related Sections</span></span>  
 [<span data-ttu-id="5741c-119">事件架構非同步模式 (EAP)</span><span class="sxs-lookup"><span data-stu-id="5741c-119">Event-based Asynchronous Pattern (EAP)</span></span>](event-based-asynchronous-pattern-eap.md)  
 <span data-ttu-id="5741c-120">描述 .NET 中的非同步程式設計。</span><span class="sxs-lookup"><span data-stu-id="5741c-120">Describes asynchronous programming in .NET.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="5741c-121">另請參閱</span><span class="sxs-lookup"><span data-stu-id="5741c-121">See also</span></span>

- <xref:System.Delegate>
