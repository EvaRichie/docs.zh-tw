---
title: CoordinatorRecoveryLogEntryCorrupt
ms.date: 03/30/2017
ms.assetid: 3cd0c3e3-84c8-4d43-a561-a8851c78e565
ms.openlocfilehash: c3174e70d42385923674a3db5f696a0f64eda29f
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96295352"
---
# <a name="coordinatorrecoverylogentrycorrupt"></a>CoordinatorRecoveryLogEntryCorrupt

識別碼：139  
  
 嚴重性：錯誤  
  
 分類：TransactionBridge  
  
## <a name="description"></a>描述  

 此事件表示協調器修復記錄項目損毀，且無法還原序列化。 這個錯誤可能會造成資料遺失。 事件會列出異動識別碼、修復資料 (以 Base64 編碼)、例外狀況、處理序名稱和處理序識別碼。  
  
## <a name="see-also"></a>另請參閱

- [事件記錄](index.md)
- [事件一般參考](events-general-reference.md)
