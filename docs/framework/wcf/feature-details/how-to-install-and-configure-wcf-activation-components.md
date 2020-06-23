---
title: HOW TO：安裝和設定 WCF 啟用元件
description: 瞭解如何在 Windows Vista 上設定 Windows 進程啟用服務（WAS），以裝載不透過 HTTP 進行通訊的 WCF 服務。
ms.date: 03/30/2017
helpviewer_keywords:
- HTTP activation [WCF]
ms.assetid: 33a7054a-73ec-464d-83e5-b203aeded658
ms.openlocfilehash: 84a0dcc4fed28ebd7a536bdabfcdc389be6072d8
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/23/2020
ms.locfileid: "85246879"
---
# <a name="how-to-install-and-configure-wcf-activation-components"></a><span data-ttu-id="2a344-103">HOW TO：安裝和設定 WCF 啟用元件</span><span class="sxs-lookup"><span data-stu-id="2a344-103">How to: Install and Configure WCF Activation Components</span></span>

<span data-ttu-id="2a344-104">本主題說明在 Windows Vista 上設定 Windows 進程啟用服務（也稱為 WAS）來裝載無法透過 HTTP 網路通訊協定進行通訊的 Windows Communication Foundation （WCF）服務時，所需執行的步驟。</span><span class="sxs-lookup"><span data-stu-id="2a344-104">This topic describes the steps required to set up Windows Process Activation Service (also known as WAS) on Windows Vista to host Windows Communication Foundation (WCF) services that do not communicate over HTTP network protocols.</span></span> <span data-ttu-id="2a344-105">下列各節將概述此組態的各項步驟：</span><span class="sxs-lookup"><span data-stu-id="2a344-105">The following sections outline the steps for this configuration:</span></span>

- <span data-ttu-id="2a344-106">安裝（或確認安裝） WCF 啟用元件。</span><span class="sxs-lookup"><span data-stu-id="2a344-106">Install (or confirm the installation of) the WCF activation components.</span></span>

- <span data-ttu-id="2a344-107">設定 WAS 支援非 HTTP 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="2a344-107">Configure WAS to support a non-HTTP protocol.</span></span> <span data-ttu-id="2a344-108">下列程式會設定 Windows Vista 以進行 TCP 啟用。</span><span class="sxs-lookup"><span data-stu-id="2a344-108">The following procedure configures Windows Vista for TCP activation.</span></span>

<span data-ttu-id="2a344-109">安裝和設定 WAS 之後，請參閱[如何：在 WAS 中裝載 Wcf 服務](how-to-host-a-wcf-service-in-was.md)，以取得建立 wcf 服務的程式，以公開採用 WAS 的非 HTTP 端點。</span><span class="sxs-lookup"><span data-stu-id="2a344-109">After installing and configuring WAS, see [How to: Host a WCF Service in WAS](how-to-host-a-wcf-service-in-was.md) for the procedures to create a WCF service that exposes an non-HTTP endpoint that employs WAS.</span></span>

## <a name="to-install-the-wcf-non-http-activation-components"></a><span data-ttu-id="2a344-110">若要安裝 WCF 非 HTTP 啟動元件</span><span class="sxs-lookup"><span data-stu-id="2a344-110">To install the WCF non-HTTP activation components</span></span>

1. <span data-ttu-id="2a344-111">按一下 **[開始]** 按鈕，然後按一下 **[控制台]**。</span><span class="sxs-lookup"><span data-stu-id="2a344-111">Click the **Start** button, and then click **Control Panel**.</span></span>

2. <span data-ttu-id="2a344-112">按一下 [程式集]\*\*\*\*，然後按一下 [程式和功能]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="2a344-112">Click **Programs**, and then click **Programs and Features**.</span></span>

3. <span data-ttu-id="2a344-113">**在 [工作**] 功能表上，按一下 [**開啟或關閉 Windows 功能**]。</span><span class="sxs-lookup"><span data-stu-id="2a344-113">On the **Tasks** menu, click **Turn Windows features on or off**.</span></span>

4. <span data-ttu-id="2a344-114">尋找 WinFX 節點，選取，然後將它展開。</span><span class="sxs-lookup"><span data-stu-id="2a344-114">Find the WinFX node, select and then expand it.</span></span>

