---
title: 雲端原生應用程式中的驗證和授權
description: 架構適用于 Azure 的雲端原生 .NET 應用程式 |雲端原生應用程式中的驗證和授權
ms.date: 05/13/2020
ms.openlocfilehash: e5254560ac82662e5e3ea6a25997516cd2b478b0
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2020
ms.locfileid: "83614301"
---
# <a name="authentication-and-authorization-in-cloud-native-apps"></a>雲端原生應用程式中的驗證與授權

*驗證*是判斷安全性主體身分識別的程式。 *授權*是授與已驗證的主體許可權來執行動作或存取資源的動作。 有時會將驗證縮短為 `AuthN` ，並將授權縮短為 `AuthZ` 。 雲端原生應用程式必須依賴 open HTTP 型通訊協定來驗證安全性主體，因為用戶端和應用程式都可以在任何平臺或裝置上的世界各地執行。 唯一的常見因素是 HTTP。

許多組織仍依賴本機驗證服務，例如 Active Directory 同盟服務（ADFS）。 雖然這種方法在過去是針對內部部署驗證需求而提供服務，但雲端原生應用程式可受益于專為雲端設計的系統。 最近的2019英國國家網路安全中心（NCSC）諮詢指出「使用 Azure AD 做為主要驗證來源的組織，實際上會降低其與 ADFS 的風險。」 [這項分析](https://oxfordcomputergroup.com/resources/o365-security-native-cloud-authentication/)中所述的一些原因包括：

- 存取一組完整的 Microsoft 認證保護技術。
- 大部分的組織都已經依賴 Azure AD 到某種程度。
- NTLM 雜湊的雙重雜湊可確保洩露不會允許在本機 Active Directory 中使用的認證。

## <a name="references"></a>參考

- [驗證基本概念](https://docs.microsoft.com/azure/active-directory/develop/authentication-scenarios)
- [存取權杖和宣告](https://docs.microsoft.com/azure/active-directory/develop/access-tokens)
- [可能有時間揚棄您的內部部署驗證服務](https://oxfordcomputergroup.com/resources/o365-security-native-cloud-authentication/)

>[!div class="step-by-step"]
>[上一個](identity.md) 
>[下一步](azure-active-directory.md)
