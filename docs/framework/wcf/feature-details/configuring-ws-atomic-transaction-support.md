---
title: 設定 WS-Atomic 交易支援
ms.date: 03/30/2017
helpviewer_keywords:
- WS-AT protocol [WCF], configuring WS-Atomic Transaction
ms.assetid: cb9f1c9c-1439-4172-b9bc-b01c3e09ac48
ms.openlocfilehash: 9c0e75d58fbcf61137ceae3fba9d8acfe3902171
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90556586"
---
# <a name="configure-ws-atomic-transaction-support"></a><span data-ttu-id="f1b88-102">設定 WS-不可部分完成的交易支援</span><span class="sxs-lookup"><span data-stu-id="f1b88-102">Configure WS-Atomic Transaction support</span></span>

<span data-ttu-id="f1b88-103">這個主題說明如何使用 [WS-AT 組態公用程式] 來設定 WS-AtomicTransaction (WS-AT) 支援。</span><span class="sxs-lookup"><span data-stu-id="f1b88-103">This topic describes how you can configure WS-AtomicTransaction (WS-AT) support by using the WS-AT Configuration Utility.</span></span>

## <a name="use-the-ws-at-configuration-utility"></a><span data-ttu-id="f1b88-104">使用 WS-AT 設定公用程式</span><span class="sxs-lookup"><span data-stu-id="f1b88-104">Use the WS-AT configuration utility</span></span>

<span data-ttu-id="f1b88-105">WS-AT 組態公用程式 (wsatConfig.exe) 可用來進行 WS-AT 設定。</span><span class="sxs-lookup"><span data-stu-id="f1b88-105">The WS-AT Configuration Utility (wsatConfig.exe) is used to configure WS-AT settings.</span></span> <span data-ttu-id="f1b88-106">若要啟用 WS-AT 通訊協定服務，您必須使用組態公用程式來設定 WS-AT 的 HTTPS 連接埠、將 X.509 憑證繫結至 HTTPS 連接埠，並藉由指定憑證主體名稱或指紋來設定授權的夥伴憑證。</span><span class="sxs-lookup"><span data-stu-id="f1b88-106">In order to enable the WS-AT protocol service, you must use the configuration utility to configure the HTTPS port for WS-AT, bind an X.509 certificate to the HTTPS port, and configure authorized partner certificates by specifying certificate subject names or thumbprints.</span></span> <span data-ttu-id="f1b88-107">組態公用程式也可讓您選取追蹤模式，並設定預設傳出和最大傳入的交易逾時值。</span><span class="sxs-lookup"><span data-stu-id="f1b88-107">The configuration utility also allows you to select the tracing mode and set default outgoing and maximum incoming transaction timeouts.</span></span>

<span data-ttu-id="f1b88-108">您可以使用 [元件服務] 管理主控台中的 Microsoft Management Console (MMC) 屬性頁嵌入式管理單元，或透過命令列視窗存取這個工具的功能。</span><span class="sxs-lookup"><span data-stu-id="f1b88-108">You can access this tool's functionality by using a Microsoft Management Console (MMC) property page snap-in in the Component Services management console, or from a command-line window.</span></span> <span data-ttu-id="f1b88-109">透過命令列視窗在本機電腦上設定 WS-AT 支援；使用 MMC 嵌入式管理單元同時在本機和遠端電腦上進行設定。</span><span class="sxs-lookup"><span data-stu-id="f1b88-109">Configure WS-AT support on the local machine through the command-line window; configure settings on both local and remote machines by using the MMC snap-in.</span></span>

<span data-ttu-id="f1b88-110">您可以在 Windows SDK 安裝位置 "%WINDIR%\Microsoft.NET\Framework\v3.0\Windows Communication Foundation" 中存取命令列視窗。</span><span class="sxs-lookup"><span data-stu-id="f1b88-110">The command-line window can be accessed in the Windows SDK installation location "%WINDIR%\Microsoft.NET\Framework\v3.0\Windows Communication Foundation".</span></span>

