---
title: 使用 WCF 開發工具
ms.date: 03/30/2017
ms.assetid: 054adb87-c244-4d5a-83d1-0b2b44bd454b
ms.openlocfilehash: 48733d27a72e864760c371e8b90e0af7b74273a0
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96273642"
---
# <a name="using-the-wcf-development-tools"></a><span data-ttu-id="1afca-102">使用 WCF 開發工具</span><span class="sxs-lookup"><span data-stu-id="1afca-102">Using the WCF Development Tools</span></span>

<span data-ttu-id="1afca-103">本節說明可協助您開發 WCFservice 的 Visual Studio 開發工具。</span><span class="sxs-lookup"><span data-stu-id="1afca-103">This section describes the Visual Studio development tools that can assist you in developing your WCFservice.</span></span>  
  
 <span data-ttu-id="1afca-104">您可以使用 Visual Studio 範本作為基礎來快速建立您自己的服務，然後使用 WCF 服務自動主機和 WCF 測試用戶端來對您的服務進行 debug 錯和測試。</span><span class="sxs-lookup"><span data-stu-id="1afca-104">You can use the Visual Studio templates as a foundation to quickly build your own service, then use WCF Service Auto Host and WCF Test Client to debug and test your service.</span></span> <span data-ttu-id="1afca-105">這些工具都提供了迅速完善的偵錯與測試循環，而且在早期階段不需要認可裝載模型。</span><span class="sxs-lookup"><span data-stu-id="1afca-105">These tools together provide a fast and seamless debug and testing cycle, and preclude the need to commit to a hosting model at an early stage.</span></span>  

 > [!NOTE]
 > <span data-ttu-id="1afca-106">從 Visual Studio 2017 開始，預設不會安裝 WCF 開發工具。</span><span class="sxs-lookup"><span data-stu-id="1afca-106">Starting with Visual Studio 2017, the WCF development tools are not installed by default.</span></span> <span data-ttu-id="1afca-107">為了使用這些功能，您必須確定已在 Visual Studio 安裝程式中選取 Windows Communication Foundation 元件。</span><span class="sxs-lookup"><span data-stu-id="1afca-107">In order to use these features, you must ensure the Windows Communication Foundation component is selected in the Visual Studio installer.</span></span>
  
