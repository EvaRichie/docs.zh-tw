---
title: 作法：直接執行 SQL 命令
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 04671bb0-40c0-4465-86e5-77986f454661
ms.openlocfilehash: 6c72e683c37968ce18717b70ef6d647ca287bd20
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91147638"
---
# <a name="how-to-directly-execute-sql-commands"></a><span data-ttu-id="5f4b9-102">作法：直接執行 SQL 命令</span><span class="sxs-lookup"><span data-stu-id="5f4b9-102">How to: Directly Execute SQL Commands</span></span>

<span data-ttu-id="5f4b9-103">在假設使用 <xref:System.Data.Linq.DataContext> 集合的情況下，您可以使用 <xref:System.Data.Linq.DataContext.ExecuteCommand%2A> 執行不會傳回物件的 SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="5f4b9-103">Assuming a <xref:System.Data.Linq.DataContext> connection, you can use <xref:System.Data.Linq.DataContext.ExecuteCommand%2A> to execute SQL commands that do not return objects.</span></span>  
  
## <a name="example"></a><span data-ttu-id="5f4b9-104">範例</span><span class="sxs-lookup"><span data-stu-id="5f4b9-104">Example</span></span>  

 <span data-ttu-id="5f4b9-105">下列範例會讓 SQL Server 將 UnitPrice 增加 1.00。</span><span class="sxs-lookup"><span data-stu-id="5f4b9-105">The following example causes SQL Server to increase UnitPrice by 1.00.</span></span>  
  
 [!code-csharp[DLinqCommunicatingWithDatabase#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqCommunicatingWithDatabase/cs/Program.cs#3)]
 [!code-vb[DLinqCommunicatingWithDatabase#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqCommunicatingWithDatabase/vb/Module1.vb#3)]  
  
## <a name="see-also"></a><span data-ttu-id="5f4b9-106">另請參閱</span><span class="sxs-lookup"><span data-stu-id="5f4b9-106">See also</span></span>

- [<span data-ttu-id="5f4b9-107">作法：直接執行 SQL 查詢</span><span class="sxs-lookup"><span data-stu-id="5f4b9-107">How to: Directly Execute SQL Queries</span></span>](how-to-directly-execute-sql-queries.md)
- [<span data-ttu-id="5f4b9-108">與資料庫通訊</span><span class="sxs-lookup"><span data-stu-id="5f4b9-108">Communicating with the Database</span></span>](communicating-with-the-database.md)
