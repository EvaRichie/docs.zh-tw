---
title: SQL Server 中的授權和權限
description: 瞭解如何明確授與許可權，讓您可以在 SQL Server 中使用 ADO.NET 存取您所建立的資料庫物件。
ms.date: 03/30/2017
ms.assetid: d340405c-91f4-4837-a3cc-a238ee89888a
ms.openlocfilehash: 748d40ff2c64ae59f43e6296ef591efcb5ff9831
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91197491"
---
# <a name="authorization-and-permissions-in-sql-server"></a>SQL Server 中的授權和權限

當您建立資料庫物件時，必須明確地授與權限，讓使用者能夠存取這些物件。 每個安全性實體物件都具有可利用權限陳述式來授與主體的權限。  
  
## <a name="the-principle-of-least-privilege"></a>最小權限的原則  

 使用最小權限使用者帳戶 (LUA) 方法來開發應用程式是抵禦安全性威脅之深入防禦策略中很重要的一部分。 LUA 方法可確保使用者遵循最小權限的原則而且永遠以受限制的使用者帳戶進行登入。 管理工作是使用固定伺服器角色區分的，而且 `sysadmin` 固定伺服器角色的使用方式嚴格受限。  
  
 授與權限給資料庫使用者時，請務必遵守最小權限的原則。 請授與完成指定工作所需的最小權限給使用者或角色。  
  
> [!IMPORTANT]
> 使用 LUA 方法來開發和測試應用程式會對開發程序造成某種程度的困難。 就建立物件和撰寫程式碼而言，以系統管理員或資料庫擁有者的身分登入會比使用 LUA 帳戶更方便。 不過，當最小權限的使用者嘗試執行需要更高權限才能正常運作的應用程式時，使用高權限帳戶來開發應用程式可能會模糊化縮減功能的影響。 授與過高權限給使用者以便重新取得喪失的功能可能會讓應用程式容易遭受攻擊。 以 LUA 帳戶登入並設計、開發和測試應用程式會對安全性規劃強制執行規範的方法，進而排除不愉快的意外情況以及授與更高權限當做快速修正的誘惑。 即使您的應用程式必須使用 Windows 驗證進行部署，您還是可以使用 SQL Server 登入進行測試。  
  
## <a name="role-based-permissions"></a>以角色為基礎的權限  

 授與權限給角色而非使用者可簡化安全性管理作業。 指派給角色的權限集合會由該角色的所有成員繼承。 在某個角色中加入或移除使用者會比針對個別使用者重新建立不同的權限集合更容易。 雖然角色可以巢狀化，但是巢狀層級過多可能會降低效能。 此外，您也可以將使用者加入至固定資料庫角色，以便簡化指派權限的作業。  
  
 您可以在結構描述層級授與權限。 使用者會自動繼承在該結構描述中建立之所有新物件的權限。您不需要在建立新物件時授與權限。  
  
## <a name="permissions-through-procedural-code"></a>透過程序性程式碼授與權限  

 透過預存程序 (Stored Procedure) 和使用者定義函式等模組來封裝資料存取會對應用程式提供額外的保護層。 您可以單獨授與預存程序或函式的權限而拒絕基礎物件 (例如資料表) 的權限，藉以防止使用者直接與資料庫物件進行互動。 SQL Server 可透過擁有權鏈結達到此目的。  
  
## <a name="permission-statements"></a>權限陳述式  

 下表將描述三個 Transact-SQL 權限陳述式。  
  
|權限陳述式|描述|  
|--------------------------|-----------------|  
|GRANT|授與權限。|  
|REVOKE|撤銷權限。 這是新物件的預設狀態。 從某個使用者或角色中撤銷的權限仍然可以繼承自被指派主體的其他群組或角色。|  
|拒絕|DENY 會撤銷權限，讓它無法被繼承。 DENY 的優先順序高於所有權限，但是 DENY 無法套用至物件擁有者或 `sysadmin` 的成員。 如果您針對 `public` 角色拒絕 (DENY) 某個物件的權限，就會一併拒絕所有使用者和角色，但物件擁有者和 `sysadmin` 成員除外。|  
  
- GRANT 陳述式可以指派權限給某個群組或角色，而資料庫角色可以繼承這些權限。 不過，DENY 陳述式的優先順序高於所有其他權限陳述式。 因此，已經被拒絕某個權限的使用者無法從另一個角色繼承該權限。  
  
> [!NOTE]
> `sysadmin` 固定伺服器角色的成員和物件擁有者無法被拒絕權限。  
  
## <a name="ownership-chains"></a>擁有權鏈結  

 SQL Server 會確保只有已經被授與權限的主體才能存取物件。 當多個資料庫物件彼此存取時，這個序列 (Sequence) 便稱為鏈結。 當 SQL Server 周遊鏈結中的連結時，它評估權限的方式與個別存取每個項目時的處理方式不同。 透過鏈結存取物件時，SQL Server 會先比較物件的擁有者與呼叫物件的擁有者 (鏈結中的上一個連結)。 如果這兩個物件具有相同的擁有者，系統就不會檢查參考物件的權限。 只要某個物件存取具有不同擁有者的另一個物件，擁有權鏈結就會中斷而且 SQL Server 必須檢查呼叫端的安全性內容。  
  
## <a name="procedural-code-and-ownership-chaining"></a>程序性程式碼和擁有權鏈結  

 假設某位使用者被授與從資料表中選取資料之預存程序的執行權限。 如果此預存程序與資料表具有相同的擁有者，使用者就不需要被授與資料表的任何權限，甚至可以被拒絕權限。 不過，如果此預存程序與資料表具有不同的擁有者，SQL Server 就必須檢查使用者對資料表擁有的權限，然後再允許存取資料。  
  
> [!NOTE]
> 在動態 SQL 陳述式的情況中，擁有權鏈結並不適用。 為了呼叫執行 SQL 陳述式的程序，呼叫端必須被授與基礎資料表的權限，因而讓應用程式容易遭受 SQL 插入式攻擊。 SQL Server 提供不需要授與基礎資料表之權限的全新機制，例如模擬以及使用憑證來簽署模組。 這些機制也可以搭配 CLR 預存程序使用。  
  
## <a name="external-resources"></a>外部資源  

 如需詳細資訊，請參閱下列資源。  
  
|資源|描述|  
|--------------|-----------------|  
|[權限](/sql/relational-databases/security/permissions-database-engine)|包含說明權限階層、目錄檢視以及固定伺服器與資料庫角色之權限的主題。|
  
## <a name="see-also"></a>另請參閱

- [設定 ADO.NET 應用程式的安全性](../securing-ado-net-applications.md)
- [SQL Server 中的應用程式安全性案例](application-security-scenarios-in-sql-server.md)
- [在 SQL Server 中進行驗證](authentication-in-sql-server.md)
- [SQL Server 中的伺服器和資料庫角色](server-and-database-roles-in-sql-server.md)
- [SQL Server 中的擁有權和使用者結構描述分離](ownership-and-user-schema-separation-in-sql-server.md)
- [ADO.NET 概觀](../ado-net-overview.md) \(部分機器翻譯\)
