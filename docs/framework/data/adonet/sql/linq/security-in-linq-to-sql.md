---
title: LINQ to SQL 中的安全性
ms.date: 03/30/2017
ms.assetid: d49787f7-414e-4c71-aa33-80a5895536b1
ms.openlocfilehash: 6260f0c565a25764c8fabd2770d4f06a987aa9bb
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91173389"
---
# <a name="security-in-linq-to-sql"></a>LINQ to SQL 中的安全性

當您連接至資料庫時，永遠都會存在安全性風險。 雖然 LINQ to SQL 可能會包含一些使用 SQL Server 資料的新方式，但是並不會提供任何額外的安全性機制。  
  
## <a name="access-control-and-authentication"></a>存取控制和驗證  

 LINQ to SQL 本身並沒有使用者模型或驗證機制。 您可以使用 SQL Server 安全性來控制對應至物件模型 (Object Model) 之資料庫、資料庫資料表、檢視表和預存程序 (Stored Procedure) 的存取權。 請將最低必要存取權授與使用者，並且要求增強式密碼來進行使用者驗證。  
  
## <a name="mapping-and-schema-information"></a>對應和結構描述資訊  

 物件模型或外部對應檔案中的 SQL-CLR 型別對應和資料庫結構描述資訊可供所有在檔案系統中擁有這些檔案之存取權的使用者使用。 假設可以存取物件模型或外部對應檔案的所有人員都可以使用架構資訊。 若要避免更廣泛地存取架構資訊，請使用檔案安全性機制來保護來源檔案和對應檔。  
  
## <a name="connection-strings"></a>連接字串  

 請盡可能避免在連接字串中使用密碼。 不但連接字串本身會產生安全性風險，而且使用物件關聯式設計工具或 SQLMetal 命令列工具時，連接字串可能也會以純文字的方式加入至物件模型或外部對應檔案。 可經由檔案系統存取物件模型或外部對應檔案的任何人都可能會看見連接密碼 (如果包含在連接字串中的話)。  
  
 若要將這類風險降至最低，請使用整合式安全性來建立與 SQL Server 的信任連線。 使用這種方法，就不需要將密碼儲存在連接字串中。 如需詳細資訊，請參閱 [SQL Server 安全性](../sql-server-security.md)。  
  
 如果沒有整合式安全性，連接字串將會需要純文字密碼。 協助保護連接字串安全的最佳方法如下所示 (按照風險的遞增順序列出)：  
  
- 使用整合式安全性。  
  
- 使用密碼來保護連接字串的安全，並且盡可能減少在連接字串前後傳遞密碼。  
  
- 使用 <xref:System.Data.SqlClient.SqlConnection?displayProperty=nameWithType> 類別 (Class) 來取代連接字串，因為它會限制公開的持續期間。 您可以使用 <xref:System.Data.Linq.DataContext?displayProperty=nameWithType> 來具現化 LINQ to SQL <xref:System.Data.SqlClient.SqlConnection> 類別。  
  
- 盡可能減少所有連接字串的存留期 (Lifetime) 和接觸點。  
  
## <a name="see-also"></a>另請參閱

- [背景資訊](background-information.md)
- [常見問題集](frequently-asked-questions.md)