5. <span data-ttu-id="2a344-115">選取 [ **WCF 非 Http 啟用元件**] 方塊，然後儲存設定。</span><span class="sxs-lookup"><span data-stu-id="2a344-115">Select the **WCF Non-Http Activation Components** box and save the setting.</span></span>

## <a name="to-configure-the-was-to-support-tcp-activation"></a><span data-ttu-id="2a344-116">若要設定 WAS 來支援 TCP 啟動</span><span class="sxs-lookup"><span data-stu-id="2a344-116">To configure the WAS to support TCP activation</span></span>

1. <span data-ttu-id="2a344-117">若要支援 net.tcp 啟動，預設的網站必須先繫結至 net.tcp 連接埠。</span><span class="sxs-lookup"><span data-stu-id="2a344-117">To support net.tcp activation, the default Web site must first be bound to a net.tcp port.</span></span> <span data-ttu-id="2a344-118">您可以使用與 IIS 7.0 管理工具組一起安裝的 Appcmd.exe 來執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="2a344-118">You can do this by using Appcmd.exe, which is installed with the IIS 7.0 management toolset.</span></span> <span data-ttu-id="2a344-119">從系統管理員層級的 [命令提示字元] 視窗中，執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="2a344-119">In an administrator-level Command Prompt window, run the following command.</span></span>

    ```console
    %windir%\system32\inetsrv\appcmd.exe set site "Default Web Site" -+bindings.[protocol='net.tcp',bindingInformation='808:*']
    ```

    > [!NOTE]
    > <span data-ttu-id="2a344-120">這個命令是單行文字。</span><span class="sxs-lookup"><span data-stu-id="2a344-120">This command is a single line of text.</span></span> <span data-ttu-id="2a344-121">此命令會將 net.tcp 網站繫結新增至使用任何主機名稱來接聽 TCP 連接埠編號 808 的預設網站。</span><span class="sxs-lookup"><span data-stu-id="2a344-121">This command adds a net.tcp site binding to the default Web site listening on TCP port 808 with any host name.</span></span>

2. <span data-ttu-id="2a344-122">雖然網站中的所有應用程式共用常見的 net.tcp 繫結，但每個應用程式都可以個別啟用 net.tcp 支援。</span><span class="sxs-lookup"><span data-stu-id="2a344-122">Although all applications within a site share a common net.tcp binding, each application can enable net.tcp support individually.</span></span> <span data-ttu-id="2a344-123">若要啟用應用程式的 net.tcp，請從系統管理員層級的命令提示字元中執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="2a344-123">To enable net.tcp for the application, run the following command from an administrator-level command prompt.</span></span>

    ```console
    %windir%\system32\inetsrv\appcmd.exe set app
    "Default Web Site/<WCF Application>" /enabledProtocols:http,net.tcp
    ```

    > [!NOTE]
    > <span data-ttu-id="2a344-124">這個命令是單行文字。</span><span class="sxs-lookup"><span data-stu-id="2a344-124">This command is a single line of text.</span></span> <span data-ttu-id="2a344-125">此命令可讓/ \<*WCF Application*> 應用程式使用和來存取 `http://localhost/<WCF Application>` `net.tcp://localhost/<WCF Application>` 。</span><span class="sxs-lookup"><span data-stu-id="2a344-125">This command enables the /\<*WCF Application*> application to be accessed using both `http://localhost/<WCF Application>` and `net.tcp://localhost/<WCF Application>`.</span></span>

     <span data-ttu-id="2a344-126">移除您為此範例新增的 net.tcp 網站繫結。</span><span class="sxs-lookup"><span data-stu-id="2a344-126">Remove the net.tcp site binding you added for this sample.</span></span>

     <span data-ttu-id="2a344-127">為了方便起見，下列兩個步驟會以範例目錄中名為 RemoveNetTcpSiteBinding.cmd 的批次檔來加以實作。</span><span class="sxs-lookup"><span data-stu-id="2a344-127">As a convenience, the following two steps are implemented in a batch file called RemoveNetTcpSiteBinding.cmd located in the sample directory.</span></span>

    1. <span data-ttu-id="2a344-128">透過系統管理員層級的 [命令提示字元] 視窗執行下列命令，以從啟用的通訊協定清單中移除 net.tcp。</span><span class="sxs-lookup"><span data-stu-id="2a344-128">Remove net.tcp from the list of enabled protocols by running the following command in an administrator-level Command Prompt window.</span></span>

        ```console
        %windir%\system32\inetsrv\appcmd.exe set app
        "Default Web Site/servicemodelsamples<WCF Application>" " /enabledProtocols:http
        ```

        > [!NOTE]
        > <span data-ttu-id="2a344-129">這個命令是單行文字。</span><span class="sxs-lookup"><span data-stu-id="2a344-129">This command is a single line of text.</span></span>

    2. <span data-ttu-id="2a344-130">從提高權限的 [命令提示字元] 視窗中執行下列命令以移除 net.tcp 網站繫結：</span><span class="sxs-lookup"><span data-stu-id="2a344-130">Remove the net.tcp site binding by running the following command in an elevated Command Prompt window:</span></span>

        ```console
        %windir%\system32\inetsrv\appcmd.exe set site "Default Web Site"
        --bindings.[protocol='net.tcp',bindingInformation='808:*']
        ```

        > [!NOTE]
        > <span data-ttu-id="2a344-131">這個命令是單行文字。</span><span class="sxs-lookup"><span data-stu-id="2a344-131">This command is a single line of text.</span></span>