<span data-ttu-id="f1b88-111">如需命令列工具的詳細資訊，請參閱 [ws-atomictransaction 設定公用程式 ( # A0) ](../ws-atomictransaction-configuration-utility-wsatconfig-exe.md)。</span><span class="sxs-lookup"><span data-stu-id="f1b88-111">For more information about the command-line tool, see [WS-AtomicTransaction Configuration Utility (wsatConfig.exe)](../ws-atomictransaction-configuration-utility-wsatconfig-exe.md).</span></span>

<span data-ttu-id="f1b88-112">如果您執行的是 Windows XP 或 Windows Server 2003，您可以流覽至 [ **主控台/系統管理工具/元件服務**]，以滑鼠右鍵按一下 **我的電腦**， **然後選取 [** 內容]，來存取 MMC 嵌入式管理單元。</span><span class="sxs-lookup"><span data-stu-id="f1b88-112">If you are running Windows XP or Windows Server 2003, you can access the MMC snap-in by navigating to **Control Panel/Administrative Tools/Component Services**, right-clicking **My Computer**, and selecting **Properties**.</span></span> <span data-ttu-id="f1b88-113">這個位置和您設定 Microsoft Distributed Transaction Coordinator (MSDTC) 的位置一樣。</span><span class="sxs-lookup"><span data-stu-id="f1b88-113">This is the same location where you can configure the Microsoft Distributed Transaction Coordinator (MSDTC).</span></span> <span data-ttu-id="f1b88-114">可供設定的選項會在 [ **ws-at** ] 索引標籤底下分組。如果您執行的是 Windows Vista 或 Windows Server 2008，您可以按一下 [ **開始** ] 按鈕，然後 `dcomcnfg.exe` 在 [ **搜尋** ] 方塊中輸入，即可找到 MMC 嵌入式管理單元。</span><span class="sxs-lookup"><span data-stu-id="f1b88-114">Options available for configuration are grouped under the **WS-AT** tab. If you are running Windows Vista or Windows Server 2008, the MMC snap-in can be found by clicking the **Start** button, and entering `dcomcnfg.exe` in the **Search** box.</span></span> <span data-ttu-id="f1b88-115">當 MMC 開啟時，流覽至 [ **My 電腦 \ 分散式 Transaction COORDINATOR\LOCAL DTC** ] 節點，以滑鼠右鍵按一下並選取 [ **屬性**]。</span><span class="sxs-lookup"><span data-stu-id="f1b88-115">When the MMC is opened, navigate to the **My Computer\Distributed Transaction Coordinator\Local DTC** node, right click and select **Properties**.</span></span> <span data-ttu-id="f1b88-116">可供設定的選項會在 [ **ws-at** ] 索引標籤底下分組。</span><span class="sxs-lookup"><span data-stu-id="f1b88-116">Options available for configuration are grouped under the **WS-AT** tab.</span></span>

<span data-ttu-id="f1b88-117">如需嵌入式管理單元的詳細資訊，請參閱 [ws-atomictransaction 設定 MMC 嵌入式管理](../ws-atomictransaction-configuration-mmc-snap-in.md)單元。</span><span class="sxs-lookup"><span data-stu-id="f1b88-117">For more information about the snap-in, see the [WS-AtomicTransaction Configuration MMC Snap-in](../ws-atomictransaction-configuration-mmc-snap-in.md).</span></span>

<span data-ttu-id="f1b88-118">若要啟用工具的使用者介面，您必須先登錄下列路徑中的 WsatUI.dll 檔</span><span class="sxs-lookup"><span data-stu-id="f1b88-118">To enable the tool's user interface, you must first register the WsatUI.dll file, located at the following path</span></span>

<span data-ttu-id="f1b88-119">%PROGRAMFILES%\Microsoft SDKs\Windows\v6.0\Bin</span><span class="sxs-lookup"><span data-stu-id="f1b88-119">%PROGRAMFILES%\Microsoft SDKs\Windows\v6.0\Bin</span></span>

<span data-ttu-id="f1b88-120">若要登錄產品，請在 [命令提示字元] 視窗中執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="f1b88-120">To register the product, execute the following command from a Command Prompt window:</span></span>

`regasm.exe /codebase WsatUI.dll`

## <a name="enable-ws-at"></a><span data-ttu-id="f1b88-121">啟用 WS-AT</span><span class="sxs-lookup"><span data-stu-id="f1b88-121">Enable WS-AT</span></span>

<span data-ttu-id="f1b88-122">若要使用連接埠 443 和 X.509 憑證 (此憑證具有已安裝在本機電腦存放區中的私密金鑰) 啟用 MSDTC 內部的 WS-AT 通訊協定服務，請以下列命令使用 wsatConfig.exe 工具。</span><span class="sxs-lookup"><span data-stu-id="f1b88-122">To enable the WS-AT protocol service inside MSDTC using port 443 and an X.509 certificate with a private key that has been installed in the local machine store, use the wsatConfig.exe tool with the following command.</span></span>

`WsatConfig.exe –network:enable –port:8443 –endpointCert:<machine|"Issuer\SubjectName"> -accountsCerts:<thumbprint|"Issuer\SubjectName"> -restart`

<span data-ttu-id="f1b88-123">以與您環境相關的值取代相對的參數。</span><span class="sxs-lookup"><span data-stu-id="f1b88-123">Substitute the respective parameters with values relevant to your environment.</span></span>

<span data-ttu-id="f1b88-124">若要停用 MSDTC 內部的 WS-AT 通訊協定服務，請以下列命列使用 wsatConfig.exe 工具。</span><span class="sxs-lookup"><span data-stu-id="f1b88-124">To disable the WS-AT protocol service inside MSDTC, use the wsatConfig.exe tool with the following command.</span></span>

`WsatConfig.exe –network:disable -restart`

## <a name="configure-trust-between-two-machines"></a><span data-ttu-id="f1b88-125">設定兩部電腦之間的信任</span><span class="sxs-lookup"><span data-stu-id="f1b88-125">Configure trust between two machines</span></span>

<span data-ttu-id="f1b88-126">WS-AT 通訊協定服務需要系統管理員明確授權個別帳戶，才能參與分散式異動。</span><span class="sxs-lookup"><span data-stu-id="f1b88-126">The WS-AT protocol service requires the administrator to explicitly authorize individual accounts to participate in distributed transactions.</span></span> <span data-ttu-id="f1b88-127">如果您是兩部電腦的系統管理員，可以透過下列方式設定這兩部電腦，以建立相互信任關係：交換這兩部電腦之間的正確憑證組、將這些憑證安裝到適當的憑證存放區，然後使用 wsatConfig.exe 工具將每部電腦的憑證新增至授權之參與者憑證的其他清單。</span><span class="sxs-lookup"><span data-stu-id="f1b88-127">If you are an administrator for two machines, you can configure both machines to establish a mutual trust relationship by exchanging the right set of certificates between the machines, installing them into the appropriate certificate stores, and using the wsatConfig.exe tool to add each machine's certificate to the other's list of authorized participant certificates.</span></span> <span data-ttu-id="f1b88-128">這是使用 WS-AT 在兩部電腦之間執行分散式異動的必要步驟。</span><span class="sxs-lookup"><span data-stu-id="f1b88-128">This step is necessary to perform distributed transactions between two machines using WS-AT.</span></span>

<span data-ttu-id="f1b88-129">下列範例說明在 A 和 B 這兩部電腦之間建立信任的步驟。</span><span class="sxs-lookup"><span data-stu-id="f1b88-129">In the following example outlines the steps to establish trust between two machines, A and B.</span></span>

### <a name="create-and-export-certificates"></a><span data-ttu-id="f1b88-130">建立和匯出憑證</span><span class="sxs-lookup"><span data-stu-id="f1b88-130">Create and export certificates</span></span>

<span data-ttu-id="f1b88-131">這個程序需要 MMC 憑證嵌入式管理單元。</span><span class="sxs-lookup"><span data-stu-id="f1b88-131">This procedure requires the MMC Certificates snap-in.</span></span> <span data-ttu-id="f1b88-132">依序開啟 [開始]、[執行] 功能表，並在輸入方塊中輸入 "mmc" 然後按下 [確定]，即可存取嵌入式管理單元。</span><span class="sxs-lookup"><span data-stu-id="f1b88-132">The snap-in can be accessed by opening the Start/Run menu, typing "mmc" in the input box and pressing OK.</span></span> <span data-ttu-id="f1b88-133">然後，在 [**主控台**1] 視窗中，流覽至 **[檔案/新增-移除**] 嵌入式管理單元，按一下 [新增]，然後從 [**可用的獨立嵌入式管理單元**] 清單中選擇 [**憑證**]。</span><span class="sxs-lookup"><span data-stu-id="f1b88-133">Then, in the **Console1** window, navigate to **the File/Add-Remove** Snap-in, click Add, and choose **Certificates** from the **Available Standalone Snapins** list.</span></span> <span data-ttu-id="f1b88-134">最後，選取要管理的 **電腦帳戶** ，然後按一下 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="f1b88-134">Finally, select **Computer Account** to manage and click **OK**.</span></span> <span data-ttu-id="f1b88-135">[ **憑證** ] 節點會出現在嵌入式管理單元主控台中。</span><span class="sxs-lookup"><span data-stu-id="f1b88-135">The **Certificates** node appears in the snap-in console.</span></span>

<span data-ttu-id="f1b88-136">您必須已擁有必要的憑證，才能建立信任。</span><span class="sxs-lookup"><span data-stu-id="f1b88-136">You must already possess the required certificates to establish trust.</span></span> <span data-ttu-id="f1b88-137">若要瞭解如何在下列步驟之前建立和安裝新憑證，請參閱 [如何：在開發期間于 WCF 中建立和安裝暫存用戶端憑證](/previous-versions/msp-n-p/ff650751(v=pandp.10))。</span><span class="sxs-lookup"><span data-stu-id="f1b88-137">To learn how to create and install new certificates prior to the following steps, see [How to: Create and Install Temporary Client Certificates in WCF During Development](/previous-versions/msp-n-p/ff650751(v=pandp.10)).</span></span>

1. <span data-ttu-id="f1b88-138">在電腦 A 上，使用 MMC 憑證嵌入式管理單元將現有的憑證 (certA) 匯入 LocalMachine\MY (個人節點) 和 LocalMachine\ROOT 存放區 (受信任的根憑證授權單位節點)。</span><span class="sxs-lookup"><span data-stu-id="f1b88-138">On machine A, using the MMC Certificates snap-in, import the existing certificate (certA) into the LocalMachine\MY (Personal Node) and LocalMachine\ROOT store (trusted root certification authority node).</span></span> <span data-ttu-id="f1b88-139">若要將憑證匯入至特定的節點，請以滑鼠右鍵按一下節點，然後選擇 [ **所有工作/匯入**]。</span><span class="sxs-lookup"><span data-stu-id="f1b88-139">To import a certificate to a specific node, right-click the node and choose **All Tasks/Import**.</span></span>

2. <span data-ttu-id="f1b88-140">在電腦 B 上，使用 MMC 憑證嵌入式管理單元，建立或取得具有私密金鑰的憑證 certB，並將該憑證匯入 LocalMachine\MY (個人節點) 和 LocalMachine\ROOT 存放區 (受信任的根憑證授權單位節點)。</span><span class="sxs-lookup"><span data-stu-id="f1b88-140">On machine B, using the MMC Certificates snap-in, create or obtain a certificate certB with a private key and import it into the LocalMachine\MY (Personal Node) and LocalMachine\ROOT store (trusted root certification authority node).</span></span>

3. <span data-ttu-id="f1b88-141">將 certA 的公開金鑰匯出至檔案 (如果尚未匯出的話)。</span><span class="sxs-lookup"><span data-stu-id="f1b88-141">Export certA's public key to a file if this has not been done already.</span></span>

4. <span data-ttu-id="f1b88-142">將 certB 的公開金鑰匯出至檔案 (如果尚未匯出的話)。</span><span class="sxs-lookup"><span data-stu-id="f1b88-142">Export certB's public key to a file if this has not been done already.</span></span>

### <a name="establish-mutual-trust-between-machines"></a><span data-ttu-id="f1b88-143">在電腦之間建立相互信任</span><span class="sxs-lookup"><span data-stu-id="f1b88-143">Establish mutual trust between machines</span></span>

1. <span data-ttu-id="f1b88-144">在電腦 A 上，將 certB 的檔案代表匯入 LocalMachine\MY 和 LocalMachine\ROOT 存放區。</span><span class="sxs-lookup"><span data-stu-id="f1b88-144">On machine A, import the file representation of certB into the LocalMachine\MY and LocalMachine\ROOT stores.</span></span> <span data-ttu-id="f1b88-145">這樣表示電腦 A 信任 certB，並可進行通訊。</span><span class="sxs-lookup"><span data-stu-id="f1b88-145">This declares that machine A trusts certB to communicate with it.</span></span>

2. <span data-ttu-id="f1b88-146">在電腦 B 上，將 certA 的檔案匯入 LocalMachine\MY 和 LocalMachine\ROOT 存放區。</span><span class="sxs-lookup"><span data-stu-id="f1b88-146">On machine B, import certA’s file into the LocalMachine\MY and LocalMachine\ROOT stores.</span></span> <span data-ttu-id="f1b88-147">這樣表示電腦 B 信任 certA，並可進行通訊。</span><span class="sxs-lookup"><span data-stu-id="f1b88-147">This implies that machine B trusts certA to communicate with it.</span></span>

<span data-ttu-id="f1b88-148">完成這些步驟之後，兩部電腦之間隨即建立信任，並可將這些電腦設定為使用 WS-AT 彼此通訊。</span><span class="sxs-lookup"><span data-stu-id="f1b88-148">After completing these steps, trust is established between the two machines, and they can be configured to communicate with each other using WS-AT.</span></span>

### <a name="configure-msdtc-to-use-certificates"></a><span data-ttu-id="f1b88-149">將 MSDTC 設定為使用憑證</span><span class="sxs-lookup"><span data-stu-id="f1b88-149">Configure MSDTC to use certificates</span></span>

<span data-ttu-id="f1b88-150">由於 WS-AT 通訊協定服務可同時作用為用戶端和伺服器，此服務必須同時接聽連入連線並初始化連出連線。</span><span class="sxs-lookup"><span data-stu-id="f1b88-150">Since the WS-AT protocol service acts as both a client and a server, it must both listen for incoming connections and initiate outgoing connections.</span></span> <span data-ttu-id="f1b88-151">因此，您必須設定 MSDTC，讓它在與外部的另一方進行通訊時知道要使用的憑證，以及在接受連入通訊時知道要授權的憑證。</span><span class="sxs-lookup"><span data-stu-id="f1b88-151">Therefore, you need to configure MSDTC so that it knows which certificate to use when communicating with external parties, and which certificates to authorize when accepting incoming communication.</span></span>

<span data-ttu-id="f1b88-152">您可以使用 MMC WS-AT 嵌入式管理單元設定此項。</span><span class="sxs-lookup"><span data-stu-id="f1b88-152">You can configure this by using the MMC WS-AT snap-in.</span></span> <span data-ttu-id="f1b88-153">如需此工具的詳細資訊，請參閱 [ws-atomictransaction 設定 MMC 嵌入式管理](../ws-atomictransaction-configuration-mmc-snap-in.md) 單元主題。</span><span class="sxs-lookup"><span data-stu-id="f1b88-153">For more information about this tool, see the [WS-AtomicTransaction Configuration MMC Snap-in](../ws-atomictransaction-configuration-mmc-snap-in.md) topic.</span></span> <span data-ttu-id="f1b88-154">下列步驟描述如何在執行 MSDTC 的兩部電腦之間建立信任。</span><span class="sxs-lookup"><span data-stu-id="f1b88-154">The following steps describe how to establish trust between two computers running MSDTC.</span></span>

1. <span data-ttu-id="f1b88-155">進行電腦 A 的設定。</span><span class="sxs-lookup"><span data-stu-id="f1b88-155">Configure machine A's settings.</span></span> <span data-ttu-id="f1b88-156">針對 [端點憑證]，選取 [certA]。</span><span class="sxs-lookup"><span data-stu-id="f1b88-156">For "Endpoint Certificate", select certA.</span></span> <span data-ttu-id="f1b88-157">針對「授權憑證」，請選取 certB。</span><span class="sxs-lookup"><span data-stu-id="f1b88-157">For "Authorized Certificates", select the certB.</span></span>

2. <span data-ttu-id="f1b88-158">進行電腦 B 的設定。</span><span class="sxs-lookup"><span data-stu-id="f1b88-158">Configure machine B's settings.</span></span> <span data-ttu-id="f1b88-159">針對 [端點憑證]，選取 [certB]。</span><span class="sxs-lookup"><span data-stu-id="f1b88-159">For "Endpoint Certificate", select certB.</span></span> <span data-ttu-id="f1b88-160">針對「授權憑證」，請選取 certA。</span><span class="sxs-lookup"><span data-stu-id="f1b88-160">For "Authorized Certificates", select the certA.</span></span>

> [!NOTE]
> <span data-ttu-id="f1b88-161">當某一部電腦將訊息傳送至其他電腦時，傳送者會嘗試驗證收件者憑證的主體名稱和收件者的電腦名稱是否相符。</span><span class="sxs-lookup"><span data-stu-id="f1b88-161">When one machine sends a message to the other machine, the sender attempts to verify that the subject name of the recipient’s certificate and the name of the recipient’s machine match.</span></span> <span data-ttu-id="f1b88-162">如果不符，憑證驗證就會失敗，而這兩部電腦則無法進行通訊。</span><span class="sxs-lookup"><span data-stu-id="f1b88-162">If they do not match, certificate verification fails and the two machines cannot communicate.</span></span>
>
> <span data-ttu-id="f1b88-163">若要讓電腦加入網域，該名稱必須為完整的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="f1b88-163">For a machine joined to a domain, the name is the fully qualified domain name.</span></span> <span data-ttu-id="f1b88-164">根據預設，工作群組上的電腦名稱為電腦的 NetBIOS 名稱。</span><span class="sxs-lookup"><span data-stu-id="f1b88-164">By default, the name of a machine on a workgroup is the machine’s NetBIOS name.</span></span> <span data-ttu-id="f1b88-165">不過，如果兩部電腦之間使用的連線中顯示了網域名稱系統 (DNS) 尾碼，則名稱也可以是該尾碼。</span><span class="sxs-lookup"><span data-stu-id="f1b88-165">However, the name can also include a Domain Name System (DNS) suffix if one is present for the connection being used between the two machines.</span></span>
>
> <span data-ttu-id="f1b88-166">如果變更電腦的名稱，例如工作群組電腦加入網域時，您必須重新發出憑證或手動設定 DNS 尾碼。</span><span class="sxs-lookup"><span data-stu-id="f1b88-166">If the name of the machine changes, for example, when a workgroup machine joins a domain, you must reissue certificates or manually configure DNS suffixes.</span></span>

## <a name="security"></a><span data-ttu-id="f1b88-167">安全性</span><span class="sxs-lookup"><span data-stu-id="f1b88-167">Security</span></span>

<span data-ttu-id="f1b88-168">由於某些與 MSDTC 和 WS-AT 相關的設定會分別存放在 HKLM\Software\Microsoft\MSDTC 和 HKLM\Software\Microsoft\WSAT 登錄中，請確定這些登錄機碼都已受到保護，只有系統管理員可以寫入。</span><span class="sxs-lookup"><span data-stu-id="f1b88-168">Since some of the settings related to MSDTC and WS-AT are stored in the registry at HKLM\Software\Microsoft\MSDTC and at HKLM\Software\Microsoft\WSAT, respectively, ensure that these registry keys are secured so that only administrators can write to them.</span></span> <span data-ttu-id="f1b88-169">在 [登錄編輯程式] 工具中，以滑鼠右鍵按一下您要保護的機碼，然後選取 [ **許可權** ] 以設定適當的存取控制。</span><span class="sxs-lookup"><span data-stu-id="f1b88-169">In the Registry Editor tool, right-click the key you want to secure and select **Permission** to set the appropriate access control.</span></span> <span data-ttu-id="f1b88-170">低權限使用者對於重要機碼只有唯讀權限這點，對於系統的安全性和完整性相當重要。</span><span class="sxs-lookup"><span data-stu-id="f1b88-170">It is crucial to the security and integrity of the system that important keys are read-only for low-privileged users.</span></span>

<span data-ttu-id="f1b88-171">部署 MSDTC 時，系統管理員必須確定任何 MSDTC 資料交換都很安全。</span><span class="sxs-lookup"><span data-stu-id="f1b88-171">When deploying MSDTC, the administrator must ensure that any MSDTC data interchange is secure.</span></span> <span data-ttu-id="f1b88-172">在工作群組部署中，請對惡意使用者隔離異動基礎結構；在叢集部署中，請保護叢集登錄。</span><span class="sxs-lookup"><span data-stu-id="f1b88-172">In a workgroup deployment, isolate the transactional infrastructure from malicious users; in a cluster deployment, secure the cluster registry.</span></span>

## <a name="tracing"></a><span data-ttu-id="f1b88-173">追蹤</span><span class="sxs-lookup"><span data-stu-id="f1b88-173">Tracing</span></span>

<span data-ttu-id="f1b88-174">WS-AT 通訊協定服務支援整合式的交易特定追蹤，可透過使用 [ws-atomictransaction 設定 MMC 嵌入式管理](../ws-atomictransaction-configuration-mmc-snap-in.md) 單元工具來啟用和管理。</span><span class="sxs-lookup"><span data-stu-id="f1b88-174">The WS-AT protocol service supports integrated, transaction-specific tracing that can be enabled and managed through the use of the [WS-AtomicTransaction Configuration MMC Snap-in](../ws-atomictransaction-configuration-mmc-snap-in.md) tool.</span></span> <span data-ttu-id="f1b88-175">追蹤所包含的資料會指出登記特定交易的時間、交易到達終結狀態的時間、每個交易登記所接收的結果等。</span><span class="sxs-lookup"><span data-stu-id="f1b88-175">Traces can include data indicating the time an enlistment is made for a specific transaction, the time a transaction reaches its terminal state, the outcome each transaction enlistment has received.</span></span> <span data-ttu-id="f1b88-176">您可以使用 [服務追蹤檢視器工具 ( # A0) ](../service-trace-viewer-tool-svctraceviewer-exe.md) 工具來查看所有追蹤。</span><span class="sxs-lookup"><span data-stu-id="f1b88-176">All traces can be viewed using the [Service Trace Viewer Tool (SvcTraceViewer.exe)](../service-trace-viewer-tool-svctraceviewer-exe.md) tool.</span></span>

<span data-ttu-id="f1b88-177">WS-AT 通訊協定服務也支援經由 ETW 追蹤工作階段的整合式 ServiceModel 追蹤。</span><span class="sxs-lookup"><span data-stu-id="f1b88-177">The WS-AT protocol service also supports integrated ServiceModel tracing through the ETW trace session.</span></span> <span data-ttu-id="f1b88-178">如此除了現有的交易追蹤之外，也會提供更詳細的通訊特定追蹤。</span><span class="sxs-lookup"><span data-stu-id="f1b88-178">This provides more detailed, communication-specific traces in addition to the existing transaction traces.</span></span>  <span data-ttu-id="f1b88-179">若要啟用這些額外的追蹤，請遵循這些步驟</span><span class="sxs-lookup"><span data-stu-id="f1b88-179">To enable these additional traces, follow these steps</span></span>

1. <span data-ttu-id="f1b88-180">開啟 [ **開始]/[執行** ] 功能表，在 [輸入] 方塊中輸入 "regedit"，然後選取 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="f1b88-180">Open the **Start/Run** menu, type "regedit" in the input box and select **OK**.</span></span>

2. <span data-ttu-id="f1b88-181">在 [ **登錄編輯程式**] 中，流覽至左窗格中的下列資料夾，Hkey_Local_Machine: \software\microsoft\wsat\3.0</span><span class="sxs-lookup"><span data-stu-id="f1b88-181">In the **Registry Editor**, navigate to the following folder on the left pane, Hkey_Local_Machine\SOFTWARE\Microsoft\WSAT\3.0</span></span>\

3. <span data-ttu-id="f1b88-182">以滑鼠右鍵按一下 `ServiceModelDiagnosticTracing` 右窗格中的值，然後選取 [ **修改**]。</span><span class="sxs-lookup"><span data-stu-id="f1b88-182">Right-click the `ServiceModelDiagnosticTracing` value in the right pane and select **Modify**.</span></span>

4. <span data-ttu-id="f1b88-183">在 [ **數值資料** 輸入] 方塊中，輸入下列其中一個有效值，以指定您要啟用的追蹤層級。</span><span class="sxs-lookup"><span data-stu-id="f1b88-183">In the **Value data** input box, enter one of the following valid values to specify the trace level you want to enable.</span></span>

- <span data-ttu-id="f1b88-184">0：關閉</span><span class="sxs-lookup"><span data-stu-id="f1b88-184">0: off</span></span>

- <span data-ttu-id="f1b88-185">1：嚴重</span><span class="sxs-lookup"><span data-stu-id="f1b88-185">1: critical</span></span>

- <span data-ttu-id="f1b88-186">3：錯誤。</span><span class="sxs-lookup"><span data-stu-id="f1b88-186">3: error.</span></span> <span data-ttu-id="f1b88-187">這是預設值。</span><span class="sxs-lookup"><span data-stu-id="f1b88-187">This is the default value</span></span>

- <span data-ttu-id="f1b88-188">7：警告</span><span class="sxs-lookup"><span data-stu-id="f1b88-188">7: warning</span></span>

- <span data-ttu-id="f1b88-189">15：資訊</span><span class="sxs-lookup"><span data-stu-id="f1b88-189">15: information</span></span>

- <span data-ttu-id="f1b88-190">31：詳細資訊</span><span class="sxs-lookup"><span data-stu-id="f1b88-190">31: verbose</span></span>

## <a name="see-also"></a><span data-ttu-id="f1b88-191">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f1b88-191">See also</span></span>

- [<span data-ttu-id="f1b88-192">WS-AtomicTransaction 組態公用程式 (wsatConfig.exe)</span><span class="sxs-lookup"><span data-stu-id="f1b88-192">WS-AtomicTransaction Configuration Utility (wsatConfig.exe)</span></span>](../ws-atomictransaction-configuration-utility-wsatconfig-exe.md)
- [<span data-ttu-id="f1b88-193">WS-AtomicTransaction 組態 MMC 嵌入式管理單元</span><span class="sxs-lookup"><span data-stu-id="f1b88-193">WS-AtomicTransaction Configuration MMC Snap-in</span></span>](../ws-atomictransaction-configuration-mmc-snap-in.md)
