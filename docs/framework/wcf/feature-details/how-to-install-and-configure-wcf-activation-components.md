---
title: HOW TO：安裝和設定 WCF 啟用元件
ms.date: 03/30/2017
helpviewer_keywords:
- HTTP activation [WCF]
ms.assetid: 33a7054a-73ec-464d-83e5-b203aeded658
ms.openlocfilehash: f7a846b076691394cb855e4978e890cdcac76eb2
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84597029"
---
# <a name="how-to-install-and-configure-wcf-activation-components"></a>HOW TO：安裝和設定 WCF 啟用元件

本主題說明在 Windows Vista 上設定 Windows 進程啟用服務（也稱為 WAS）來裝載無法透過 HTTP 網路通訊協定進行通訊的 Windows Communication Foundation （WCF）服務時，所需執行的步驟。 下列各節將概述此組態的各項步驟：

- 安裝（或確認安裝） WCF 啟用元件。

- 設定 WAS 支援非 HTTP 通訊協定。 下列程式會設定 Windows Vista 以進行 TCP 啟用。

安裝和設定 WAS 之後，請參閱[如何：在 WAS 中裝載 Wcf 服務](how-to-host-a-wcf-service-in-was.md)，以取得建立 wcf 服務的程式，以公開採用 WAS 的非 HTTP 端點。

## <a name="to-install-the-wcf-non-http-activation-components"></a>若要安裝 WCF 非 HTTP 啟動元件

1. 按一下 **[開始]** 按鈕，然後按一下 **[控制台]**。

2. 按一下 [程式集]****，然後按一下 [程式和功能]****。

3. **在 [工作**] 功能表上，按一下 [**開啟或關閉 Windows 功能**]。

4. 尋找 WinFX 節點，選取，然後將它展開。

5. 選取 [ **WCF 非 Http 啟用元件**] 方塊，然後儲存設定。

## <a name="to-configure-the-was-to-support-tcp-activation"></a>若要設定 WAS 來支援 TCP 啟動

1. 若要支援 net.tcp 啟動，預設的網站必須先繫結至 net.tcp 連接埠。 您可以使用與 IIS 7.0 管理工具組一起安裝的 Appcmd.exe 來執行這項操作。 從系統管理員層級的 [命令提示字元] 視窗中，執行下列命令。

    ```console
    %windir%\system32\inetsrv\appcmd.exe set site "Default Web Site" -+bindings.[protocol='net.tcp',bindingInformation='808:*']
    ```

    > [!NOTE]
    > 這個命令是單行文字。 此命令會將 net.tcp 網站繫結新增至使用任何主機名稱來接聽 TCP 連接埠編號 808 的預設網站。

2. 雖然網站中的所有應用程式共用常見的 net.tcp 繫結，但每個應用程式都可以個別啟用 net.tcp 支援。 若要啟用應用程式的 net.tcp，請從系統管理員層級的命令提示字元中執行下列命令。

    ```console
    %windir%\system32\inetsrv\appcmd.exe set app
    "Default Web Site/<WCF Application>" /enabledProtocols:http,net.tcp
    ```

    > [!NOTE]
    > 這個命令是單行文字。 此命令可讓/ \<*WCF Application*> 應用程式使用和來存取 `http://localhost/<WCF Application>` `net.tcp://localhost/<WCF Application>` 。

     移除您為此範例新增的 net.tcp 網站繫結。

     為了方便起見，下列兩個步驟會以範例目錄中名為 RemoveNetTcpSiteBinding.cmd 的批次檔來加以實作。

    1. 透過系統管理員層級的 [命令提示字元] 視窗執行下列命令，以從啟用的通訊協定清單中移除 net.tcp。

        ```console
        %windir%\system32\inetsrv\appcmd.exe set app
        "Default Web Site/servicemodelsamples<WCF Application>" " /enabledProtocols:http
        ```

        > [!NOTE]
        > 這個命令是單行文字。

    2. 從提高權限的 [命令提示字元] 視窗中執行下列命令以移除 net.tcp 網站繫結：

        ```console
        %windir%\system32\inetsrv\appcmd.exe set site "Default Web Site"
        --bindings.[protocol='net.tcp',bindingInformation='808:*']
        ```

        > [!NOTE]
        > 這個命令是單行文字。

## <a name="to-remove-nettcp-from-the-list-of-enabled-protocols"></a>若要從啟用的通訊協定清單中移除 net.tcp

1. 若要從啟用的通訊協定清單中移除 net.tcp，請透過系統管理員層級的 [命令提示字元] 視窗執行下列命令。

    ```console
    %windir%\system32\inetsrv\appcmd.exe set app "Default Web Site/servicemodelsamples<WCF Application>" " /enabledProtocols:http
    ```

    > [!NOTE]
    > 這個命令是單行文字。

## <a name="to-remove-the-nettcp-site-binding"></a>若要移除 net.tcp 網站繫結

1. 若要移除 net.tcp 網站繫結，請透過系統管理員層級的 [命令提示字元] 視窗執行下列命令。

    ```console
    %windir%\system32\inetsrv\appcmd.exe set site "Default Web Site"
    -bindings.[protocol='net.tcp',bindingInformation='808:*']
    ```

    > [!NOTE]
    > 這個命令是單行文字。

## <a name="see-also"></a>請參閱

- [TCP 啟用](../samples/tcp-activation.md)
- [MSMQ 啟用](../samples/msmq-activation.md)
- [NamedPipe 啟用](../samples/namedpipe-activation.md)
- [Windows Server AppFabric 裝載功能](https://docs.microsoft.com/previous-versions/appfabric/ee677189(v=azure.10))
