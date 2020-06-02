---
title: 模擬和還原
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WindowsIdentity objects, impersonating
- security [.NET Framework], impersonating Windows accounts
- impersonating Windows accounts
ms.assetid: b93d402c-6c28-4f50-b2bc-d9607dc3e470
ms.openlocfilehash: dbfd71830ace1eb8af9f55f06c9ce35c32d592bb
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84288013"
---
# <a name="impersonating-and-reverting"></a>模擬和還原
有時候您可能需要取得 Windows 帳戶權杖，才能模擬 Windows 帳戶。 例如，ASP.NET 型應用程式可能必須在不同的時間代表數個使用者。 您的應用程式可能會接受來自網際網路資訊服務 (IIS) 代表系統管理員的權杖、模擬該使用者、執行作業，然後還原成之前的身分識別。 接下來，它可能會接受來自 IIS 代表具有較少權限的使用者的權杖、執行某項作業，然後再次還原。  
  
 當您的應用程式必須模擬尚未由 IIS 附加至目前執行緒的 Windows 帳戶時，您必須擷取該帳戶的權杖並使用它來啟動帳戶。 您可以執行下列工作來達成這點：  
  
1. 藉由呼叫未受管理的 **LogonUser** 方法，擷取特定使用者的帳戶權杖。 這個方法不在 .NET Framework 基底類別庫中，而是位於未受管理的 **advapi32.dll**。 存取 Unmanaged 程式碼中的方法是進階的操作，已超出本文的討論範圍。 如需詳細資訊，請參閱[與 Unmanaged 程式碼互通](../../framework/interop/index.md)。 如需 **LogonUser** 方法和 **advapi32.dll** 的詳細資訊，請參閱 Platform SDK 文件。  
  
2. 建立 **WindowsIdentity** 類別的新執行個體，並傳遞權杖。 下列程式碼會示範此呼叫，其中 `hToken` 代表 Windows 權杖。  
  
    ```csharp  
    WindowsIdentity impersonatedIdentity = new WindowsIdentity(hToken);  
    ```  
  
    ```vb  
    Dim impersonatedIdentity As New WindowsIdentity(hToken)  
    ```  
  
3. 開始模擬時請先建立 <xref:System.Security.Principal.WindowsImpersonationContext> 類別的新執行個體，並使用已始化類別的 <xref:System.Security.Principal.WindowsIdentity.Impersonate%2A?displayProperty=nameWithType> 方法來將它初始化，如下列程式碼所示。  
  
    ```csharp  
    WindowsImpersonationContext myImpersonation = impersonatedIdentity.Impersonate();  
    ```  
  
    ```vb  
    WindowsImpersonationContext myImpersonation = impersonatedIdentity.Impersonate()  
    ```  
  
4. 當您不再需要模擬時，呼叫 <xref:System.Security.Principal.WindowsImpersonationContext.Undo%2A?displayProperty=nameWithType> 方法將模擬還原，如下列程式碼所示。  
  
    ```csharp  
    myImpersonation.Undo();  
    ```  
  
    ```vb  
    myImpersonation.Undo()  
    ```  
  
 如果信任的程式碼已將 <xref:System.Security.Principal.WindowsPrincipal> 物件附加至執行緒，您可以呼叫實例方法模擬**Impersonate**，這不會採用帳戶 token。 請注意，這只適用於執行緒上的 **WindowsPrincipal** 物件代表非處理序目前執行所使用之使用者身分的使用者。 比方說，您可能會在使用 ASP.NET 並開啟 Windows 驗證、關閉模擬時遇到這種情況。 在此情況下，處理序會以網際網路資訊服務 (IIS) 中設定的帳戶身分執行，同時主體代表正在存取網頁的 Windows 使用者。  
  
 請注意，**模擬**或**復原**都不**Principal**會變更 <xref:System.Security.Principal.IPrincipal> 與目前呼叫內容關聯的主體物件（）。 相反地，模擬和還原會變更與目前作業系統處理序相關聯的權杖。  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Security.Principal.WindowsIdentity>
- <xref:System.Security.Principal.WindowsImpersonationContext>
- [Principal 和 Identity 物件](principal-and-identity-objects.md)
- [與 Unmanaged 程式碼互通](../../framework/interop/index.md)
