---
title: 保護用戶端應用程式的安全
ms.date: 03/30/2017
ms.assetid: 6239592e-fa7d-4dea-9f00-d296d0048b01
ms.openlocfilehash: 96b43d28d3e22df66cb7f7010916b5c7f7a86b77
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91189002"
---
# <a name="secure-client-applications"></a>保護用戶端應用程式的安全

應用程式通常含有許多部分，而這所有的部分都必須受到保護，以免產生漏洞而造成資料遺失，或因其他原因而危及系統。 建立安全的使用者介面可以避免許多問題，因為可以在攻擊者存取資料或系統資源之前就加以防堵。  
  
## <a name="validate-user-input"></a>驗證使用者輸入  

 建構存取資料的應用程式時，在證明使用者輸入沒有惡意前，應該假設他們都不懷好意， 否則應用程式可能容易遭到攻擊。 .NET Framework 所包含的類別 (Class) 可協助您強制執行輸入控制項的值領域，例如限制可輸入的字元數。 事件攔截程序則可用於撰寫程序以檢查值是否有效。 使用者輸入資料可進行驗證並使用強式型別，以限制應用程式暴露於指令碼和 SQL 插入式攻擊的機會。  
  
> [!IMPORTANT]
> 除了在用戶端應用程式中驗證使用者輸入外，您也必須在資料來源驗證使用者輸入。 攻擊者可能會選擇避開您的應用程式而直接攻擊資料來源。  
  
 [安全性和使用者輸入](../../../standard/security/security-and-user-input.md)  
 說明如何處理涉及使用者輸入而可能具有危險性的細微錯誤。  
  
 [驗證 ASP.NET Web Pages 中的使用者輸入](/previous-versions/aspnet/7kh55542(v=vs.100))  
 使用 ASP.NET 驗證控制項來驗證使用者輸入的概觀。  
  
 [Windows Form 中的使用者輸入](/dotnet/desktop/winforms/user-input-in-windows-forms)  
 針對在 Windows Forms 應用程式中驗證滑鼠及鍵盤輸入而提供連結及資訊。  
  
 [.NET Framework 規則運算式](../../../standard/base-types/regular-expressions.md)  
 說明如何使用 <xref:System.Text.RegularExpressions.Regex> 類別來檢查使用者輸入的驗證。  
  
## <a name="windows-applications"></a>Windows 應用程式  

 以往通常會以完整的使用權限來執行 Windows 應用程式。 .NET Framework 提供的基礎結構可藉由程式碼存取安全性 (CAS)，限制在 Windows 應用程式中執行的程式碼。 不過，單靠 CAS 並不足以保護應用程式。  
  
 [Windows Form 安全性](/dotnet/desktop/winforms/windows-forms-security)  
 討論如何保護 Windows Forms 應用程式並提供相關主題的連結。  
  
 [Windows Form 和 Unmanaged 應用程式](/dotnet/desktop/winforms/advanced/windows-forms-and-unmanaged-applications)  
 說明如何在 Windows Forms 應用程式中與 Unmanaged 應用程式互動。  
  
 [Windows Forms 的 ClickOnce 部署](/dotnet/desktop/winforms/clickonce-deployment-for-windows-forms)  
 說明如何在 Windows Forms 應用程式中使用 `ClickOnce` 部署，並討論安全性含意。  
  
## <a name="aspnet-and-xml-web-services"></a>ASP.NET 和 XML Web Service  

 ASP.NET 應用程式通常需要限制網站某部份的存取，並提供其他機制以保護資料和網站安全性。 這些連結提供保護 ASP.NET 應用程式的有用資訊。  
  
 XML Web Service 所提供的資料可由 ASP.NET 應用程式、Windows Forms 應用程式或其他 Web 服務使用。 除了管理 Web 服務本身的安全性外，也需要管理用戶端應用程式的安全性。  
  
 如需詳細資訊，請參閱下列資源。  
  
|資源|描述|  
|--------------|-----------------|  
|[保護 ASP.NET 的網站](/previous-versions/aspnet/91f66yxt(v=vs.100))|討論如何保護 ASP.NET 應用程式。|  
|[為使用 ASP.NET 建立的 XML Web Service 設定安全性](/previous-versions/dotnet/netframework-4.0/w67h0dw7(v=vs.100))|討論如何實作 ASP.NET Web 服務的安全性。|  
|[腳本入侵總覽](/previous-versions/aspnet/w1sw53ds(v=vs.100))|說明如何防堵指令碼式攻擊，此類攻擊會嘗試在網頁中插入惡意的字元。|  
|[Web 應用程式的基本安全性做法](/previous-versions/aspnet/zdh19h94(v=vs.100))|一般安全性資訊以及進階討論區的連結。|  
  
## <a name="remoting"></a>遠端  

 .NET 遠端處理可讓您輕鬆建置四處分散的應用程式，不論應用程式元件全都集中在同一台電腦或散佈在全世界各個角落。 您可以建置用戶端應用程式，讓它們使用相同電腦 (或其網路上可連接的任何其他電腦) 上其他處理序中的物件。 也可以使用 .NET 遠端處理，與同一處理序中的其他應用程式定義域通訊。  
  
|資源|描述|  
|--------------|-----------------|  
|[遠端應用程式的組態](/previous-versions/dotnet/netframework-4.0/b8tysty8(v=vs.100))|討論如何設定遠端處理應用程式以避免常見問題。|  
|[遠端處理中的安全性](/previous-versions/dotnet/netframework-4.0/9hwst9th(v=vs.100))|說明驗證和加密，以及與遠端處理相關的其他安全性主題。|  
|[安全性和遠端處理考量](../../misc/security-and-remoting-considerations.md)|說明受保護的物件和跨應用程式定義域的安全性問題。|  
  
## <a name="see-also"></a>另請參閱

- [設定 ADO.NET 應用程式的安全性](securing-ado-net-applications.md)
- [資料存取策略的建議](/previous-versions/visualstudio/visual-studio-2008/8fxztkff(v=vs.90))
- [保護應用程式](/visualstudio/ide/securing-applications)
- [保護連接資訊](protecting-connection-information.md)
- [ADO.NET 概觀](ado-net-overview.md) \(部分機器翻譯\)
