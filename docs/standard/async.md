---
title: 非同步總覽
description: 了解非同步程式設計此一重要技術，如何讓您更容易處理對多個核心的封鎖 I/O 和並行作業。
author: cartermp
ms.author: wiwagn
ms.date: 06/20/2016
ms.assetid: 1e38e9d9-8284-46ee-a15f-199adc4f26f4
ms.openlocfilehash: 495f225a3732812666dfa2f5c8c07f6f5b849c95
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94824801"
---
# <a name="async-overview"></a><span data-ttu-id="f7da3-103">非同步總覽</span><span class="sxs-lookup"><span data-stu-id="f7da3-103">Async Overview</span></span>

<span data-ttu-id="f7da3-104">不久之前，只要購買較新的電腦或伺服器，應用程式的執行速度就會更快，然後逐漸停止。</span><span class="sxs-lookup"><span data-stu-id="f7da3-104">Not so long ago, apps got faster simply by buying a newer PC or server and then that trend stopped.</span></span> <span data-ttu-id="f7da3-105">這事實上相反。</span><span class="sxs-lookup"><span data-stu-id="f7da3-105">In fact, it reversed.</span></span> <span data-ttu-id="f7da3-106">具有 1ghz 單一核心 ARM 晶片和伺服器工作負載的行動電話已轉換為 VM。</span><span class="sxs-lookup"><span data-stu-id="f7da3-106">Mobile phones appeared with 1ghz single core ARM chips and server workloads transitioned to VMs.</span></span> <span data-ttu-id="f7da3-107">使用者仍然想要回應式 UI，而且企業擁有者想要擁有隨其業務調整的伺服器。</span><span class="sxs-lookup"><span data-stu-id="f7da3-107">Users still want responsive UI and business owners want servers that scale with their business.</span></span> <span data-ttu-id="f7da3-108">行動和雲端以及已連接網際網路母體 >3B 使用者的轉換已導致新的一組軟體模式。</span><span class="sxs-lookup"><span data-stu-id="f7da3-108">The transition to mobile and cloud and an internet-connected population of >3B users has resulted in a new set of software patterns.</span></span>

- <span data-ttu-id="f7da3-109">用戶端應用程式應該一律啟動、一律連線，並持續回應使用者互動 (例如觸控)，而且在應用程式市集具有高評價！</span><span class="sxs-lookup"><span data-stu-id="f7da3-109">Client applications are expected to be always-on, always-connected and constantly responsive to user interaction (for example, touch) with high app store ratings!</span></span>
- <span data-ttu-id="f7da3-110">服務應該透過正常相應增加和相應減少來處理流量暴增情況。</span><span class="sxs-lookup"><span data-stu-id="f7da3-110">Services are expected to handle spikes in traffic by gracefully scaling up and down.</span></span>

<span data-ttu-id="f7da3-111">非同步程式設計是一項重要技術，可讓您更容易處理對多個核心的封鎖 I/O 和並行作業。</span><span class="sxs-lookup"><span data-stu-id="f7da3-111">Async programming is a key technique that makes it straightforward to handle blocking I/O and concurrent operations on multiple cores.</span></span> <span data-ttu-id="f7da3-112">.NET 提供的功能可讓應用程式和服務透過簡單易用的語言層級非同步程式設計模型，以 c #、Visual Basic 和 F # 進行回應和彈性。</span><span class="sxs-lookup"><span data-stu-id="f7da3-112">.NET provides the capability for apps and services to be responsive and elastic with easy-to-use, language-level asynchronous programming models in C#, Visual Basic, and F#.</span></span>

## <a name="why-write-async-code"></a><span data-ttu-id="f7da3-113">為什麼撰寫非同步程式碼？</span><span class="sxs-lookup"><span data-stu-id="f7da3-113">Why Write Async Code?</span></span>

<span data-ttu-id="f7da3-114">現代應用程式大量使用檔案和網路 I/O。</span><span class="sxs-lookup"><span data-stu-id="f7da3-114">Modern apps make extensive use of file and networking I/O.</span></span> <span data-ttu-id="f7da3-115">除非您想要學習和使用具挑戰性的模式，否則 I/O API 傳統上預設會進行封鎖，進而導致不佳的使用者經驗和硬體使用。</span><span class="sxs-lookup"><span data-stu-id="f7da3-115">I/O APIs traditionally block by default, resulting in poor user experiences and hardware utilization unless you want to learn and use challenging patterns.</span></span> <span data-ttu-id="f7da3-116">工作架構非同步 API 和語言層級非同步程式設計模型則與此模型相反，只要學習幾個新的概念就可讓非同步執行成為預設值。</span><span class="sxs-lookup"><span data-stu-id="f7da3-116">Task-based async APIs and the language-level asynchronous programming model invert this model, making async execution the default with few new concepts to learn.</span></span>

