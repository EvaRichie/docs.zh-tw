---
title: 作法：使用具名管道進行網路處理序間通訊
description: 查看兩個使用具名管道進行管道伺服器之間的處理序間通訊，以及網路中一或多個管道用戶端的範例。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- message-based communication [.NET], named pipes
- named pipes [.NET]
- pipes [.NET]
- multiple connections via named pipes
- network communications [.NET], named pipes
- impersonation [.NET], named pipes
- full duplex communication [.NET], named pipes
ms.assetid: 4e4d7e64-9f1b-4026-98f7-20488ac7b42b
ms.openlocfilehash: aad9ede3fb257899eec7bff95b6d77eaec5b97ca
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94829735"
---
# <a name="how-to-use-named-pipes-for-network-interprocess-communication"></a><span data-ttu-id="f7e36-103">作法：使用具名管道進行網路處理序間通訊</span><span class="sxs-lookup"><span data-stu-id="f7e36-103">How to: Use Named Pipes for Network Interprocess Communication</span></span>

<span data-ttu-id="f7e36-104">具名管道可在管道伺服器及一個或多個管道用戶端之間提供處理序間通訊。</span><span class="sxs-lookup"><span data-stu-id="f7e36-104">Named pipes provide interprocess communication between a pipe server and one or more pipe clients.</span></span> <span data-ttu-id="f7e36-105">它們比在本機電腦上處理流程間通訊的匿名管道提供更多的功能。</span><span class="sxs-lookup"><span data-stu-id="f7e36-105">They offer more functionality than anonymous pipes, which provide interprocess communication on a local computer.</span></span> <span data-ttu-id="f7e36-106">具名管道支援在網路及多個伺服器執行個體上進行全雙工通訊、訊息架構通訊及用戶端模擬。用戶端模擬可讓連接處理序在遠端伺服器上使用本身的權限集合。</span><span class="sxs-lookup"><span data-stu-id="f7e36-106">Named pipes support full duplex communication over a network and multiple server instances, message-based communication, and client impersonation, which enables connecting processes to use their own set of permissions on remote servers.</span></span>  
  
 <span data-ttu-id="f7e36-107">若要實作具名管道，請使用 <xref:System.IO.Pipes.NamedPipeServerStream> 和 <xref:System.IO.Pipes.NamedPipeClientStream> 類別。</span><span class="sxs-lookup"><span data-stu-id="f7e36-107">To implement name pipes, use the <xref:System.IO.Pipes.NamedPipeServerStream> and <xref:System.IO.Pipes.NamedPipeClientStream> classes.</span></span>  
  
