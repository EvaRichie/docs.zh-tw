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
# <a name="how-to-traverse-a-binary-tree-with-parallel-tasks"></a>作法：使用平行工作周遊二進位樹狀目錄
下列範例示範可以使用平行工作來周遊樹狀資料結構的兩種方式。 建立樹狀的部分則留待練習。  
  
## <a name="example"></a>範例  
 [!code-csharp[TPL#16](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl/cs/tpl.cs#16)]
 [!code-vb[TPL#16](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl/vb/treewalk.vb#16)]  
  
 這兩個方法的功能相同。 透過使用 <xref:System.Threading.Tasks.TaskFactory.StartNew%2A> 方法來建立並執行工作，您會收到來自工作的控制代碼，用於等待工作及處理例外狀況。  
  
## <a name="see-also"></a>請參閱

- [工作平行程式庫 (TPL)](task-parallel-library-tpl.md)
