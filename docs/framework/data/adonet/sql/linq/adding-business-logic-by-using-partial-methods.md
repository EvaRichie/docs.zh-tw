---
title: 使用部分方法加入商務邏輯
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 3a73991e-fd4e-4610-93fb-7ced4dc6b7f9
ms.openlocfilehash: 9ad3329c621b8bf8eaa0fd5f986ac7e8cff97d9e
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91156156"
---
# <a name="adding-business-logic-by-using-partial-methods"></a><span data-ttu-id="e8c5b-102">使用部分方法加入商務邏輯</span><span class="sxs-lookup"><span data-stu-id="e8c5b-102">Adding Business Logic By Using Partial Methods</span></span>

<span data-ttu-id="e8c5b-103">您可以 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 使用 *部分方法*，在專案中自訂 Visual Basic 和 c # 產生的程式碼。</span><span class="sxs-lookup"><span data-stu-id="e8c5b-103">You can customize Visual Basic and C# generated code in your [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] projects by using *partial methods*.</span></span> <span data-ttu-id="e8c5b-104">[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 產生的程式碼會將簽章定義成部分方法的一部分。</span><span class="sxs-lookup"><span data-stu-id="e8c5b-104">The code that [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] generates defines signatures as one part of a partial method.</span></span> <span data-ttu-id="e8c5b-105">如果您想實作此方法，可以加入自己的部分方法。</span><span class="sxs-lookup"><span data-stu-id="e8c5b-105">If you want to implement the method, you can add your own partial method.</span></span> <span data-ttu-id="e8c5b-106">如果您未加入自己的實作 (Implementation)，則編譯器 (Compiler) 會捨棄部分方法簽章並呼叫 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 中的預設方法。</span><span class="sxs-lookup"><span data-stu-id="e8c5b-106">If you do not add your own implementation, the compiler discards the partial methods signature and calls the default methods in [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].</span></span>  
  