## <a name="example"></a><span data-ttu-id="f7e36-108">範例</span><span class="sxs-lookup"><span data-stu-id="f7e36-108">Example</span></span>  
 <span data-ttu-id="f7e36-109">下列範例示範如何使用 <xref:System.IO.Pipes.NamedPipeServerStream> 類別建立具名管道。</span><span class="sxs-lookup"><span data-stu-id="f7e36-109">The following example demonstrates how to create a named pipe by using the <xref:System.IO.Pipes.NamedPipeServerStream> class.</span></span> <span data-ttu-id="f7e36-110">在此範例中，伺服器處理序會建立四個執行緒。</span><span class="sxs-lookup"><span data-stu-id="f7e36-110">In this example, the server process creates four threads.</span></span> <span data-ttu-id="f7e36-111">每個執行緒都可以接受用戶端連線。</span><span class="sxs-lookup"><span data-stu-id="f7e36-111">Each thread can accept a client connection.</span></span> <span data-ttu-id="f7e36-112">接著，連線的用戶端處理序會提供具有檔案名稱的伺服器。</span><span class="sxs-lookup"><span data-stu-id="f7e36-112">The connected client process then supplies the server with a file name.</span></span> <span data-ttu-id="f7e36-113">如果用戶端有足夠的權限，伺服器處理序就會開啟檔案，並將其內容傳回用戶端。</span><span class="sxs-lookup"><span data-stu-id="f7e36-113">If the client has sufficient permissions, the server process opens the file and sends its contents back to the client.</span></span>  
  
 [!code-cpp[System.IO.Pipes.NamedPipeServerStream_ImpersonationSample1#01](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.IO.Pipes.NamedPipeServerStream_ImpersonationSample1/cpp/program.cpp#01)]
 [!code-csharp[System.IO.Pipes.NamedPipeServerStream_ImpersonationSample1#01](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.IO.Pipes.NamedPipeServerStream_ImpersonationSample1/cs/Program.cs#01)]
 [!code-vb[System.IO.Pipes.NamedPipeServerStream_ImpersonationSample1#01](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.IO.Pipes.NamedPipeServerStream_ImpersonationSample1/vb/program.vb#01)]  
  
## <a name="example"></a><span data-ttu-id="f7e36-114">範例</span><span class="sxs-lookup"><span data-stu-id="f7e36-114">Example</span></span>  
 <span data-ttu-id="f7e36-115">下列範例示範使用 <xref:System.IO.Pipes.NamedPipeClientStream> 類別的用戶端處理序。</span><span class="sxs-lookup"><span data-stu-id="f7e36-115">The following example shows the client process, which uses the <xref:System.IO.Pipes.NamedPipeClientStream> class.</span></span> <span data-ttu-id="f7e36-116">用戶端會連線至伺服器處理序，並將檔案名稱傳送至伺服器。</span><span class="sxs-lookup"><span data-stu-id="f7e36-116">The client connects to the server process and sends a file name to the server.</span></span> <span data-ttu-id="f7e36-117">此範例會使用模擬，因此，執行用戶端應用程式的身分識別必須擁有存取該檔案的權限。</span><span class="sxs-lookup"><span data-stu-id="f7e36-117">The example uses impersonation, so the identity that is running the client application must have permission to access the file.</span></span> <span data-ttu-id="f7e36-118">接著，伺服器會將檔案的內容傳回用戶端。</span><span class="sxs-lookup"><span data-stu-id="f7e36-118">The server then sends the contents of the file back to the client.</span></span> <span data-ttu-id="f7e36-119">檔案內容隨即顯示到主控台。</span><span class="sxs-lookup"><span data-stu-id="f7e36-119">The file contents are then displayed to the console.</span></span>  
  
 [!code-csharp[System.IO.Pipes.NamedPipeClientStream_ImpersonationSample1#01](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.IO.Pipes.NamedPipeClientStream_ImpersonationSample1/cs/Program.cs#01)]
 [!code-vb[System.IO.Pipes.NamedPipeClientStream_ImpersonationSample1#01](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.IO.Pipes.NamedPipeClientStream_ImpersonationSample1/vb/program.vb#01)]  
  
## <a name="robust-programming"></a><span data-ttu-id="f7e36-120">穩固程式設計</span><span class="sxs-lookup"><span data-stu-id="f7e36-120">Robust Programming</span></span>  
 <span data-ttu-id="f7e36-121">此範例中的用戶端和伺服器處理序要在相同的電腦上執行，因此，提供給 <xref:System.IO.Pipes.NamedPipeClientStream> 物件的伺服器名稱為 `"."`。</span><span class="sxs-lookup"><span data-stu-id="f7e36-121">The client and server processes in this example are intended to run on the same computer, so the server name provided to the <xref:System.IO.Pipes.NamedPipeClientStream> object is `"."`.</span></span> <span data-ttu-id="f7e36-122">如果用戶端和伺服器處理序在不同的電腦上，`"."` 將會取代成執行伺服器處理序之電腦的網路名稱。</span><span class="sxs-lookup"><span data-stu-id="f7e36-122">If the client and server processes were on separate computers, `"."` would be replaced with the network name of the computer that runs the server process.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="f7e36-123">請參閱</span><span class="sxs-lookup"><span data-stu-id="f7e36-123">See also</span></span>

- <xref:System.Security.Principal.TokenImpersonationLevel>
- <xref:System.IO.Pipes.NamedPipeServerStream.GetImpersonationUserName%2A>
- [<span data-ttu-id="f7e36-124">管道</span><span class="sxs-lookup"><span data-stu-id="f7e36-124">Pipes</span></span>](pipe-operations.md)
- [<span data-ttu-id="f7e36-125">作法：使用匿名管道進行本機處理序間通訊</span><span class="sxs-lookup"><span data-stu-id="f7e36-125">How to: Use Anonymous Pipes for Local Interprocess Communication</span></span>](how-to-use-anonymous-pipes-for-local-interprocess-communication.md)
