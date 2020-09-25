---
title: 作法：指定並行衝突檢查
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: c2547fcb-58eb-4377-9948-1b8d76a0f3d7
ms.openlocfilehash: 7adacdccd12c6493ff7c62c0e6a44058a9719d7d
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91197205"
---
# <a name="how-to-specify-concurrency-conflict-checking"></a><span data-ttu-id="dc76b-102">作法：指定並行衝突檢查</span><span class="sxs-lookup"><span data-stu-id="dc76b-102">How to: Specify Concurrency-Conflict Checking</span></span>

<span data-ttu-id="dc76b-103">您可以指定在呼叫 <xref:System.Data.Linq.DataContext.SubmitChanges%2A> 時要檢查並行存取衝突的資料庫資料行。</span><span class="sxs-lookup"><span data-stu-id="dc76b-103">You can specify which columns of the database are to be checked for concurrency conflicts when you call <xref:System.Data.Linq.DataContext.SubmitChanges%2A>.</span></span> <span data-ttu-id="dc76b-104">如需詳細資訊，請參閱 [如何：指定測試並行衝突的成員](how-to-specify-which-members-are-tested-for-concurrency-conflicts.md)。</span><span class="sxs-lookup"><span data-stu-id="dc76b-104">For more information, see [How to: Specify Which Members are Tested for Concurrency Conflicts](how-to-specify-which-members-are-tested-for-concurrency-conflicts.md).</span></span>  
  
## <a name="example"></a><span data-ttu-id="dc76b-105">範例</span><span class="sxs-lookup"><span data-stu-id="dc76b-105">Example</span></span>  

 <span data-ttu-id="dc76b-106">下列程式碼指定 `HomePage` 成員永遠不應該在更新檢查期間進行測試。</span><span class="sxs-lookup"><span data-stu-id="dc76b-106">The following code specifies that the `HomePage` member should never be tested during update checks.</span></span> <span data-ttu-id="dc76b-107">如需詳細資訊，請參閱<xref:System.Data.Linq.Mapping.ColumnAttribute.UpdateCheck%2A>。</span><span class="sxs-lookup"><span data-stu-id="dc76b-107">For more information, see <xref:System.Data.Linq.Mapping.ColumnAttribute.UpdateCheck%2A>.</span></span>  
  
 [!code-csharp[System.Data.Linq.Mapping.UpdateCheck#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/system.data.linq.mapping.updatecheck/cs/northwind.cs#1)]
 [!code-vb[System.Data.Linq.Mapping.UpdateCheck#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/system.data.linq.mapping.updatecheck/vb/northwind.vb#1)]  
  
## <a name="see-also"></a><span data-ttu-id="dc76b-108">另請參閱</span><span class="sxs-lookup"><span data-stu-id="dc76b-108">See also</span></span>

- [<span data-ttu-id="dc76b-109">LINQ to SQL 物件模型</span><span class="sxs-lookup"><span data-stu-id="dc76b-109">The LINQ to SQL Object Model</span></span>](the-linq-to-sql-object-model.md)
- [<span data-ttu-id="dc76b-110">作法：使用程式碼編輯器自訂實體類別</span><span class="sxs-lookup"><span data-stu-id="dc76b-110">How to: Customize Entity Classes by Using the Code Editor</span></span>](how-to-customize-entity-classes-by-using-the-code-editor.md)
