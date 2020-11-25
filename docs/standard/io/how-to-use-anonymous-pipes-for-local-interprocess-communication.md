---
title: 作法：使用匿名管道進行本機處理序間通訊
description: 瞭解如何在 .NET 中的本機電腦上，使用匿名管道進行本機進程間的通訊。 匿名管道需要的額外負荷比具名管道少。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- anonymous pipes [.NET]
- parent-child communication [.NET]
- pipes [.NET]
- one-way communication [.NET]
- local computer communication [.NET], pipes
ms.assetid: e7773c77-c646-4a01-8a96-a003d59fc4c9
ms.openlocfilehash: 389451d1c6c313ac4a10652c7aa614a5e4e7bf1c
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95734552"
---
# <a name="how-to-use-anonymous-pipes-for-local-interprocess-communication"></a>作法：使用匿名管道進行本機處理序間通訊

匿名管道會在本機電腦上提供處理序間通訊。 它們提供的功能比具名管道少，但其負荷也比較小。 您可以使用匿名管道，讓本機電腦上的處理序間通訊更容易。 您無法透過網路，使用匿名管道進行通訊。  
  
 若要實作匿名管道，請使用 <xref:System.IO.Pipes.AnonymousPipeServerStream> 和 <xref:System.IO.Pipes.AnonymousPipeClientStream> 類別。  
  
## <a name="example"></a>範例  

 下列範例會示範如何使用匿名管道，將字串從父處理序傳送至子處理序。 此範例會在父處理序中，使用 <xref:System.IO.Pipes.PipeDirection.Out> 的 <xref:System.IO.Pipes.PipeDirection> 值建立 <xref:System.IO.Pipes.AnonymousPipeServerStream> 物件。 接著，父處理序會使用建立 <xref:System.IO.Pipes.AnonymousPipeClientStream> 物件的用戶端控制代碼來建立子處理序。 子處理序具有 <xref:System.IO.Pipes.PipeDirection.In> 的 <xref:System.IO.Pipes.PipeDirection> 值。  
  
 接著，父處理序會將使用者提供的字串傳送給子處理序。 此字串會顯示到子處理序中的主控台。  
  
 下列範例示範伺服器處理序。  
  
 [!code-cpp[System.IO.Pipes.AnonymousPipeServerStream_Sample#01](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.IO.Pipes.AnonymousPipeServerStream_Sample/cpp/program.cpp#01)]
 [!code-csharp[System.IO.Pipes.AnonymousPipeServerStream_Sample#01](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.IO.Pipes.AnonymousPipeServerStream_Sample/cs/Program.cs#01)]
 [!code-vb[System.IO.Pipes.AnonymousPipeServerStream_Sample#01](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.IO.Pipes.AnonymousPipeServerStream_Sample/vb/program.vb#01)]  

[!INCLUDE [localized code comments](../../../includes/code-comments-loc.md)]
  
## <a name="example"></a>範例  

 下列範例示範用戶端處理序。 伺服器處理序會啟動用戶端處理序，並為該處理序提供一個用戶端控制代碼。 從用戶端程式碼產生的可執行檔應該命名為 `pipeClient.exe`，並在執行伺服器處理序之前，複製到與伺服器可執行檔相同的目錄。  
  
 [!code-cpp[System.IO.Pipes.AnonymousPipeClientStream_Sample#01](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.IO.Pipes.AnonymousPipeClientStream_Sample/cpp/program.cpp#01)]
 [!code-csharp[System.IO.Pipes.AnonymousPipeClientStream_Sample#01](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.IO.Pipes.AnonymousPipeClientStream_Sample/cs/Program.cs#01)]
 [!code-vb[System.IO.Pipes.AnonymousPipeClientStream_Sample#01](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.IO.Pipes.AnonymousPipeClientStream_Sample/vb/program.vb#01)]  
  
## <a name="see-also"></a>另請參閱

- [管道](pipe-operations.md)
- [作法：使用具名管道進行網路處理序間通訊](how-to-use-named-pipes-for-network-interprocess-communication.md)
