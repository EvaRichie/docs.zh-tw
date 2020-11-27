---
title: 作法：指定服務的資訊安全內容
description: 指定服務的安全性內容。 在預設系統帳戶內容中執行的服務，其系統資源存取權限與已登入的使用者不同。
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Service applications, security
- security [Visual Studio], contexts
- contexts, Visual Studio security
- security [Visual Studio], service applications
- ServiceProcessInstaller class, security context
- services, security
- ServiceInstaller class, security context
ms.assetid: 02187c7b-dbf2-45f2-96c2-e11010225a22
ms.openlocfilehash: dcf0680f1bcb0f0e927bdb37ea56f7b3025be09b
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96270533"
---
# <a name="how-to-specify-the-security-context-for-services"></a>作法：指定服務的資訊安全內容

根據預設，服務會在與登入使用者不同的安全性內容中執行。 服務會在稱為 `LocalSystem` 的預設系統帳戶內容中執行，授與他們與使用者不同的系統資源存取權限。 您可以變更此行為，以指定服務應在其中執行的不同使用者帳戶。  
  
 您可以藉由針對服務執行所在的處理序，操作 <xref:System.ServiceProcess.ServiceProcessInstaller.Account%2A> 屬性來設定安全性內容。 這個屬性可讓您將服務設定為下列其中一種帳戶類型：  
  
- `User`，其會導致系統在安裝服務時提示輸入有效的使用者名稱和密碼，並在網路上由單一使用者所指定的帳戶內容中執行；  
  
- `LocalService`，其會在帳戶的內容中執行，以便在本機電腦上作為沒有權限的使用者，並提供匿名認證給任何遠端伺服器；  
  
- `LocalSystem`，其會在帳戶的內容中執行，以提供更廣泛的本機權限，並提供電腦的認證給任何遠端伺服器；  
  
- `NetworkService`，其會在帳戶的內容中執行，以便在本機電腦上作為沒有權限的使用者，並提供電腦的認證給任何遠端伺服器。  
  
 如需詳細資訊，請參閱 <xref:System.ServiceProcess.ServiceAccount> 列舉。  
  
### <a name="to-specify-the-security-context-for-a-service"></a>指定服務的安全性內容  
  
1. 建立服務之後，為其加入必要的安裝程式。 如需詳細資訊，請參閱[如何：將安裝程式加入服務應用程式](how-to-add-installers-to-your-service-application.md)。  
  
2. 在設計工具中，存取 `ProjectInstaller` 類別，然後按一下所要使用服務的服務處理序安裝程式。  
  
    > [!NOTE]
    > 針對每個服務應用程式，`ProjectInstaller` 類別中至少有兩個安裝元件：一個用於安裝專案中所有服務的處理序，以及一個適用於應用程式所包含每個服務的安裝程式。 在此執行個體中，您想要選取 <xref:System.ServiceProcess.ServiceProcessInstaller>。  
  
3. 在 [屬性] 視窗中，將 <xref:System.ServiceProcess.ServiceProcessInstaller.Account%2A> 屬性設定為適當的值。  
  
## <a name="see-also"></a>另請參閱

- [Windows 服務應用程式簡介](introduction-to-windows-service-applications.md)
- [作法：將安裝程式新增至服務應用程式](how-to-add-installers-to-your-service-application.md)
- [作法：建立 Windows 服務](how-to-create-windows-services.md)
