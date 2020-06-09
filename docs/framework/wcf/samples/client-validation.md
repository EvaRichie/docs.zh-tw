---
title: 用戶端驗證
ms.date: 03/30/2017
ms.assetid: f0c1f805-1a81-4d0d-a112-bf5e2e87a631
ms.openlocfilehash: dce11ec2e3ef552c0c53e1faf89a12bc13b66ae0
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84585320"
---
# <a name="client-validation"></a><span data-ttu-id="f94f7-102">用戶端驗證</span><span class="sxs-lookup"><span data-stu-id="f94f7-102">Client Validation</span></span>
<span data-ttu-id="f94f7-103">服務經常會發行中繼資料，以便自動產生和設定用戶端 Proxy 型別。</span><span class="sxs-lookup"><span data-stu-id="f94f7-103">Services frequently publish metadata to enable automatic generation and configuration of client proxy types.</span></span> <span data-ttu-id="f94f7-104">當服務不受信任時，用戶端應用程式應該根據安全性、交易和服務合約類型等條件，驗證中繼資料是否符合用戶端應用程式的原則。</span><span class="sxs-lookup"><span data-stu-id="f94f7-104">When the service is not trusted, client applications should validate that the metadata conforms to the client application's policy regarding security, transactions, the type of service contract and so on.</span></span> <span data-ttu-id="f94f7-105">下列範例會示範如何撰寫用戶端端點行為，此行為會驗證服務端點以確定能夠安全地使用服務端點。</span><span class="sxs-lookup"><span data-stu-id="f94f7-105">The following sample demonstrates how to write a client endpoint behavior that validates the service endpoint to ensure that service endpoint is safe to use.</span></span>  
  
 <span data-ttu-id="f94f7-106">服務會公開 (Expose) 四個服務端點。</span><span class="sxs-lookup"><span data-stu-id="f94f7-106">The service exposes four service endpoints.</span></span> <span data-ttu-id="f94f7-107">第一個端點使用 WSDualHttpBinding，第二個端點會使用 NTLM 驗證，第三個端點會啟用異動流程，而第四個端點會使用憑證架構的驗證。</span><span class="sxs-lookup"><span data-stu-id="f94f7-107">The first endpoint uses the WSDualHttpBinding, the second endpoint uses NTLM authentication, the third endpoint enables transaction flow, and the fourth endpoint uses certificate-based authentication.</span></span>  
  
 <span data-ttu-id="f94f7-108">用戶端會使用 <xref:System.ServiceModel.Description.MetadataResolver> 類別來擷取服務的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="f94f7-108">The client uses the <xref:System.ServiceModel.Description.MetadataResolver> class to retrieve the metadata for the service.</span></span> <span data-ttu-id="f94f7-109">用戶端會使用驗證行為，強制禁止雙工繫結、NTLM 驗證與交易流程的原則。</span><span class="sxs-lookup"><span data-stu-id="f94f7-109">The client enforces a policy of prohibiting duplex bindings, NTLM authentication, and transaction flow using a validating behavior.</span></span> <span data-ttu-id="f94f7-110">針對 <xref:System.ServiceModel.Description.ServiceEndpoint> 從服務的中繼資料匯入的每個實例，用戶端應用程式會 `InternetClientValidatorBehavior` 先將端點行為的實例加入至， <xref:System.ServiceModel.Description.ServiceEndpoint> 再嘗試使用 Windows Communication Foundation （WCF）用戶端連接到端點。</span><span class="sxs-lookup"><span data-stu-id="f94f7-110">For each <xref:System.ServiceModel.Description.ServiceEndpoint> instance imported from the service's metadata, the client application adds an instance of the `InternetClientValidatorBehavior` endpoint behavior to the <xref:System.ServiceModel.Description.ServiceEndpoint> before attempting to use a Windows Communication Foundation (WCF) client to connect to the endpoint.</span></span> <span data-ttu-id="f94f7-111">此行為的 `Validate` 方法會在呼叫服務的任何作業之前執行，並且擲回 `InvalidOperationExceptions` 以強制執行該用戶端的原則。</span><span class="sxs-lookup"><span data-stu-id="f94f7-111">The behavior's `Validate` method runs before any operations on the service are called and enforces the client's policy by throwing `InvalidOperationExceptions`.</span></span>  
  
