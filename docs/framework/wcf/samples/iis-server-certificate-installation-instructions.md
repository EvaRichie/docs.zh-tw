---
title: 網際網路資訊服務 (IIS) 伺服器憑證安裝指示
ms.date: 03/30/2017
ms.assetid: 11281490-d2ac-4324-8f33-e7714611a34b
ms.openlocfilehash: 301a10c615a13a42e1a6e1b89d2724476ca4fbae
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84594656"
---
# <a name="internet-information-services-iis-server-certificate-installation-instructions"></a><span data-ttu-id="abd64-102">網際網路資訊服務 (IIS) 伺服器憑證安裝指示</span><span class="sxs-lookup"><span data-stu-id="abd64-102">Internet Information Services (IIS) Server Certificate Installation Instructions</span></span>
<span data-ttu-id="abd64-103">若要執行能與網際網路資訊服務 (IIS) 安全通訊的範例，您必須建立並安裝伺服器憑證。</span><span class="sxs-lookup"><span data-stu-id="abd64-103">To run the samples that securely communicate with Internet Information Services (IIS), you must create and install a server certificate.</span></span>  
  
## <a name="step-1-creating-certificates"></a><span data-ttu-id="abd64-104">步驟 1：</span><span class="sxs-lookup"><span data-stu-id="abd64-104">Step 1.</span></span> <span data-ttu-id="abd64-105">建立憑證</span><span class="sxs-lookup"><span data-stu-id="abd64-105">Creating Certificates</span></span>  
 <span data-ttu-id="abd64-106">若要為您的電腦建立憑證，請以系統管理員許可權開啟 Visual Studio 的開發人員命令提示字元，然後執行每個使用與 IIS 安全通訊的範例中所包含的安裝程式 .bat。</span><span class="sxs-lookup"><span data-stu-id="abd64-106">To create a certificate for your computer, open a Developer Command Prompt for Visual Studio with administrator privileges and run the Setup.bat that is included in each of the samples that use secure communication with IIS.</span></span> <span data-ttu-id="abd64-107">請先確定路徑有將 Makecert.exe 上一層的資料夾包含在內，再執行此批次 (Batch) 檔。</span><span class="sxs-lookup"><span data-stu-id="abd64-107">Ensure that the path includes the folder that contains Makecert.exe before you run this batch file.</span></span> <span data-ttu-id="abd64-108">下列命令是用來建立 Setup.bat 中的憑證。</span><span class="sxs-lookup"><span data-stu-id="abd64-108">The following command is used to create the certificate in Setup.bat.</span></span>  
  
```console  
makecert -sr LocalMachine -ss My -n CN=ServiceModelSamples-HTTPS-Server -sky exchange -sk ServiceModelSamples-HTTPS-Key  
```  
  
## <a name="step-2-installing-certificates"></a><span data-ttu-id="abd64-109">步驟 2：</span><span class="sxs-lookup"><span data-stu-id="abd64-109">Step 2.</span></span> <span data-ttu-id="abd64-110">安裝憑證</span><span class="sxs-lookup"><span data-stu-id="abd64-110">Installing Certificates</span></span>  
 <span data-ttu-id="abd64-111">安裝您剛才建立的憑證所需的步驟，視您使用的 IIS 版本而定。</span><span class="sxs-lookup"><span data-stu-id="abd64-111">The steps required to install the certificates you just created depend on which version of IIS you are using.</span></span>  
  
#### <a name="to-install-iis-on-iis-51-windows-xp-and-iis-60-windows-server-2003"></a><span data-ttu-id="abd64-112">在 IIS 5.1 (Windows XP) 和 IIS 6.0 (Windows Server 2003) 上安裝 IIS</span><span class="sxs-lookup"><span data-stu-id="abd64-112">To install IIS on IIS 5.1 (Windows XP) and IIS 6.0 (Windows Server 2003)</span></span>  
  
