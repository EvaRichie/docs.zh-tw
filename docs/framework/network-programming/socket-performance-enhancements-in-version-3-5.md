---
title: 3.5 版中的通訊端效能增強功能
description: 瞭解 .NET Framework 中3.5 版中的系統 .Net Socket 類別的效能改進。
ms.date: 03/30/2017
ms.assetid: 225aa5f9-c54b-4620-ab64-5cd100cfd54c
ms.openlocfilehash: 5bd7c97d6a6edd5f914d6fe3118b6d81b64544e0
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96263135"
---
# <a name="socket-performance-enhancements-in-version-35"></a><span data-ttu-id="21a1a-103">3.5 版中的通訊端效能增強功能</span><span class="sxs-lookup"><span data-stu-id="21a1a-103">Socket Performance Enhancements in Version 3.5</span></span>

<span data-ttu-id="21a1a-104"><xref:System.Net.Sockets.Socket?displayProperty=nameWithType> 類別已經在版本 3.5 中增強，以供使用非同步網路 I/O 的應用程式使用，以達到最高的效能。</span><span class="sxs-lookup"><span data-stu-id="21a1a-104">The <xref:System.Net.Sockets.Socket?displayProperty=nameWithType> class has been enhanced in Version 3.5 for use by applications that use asynchronous network I/O to achieve the highest performance.</span></span> <span data-ttu-id="21a1a-105">一系列新類別已新增在 <xref:System.Net.Sockets.Socket> 類別的一組增強功能當中，提供另一種非同步模式，可供專業化的高效能通訊端應用程式使用。</span><span class="sxs-lookup"><span data-stu-id="21a1a-105">A series of new classes have been added as part of a set of enhancements to the <xref:System.Net.Sockets.Socket> class that provide an alternative asynchronous pattern that can be used by specialized high-performance socket applications.</span></span> <span data-ttu-id="21a1a-106">這些增強功能專為需要高效能的網路伺服器應用程式而設計。</span><span class="sxs-lookup"><span data-stu-id="21a1a-106">These enhancements were specifically designed for network server applications that require high performance.</span></span> <span data-ttu-id="21a1a-107">應用程式可以獨佔方式，使用增強的非同步模式，或是只在其應用程式的目標熱區使用 (例如接收大量資料時)。</span><span class="sxs-lookup"><span data-stu-id="21a1a-107">An application can use the enhanced asynchronous pattern exclusively, or only in targeted hot areas of their application (when receiving large amounts of data, for example).</span></span>  
  
## <a name="class-enhancements"></a><span data-ttu-id="21a1a-108">類別增強功能</span><span class="sxs-lookup"><span data-stu-id="21a1a-108">Class Enhancements</span></span>  

 <span data-ttu-id="21a1a-109">這些增強功能的主要功能是在大量的非同步通訊端 I/O 期間，避免重複配置和同步處理物件。</span><span class="sxs-lookup"><span data-stu-id="21a1a-109">The main feature of these enhancements is the avoidance of the repeated allocation and synchronization of objects during high-volume asynchronous socket I/O.</span></span> <span data-ttu-id="21a1a-110"><xref:System.Net.Sockets.Socket> 類別目前針對非同步通訊端 I/O 所實作的 Begin/End 設計模式，需要為每個非同步通訊端作業配置一個 <xref:System.IAsyncResult?displayProperty=nameWithType> 物件。</span><span class="sxs-lookup"><span data-stu-id="21a1a-110">The Begin/End design pattern currently implemented by the <xref:System.Net.Sockets.Socket> class for asynchronous socket I/O requires a <xref:System.IAsyncResult?displayProperty=nameWithType> object be allocated for each asynchronous socket operation.</span></span>  
  
 <span data-ttu-id="21a1a-111">在新的 <xref:System.Net.Sockets.Socket> 類別增強功能中，應用程式所配置和維護的可重複使用 <xref:System.Net.Sockets.SocketAsyncEventArgs?displayProperty=nameWithType> 類別物件會描述非同步通訊端作業。</span><span class="sxs-lookup"><span data-stu-id="21a1a-111">In the new <xref:System.Net.Sockets.Socket> class enhancements, asynchronous socket operations are described by reusable <xref:System.Net.Sockets.SocketAsyncEventArgs?displayProperty=nameWithType> class objects allocated and maintained by the application.</span></span> <span data-ttu-id="21a1a-112">高效能通訊端應用程式最知道必須維持的重疊通訊端作業量。</span><span class="sxs-lookup"><span data-stu-id="21a1a-112">High-performance socket applications know best the amount of overlapped socket operations that must be sustained.</span></span> <span data-ttu-id="21a1a-113">應用程式可以視需要建立許多 <xref:System.Net.Sockets.SocketAsyncEventArgs> 物件。</span><span class="sxs-lookup"><span data-stu-id="21a1a-113">The application can create as many of the <xref:System.Net.Sockets.SocketAsyncEventArgs> objects that it needs.</span></span> <span data-ttu-id="21a1a-114">例如，如果伺服器應用程式需要隨時有 15 個通訊端接受作業，以支援內送的用戶端連線比率，它可以事先配置 15 個可重複使用的 <xref:System.Net.Sockets.SocketAsyncEventArgs> 物件以用於此用途。</span><span class="sxs-lookup"><span data-stu-id="21a1a-114">For example, if a server application needs to have 15 socket accept operations outstanding at all times to support incoming client connection rates, it can allocate 15 reusable <xref:System.Net.Sockets.SocketAsyncEventArgs> objects in advance for that purpose.</span></span>  
  
 <span data-ttu-id="21a1a-115">以這個類別執行非同步通訊端作業的模式，包含下列步驟：</span><span class="sxs-lookup"><span data-stu-id="21a1a-115">The pattern for performing an asynchronous socket operation with this class consists of the following steps:</span></span>  
  