### <a name="to-build-the-sample"></a><span data-ttu-id="f94f7-112">若要建置範例</span><span class="sxs-lookup"><span data-stu-id="f94f7-112">To build the sample</span></span>  
  
1. <span data-ttu-id="f94f7-113">若要建立方案，請依照[建立 Windows Communication Foundation 範例](building-the-samples.md)中的指示進行。</span><span class="sxs-lookup"><span data-stu-id="f94f7-113">To build the solution, follow the instructions in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>  
  
### <a name="to-run-the-sample-on-the-same-computer"></a><span data-ttu-id="f94f7-114">若要在同一部電腦上執行範例</span><span class="sxs-lookup"><span data-stu-id="f94f7-114">To run the sample on the same computer</span></span>  
  
1. <span data-ttu-id="f94f7-115">以系統管理員許可權開啟 Visual Studio 的開發人員命令提示字元，然後從範例安裝資料夾中執行安裝程式 .bat。</span><span class="sxs-lookup"><span data-stu-id="f94f7-115">Open a Developer Command Prompt for Visual Studio with administrator privileges and run Setup.bat from the sample install folder.</span></span> <span data-ttu-id="f94f7-116">這會安裝執行範例所需的所有憑證。</span><span class="sxs-lookup"><span data-stu-id="f94f7-116">This installs all the certificates required for running the sample.</span></span>  
  
2. <span data-ttu-id="f94f7-117">從 \service\bin\Debug 執行服務應用程式。</span><span class="sxs-lookup"><span data-stu-id="f94f7-117">Run the service application from \service\bin\Debug.</span></span>  
  
3. <span data-ttu-id="f94f7-118">從 \client\bin\Debug 執行用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="f94f7-118">Run the client application from \client\bin\Debug.</span></span> <span data-ttu-id="f94f7-119">用戶端活動會顯示在用戶端主控台應用程式上。</span><span class="sxs-lookup"><span data-stu-id="f94f7-119">Client activity is displayed on the client console application.</span></span>  
  
4. <span data-ttu-id="f94f7-120">如果用戶端和服務無法通訊，請參閱[WCF 範例的疑難排解秘訣](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90))。</span><span class="sxs-lookup"><span data-stu-id="f94f7-120">If the client and service are not able to communicate, see [Troubleshooting Tips for WCF Samples](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90)).</span></span>  
  
5. <span data-ttu-id="f94f7-121">當您完成範例時，請執行 Cleanup.bat 以移除憑證。</span><span class="sxs-lookup"><span data-stu-id="f94f7-121">Remove the certificates by running Cleanup.bat when you have finished with the sample.</span></span> <span data-ttu-id="f94f7-122">其他安全性範例使用相同的憑證。</span><span class="sxs-lookup"><span data-stu-id="f94f7-122">Other security samples use the same certificates.</span></span>  
  
### <a name="to-run-the-sample-across-computers"></a><span data-ttu-id="f94f7-123">若要跨電腦執行範例</span><span class="sxs-lookup"><span data-stu-id="f94f7-123">To run the sample across computers</span></span>  
  
1. <span data-ttu-id="f94f7-124">在伺服器上，于 Visual Studio 以系統管理員許可權執行的開發人員命令提示字元中，輸入 `setup.bat service` 。</span><span class="sxs-lookup"><span data-stu-id="f94f7-124">On the server, in a Developer Command Prompt for Visual Studio run with administrator privileges, type `setup.bat service`.</span></span> <span data-ttu-id="f94f7-125">`setup.bat`使用引數執行時，會 `service` 建立具有電腦完整功能變數名稱的服務憑證，並將服務憑證匯出至名為 .cer 的檔案。</span><span class="sxs-lookup"><span data-stu-id="f94f7-125">Running `setup.bat` with the `service` argument creates a service certificate with the fully-qualified domain name of the computer and exports the service certificate to a file named Service.cer.</span></span>  
  
