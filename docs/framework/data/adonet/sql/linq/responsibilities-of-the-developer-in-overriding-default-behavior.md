---
title: 開發人員覆寫預設行為的責任
ms.date: 03/30/2017
ms.assetid: c6909ddd-e053-46a8-980c-0e12a9797be1
ms.openlocfilehash: 88a7076e12e39ed23aa6d661aa90f74258f3dded
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91200429"
---
# <a name="responsibilities-of-the-developer-in-overriding-default-behavior"></a>開發人員覆寫預設行為的責任

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 不會強制執行下列需求，但如果不符合這些需求，則行為會是未定義的。  
  
- 覆寫方法不得呼叫 <xref:System.Data.Linq.DataContext.SubmitChanges%2A> 或 <xref:System.Data.Linq.Table%601.Attach%2A>。 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 如果在覆寫方法中呼叫這些方法，則會擲回例外狀況。  
  
- 覆寫方法不可以用來啟動、認可或停止異動。 <xref:System.Data.Linq.DataContext.SubmitChanges%2A> 作業是在交易下執行。 而內部巢狀交易會干擾外部交易。 只有在載入覆寫方法判斷作業未在 <xref:System.Transactions.Transaction> 中執行之後，載入覆寫方法才可以啟動異動。  
  
- 需要有覆寫方法，才能遵循適用的開放式並行存取 (Optimistic Concurrency) 對應。 開放式並行存取發生衝突時，覆寫方法應該會擲回 <xref:System.Data.Linq.ChangeConflictException>。 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 攔截這個例外狀況，讓您可以正確地處理 <xref:System.Data.Linq.DataContext.SubmitChanges%2A> 提供的選項 <xref:System.Data.Linq.DataContext.SubmitChanges%2A> 。  
  
- 作業順利完成時，則需要建立 (`Insert`) 和 `Update` 覆寫方法將資料庫所產生的資料行值送回給對應的物件成員。  
  
     例如，如果 `Order.OrderID` 對應到識別資料行 (*自動遞增* 主鍵) ，則覆 `InsertOrder()` 寫方法必須抓取資料庫產生的識別碼，並將 `Order.OrderID` 成員設定為該識別碼。 同樣地，必須將時間戳記成員更新為資料庫產生的時間戳記值，以確定更新的物件一致。 散佈資料庫產生的值失敗，會造成資料庫與 <xref:System.Data.Linq.DataContext> 追蹤的物件不一致。  
  
- 使用者必須負責叫用 (Invoke) 正確的動態 API。 例如，在更新覆寫方法中，您只能呼叫 <xref:System.Data.Linq.DataContext.ExecuteDynamicUpdate%2A>。 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 並不會偵測或驗證所叫用的動態方法是否符合適用的作業。 如果呼叫不適用的方法 (例如，對要更新的物件呼叫 <xref:System.Data.Linq.DataContext.ExecuteDynamicDelete%2A>)，則會產生無法定義的結果。  
  
- 最後，需要有覆寫方法才能執行陳述的作業。 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 作業 (例如立即載入、延後載入和 <xref:System.Data.Linq.DataContext.SubmitChanges%2A>) 的語意 (Semantics) 需要有覆寫，才能提供陳述的服務。 例如，只傳回空集合而不檢查資料庫內容的載入覆寫，可能會導致資料不一致。  
  
## <a name="see-also"></a>另請參閱

- [自訂插入、更新和刪除作業](customizing-insert-update-and-delete-operations.md)