1. <span data-ttu-id="21a1a-116">配置新 <xref:System.Net.Sockets.SocketAsyncEventArgs> 內容物件，或從應用程式集區取得一個可用的內容物件。</span><span class="sxs-lookup"><span data-stu-id="21a1a-116">Allocate a new <xref:System.Net.Sockets.SocketAsyncEventArgs> context object, or get a free one from an application pool.</span></span>  
  
2. <span data-ttu-id="21a1a-117">將內容物件上的屬性設為即將執行的作業 (例如回呼委派方法和資料緩衝處理)。</span><span class="sxs-lookup"><span data-stu-id="21a1a-117">Set properties on the context object to the operation about to be performed (the callback delegate method and data buffer, for example).</span></span>  
  
3. <span data-ttu-id="21a1a-118">呼叫適當的通訊端方法 (xxxAsync) 來啟始非同步作業。</span><span class="sxs-lookup"><span data-stu-id="21a1a-118">Call the appropriate socket method (xxxAsync) to initiate the asynchronous operation.</span></span>  
  
4. <span data-ttu-id="21a1a-119">如果非同步通訊端方法 (xxxAsync) 在回呼中傳回 true，請查詢內容屬性以取得完成狀態。</span><span class="sxs-lookup"><span data-stu-id="21a1a-119">If the asynchronous socket method (xxxAsync) returns true in the callback, query the context properties for completion status.</span></span>  
  
5. <span data-ttu-id="21a1a-120">如果非同步通訊端方法 (xxxAsync) 在回呼中傳回 false，則作業以同步方式完成。</span><span class="sxs-lookup"><span data-stu-id="21a1a-120">If the asynchronous socket method (xxxAsync) returns false in the callback, the operation completed synchronously.</span></span> <span data-ttu-id="21a1a-121">可以查詢內容屬性以取得作業結果。</span><span class="sxs-lookup"><span data-stu-id="21a1a-121">The context properties may be queried for the operation result.</span></span>  
  
6. <span data-ttu-id="21a1a-122">重複使用內容進行另一個作業、將它放入集區，或是將它捨棄。</span><span class="sxs-lookup"><span data-stu-id="21a1a-122">Reuse the context for another operation, put it back in the pool, or discard it.</span></span>  
  
 <span data-ttu-id="21a1a-123">新非同步通訊端作業內容物件的存留期，取決於應用程式程式碼中的參考和非同步 I/O 參考。</span><span class="sxs-lookup"><span data-stu-id="21a1a-123">The lifetime of the new asynchronous socket operation context object is determined by references in the application code and asynchronous I/O references.</span></span> <span data-ttu-id="21a1a-124">應用程式不需要在送出作為其中一個非同步通訊端作業方法的參數之後，保留對非同步通訊端作業內容物件的參考。</span><span class="sxs-lookup"><span data-stu-id="21a1a-124">It is not necessary for the application to retain a reference to an asynchronous socket operation context object after it is submitted as a parameter to one of the asynchronous socket operation methods.</span></span> <span data-ttu-id="21a1a-125">在完成回呼傳回之前，它會一直被參考。</span><span class="sxs-lookup"><span data-stu-id="21a1a-125">It will remain referenced until the completion callback returns.</span></span> <span data-ttu-id="21a1a-126">不過讓應用程式保留內容物件的參考有好處，它可以重複用於未來的非同步通訊端作業。</span><span class="sxs-lookup"><span data-stu-id="21a1a-126">However it is advantageous for the application to retain the reference to the context object so that it can be reused for a future asynchronous socket operation.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="21a1a-127">另請參閱</span><span class="sxs-lookup"><span data-stu-id="21a1a-127">See also</span></span>

- <xref:System.Net.Sockets.Socket?displayProperty=nameWithType>
- <xref:System.Net.Sockets.SendPacketsElement?displayProperty=nameWithType>
- <xref:System.Net.Sockets.SocketAsyncEventArgs?displayProperty=nameWithType>
- <xref:System.Net.Sockets.SocketAsyncOperation?displayProperty=nameWithType>
- [<span data-ttu-id="21a1a-128">網路程式設計範例</span><span class="sxs-lookup"><span data-stu-id="21a1a-128">Network Programming Samples</span></span>](network-programming-samples.md)
- [<span data-ttu-id="21a1a-129">通訊端程式碼範例</span><span class="sxs-lookup"><span data-stu-id="21a1a-129">Socket Code Examples</span></span>](socket-code-examples.md)