2. <span data-ttu-id="f94f7-126">在伺服器上，編輯 App.config 以反映新的憑證名稱。</span><span class="sxs-lookup"><span data-stu-id="f94f7-126">On the server, edit App.config to reflect the new certificate name.</span></span> <span data-ttu-id="f94f7-127">也就是，將 `findValue` 元素中的屬性變更 [\<serviceCertificate>](../../configure-apps/file-schema/wcf/servicecertificate-of-clientcredentials-element.md) 為電腦的完整功能變數名稱。</span><span class="sxs-lookup"><span data-stu-id="f94f7-127">That is, change the `findValue` attribute in the [\<serviceCertificate>](../../configure-apps/file-schema/wcf/servicecertificate-of-clientcredentials-element.md) element to the fully-qualified domain name of the computer.</span></span>  
  
3. <span data-ttu-id="f94f7-128">從服務目錄中將 Service.cer 檔案複製至用戶端電腦上的用戶端目錄。</span><span class="sxs-lookup"><span data-stu-id="f94f7-128">Copy the Service.cer file from the service directory to the client directory on the client computer.</span></span>  
  
4. <span data-ttu-id="f94f7-129">在用戶端上，以系統管理員許可權開啟 Visual Studio 的開發人員命令提示字元，然後輸入 `setup.bat client` 。</span><span class="sxs-lookup"><span data-stu-id="f94f7-129">On the client, open a Developer Command Prompt for Visual Studio with administrator privileges, and type `setup.bat client`.</span></span> <span data-ttu-id="f94f7-130">`setup.bat`使用 `client` 引數執行會建立名為 Client.com 的用戶端憑證，並將用戶端憑證匯出至名為 client .cer 的檔案。</span><span class="sxs-lookup"><span data-stu-id="f94f7-130">Running `setup.bat` with the `client` argument creates a client certificate named Client.com and exports the client certificate to a file named Client.cer.</span></span>  
  
5. <span data-ttu-id="f94f7-131">在 client.cs 檔中變更 MEX 端點的位址值和 `findValue`，以便將預設伺服器憑證設定成符合您服務的新位址。</span><span class="sxs-lookup"><span data-stu-id="f94f7-131">In the client.cs file change the address value of the MEX endpoint and the `findValue` for setting the default server certificate to match the new address of your service.</span></span> <span data-ttu-id="f94f7-132">您可以藉由使用伺服器的完整網域名稱取代 localhost，完成這個動作。</span><span class="sxs-lookup"><span data-stu-id="f94f7-132">You do this by replacing localhost with the fully-qualified domain name of the server.</span></span> <span data-ttu-id="f94f7-133">接著重新建置。</span><span class="sxs-lookup"><span data-stu-id="f94f7-133">Rebuild.</span></span>  
  
6. <span data-ttu-id="f94f7-134">從用戶端目錄將 Client.cer 檔案複製到伺服器上的服務目錄中。</span><span class="sxs-lookup"><span data-stu-id="f94f7-134">Copy the Client.cer file from the client directory to the service directory on the server.</span></span>  
  
7. <span data-ttu-id="f94f7-135">在用戶端上，于 Visual Studio 以系統管理員許可權開啟的開發人員命令提示字元中執行 Importservicecert.bat。</span><span class="sxs-lookup"><span data-stu-id="f94f7-135">On the client, run ImportServiceCert.bat in a Developer Command Prompt for Visual Studio opened with administrator privileges.</span></span> <span data-ttu-id="f94f7-136">這樣會將服務憑證從 Service.cer 檔案匯入至 CurrentUser - TrustedPeople 存放區中。</span><span class="sxs-lookup"><span data-stu-id="f94f7-136">This imports the service certificate from the Service.cer file into the CurrentUser - TrustedPeople store.</span></span>  
  
