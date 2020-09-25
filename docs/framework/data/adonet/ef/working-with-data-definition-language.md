---
title: 使用資料定義語言
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: ec50083d-44f4-4093-9b23-5eacd601f96e
ms.openlocfilehash: c30cbbc1eae6d4cbcadb9bfe8d267fb428764971
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91200884"
---
# <a name="working-with-data-definition-language"></a>使用資料定義語言

從 .NET Framework 第4版開始，Entity Framework 支援 (DDL) 資料定義語言。 這可讓您根據連接字串和儲存體 (SSDL) 模型的中繼資料，建立或刪除資料庫執行個體。  
  
 <xref:System.Data.Objects.ObjectContext> 的下列方法會使用連接字串和 SSDL 內容來達成下列目的：建立或刪除資料庫、檢查資料庫是否存在，以及檢視產生的 DDL 指令碼：  
  
- <xref:System.Data.Objects.ObjectContext.CreateDatabase%2A>  
  
- <xref:System.Data.Objects.ObjectContext.DeleteDatabase%2A>  
  
- <xref:System.Data.Objects.ObjectContext.DatabaseExists%2A>  
  
- <xref:System.Data.Objects.ObjectContext.CreateDatabaseScript%2A>  
  
> [!NOTE]
> 執行 DDL 命令需要足夠的權限。  
  
 先前所列的方法會將大部分工作委派給基礎 ADO.NET 資料提供者。 提供者要負責確保用來產生資料庫物件的命名慣例與用於查詢和更新的慣例一致。  
  
 下列範例將為您示範如何根據現有的模型產生資料庫。 此外，這個範例也會將新的實體物件加入至物件內容，然後將它儲存至資料庫。  
  
## <a name="procedures"></a>程序  
  
### <a name="to-define-a-database-based-on-the-existing-model"></a>若要根據現有的模型定義資料庫  
  
1. 建立主控台應用程式。  
  
2. 將現有的模型加入至應用程式。  
  
    1. 加入名為的空模型 `SchoolModel` 。 若要建立空的模型，請參閱 [如何：建立新的 .edmx](/previous-versions/dotnet/netframework-4.0/cc716703(v=vs.100)) 檔主題。  
  
     SchoolModel.edmx 檔案就會加入至您的專案。  
  
    1. 從 [School 模型](/previous-versions/dotnet/netframework-4.0/bb896300(v=vs.100)) 主題複製 school 模型的概念、儲存體和對應內容。  
  
    2. 開啟 SchoolModel.edmx 檔案並在 `edmx:Runtime` 標記中貼上內容。  
  
3. 將下列程式碼加入至 main 函式。 此程式碼會將連接字串初始化為資料庫伺服器、檢視 DDL 指令碼、建立資料庫、將新的實體加入至內容，並且將變更儲存至資料庫。  
  
     [!code-csharp[DP ObjectServices Concepts#DDL](../../../../../samples/snippets/csharp/VS_Snippets_Data/DP ObjectServices Concepts/CS/Source.cs#ddl)]
     [!code-vb[DP ObjectServices Concepts#DDL](../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP ObjectServices Concepts/VB/Source.vb#ddl)]
