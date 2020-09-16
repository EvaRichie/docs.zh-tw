---
title: 作法：使用 Navigate 運算子巡覽關聯性
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 79996d2d-9b03-4a9d-82cc-7c5e7c2ad93d
ms.openlocfilehash: c51b093c1b74157b957566c4c67712278e50b9e3
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90546662"
---
# <a name="how-to-navigate-relationships-with-the-navigate-operator"></a><span data-ttu-id="a2f21-102">作法：使用 Navigate 運算子巡覽關聯性</span><span class="sxs-lookup"><span data-stu-id="a2f21-102">How to: Navigate Relationships with the Navigate Operator</span></span>
<span data-ttu-id="a2f21-103">本主題顯示如何使用 <xref:System.Data.EntityClient.EntityCommand> 物件，針對概念模型執行命令，以及如何使用 <xref:System.Data.Metadata.Edm.RefType> 擷取 <xref:System.Data.EntityClient.EntityDataReader> 結果。</span><span class="sxs-lookup"><span data-stu-id="a2f21-103">This topic shows how to execute a command against a conceptual model by using an <xref:System.Data.EntityClient.EntityCommand> object, and how to retrieve the <xref:System.Data.Metadata.Edm.RefType> results by using an <xref:System.Data.EntityClient.EntityDataReader>.</span></span>  
  
### <a name="to-run-the-code-in-this-example"></a><span data-ttu-id="a2f21-104">執行此範例中的程式碼</span><span class="sxs-lookup"><span data-stu-id="a2f21-104">To run the code in this example</span></span>  
  
1. <span data-ttu-id="a2f21-105">將 [AdventureWorks Sales 模型](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) 加入至您的專案，並將您的專案設定為使用 Entity Framework。</span><span class="sxs-lookup"><span data-stu-id="a2f21-105">Add the [AdventureWorks Sales Model](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) to your project and configure your project to use the Entity Framework.</span></span> <span data-ttu-id="a2f21-106">如需詳細資訊，請參閱 [如何：使用實體資料模型 Wizard](/previous-versions/dotnet/netframework-4.0/bb738677(v=vs.100))。</span><span class="sxs-lookup"><span data-stu-id="a2f21-106">For more information, see [How to: Use the Entity Data Model Wizard](/previous-versions/dotnet/netframework-4.0/bb738677(v=vs.100)).</span></span>  
  
2. <span data-ttu-id="a2f21-107">在應用程式的字碼頁中加入下列 `using` 陳述式 (在 Visual Basic 中為 `Imports`)：</span><span class="sxs-lookup"><span data-stu-id="a2f21-107">In the code page for your application, add the following `using` statements (`Imports` in Visual Basic):</span></span>  
  
     [!code-csharp[DP EntityServices Concepts#Namespaces](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/source.cs#namespaces)]
     [!code-vb[DP EntityServices Concepts#Namespaces](../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp entityservices concepts/vb/source.vb#namespaces)]  
  
## <a name="example"></a><span data-ttu-id="a2f21-108">範例</span><span class="sxs-lookup"><span data-stu-id="a2f21-108">Example</span></span>  
 <span data-ttu-id="a2f21-109">下列範例示範如何 [!INCLUDE[esql](../../../../../includes/esql-md.md)] 使用 [導覽](./language-reference/navigate-entity-sql.md) 運算子來導覽中的關聯性。</span><span class="sxs-lookup"><span data-stu-id="a2f21-109">The following example shows how to navigate relationships in [!INCLUDE[esql](../../../../../includes/esql-md.md)] by using the [NAVIGATE](./language-reference/navigate-entity-sql.md) operator.</span></span> <span data-ttu-id="a2f21-110">`Navigate`運算子會使用下列參數：實體的實例、關聯性類型、關聯性的結尾，以及關聯性的開頭。</span><span class="sxs-lookup"><span data-stu-id="a2f21-110">The `Navigate` operator takes the following parameters: an instance of an entity, the relationship type, the end of the relationship, and the beginning of the relationship.</span></span> <span data-ttu-id="a2f21-111">（選擇性）您只能將實體的實例和關聯性類型傳遞給 `Navigate` 運算子。</span><span class="sxs-lookup"><span data-stu-id="a2f21-111">Optionally, you can pass only an instance of an entity and the relationship type to the `Navigate` operator.</span></span>  
  
 [!code-csharp[DP EntityServices Concepts#NavigateWithNavOperatorWithEntityCommand](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/source.cs#navigatewithnavoperatorwithentitycommand)]
 [!code-vb[DP EntityServices Concepts#NavigateWithNavOperatorWithEntityCommand](../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp entityservices concepts/vb/source.vb#navigatewithnavoperatorwithentitycommand)]  
  
## <a name="see-also"></a><span data-ttu-id="a2f21-112">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a2f21-112">See also</span></span>

- [<span data-ttu-id="a2f21-113">Entity Framework 的 EntityClient 提供者</span><span class="sxs-lookup"><span data-stu-id="a2f21-113">EntityClient Provider for the Entity Framework</span></span>](entityclient-provider-for-the-entity-framework.md)
- [<span data-ttu-id="a2f21-114">Entity SQL 語言</span><span class="sxs-lookup"><span data-stu-id="a2f21-114">Entity SQL Language</span></span>](./language-reference/entity-sql-language.md)