8. <span data-ttu-id="f94f7-137">在伺服器上，于 Visual Studio 以系統管理員許可權開啟的開發人員命令提示字元中執行 Importclientcert.bat。</span><span class="sxs-lookup"><span data-stu-id="f94f7-137">On the server, run ImportClientCert.bat in a Developer Command Prompt for Visual Studio opened with administrator privileges.</span></span> <span data-ttu-id="f94f7-138">這樣便會從 Client.cer 檔將用戶端憑證匯入至 LocalMachine - TrustedPeople 存放區中。</span><span class="sxs-lookup"><span data-stu-id="f94f7-138">This imports the client certificate from the Client.cer file into the LocalMachine - TrustedPeople store.</span></span>  
  
9. <span data-ttu-id="f94f7-139">在服務電腦上，使用 Visual Studio 來建置此服務專案並執行 service.exe。</span><span class="sxs-lookup"><span data-stu-id="f94f7-139">On the service computer, build the service project in Visual Studio and run service.exe.</span></span>  
  
10. <span data-ttu-id="f94f7-140">在用戶端電腦上執行 client.exe。</span><span class="sxs-lookup"><span data-stu-id="f94f7-140">On the client computer, run client.exe.</span></span>  
  
    1. <span data-ttu-id="f94f7-141">如果用戶端和服務無法通訊，請參閱[WCF 範例的疑難排解秘訣](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90))。</span><span class="sxs-lookup"><span data-stu-id="f94f7-141">If the client and service are not able to communicate, see [Troubleshooting Tips for WCF Samples](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90)).</span></span>  
  
### <a name="to-clean-up-after-the-sample"></a><span data-ttu-id="f94f7-142">若要在使用範例之後進行清除</span><span class="sxs-lookup"><span data-stu-id="f94f7-142">To clean up after the sample</span></span>  
  
- <span data-ttu-id="f94f7-143">當您完成執行範例後，請執行範例資料夾中的 Cleanup.bat。</span><span class="sxs-lookup"><span data-stu-id="f94f7-143">Run Cleanup.bat in the samples folder once you have finished running the sample.</span></span>  
  
    > [!NOTE]
    > <span data-ttu-id="f94f7-144">跨電腦執行此範例時，這個指令碼不會移除用戶端上的服務憑證。</span><span class="sxs-lookup"><span data-stu-id="f94f7-144">This script does not remove service certificates on a client when running this sample across computers.</span></span> <span data-ttu-id="f94f7-145">如果您已執行跨電腦使用憑證的 WCF 範例，請務必清除已安裝在 CurrentUser-TrustedPeople 存放區中的服務憑證。</span><span class="sxs-lookup"><span data-stu-id="f94f7-145">If you have run WCF samples that use certificates across computers, be sure to clear the service certificates that have been installed in the CurrentUser - TrustedPeople store.</span></span> <span data-ttu-id="f94f7-146">若要這麼做，請使用下列命令：`certmgr -del -r CurrentUser -s TrustedPeople -c -n <Fully Qualified Server Machine Name>. For example: certmgr -del -r CurrentUser -s TrustedPeople -c -n server1.contoso.com`。</span><span class="sxs-lookup"><span data-stu-id="f94f7-146">To do this, use the following command: `certmgr -del -r CurrentUser -s TrustedPeople -c -n <Fully Qualified Server Machine Name>. For example: certmgr -del -r CurrentUser -s TrustedPeople -c -n server1.contoso.com`.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="f94f7-147">請參閱</span><span class="sxs-lookup"><span data-stu-id="f94f7-147">See also</span></span>

- [<span data-ttu-id="f94f7-148">使用中繼資料</span><span class="sxs-lookup"><span data-stu-id="f94f7-148">Using Metadata</span></span>](../feature-details/using-metadata.md)