1. <span data-ttu-id="abd64-113">開啟網際網路資訊服務管理員 MMC 嵌入式管理單元。</span><span class="sxs-lookup"><span data-stu-id="abd64-113">Open the Internet Information Services Manager MMC Snap-In.</span></span>  
  
2. <span data-ttu-id="abd64-114">以滑鼠右鍵按一下 [預設的網站]，然後選取 [**屬性**]。</span><span class="sxs-lookup"><span data-stu-id="abd64-114">Right-click the default Web site and select **Properties**.</span></span>  
  
3. <span data-ttu-id="abd64-115">選取 [**目錄安全性**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="abd64-115">Select the **Directory Security** tab.</span></span>  
  
4. <span data-ttu-id="abd64-116">按一下 [**伺服器憑證**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="abd64-116">Click the **Server Certificate** button.</span></span> <span data-ttu-id="abd64-117">[Web 伺服器憑證精靈] 隨即啟動。</span><span class="sxs-lookup"><span data-stu-id="abd64-117">The Web Server Certificate Wizard starts.</span></span>  
  
5. <span data-ttu-id="abd64-118">完成精靈。</span><span class="sxs-lookup"><span data-stu-id="abd64-118">Complete the wizard.</span></span> <span data-ttu-id="abd64-119">選取選項以指派憑證。</span><span class="sxs-lookup"><span data-stu-id="abd64-119">Select the option to assign a certificate.</span></span> <span data-ttu-id="abd64-120">從顯示的憑證清單中，選取 ServiceModelSamples-HTTPS-Server 憑證。</span><span class="sxs-lookup"><span data-stu-id="abd64-120">Select the ServiceModelSamples-HTTPS-Server certificate from the list of certificates that are displayed.</span></span>  
  
     <span data-ttu-id="abd64-121">![IIS 憑證精靈](media/iiscertificate-wizard.GIF "IISCertificate_Wizard")</span><span class="sxs-lookup"><span data-stu-id="abd64-121">![IIS Certificate Wizard](media/iiscertificate-wizard.GIF "IISCertificate_Wizard")</span></span>  
  
6. <span data-ttu-id="abd64-122">使用 HTTPS 位址，在瀏覽器中測試服務的存取權 `https://localhost/servicemodelsamples/service.svc` 。</span><span class="sxs-lookup"><span data-stu-id="abd64-122">Test access to the service in a browser by using the HTTPS address `https://localhost/servicemodelsamples/service.svc`.</span></span>  
  
#### <a name="if-ssl-was-previously-configured-by-using-httpcfgexe"></a><span data-ttu-id="abd64-123">如果先前是使用 Httpcfg.exe 設定 SSL</span><span class="sxs-lookup"><span data-stu-id="abd64-123">If SSL was previously configured by using Httpcfg.exe</span></span>  
  
1. <span data-ttu-id="abd64-124">請使用 Makecert.exe (或執行 Setup.bat) 來建立伺服器憑證。</span><span class="sxs-lookup"><span data-stu-id="abd64-124">Use Makecert.exe (or run Setup.bat) to create the server certificate.</span></span>  
  
2. <span data-ttu-id="abd64-125">執行 IIS 管理員，並根據先前的步驟安裝憑證。</span><span class="sxs-lookup"><span data-stu-id="abd64-125">Run the IIS manager and install the certificate according to the previous steps.</span></span>  
  
3. <span data-ttu-id="abd64-126">在用戶端程式加入下面這行程式碼。</span><span class="sxs-lookup"><span data-stu-id="abd64-126">Add the following line of code to the client program.</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="abd64-127">只有測試憑證才需要這段程式碼，例如 Makecert.exe 建立的憑證。</span><span class="sxs-lookup"><span data-stu-id="abd64-127">This code is only required for test certificates such as those created by Makecert.exe.</span></span> <span data-ttu-id="abd64-128">在實際執行程式碼中不建議這樣做。</span><span class="sxs-lookup"><span data-stu-id="abd64-128">It is not recommended for production code.</span></span>  
  
```csharp  
PermissiveCertificatePolicy.Enact("CN=ServiceModelSamples-HTTPS-Server");  
```  
  
#### <a name="to-install-iis-on-iis-70-windows-vista-and-windows-server-2008"></a><span data-ttu-id="abd64-129">在 IIS 7.0 (Windows Vista 和 Windows Server 2008) 上安裝 IIS</span><span class="sxs-lookup"><span data-stu-id="abd64-129">To install IIS on IIS 7.0 (Windows Vista and Windows Server 2008)</span></span>  
  
1. <span data-ttu-id="abd64-130">在 [**開始**] 功能表中，按一下 [**執行**]，然後輸入**inetmgr**以開啟 [Internet Information Services （IIS） mmc 嵌入式管理單元]。</span><span class="sxs-lookup"><span data-stu-id="abd64-130">From the **Start** menu, click **Run**, then type **inetmgr** to open the Internet Information Services (IIS) MMC snap-in.</span></span>  
  
2. <span data-ttu-id="abd64-131">以滑鼠右鍵按一下 [**預設的網站**]，然後選取 [編輯系結 **...** ]</span><span class="sxs-lookup"><span data-stu-id="abd64-131">Right-click the **Default Web Site** and select **Edit Bindings…**</span></span>  
  
3. <span data-ttu-id="abd64-132">按一下 [**網站**系結] 對話方塊的 [**新增**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="abd64-132">Click the **Add** button of the **Site Bindings** dialog box.</span></span>  
  
4. <span data-ttu-id="abd64-133">從 [**類型**] 下拉式清單中選取 [ **HTTPS** ]。</span><span class="sxs-lookup"><span data-stu-id="abd64-133">Select **HTTPS** from the **Type** drop-down list.</span></span>  
  
5. <span data-ttu-id="abd64-134">從 [ **SSL 憑證**] 下拉式清單中選取 [ **ServiceModelSamples-HTTPS-伺服器**]，然後按一下 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="abd64-134">Select the **ServiceModelSamples-HTTPS-Server** from the **SSL certificate** drop-down list and click **OK**.</span></span>  
  
6. <span data-ttu-id="abd64-135">使用 HTTPS 位址，在瀏覽器中測試服務的存取權 `https://localhost/servicemodelsamples/service.svc` 。</span><span class="sxs-lookup"><span data-stu-id="abd64-135">Test access to the service in a browser by using the HTTPS address `https://localhost/servicemodelsamples/service.svc`.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="abd64-136">因為您剛剛安裝的測試憑證不是受信任的憑證，您在瀏覽使用這個憑證保護的本機網址時，可能會碰到其他 Internet Explorer 安全性警告。</span><span class="sxs-lookup"><span data-stu-id="abd64-136">Because the test certificate you have just installed is not a trusted certificate, you may encounter additional Internet Explorer security warnings when browsing to local Web addresses secured with this certificate.</span></span>  
  
## <a name="removing-certificates"></a><span data-ttu-id="abd64-137">移除憑證</span><span class="sxs-lookup"><span data-stu-id="abd64-137">Removing Certificates</span></span>  
  
- <span data-ttu-id="abd64-138">依照前述指示使用 Internet Information Services 管理員，但是改為移除憑證或繫結，而非新增。</span><span class="sxs-lookup"><span data-stu-id="abd64-138">Use the Internet Information Services Manager as previously directed, but remove the certificate or binding instead of adding it.</span></span>  
  
- <span data-ttu-id="abd64-139">使用下列命令移除電腦憑證。</span><span class="sxs-lookup"><span data-stu-id="abd64-139">Remove the computer certificate by using the following command.</span></span>  
  
    ```console  
    httpcfg delete ssl -i 0.0.0.0:443  
    ```
