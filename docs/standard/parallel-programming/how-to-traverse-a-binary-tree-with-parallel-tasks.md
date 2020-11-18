---
title: 作法：使用平行工作周遊二進位樹狀目錄
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- tasks, how to traverse a tree
ms.assetid: 4265d169-6c69-4f36-b10d-b7ae7f72f4df
ms.openlocfilehash: ca70021c7d071abe480cb4ed866e34f171cc3b45
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94825529"
---
# <a name="how-to-traverse-a-binary-tree-with-parallel-tasks"></a><span data-ttu-id="727ef-102">作法：使用平行工作周遊二進位樹狀目錄</span><span class="sxs-lookup"><span data-stu-id="727ef-102">How to: Traverse a Binary Tree with Parallel Tasks</span></span>
<span data-ttu-id="727ef-103">下列範例示範可以使用平行工作來周遊樹狀資料結構的兩種方式。</span><span class="sxs-lookup"><span data-stu-id="727ef-103">The following example shows two ways in which parallel tasks can be used to traverse a tree data structure.</span></span> <span data-ttu-id="727ef-104">建立樹狀的部分則留待練習。</span><span class="sxs-lookup"><span data-stu-id="727ef-104">The creation of the tree itself is left as an exercise.</span></span>  
  
## <a name="example"></a><span data-ttu-id="727ef-105">範例</span><span class="sxs-lookup"><span data-stu-id="727ef-105">Example</span></span>  
 [!code-csharp[TPL#16](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl/cs/tpl.cs#16)]
 [!code-vb[TPL#16](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl/vb/treewalk.vb#16)]  
  
 <span data-ttu-id="727ef-106">這兩個方法的功能相同。</span><span class="sxs-lookup"><span data-stu-id="727ef-106">The two methods shown are functionally equivalent.</span></span> <span data-ttu-id="727ef-107">透過使用 <xref:System.Threading.Tasks.TaskFactory.StartNew%2A> 方法來建立並執行工作，您會收到來自工作的控制代碼，用於等待工作及處理例外狀況。</span><span class="sxs-lookup"><span data-stu-id="727ef-107">By using the <xref:System.Threading.Tasks.TaskFactory.StartNew%2A> method to create and run the tasks, you get a handle back from the tasks which can be used to wait on the tasks and handle exceptions.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="727ef-108">請參閱</span><span class="sxs-lookup"><span data-stu-id="727ef-108">See also</span></span>

- [<span data-ttu-id="727ef-109">工作平行程式庫 (TPL)</span><span class="sxs-lookup"><span data-stu-id="727ef-109">Task Parallel Library (TPL)</span></span>](task-parallel-library-tpl.md)
