---
title: 作法：使用純量值使用者定義函式
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 714e252f-c053-4bbb-b1f3-924111cd4d97
ms.openlocfilehash: faf8d6e94c88575f6cb73003fa5bed87650d7d54
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91196932"
---
# <a name="how-to-use-scalar-valued-user-defined-functions"></a><span data-ttu-id="7fcd2-102">作法：使用純量值使用者定義函式</span><span class="sxs-lookup"><span data-stu-id="7fcd2-102">How to: Use Scalar-Valued User-Defined Functions</span></span>

<span data-ttu-id="7fcd2-103">您可以使用 <xref:System.Data.Linq.Mapping.FunctionAttribute> 屬性，將定義於類別的用戶端方法對應至使用者定義的函式。</span><span class="sxs-lookup"><span data-stu-id="7fcd2-103">You can map a client method defined on a class to a user-defined function by using the <xref:System.Data.Linq.Mapping.FunctionAttribute> attribute.</span></span> <span data-ttu-id="7fcd2-104">請注意，方法的主體會建構一個可擷取方法呼叫用途的運算式，並將該運算式傳遞至 <xref:System.Data.Linq.DataContext> 進行轉譯和執行。</span><span class="sxs-lookup"><span data-stu-id="7fcd2-104">Note that the body of the method constructs an expression that captures the intent of the method call, and passes that expression to the <xref:System.Data.Linq.DataContext> for translation and execution.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="7fcd2-105">唯有在查詢之外呼叫函式時，才會發生直接執行。</span><span class="sxs-lookup"><span data-stu-id="7fcd2-105">Direct execution occurs only if the function is called outside a query.</span></span> <span data-ttu-id="7fcd2-106">如需詳細資訊，請參閱 [如何：以內嵌方式呼叫使用者定義函數](how-to-call-user-defined-functions-inline.md)。</span><span class="sxs-lookup"><span data-stu-id="7fcd2-106">For more information, see [How to: Call User-Defined Functions Inline](how-to-call-user-defined-functions-inline.md).</span></span>  
  
## <a name="example"></a><span data-ttu-id="7fcd2-107">範例</span><span class="sxs-lookup"><span data-stu-id="7fcd2-107">Example</span></span>  

 <span data-ttu-id="7fcd2-108">下列 SQL 程式碼展示使用者定義的純量值函式 `ReverseCustName()`。</span><span class="sxs-lookup"><span data-stu-id="7fcd2-108">The following SQL code presents a scalar-valued user-defined function `ReverseCustName()`.</span></span>  
  
```sql  
CREATE FUNCTION ReverseCustName(@string varchar(100))  
RETURNS varchar(100)  
AS  
BEGIN  
    DECLARE @custName varchar(100)  
    -- Implementation left as exercise for users.  
    RETURN @custName  
END  
```  
  
 <span data-ttu-id="7fcd2-109">您可以對此程式碼對應如下所列的用戶端方法：</span><span class="sxs-lookup"><span data-stu-id="7fcd2-109">You would map a client method such as the following for this code:</span></span>  
  
 [!code-csharp[DLinqUDFS#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqUDFS/cs/northwind-tfunc.cs#3)]
 [!code-vb[DLinqUDFS#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqUDFS/vb/northwind-tfunc.vb#3)]  
  
## <a name="see-also"></a><span data-ttu-id="7fcd2-110">另請參閱</span><span class="sxs-lookup"><span data-stu-id="7fcd2-110">See also</span></span>

- [<span data-ttu-id="7fcd2-111">使用者定義的函式</span><span class="sxs-lookup"><span data-stu-id="7fcd2-111">User-Defined Functions</span></span>](user-defined-functions.md)
