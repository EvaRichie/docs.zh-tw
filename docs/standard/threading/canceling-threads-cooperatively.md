---
title: 以合作方式取消執行緒
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- threads, cancellation
ms.assetid: d2d6d5fd-e263-4fa0-847b-2fc3e0d82337
ms.openlocfilehash: 9e9224e9dc9ac57defe75e916dd6b9844bba7f12
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94826608"
---
# <a name="canceling-threads-cooperatively"></a>以合作方式取消執行緒

在 .NET Framework 4 之前，.NET 未提供任何內建的方法，可在啟動後以合作方式取消執行緒。 不過，從 .NET Framework 4 開始，您可以使用 <xref:System.Threading.CancellationToken?displayProperty=nameWithType> 來取消執行緒，就像您可以使用它們來取消 <xref:System.Threading.Tasks.Task?displayProperty=nameWithType> 物件或 PLINQ 查詢一樣。 雖然 <xref:System.Threading.Thread?displayProperty=nameWithType> 類別不提供取消語彙基元的內建支援，您仍可透過使用採取 <xref:System.Threading.Thread> 委派的 <xref:System.Threading.ParameterizedThreadStart> 建構函式，將語彙基元傳遞至執行緒程序。 下列範例示範如何進行這項操作。  
  
 [!code-csharp[Cancellation#14](../../../samples/snippets/csharp/VS_Snippets_Misc/cancellation/cs/CooperativeThreads.cs#14)]
 [!code-vb[Cancellation#14](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cancellation/vb/CooperativeThreads.vb#14)]  
  
## <a name="see-also"></a>請參閱

- [使用執行緒和執行緒](using-threads-and-threading.md)