<span data-ttu-id="f7da3-117">非同步程式碼具有下列特性：</span><span class="sxs-lookup"><span data-stu-id="f7da3-117">Async code has the following characteristics:</span></span>

- <span data-ttu-id="f7da3-118">處理更多的伺服器要求，方法是在等候傳回 I/O 要求時產生執行緒以處理更多的要求。</span><span class="sxs-lookup"><span data-stu-id="f7da3-118">Handles more server requests by yielding threads to handle more requests while waiting for I/O requests to return.</span></span>
- <span data-ttu-id="f7da3-119">讓 UI 更具回應性，方法是在等候 I/O 要求時產生 UI 互動的執行緒，以及將長時間執行的工作轉換成其他 CPU 核心。</span><span class="sxs-lookup"><span data-stu-id="f7da3-119">Enables UIs to be more responsive by yielding threads to UI interaction while waiting for I/O requests and by transitioning long-running work to other CPU cores.</span></span>
- <span data-ttu-id="f7da3-120">許多較新的 .NET API 都是非同步的。</span><span class="sxs-lookup"><span data-stu-id="f7da3-120">Many of the newer .NET APIs are asynchronous.</span></span>
- <span data-ttu-id="f7da3-121">輕鬆地在 .NET 中撰寫非同步程式碼！</span><span class="sxs-lookup"><span data-stu-id="f7da3-121">It's easy to write async code in .NET!</span></span>

## <a name="whats-next"></a><span data-ttu-id="f7da3-122">接下來要做什麼？</span><span class="sxs-lookup"><span data-stu-id="f7da3-122">What's next?</span></span>

<span data-ttu-id="f7da3-123">如需詳細資訊，請參閱[深入了解非同步](async-in-depth.md)主題。</span><span class="sxs-lookup"><span data-stu-id="f7da3-123">For more information, see the [Async in depth](async-in-depth.md) topic.</span></span>

<span data-ttu-id="f7da3-124">[非同步程式設計模式](asynchronous-programming-patterns/index.md)主題概述 .NET 中所支援的三個非同步程式設計模式：</span><span class="sxs-lookup"><span data-stu-id="f7da3-124">The [Asynchronous Programming Patterns](asynchronous-programming-patterns/index.md) topic provides an overview of the three asynchronous programming patterns supported in .NET:</span></span>  
  
- <span data-ttu-id="f7da3-125">[非同步程式設計模型 (APM)](asynchronous-programming-patterns/asynchronous-programming-model-apm.md) (舊版)</span><span class="sxs-lookup"><span data-stu-id="f7da3-125">[Asynchronous Programming Model (APM)](asynchronous-programming-patterns/asynchronous-programming-model-apm.md) (legacy)</span></span>  
  
- <span data-ttu-id="f7da3-126">[事件架構非同步模式 (EAP)](asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md) (舊版)</span><span class="sxs-lookup"><span data-stu-id="f7da3-126">[Event-based Asynchronous Pattern (EAP)](asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md) (legacy)</span></span>  
  
- <span data-ttu-id="f7da3-127">[工作架構非同步模式 (TAP)](asynchronous-programming-patterns/task-based-asynchronous-pattern-tap.md) (新的開發建議)</span><span class="sxs-lookup"><span data-stu-id="f7da3-127">[Task-based Asynchronous Pattern (TAP)](asynchronous-programming-patterns/task-based-asynchronous-pattern-tap.md) (recommended for new development)</span></span>  

<span data-ttu-id="f7da3-128">如需建議且以工作為基礎之程式設計模型的詳細資訊，請參閱[以工作為基礎的非同步程式設計](parallel-programming/task-based-asynchronous-programming.md)主題。</span><span class="sxs-lookup"><span data-stu-id="f7da3-128">For more information about recommended task-based programming model, see the [Task-based asynchronous programming](parallel-programming/task-based-asynchronous-programming.md) topic.</span></span>
