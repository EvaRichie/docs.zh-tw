---
title: 作法：將變更提交至資料庫
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: c7cba174-9d40-491d-b32c-f2d73b7e9eab
ms.openlocfilehash: 5952cce5469d7a7e13e8b896f91ea1279fd62d8b
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91197036"
---
# <a name="how-to-submit-changes-to-the-database"></a>作法：將變更提交至資料庫

不論對物件進行多少的變更，都只會變更記憶體中的複本。 並不會變更到資料庫中的實際資料。 在 <xref:System.Data.Linq.DataContext.SubmitChanges%2A> 上明確呼叫 <xref:System.Data.Linq.DataContext> 之前，變更都不會傳輸至伺服器。  
  
 進行這個呼叫時，<xref:System.Data.Linq.DataContext> 會嘗試將變更轉譯為對等的 SQL 命令。 您可以使用自己的自訂邏輯來覆寫這些動作，但提交的順序是由 <xref:System.Data.Linq.DataContext> 稱為「 *變更處理器*」的服務所協調。 事件順序如下：  
  
1. 呼叫 <xref:System.Data.Linq.DataContext.SubmitChanges%2A> 時，[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 會檢查這組已知的物件，判斷新的執行個體 (Instance) 是否已附加至它們。 如果已連接，則這些新的執行個體會加入至這組已追蹤的物件中。  
  
2. 所有具有暫止變更的物件，都會根據它們之間的相依性來排序為一串物件。 而變更是根據其他物件的物件，則會循序放在它們的相依性後面。  
  
3. 在傳輸任何實際變更之前，[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 會先啟動交易來封裝一系列個別的命令。  
  
4. 物件的變更會一個接著一個地轉換為 SQL 命令，並傳送給伺服器。  
  
 此時，資料庫偵測到的任何錯誤都會停止提交流程，並引發例外狀況。 而資料庫的所有變更都會復原為未進行提交之前的狀態。 <xref:System.Data.Linq.DataContext> 仍然具有所有變更的完整記錄。 因此，您可以嘗試更正問題，並再次呼叫 <xref:System.Data.Linq.DataContext.SubmitChanges%2A>，如下列程式碼範例所示。  
  
## <a name="example"></a>範例  

 當提交異動順利完成時，<xref:System.Data.Linq.DataContext> 會略過變更追蹤資訊，以接受物件的變更。  
  
 [!code-csharp[DLinqSubmittingChanges#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSubmittingChanges/cs/Program.cs#1)]
 [!code-vb[DLinqSubmittingChanges#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSubmittingChanges/vb/Module1.vb#1)]  
  
## <a name="see-also"></a>另請參閱

- [作法：偵測和解決發生衝突的提交內容](how-to-detect-and-resolve-conflicting-submissions.md)
- [作法：管理變更衝突](how-to-manage-change-conflicts.md)
- [下載範例資料庫](downloading-sample-databases.md)
- [變更資料和提交](making-and-submitting-data-changes.md)
