---
title: 作法：使用 EntityCommand 執行參數化 Entity SQL 查詢
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: e93fea43-7e03-4d7d-9fee-2517b8b88cba
ms.openlocfilehash: 24b24e4c35c85edb1f960ae18a58cbc5893690d0
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90536219"
---
# <a name="how-to-execute-a-parameterized-entity-sql-query-using-entitycommand"></a><span data-ttu-id="a5a3c-102">作法：使用 EntityCommand 執行參數化 Entity SQL 查詢</span><span class="sxs-lookup"><span data-stu-id="a5a3c-102">How to: Execute a Parameterized Entity SQL Query Using EntityCommand</span></span>
<span data-ttu-id="a5a3c-103">本主題說明如何 [!INCLUDE[esql](../../../../../includes/esql-md.md)] 使用物件執行具有參數的查詢 <xref:System.Data.EntityClient.EntityCommand> 。</span><span class="sxs-lookup"><span data-stu-id="a5a3c-103">This topic shows how to execute an [!INCLUDE[esql](../../../../../includes/esql-md.md)] query that has parameters by using an <xref:System.Data.EntityClient.EntityCommand> object.</span></span>  
  
### <a name="to-run-the-code-in-this-example"></a><span data-ttu-id="a5a3c-104">執行此範例中的程式碼</span><span class="sxs-lookup"><span data-stu-id="a5a3c-104">To run the code in this example</span></span>  
  
1. <span data-ttu-id="a5a3c-105">將 [AdventureWorks Sales 模型](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) 加入至您的專案，並將您的專案設定為使用 Entity Framework。</span><span class="sxs-lookup"><span data-stu-id="a5a3c-105">Add the [AdventureWorks Sales Model](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) to your project and configure your project to use the Entity Framework.</span></span> <span data-ttu-id="a5a3c-106">如需詳細資訊，請參閱 [如何：使用實體資料模型 Wizard](/previous-versions/dotnet/netframework-4.0/bb738677(v=vs.100))。</span><span class="sxs-lookup"><span data-stu-id="a5a3c-106">For more information, see [How to: Use the Entity Data Model Wizard](/previous-versions/dotnet/netframework-4.0/bb738677(v=vs.100)).</span></span>  
  
2. <span data-ttu-id="a5a3c-107">在應用程式的字碼頁中加入下列 `using` 陳述式 (在 Visual Basic 中為 `Imports`)：</span><span class="sxs-lookup"><span data-stu-id="a5a3c-107">In the code page for your application, add the following `using` statements (`Imports` in Visual Basic):</span></span>  
  
     [!code-csharp[DP EntityServices Concepts#Namespaces](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/source.cs#namespaces)]
     [!code-vb[DP EntityServices Concepts#Namespaces](../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp entityservices concepts/vb/source.vb#namespaces)]  
  
## <a name="example"></a><span data-ttu-id="a5a3c-108">範例</span><span class="sxs-lookup"><span data-stu-id="a5a3c-108">Example</span></span>  
 <span data-ttu-id="a5a3c-109">下列範例示範如何建構具有兩個參數的查詢字串。</span><span class="sxs-lookup"><span data-stu-id="a5a3c-109">The following example shows how to construct a query string with two parameters.</span></span> <span data-ttu-id="a5a3c-110">然後它會建立 <xref:System.Data.EntityClient.EntityCommand>、將兩個參數加入到該 <xref:System.Data.EntityClient.EntityParameter> 的 <xref:System.Data.EntityClient.EntityCommand> 集合，並逐一查看 `Contact` 項目的集合。</span><span class="sxs-lookup"><span data-stu-id="a5a3c-110">It then creates an <xref:System.Data.EntityClient.EntityCommand>, adds two parameters to the <xref:System.Data.EntityClient.EntityParameter> collection of that <xref:System.Data.EntityClient.EntityCommand>, and iterates through the collection of `Contact` items.</span></span>  
  
 [!code-csharp[DP EntityServices Concepts#ParameterizedQueryWithEntityCommand](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/source.cs#parameterizedquerywithentitycommand)]
 [!code-vb[DP EntityServices Concepts#ParameterizedQueryWithEntityCommand](../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp entityservices concepts/vb/source.vb#parameterizedquerywithentitycommand)]  
  
## <a name="see-also"></a><span data-ttu-id="a5a3c-111">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a5a3c-111">See also</span></span>

- <span data-ttu-id="a5a3c-112">[如何：執行參數化查詢](/previous-versions/dotnet/netframework-4.0/bb738521(v=vs.100))</span><span class="sxs-lookup"><span data-stu-id="a5a3c-112">[How to: Execute a Parameterized Query](/previous-versions/dotnet/netframework-4.0/bb738521(v=vs.100))</span></span>
- [<span data-ttu-id="a5a3c-113">Entity SQL 語言</span><span class="sxs-lookup"><span data-stu-id="a5a3c-113">Entity SQL Language</span></span>](./language-reference/entity-sql-language.md)
