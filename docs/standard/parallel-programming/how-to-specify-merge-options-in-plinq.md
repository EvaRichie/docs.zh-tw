---
title: 作法：在 PLINQ 中指定合併選項
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- PLINQ queries, how to use merge options
ms.assetid: 0f33b527-e91a-4550-a39a-e63e396fd831
ms.openlocfilehash: 84667fa1fbe2966c580d9c6d32e52ed686af7bb3
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84288117"
---
# <a name="how-to-specify-merge-options-in-plinq"></a>作法：在 PLINQ 中指定合併選項
此範例示範如何指定將套用到 PLINQ 查詢中所有後續運算子的合併選項。 您不需明確地設定合併選項，但這樣做可改善效能。 如需合併選項的詳細資訊，請參閱 [PLINQ 中的合併選項](merge-options-in-plinq.md)。  
  
> [!WARNING]
> 這個範例是為了示範用法，執行速度可能比不上對應的循序 LINQ to Objects 查詢。 如需加速的詳細資訊，請參閱[認識 PLINQ 中的加速](understanding-speedup-in-plinq.md)。  
  
## <a name="example"></a>範例  
 下列範例示範具有未排序來源之基本案例中的合併選項行為，並將高度耗費資源的函式套用至每個元素。  
  
 [!code-csharp[PLINQ#23](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#23)]
 [!code-vb[PLINQ#23](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinq2_vb.vb#23)]  
  
 如果 <xref:System.Linq.ParallelMergeOptions.AutoBuffered> 在產生第一個元素前造成非預期的延遲，請試用 <xref:System.Linq.ParallelMergeOptions.NotBuffered> 選項，以更快且更順暢的方式產生結果元素。  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Linq.ParallelMergeOptions>
- [平行 LINQ (PLINQ)](introduction-to-plinq.md)
