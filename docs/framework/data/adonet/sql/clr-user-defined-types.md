---
title: CLR 使用者定義類型
ms.date: 03/30/2017
ms.assetid: 9f70e0b0-3a0d-4eb1-b914-07a5d0c167c2
ms.openlocfilehash: 84d588e0c415daa7de19ea695c817f3eb24f732f
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91173584"
---
# <a name="clr-user-defined-types"></a>CLR 使用者定義類型

Microsoft SQL Server 可支援以 Microsoft .NET Framework Common Language Runtime (CLR) 實作的使用者定義型別 (UDT)。 這項將 CLR 整合進 SQL Server 的機制可讓您擴充資料庫的型別系統。 UDT 可讓使用者擴充 SQL Server 資料型別系統，以及定義複雜的結構化型別。  
  
 從應用程式架構的角度來看，UDT 有兩個主要優點：  
  
- (在用戶端及伺服器上) 強式封裝內部狀態與外部行為。  
  
- 與其他相關伺服器功能深度整合。 定義自己的 UDT 後，您可在 SQL Server 中所有可以使用系統型別的內容中使用它，包括資料行定義以及做為變數、參數、函式結果、游標、觸發程序及複寫。  
  
 如需詳細資訊，請參閱您所使用之 SQL Server 版本的 [SQL Server 檔](/sql) 。
  
 **SQL Server 文件**
  
1. [CLR 使用者定義類型](/sql/relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types)  
  
## <a name="see-also"></a>另請參閱

- [ADO.NET 概觀](../ado-net-overview.md) \(部分機器翻譯\)