> [!NOTE]
> <span data-ttu-id="e8c5b-107">如果您使用 Visual Studio，可以使用物件關聯式設計工具，將驗證和其他自訂加入至實體類別。</span><span class="sxs-lookup"><span data-stu-id="e8c5b-107">If you are using Visual Studio, you can use the Object Relational Designer to add validation and other customizations to entity classes.</span></span>  
  
 <span data-ttu-id="e8c5b-108">例如，Northwind 範例資料庫中 `Customer` 類別的預設對應包含下列部分方法：</span><span class="sxs-lookup"><span data-stu-id="e8c5b-108">For example, the default mapping for the `Customer` class in the Northwind sample database includes the following partial method:</span></span>  
  
 [!code-csharp[DLinqOverrideDefault#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqOverrideDefault/cs/northwind.cs#2)]
 [!code-vb[DLinqOverrideDefault#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqOverrideDefault/vb/northwind.vb#2)]  
  
 <span data-ttu-id="e8c5b-109">您可以將下列程式碼加入至自己的部分 `Customer` 類別，進而實作自己的方法：</span><span class="sxs-lookup"><span data-stu-id="e8c5b-109">You can implement your own method by adding code such as the following to your own partial `Customer` class:</span></span>  
  
 [!code-csharp[DLinqOverrideDefault#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqOverrideDefault/cs/Program.cs#3)]
 [!code-vb[DLinqOverrideDefault#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqOverrideDefault/vb/Module1.vb#3)]  
  
 <span data-ttu-id="e8c5b-110">這種方法通常用於覆 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 寫 `Insert` 、、和的預設方法， `Update` 以在 `Delete` 物件生命週期事件期間驗證屬性。</span><span class="sxs-lookup"><span data-stu-id="e8c5b-110">This approach is typically used in [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] to override default methods for `Insert`, `Update`, `Delete`, and to validate properties during object life-cycle events.</span></span>  
  
 <span data-ttu-id="e8c5b-111">如需詳細資訊，請參閱 [部分方法](../../../../../visual-basic/programming-guide/language-features/procedures/partial-methods.md) (Visual Basic) 或 [部分 (方法) ](../../../../../csharp/language-reference/keywords/partial-method.md) (c # 參考)  (c # ) 。</span><span class="sxs-lookup"><span data-stu-id="e8c5b-111">For more information, see [Partial Methods](../../../../../visual-basic/programming-guide/language-features/procedures/partial-methods.md) (Visual Basic) or [partial (Method) (C# Reference)](../../../../../csharp/language-reference/keywords/partial-method.md) (C#).</span></span>  
  
## <a name="example"></a><span data-ttu-id="e8c5b-112">範例</span><span class="sxs-lookup"><span data-stu-id="e8c5b-112">Example</span></span>  
  
### <a name="description"></a><span data-ttu-id="e8c5b-113">描述</span><span class="sxs-lookup"><span data-stu-id="e8c5b-113">Description</span></span>  

 <span data-ttu-id="e8c5b-114">下列範例會先顯示 `ExampleClass`，因為它可能是由程式碼產生工具 (例如 SQLMetal) 所定義，然後顯示您如何僅實作其中一種方法。</span><span class="sxs-lookup"><span data-stu-id="e8c5b-114">The following example shows `ExampleClass` first as it might be defined by a code-generating tool such as SQLMetal, and then how you might implement only one of the two methods.</span></span>  
  
### <a name="code"></a><span data-ttu-id="e8c5b-115">程式碼</span><span class="sxs-lookup"><span data-stu-id="e8c5b-115">Code</span></span>  

 [!code-csharp[DLinqSubmittingChanges#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSubmittingChanges/cs/Program.cs#4)]
 [!code-vb[DLinqSubmittingChanges#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSubmittingChanges/vb/Module1.vb#4)]  
  
## <a name="example"></a><span data-ttu-id="e8c5b-116">範例</span><span class="sxs-lookup"><span data-stu-id="e8c5b-116">Example</span></span>  
  
### <a name="description"></a><span data-ttu-id="e8c5b-117">描述</span><span class="sxs-lookup"><span data-stu-id="e8c5b-117">Description</span></span>  

 <span data-ttu-id="e8c5b-118">下列範例會使用 `Shipper` 和 `Order` 實體 (Entity) 之間的關聯性 (Relationship)。</span><span class="sxs-lookup"><span data-stu-id="e8c5b-118">The following example uses the relationship between `Shipper` and `Order` entities.</span></span> <span data-ttu-id="e8c5b-119">請注意部分方法中的 `InsertShipper` 和 `DeleteShipper` 方法。</span><span class="sxs-lookup"><span data-stu-id="e8c5b-119">Note among the methods the partial methods, `InsertShipper` and `DeleteShipper`.</span></span> <span data-ttu-id="e8c5b-120">這些方法會覆寫對應所提供的預設部分方法 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 。</span><span class="sxs-lookup"><span data-stu-id="e8c5b-120">These methods override the default partial methods supplied by [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] mapping.</span></span>  
  
### <a name="code"></a><span data-ttu-id="e8c5b-121">程式碼</span><span class="sxs-lookup"><span data-stu-id="e8c5b-121">Code</span></span>  

 [!code-csharp[DLinqOverrideDefault#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqOverrideDefault/cs/northwind.cs#1)]
 [!code-vb[DLinqOverrideDefault#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqOverrideDefault/vb/northwind.vb#1)]  
  
## <a name="see-also"></a><span data-ttu-id="e8c5b-122">另請參閱</span><span class="sxs-lookup"><span data-stu-id="e8c5b-122">See also</span></span>

- [<span data-ttu-id="e8c5b-123">變更資料和提交</span><span class="sxs-lookup"><span data-stu-id="e8c5b-123">Making and Submitting Data Changes</span></span>](making-and-submitting-data-changes.md)
- [<span data-ttu-id="e8c5b-124">自訂插入、更新和刪除作業</span><span class="sxs-lookup"><span data-stu-id="e8c5b-124">Customizing Insert, Update, and Delete Operations</span></span>](customizing-insert-update-and-delete-operations.md)
