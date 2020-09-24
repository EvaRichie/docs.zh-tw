---
title: 作法：執行可傳回 StructuralType 結果的查詢
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 2314f2a2-b1c3-40c4-95bb-cdf9b21a7b53
ms.openlocfilehash: 4b3a63cb23851c6545f330ebd2371e1a34ff13e8
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91198310"
---
# <a name="how-to-execute-a-query-that-returns-structuraltype-results"></a><span data-ttu-id="fdce3-102">作法：執行可傳回 StructuralType 結果的查詢</span><span class="sxs-lookup"><span data-stu-id="fdce3-102">How to: Execute a Query that Returns StructuralType Results</span></span>

<span data-ttu-id="fdce3-103">本主題顯示如何使用 <xref:System.Data.EntityClient.EntityCommand> 物件，針對概念模型執行命令，以及如何使用 <xref:System.Data.Metadata.Edm.StructuralType> 擷取 <xref:System.Data.EntityClient.EntityDataReader> 結果。</span><span class="sxs-lookup"><span data-stu-id="fdce3-103">This topic shows how to execute a command against a conceptual model by using an <xref:System.Data.EntityClient.EntityCommand> object, and how to retrieve the <xref:System.Data.Metadata.Edm.StructuralType> results by using an <xref:System.Data.EntityClient.EntityDataReader>.</span></span> <span data-ttu-id="fdce3-104"><xref:System.Data.Metadata.Edm.EntityType>、<xref:System.Data.Metadata.Edm.RowType> 和 <xref:System.Data.Metadata.Edm.ComplexType> 類別都衍生自 <xref:System.Data.Metadata.Edm.StructuralType> 類別。</span><span class="sxs-lookup"><span data-stu-id="fdce3-104">The <xref:System.Data.Metadata.Edm.EntityType>, <xref:System.Data.Metadata.Edm.RowType> and <xref:System.Data.Metadata.Edm.ComplexType> classes derive from the <xref:System.Data.Metadata.Edm.StructuralType> class.</span></span>  
  
### <a name="to-run-the-code-in-this-example"></a><span data-ttu-id="fdce3-105">執行此範例中的程式碼</span><span class="sxs-lookup"><span data-stu-id="fdce3-105">To run the code in this example</span></span>  
  
1. <span data-ttu-id="fdce3-106">將 [AdventureWorks Sales 模型](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) 加入至您的專案，並將您的專案設定為使用 Entity Framework。</span><span class="sxs-lookup"><span data-stu-id="fdce3-106">Add the [AdventureWorks Sales Model](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) to your project and configure your project to use the Entity Framework.</span></span> <span data-ttu-id="fdce3-107">如需詳細資訊，請參閱 [如何：使用實體資料模型 Wizard](/previous-versions/dotnet/netframework-4.0/bb738677(v=vs.100))。</span><span class="sxs-lookup"><span data-stu-id="fdce3-107">For more information, see [How to: Use the Entity Data Model Wizard](/previous-versions/dotnet/netframework-4.0/bb738677(v=vs.100)).</span></span>  
  
2. <span data-ttu-id="fdce3-108">在應用程式的字碼頁中加入下列 `using` 陳述式 (在 Visual Basic 中為 `Imports`)：</span><span class="sxs-lookup"><span data-stu-id="fdce3-108">In the code page for your application, add the following `using` statements (`Imports` in Visual Basic):</span></span>  
  
     [!code-csharp[DP EntityServices Concepts#Namespaces](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/source.cs#namespaces)]
     [!code-vb[DP EntityServices Concepts#Namespaces](../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp entityservices concepts/vb/source.vb#namespaces)]  
  
## <a name="example"></a><span data-ttu-id="fdce3-109">範例</span><span class="sxs-lookup"><span data-stu-id="fdce3-109">Example</span></span>  

 <span data-ttu-id="fdce3-110">此範例會執行傳回 <xref:System.Data.Metadata.Edm.EntityType> 結果的查詢。</span><span class="sxs-lookup"><span data-stu-id="fdce3-110">This example executes a query that returns <xref:System.Data.Metadata.Edm.EntityType> results.</span></span> <span data-ttu-id="fdce3-111">如果您將下列查詢當做引數傳遞至 `ExecuteStructuralTypeQuery` 函式，則函式會顯示 `Products` 的相關詳細資料：</span><span class="sxs-lookup"><span data-stu-id="fdce3-111">If you pass the following query as an argument to the `ExecuteStructuralTypeQuery` function, the function displays details about the `Products`:</span></span>  
  
 [!code-csharp[DP EntityServices Concepts 2#SelectProduct](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#selectproduct)]  
  
 <span data-ttu-id="fdce3-112">如果您傳遞了參數型查詢 (類似下列查詢)，請將 <xref:System.Data.EntityClient.EntityParameter> 物件加入至 <xref:System.Data.EntityClient.EntityCommand.Parameters%2A> 物件的 <xref:System.Data.EntityClient.EntityCommand> 屬性。</span><span class="sxs-lookup"><span data-stu-id="fdce3-112">If you pass a parameterized query, like the following, add the <xref:System.Data.EntityClient.EntityParameter> objects to the <xref:System.Data.EntityClient.EntityCommand.Parameters%2A> property on the <xref:System.Data.EntityClient.EntityCommand> object.</span></span>  
  
 [!code-csharp[DP EntityServices Concepts 2#GREATER_OR_EQUALS](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#greater_or_equals)]  
  
 [!code-csharp[DP EntityServices Concepts#eSQLStructuralTypes](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/source.cs#esqlstructuraltypes)]
 [!code-vb[DP EntityServices Concepts#eSQLStructuralTypes](../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp entityservices concepts/vb/source.vb#esqlstructuraltypes)]  
  
## <a name="see-also"></a><span data-ttu-id="fdce3-113">另請參閱</span><span class="sxs-lookup"><span data-stu-id="fdce3-113">See also</span></span>

- [<span data-ttu-id="fdce3-114">Entity SQL 參考</span><span class="sxs-lookup"><span data-stu-id="fdce3-114">Entity SQL Reference</span></span>](./language-reference/entity-sql-reference.md)
- [<span data-ttu-id="fdce3-115">Entity Framework 的 EntityClient 提供者</span><span class="sxs-lookup"><span data-stu-id="fdce3-115">EntityClient Provider for the Entity Framework</span></span>](entityclient-provider-for-the-entity-framework.md)