## <a name="the-wcf-developer-tools"></a><span data-ttu-id="1afca-108">WCF 開發者工具</span><span class="sxs-lookup"><span data-stu-id="1afca-108">The WCF Developer Tools</span></span>  

 [<span data-ttu-id="1afca-109">WCF Visual Studio 範本</span><span class="sxs-lookup"><span data-stu-id="1afca-109">WCF Visual Studio Templates</span></span>](wcf-vs-templates.md)  
  
 <span data-ttu-id="1afca-110">您可以使用 Visual Studio 中預先定義的 Visual Studio 專案和專案範本，快速建立 WCF 服務和周圍的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1afca-110">You can use the predefined Visual Studio project and item templates in Visual Studio to quickly build WCF services and surrounding applications.</span></span>  
  
 [<span data-ttu-id="1afca-111">WCF 服務主機 (WcfSvcHost.exe)</span><span class="sxs-lookup"><span data-stu-id="1afca-111">WCF Service Host (WcfSvcHost.exe)</span></span>](wcf-service-host-wcfsvchost-exe.md)  
  
 <span data-ttu-id="1afca-112">WCF Service Auto Host ( # A0) 可讓您啟動 Visual Studio 偵錯工具 (F5) ，以自動裝載和測試您已執行的服務。</span><span class="sxs-lookup"><span data-stu-id="1afca-112">The WCF Service Auto Host (WcfSvcHost.exe) allows you to launch the Visual Studio debugger (F5) to automatically host and test a service you have implemented.</span></span> <span data-ttu-id="1afca-113">然後，您可以使用 WCF 測試用戶端 ( # A0) 或您自己的用戶端來測試服務，以尋找並修正任何可能的錯誤。</span><span class="sxs-lookup"><span data-stu-id="1afca-113">You can then test the service using the WCF Test Client (wcfTestClient.exe) or your own client to find and fix any potential errors.</span></span>  
  
 [<span data-ttu-id="1afca-114">WCF 測試用戶端 (WcfTestClient.exe)</span><span class="sxs-lookup"><span data-stu-id="1afca-114">WCF Test Client (WcfTestClient.exe)</span></span>](wcf-test-client-wcftestclient-exe.md)  
  
 <span data-ttu-id="1afca-115">WCF 測試用戶端 ( # A0) 是一種 GUI 工具，可讓您輸入任意類型的參數、將該輸入提交至服務，以及查看服務傳回的回應。</span><span class="sxs-lookup"><span data-stu-id="1afca-115">WCF Test Client (WcfTestClient.exe) is a GUI tool that allows you to input parameters of arbitrary types, submit that input to the service, and view the response the service sends back.</span></span> <span data-ttu-id="1afca-116">它會在結合 WCF 服務自動主機時提供順暢的服務測試體驗。</span><span class="sxs-lookup"><span data-stu-id="1afca-116">It provides a seamless service testing experience when combined with WCF Service Auto Host.</span></span>  
  
 [<span data-ttu-id="1afca-117">從 XML 產生資料型別類型</span><span class="sxs-lookup"><span data-stu-id="1afca-117">Generating Data Type Classes from XML</span></span>](generating-data-type-classes-from-xml.md)  
  
 <span data-ttu-id="1afca-118">儲存在剪貼簿中的 XML 資料可以貼到程式碼頁面上。</span><span class="sxs-lookup"><span data-stu-id="1afca-118">XML data stored in the clipboard can be pasted into a code page.</span></span> <span data-ttu-id="1afca-119">在資料中定義的類別將會轉換為程式碼型別。</span><span class="sxs-lookup"><span data-stu-id="1afca-119">The classes defined in the data will be converted to code types.</span></span>  
  
## <a name="using-the-tools-without-administrator-privilege"></a><span data-ttu-id="1afca-120">在沒有系統管理員權限的情況下使用工具</span><span class="sxs-lookup"><span data-stu-id="1afca-120">Using the Tools without Administrator privilege</span></span>  

 <span data-ttu-id="1afca-121">若要讓沒有系統管理員許可權的使用者開發 WCF 服務，安裝 Visual Studio 期間會為命名空間 "" 建立 ACL (存取控制清單) http://+:8731/Design_Time_Addresses 。</span><span class="sxs-lookup"><span data-stu-id="1afca-121">To enable users without administrator privilege to develop WCF services, an ACL (Access Control List) is created for the namespace "http://+:8731/Design_Time_Addresses" during the installation of Visual Studio.</span></span> <span data-ttu-id="1afca-122">ACL 會設定為 (UI)，其中包含已登入電腦的所有互動使用者。</span><span class="sxs-lookup"><span data-stu-id="1afca-122">The ACL is set to (UI), which includes all interactive users logged on to the machine.</span></span> <span data-ttu-id="1afca-123">系統管理員可以在這個 ACL 中新增或移除使用者，或是開啟其他連接埠。這個 ACL 可讓 WCF 或 WF 範本傳送及接收其預設組態中的資料。</span><span class="sxs-lookup"><span data-stu-id="1afca-123">Administrators can add or remove users from this ACL, or open additional ports.This ACL enables WCF or WF templates to send and receive data in their default configuration.</span></span> <span data-ttu-id="1afca-124">它也可讓使用者在不授與系統管理員許可權的情況下，使用 WCF Service Auto Host ( # A0) 。</span><span class="sxs-lookup"><span data-stu-id="1afca-124">It also enables users to use the WCF Service Auto Host (wcfSvcHost.exe) without granting them administrator privileges.</span></span>  
  
 <span data-ttu-id="1afca-125">您可以使用 Windows Vista 中的 [Netsh.exe] 工具，以提高許可權的系統管理員帳戶修改存取權。</span><span class="sxs-lookup"><span data-stu-id="1afca-125">You can modify access using the Netsh.exe tool in Windows Vista under the elevated administrator account.</span></span> <span data-ttu-id="1afca-126">下列是使用 Netsh.exe 的範例。</span><span class="sxs-lookup"><span data-stu-id="1afca-126">The following is an example of using Netsh.exe.</span></span>  
  
```console  
netsh http add urlacl url=http://+:8001/MyService user=<domain>\<user>  
```  
  
 <span data-ttu-id="1afca-127">如需 Netsh.exe 的詳細資訊，請參閱 [如何使用 Netsh.exe 工具和 Command-Line 參數](/previous-versions/tn-archive/bb490939(v=technet.10))。</span><span class="sxs-lookup"><span data-stu-id="1afca-127">For more information about Netsh.exe, see [How to Use the Netsh.exe Tool and Command-Line Switches](/previous-versions/tn-archive/bb490939(v=technet.10)).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="1afca-128">另請參閱</span><span class="sxs-lookup"><span data-stu-id="1afca-128">See also</span></span>

- [<span data-ttu-id="1afca-129">WCF Visual Studio 範本</span><span class="sxs-lookup"><span data-stu-id="1afca-129">WCF Visual Studio Templates</span></span>](wcf-vs-templates.md)
- [<span data-ttu-id="1afca-130">WCF 服務主機 (WcfSvcHost.exe)</span><span class="sxs-lookup"><span data-stu-id="1afca-130">WCF Service Host (WcfSvcHost.exe)</span></span>](wcf-service-host-wcfsvchost-exe.md)
- [<span data-ttu-id="1afca-131">WCF 測試用戶端 (WcfTestClient.exe)</span><span class="sxs-lookup"><span data-stu-id="1afca-131">WCF Test Client (WcfTestClient.exe)</span></span>](wcf-test-client-wcftestclient-exe.md)
