---
title: 作法：使用 EntityCommand 執行參數化預存程序
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 4f5639bf-bb7f-4982-bb1d-c7caa4348888
ms.openlocfilehash: ec1ff7cdbdc83bc409b191f0aefe2b50cbad9225
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91192161"
---
# <a name="how-to-execute-a-parameterized-stored-procedure-using-entitycommand"></a><span data-ttu-id="03cd4-102">作法：使用 EntityCommand 執行參數化預存程序</span><span class="sxs-lookup"><span data-stu-id="03cd4-102">How to: Execute a Parameterized Stored Procedure Using EntityCommand</span></span>

<span data-ttu-id="03cd4-103">本主題顯示如何使用 <xref:System.Data.EntityClient.EntityCommand> 類別，執行參數化預存程序。</span><span class="sxs-lookup"><span data-stu-id="03cd4-103">This topic shows how to execute a parameterized stored procedure by using the <xref:System.Data.EntityClient.EntityCommand> class.</span></span>  
  
### <a name="to-run-the-code-in-this-example"></a><span data-ttu-id="03cd4-104">執行此範例中的程式碼</span><span class="sxs-lookup"><span data-stu-id="03cd4-104">To run the code in this example</span></span>  
  
1. <span data-ttu-id="03cd4-105">將 [School 模型](/previous-versions/dotnet/netframework-4.0/bb896300(v=vs.100)) 新增至您的專案，並將您的專案設定為使用 Entity Framework。</span><span class="sxs-lookup"><span data-stu-id="03cd4-105">Add the [School Model](/previous-versions/dotnet/netframework-4.0/bb896300(v=vs.100)) to your project and configure your project to use the Entity Framework.</span></span> <span data-ttu-id="03cd4-106">如需詳細資訊，請參閱 [如何：使用實體資料模型 Wizard](/previous-versions/dotnet/netframework-4.0/bb738677(v=vs.100))。</span><span class="sxs-lookup"><span data-stu-id="03cd4-106">For more information, see [How to: Use the Entity Data Model Wizard](/previous-versions/dotnet/netframework-4.0/bb738677(v=vs.100)).</span></span>  
  
2. <span data-ttu-id="03cd4-107">在應用程式的字碼頁中加入下列 `using` 陳述式 (在 Visual Basic 中為 `Imports`)：</span><span class="sxs-lookup"><span data-stu-id="03cd4-107">In the code page for your application, add the following `using` statements (`Imports` in Visual Basic):</span></span>  
  
     [!code-csharp[DP EntityServices Concepts#Namespaces](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/source.cs#namespaces)]
     [!code-vb[DP EntityServices Concepts#Namespaces](../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp entityservices concepts/vb/source.vb#namespaces)]  
  
3. <span data-ttu-id="03cd4-108">匯入 `GetStudentGrades` 預存程序，並指定 `CourseGrade` 實體做為傳回型別。</span><span class="sxs-lookup"><span data-stu-id="03cd4-108">Import the `GetStudentGrades` stored procedure and specify `CourseGrade` entities as a return type.</span></span> <span data-ttu-id="03cd4-109">如需如何匯入預存程式的詳細資訊，請參閱 [如何：匯入預存](/previous-versions/dotnet/netframework-4.0/bb896231(v=vs.100))程式。</span><span class="sxs-lookup"><span data-stu-id="03cd4-109">For information on how to import a stored procedure, see [How to: Import a Stored Procedure](/previous-versions/dotnet/netframework-4.0/bb896231(v=vs.100)).</span></span>  
  
## <a name="example"></a><span data-ttu-id="03cd4-110">範例</span><span class="sxs-lookup"><span data-stu-id="03cd4-110">Example</span></span>  

 <span data-ttu-id="03cd4-111">下列程式碼會執行 `GetStudentGrades` 預存程序，其中 `StudentId` 是必要參數。</span><span class="sxs-lookup"><span data-stu-id="03cd4-111">The following code executes the `GetStudentGrades` stored procedure where `StudentId` is a required parameter.</span></span> <span data-ttu-id="03cd4-112">然後 <xref:System.Data.EntityClient.EntityDataReader> 會讀取結果。</span><span class="sxs-lookup"><span data-stu-id="03cd4-112">The results are then read by an <xref:System.Data.EntityClient.EntityDataReader>.</span></span>  
  
 [!code-csharp[DP EntityServices Concepts#StoredProcWithEntityCommand](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/source.cs#storedprocwithentitycommand)]
 [!code-vb[DP EntityServices Concepts#StoredProcWithEntityCommand](../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp entityservices concepts/vb/source.vb#storedprocwithentitycommand)]  
  
## <a name="see-also"></a><span data-ttu-id="03cd4-113">另請參閱</span><span class="sxs-lookup"><span data-stu-id="03cd4-113">See also</span></span>

- [<span data-ttu-id="03cd4-114">Entity Framework 的 EntityClient 提供者</span><span class="sxs-lookup"><span data-stu-id="03cd4-114">EntityClient Provider for the Entity Framework</span></span>](entityclient-provider-for-the-entity-framework.md)
