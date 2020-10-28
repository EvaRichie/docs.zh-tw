---
title: 工作平行程式庫 (TPL)
description: 探索 (TPL) 的工作平行程式庫，這是一組公用類型和 Api，可簡化將平行處理原則加入至 .NET 中的應用程式 & 並行處理的程式。
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- .NET, concurrency in
- .NET, parallel programming in
- Parallel Programming
ms.assetid: b8f99f43-9104-45fd-9bff-385a20488a23
ms.openlocfilehash: 35e79d0c55ca62f7df7b687c4d5a3d1fc7d0748e
ms.sourcegitcommit: 279fb6e8d515df51676528a7424a1df2f0917116
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/27/2020
ms.locfileid: "92687998"
---
# <a name="task-parallel-library-tpl"></a>工作平行程式庫 (TPL)
工作平行程式庫 (TPL) 是 <xref:System.Threading?displayProperty=nameWithType> 和 <xref:System.Threading.Tasks?displayProperty=nameWithType> 命名空間中的一組公用類型和 API。 TPL 的目的是透過簡化將平行處理原則和並行加入至應用程式的流程，讓開發人員更有生產力。 TPL 可動態調整並行程度，最有效率地使用所有可用的處理器。 此外，TPL 還會處理工作分割、<xref:System.Threading.ThreadPool> 上執行緒的排程、取消支援、狀態管理和其他低階細節。 使用 TPL，可讓您發揮程式碼的最大效能，同時專注於程式所應完成的工作。  
  
 從 .NET Framework 4 開始，TPL 是撰寫多執行緒和平行程式碼的慣用方式。 但是，並非所有程式碼都適用於平行化作業；例如，如果迴圈只會在每個反覆項目執行少量工作，或是迴圈執行的反覆項目並不多，則平行化作業帶來的額外負荷可能會讓程式碼的執行速度變慢。 再者，就像任何多執行緒執行碼，平行化作業會使程式執行變得複雜。 雖然 TPL 可簡化多執行緒案例，但建議您應先了解執行緒處理的基本概念 (例如鎖定、死結、競爭情況等)，以有效使用 TPL。  
  
## <a name="related-topics"></a>相關主題  
  
|標題|描述|  
|-|-|  
|[資料平行處理](data-parallelism-task-parallel-library.md)|說明如何建立平行 `for` 和 `foreach` 迴圈 (在 Visual Basic 中為 `For` 和 `For Each`)。|  
|[以工作為基礎的非同步程式設計](task-based-asynchronous-programming.md)|說明如何使用 <xref:System.Threading.Tasks.Parallel.Invoke%2A?displayProperty=nameWithType> (以隱含方式) 或直接使用 <xref:System.Threading.Tasks.Task> 物件 (以明確方式) 建立和執行工作。|  
|[資料流程](dataflow-task-parallel-library.md)|說明如何使用 TPL 資料流程程式庫中的資料流程元件，以處理必須彼此通訊的多項作業，或是在資料可用時處理資料。|  
|[使用具有其他非同步模式的 TPL](using-tpl-with-other-asynchronous-patterns.md)|說明如何將 TPL 搭配 .NET 中的其他非同步模式使用|  
|[資料和工作平行處理原則中可能出現的錯誤](potential-pitfalls-in-data-and-task-parallelism.md)|說明一些常見陷阱以及如何避免這些陷阱。|  
|[平行 LINQ (PLINQ)](introduction-to-plinq.md)|說明如何使用 LINQ 查詢達到資料平行處理原則。|  
|[平行程式設計](index.md)|.NET 平行程式設計的最上層節點。|  
  
## <a name="see-also"></a>請參閱

- [使用 .NET Core & 進行平行程式設計的範例 .NET Standard](/samples/browse/?products=dotnet-core%2Cdotnet-standard&term=parallel)