## <a name="to-remove-nettcp-from-the-list-of-enabled-protocols"></a><span data-ttu-id="2a344-132">若要從啟用的通訊協定清單中移除 net.tcp</span><span class="sxs-lookup"><span data-stu-id="2a344-132">To remove net.tcp from the list of enabled protocols</span></span>

1. <span data-ttu-id="2a344-133">若要從啟用的通訊協定清單中移除 net.tcp，請透過系統管理員層級的 [命令提示字元] 視窗執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="2a344-133">To remove net.tcp from the list of enabled protocols, run the following command in an administrator-level Command Prompt window.</span></span>

    ```console
    %windir%\system32\inetsrv\appcmd.exe set app "Default Web Site/servicemodelsamples<WCF Application>" " /enabledProtocols:http
    ```

    > [!NOTE]
    > <span data-ttu-id="2a344-134">這個命令是單行文字。</span><span class="sxs-lookup"><span data-stu-id="2a344-134">This command is a single line of text.</span></span>

## <a name="to-remove-the-nettcp-site-binding"></a><span data-ttu-id="2a344-135">若要移除 net.tcp 網站繫結</span><span class="sxs-lookup"><span data-stu-id="2a344-135">To remove the net.tcp site binding</span></span>

1. <span data-ttu-id="2a344-136">若要移除 net.tcp 網站繫結，請透過系統管理員層級的 [命令提示字元] 視窗執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="2a344-136">To remove the net.tcp site binding run the following command in an administrator-level Command Prompt window.</span></span>

    ```console
    %windir%\system32\inetsrv\appcmd.exe set site "Default Web Site"
    -bindings.[protocol='net.tcp',bindingInformation='808:*']
    ```

    > [!NOTE]
    > <span data-ttu-id="2a344-137">這個命令是單行文字。</span><span class="sxs-lookup"><span data-stu-id="2a344-137">This command is a single line of text.</span></span>

## <a name="see-also"></a><span data-ttu-id="2a344-138">另請參閱</span><span class="sxs-lookup"><span data-stu-id="2a344-138">See also</span></span>

- [<span data-ttu-id="2a344-139">TCP 啟用</span><span class="sxs-lookup"><span data-stu-id="2a344-139">TCP Activation</span></span>](../samples/tcp-activation.md)
- [<span data-ttu-id="2a344-140">MSMQ 啟用</span><span class="sxs-lookup"><span data-stu-id="2a344-140">MSMQ Activation</span></span>](../samples/msmq-activation.md)
- [<span data-ttu-id="2a344-141">NamedPipe 啟用</span><span class="sxs-lookup"><span data-stu-id="2a344-141">NamedPipe Activation</span></span>](../samples/namedpipe-activation.md)
- <span data-ttu-id="2a344-142">[Windows Server AppFabric 裝載功能](https://docs.microsoft.com/previous-versions/appfabric/ee677189(v=azure.10))</span><span class="sxs-lookup"><span data-stu-id="2a344-142">[Windows Server App Fabric Hosting Features](https://docs.microsoft.com/previous-versions/appfabric/ee677189(v=azure.10))</span></span>
