---
title: SQL Server 安全性
ms.date: 03/30/2017
ms.assetid: 9053724d-a1fb-4f0f-b9dc-7f6dd893e8ff
ms.openlocfilehash: 5db14e681b5a9445c034be60993661a61a038e08
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91177302"
---
# <a name="sql-server-security"></a>SQL Server 安全性

SQL Server 具有許多功能，可支援安全資料庫應用程式的建立。  
  
 資料竊取或破壞等一般的安全性考量，則適用於所使用的 SQL Server 版本。 資料完整性也應被視為安全性問題。 若資料未受到保護，那麼，如果允許進行特定的資料操作，並且利用不正確的值意外或惡意地修改資料或將其完全刪除，則它可能就會變得毫無價值。 此外，通常還必須遵守法律需求，例如正確儲存機密資訊。 視特定管轄區所適用的法律而定，會完全禁止儲存某些類型的個人資料。  
  
 每個 SQL Server 版本和每個 Windows 版本一樣，都具有不同的安全性功能，而越新的版本功能越強。 請務必了解，安全性功能本身無法保證安全的資料庫應用程式。 每個資料庫應用程式在其需求、執行環境、部署模型、實體位置及使用者群體中都是唯一的。 範圍內的某些本機應用程式可能只需要最低的安全性，而透過網際網路部署的其他本機應用程式或應用程式可能就需要嚴格的安全性措施以及持續的監視和評估。  
  
 您應該在設計階段就考量 SQL Server 資料庫應用程式的安全性需求，而不是事後才加以考量。 在開發週期的早期評估威脅，可讓您有機會減輕偵測到弱點之處所受到的潛在損害。  
  
 即使應用程式的初始設計很健全，但隨著系統的發展，可能就會出現新的威脅。 藉由在資料庫周圍建立多道防線，您就能將安全性缺口所造成的損害降到最低。 您的第一道防線是減少受攻擊面的範圍，除非絕對必要，否則不要授與權限。  
  
 本節中的主題簡要說明與開發人員相關的 SQL Server 安全性功能，並提供連結至《SQL Server 線上叢書》中相關主題的連結，以及提供更深入探討的其他資源。  
  
## <a name="in-this-section"></a>本節內容  

 [SQL Server 安全性概觀](overview-of-sql-server-security.md)  
 說明 SQL Server 的架構和安全性功能。  
  
 [SQL Server 中的應用程式安全性案例](application-security-scenarios-in-sql-server.md)  
 包含討論 ADO.NET 和 SQL Server 應用程式之各種應用程式安全性案例的主題。  
  
 [SQL Server Express 安全性](sql-server-express-security.md)  
 說明 SQL Server Express 的安全性考量。  
  
## <a name="related-sections"></a>相關章節  

[SQL Server Database Engine 和 Azure SQL Database 的資訊安全中心](/sql/relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database)  
描述 SQL Server 和 Azure SQL Database 的安全性考量。

[SQL Server 安裝的安全性考量](/sql/sql-server/install/security-considerations-for-a-sql-server-installation)  
描述安裝 SQL Server 之前要考慮的安全性考量。

## <a name="see-also"></a>另請參閱

- [設定 ADO.NET 應用程式的安全性](../securing-ado-net-applications.md)
- [SQL Server and ADO.NET](index.md) (SQL Server 和 ADO.NET)
