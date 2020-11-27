---
title: 建置 Windows Communication Foundation 範例
ms.date: 03/30/2017
ms.assetid: 2899e7a5-9cb2-4e8d-b8d2-f31391549198
ms.openlocfilehash: ee1c8101e31464fa203341d53137525433782c18
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96253828"
---
# <a name="building-the-windows-communication-foundation-samples"></a>建置 Windows Communication Foundation 範例

Windows Communication Foundation (WCF) 範例可以使用 Visual Studio IDE 或從命令列使用 **msbuild** 命令來建立。 本主題將同時說明這兩個程序。

> [!NOTE]
> 在建立或執行任何 WCF 範例之前，請確定您已執行 [Windows Communication Foundation 範例的單次安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。

## <a name="to-build-the-sample-using-a-command-prompt"></a>若要使用命令提示字元建置範例

1. 開啟 Visual Studio 的開發人員命令提示字元，然後在您安裝範例的目錄位置下流覽至特定語言的子目錄。

2. `msbuild`在命令列輸入。 用戶端程式檔案是 *client\bin* 建立的，而且服務程式檔案是 *service\bin* 的。 如果服務是由 Internet Information Services (IIS) 所裝載，則服務程式檔也會複製到 *servicemodelsamples* 目錄及其 *\bin* 子目錄中。

> [!NOTE]
> 您必須在 *%systemdrive%\inetpub\wwwroot* 上設定 acl，以將 modify 許可權授與您執行的帳戶。 否則，有些建置後事件將會失敗。 或者，您也可以不去改變這些 ACL，而以系統管理員身分來執行 SDK 命令提示字元。

## <a name="to-build-the-sample-using-visual-studio"></a>若要使用 Visual Studio 建置範例

1. 從 Visual Studio **的 [檔案**] 功能表中，選取 [**開啟**  >  **專案/方案**]。 流覽至您在其中安裝範例的目錄下的語言特定子目錄，然後按兩下 .sln 檔案圖示，在 Visual Studio 中開啟方案。

1. 從 [ **組建** ] 功能表中，選取 [ **重建方案**]。

   用戶端程式檔會建置至 client\bin，服務程式檔則建置至 service\bin。 如果服務是裝載在 IIS 中，則服務程式檔也會複製到 *servicemodelsamples* 目錄及其 *\bin* 子目錄中。

> [!NOTE]
> 您必須在 %systemdrive%\inetpub\wwwroot 上設定 ACL 以將修改權限授予您用來執行的帳戶。 否則，有些建置後事件將會失敗。 不過，您也可以不去改變這些 ACL，而以系統管理員身分來執行 SDK 命令提示字元或 Visual Studio。 某些 Visual Studio 動作 (例如，將偵錯工具附加至 ASP.NET 背景工作進程) 也需要系統管理許可權。

## <a name="setup-batch-files-and-scripts"></a>設定批次檔和指令碼

 Setup.exe 和 Cleanup.exe 批次檔和腳本應從開發人員命令提示字元執行，以進行 Visual Studio。 數種設定與清除檔案會執行需要系統管理員權限才能執行與啟動的工作。

## <a name="important-security-information-about-metadata-endpoints"></a>關於中繼資料端點的重要安全性資訊

 為了避免意外洩漏潛在的機密服務中繼資料，Windows Communication Foundation (WCF) 服務的預設設定會停用中繼資料發行。 這個行為依預設為安全行為，但也表示您無法使用中繼資料匯入工具 (例如 Svcutil.exe) 來產生呼叫服務所需的用戶端程式碼，除非組態中已明確啟用服務的中繼發行行為。 為了讓範例的實驗順利進行，幾乎所有範例都會公開不安全的中繼資料發行端點。 未經驗證的匿名使用者可能可以使用這類端點，所以部署前必須小心謹慎，才能確保公開服務中繼資料是否適切。 如需發行服務中繼資料的詳細資訊，請參閱 [中繼資料發行行為](metadata-publishing-behavior.md) 範例。 如需保護中繼資料端點的範例，請參閱 [自訂安全中繼資料端點](custom-secure-metadata-endpoint.md) 範例。

## <a name="exception-handling"></a>例外狀況處理

 一般來說，這些範例不包含例外狀況處理，以便讓程式碼專注在範例主題上。 如需例外狀況處理的詳細資訊，請參閱 [預期的例外](expected-exceptions.md) 狀況範例。

## <a name="regenerating-clients-and-configuration-with-svcutil"></a>使用 Svcutil 重新產生用戶端與組態

 您可以使用 [配置 [中繼資料公用程式] 工具 ( # A0) ](../servicemodel-metadata-utility-tool-svcutil-exe.md) 來重新產生大部分範例的用戶端程式代碼和設定。 某些範例需要您手動編輯組態。 例如，如果您使用 Svcutil.exe 針對使用用戶端憑證認證的範例重新產生組態，則您必須手動指定先前設定的認證。 某些範例使用特定的 Svcutil.exe 選項來影響產生的程式碼，而這些選項都會在特定的範例主題中加以指定。

### <a name="to-regenerate-the-client-and-configuration-files"></a>若要重新產生用戶端與組態檔

1. 開啟 [SDK 命令提示字元]，並巡覽至安裝範例所在目錄位置下任一語言特定子目錄。

2. 如果服務是 Web 裝載的型別，請使用下列命令。

    ```console
    svcutil.exe /n:"http://Microsoft.ServiceModel.Samples,Microsoft.ServiceModel.Samples" http://localhost/servicemodelsamples/service.svc/mex /out:generatedClient.cs
    ```

     如果服務是自我裝載的型別，請使用下列命令。

    ```console
    svcutil.exe /n:"http://Microsoft.ServiceModel.Samples,Microsoft.ServiceModel.Samples" http://localhost:8000/servicemodelsamples/service.svc/mex /out:generatedClient.cs
    ```

     取代 `http://localhost:8000/ServiceModelSamples/service.svc/mex` 為自我裝載服務 mex 端點的位址。

     若要以 Visual Basic 型別來產生用戶端，請使用下列命令。

    ```console
    svcutil.exe /n:"http://Microsoft.ServiceModel.Samples,Microsoft.ServiceModel.Samples" http://localhost/servicemodelsamples/service.svc/mex /l:vb /out:generatedClient.vb
    ```

     如果服務是自我裝載的型別，請使用下列命令。

    ```console
    svcutil.exe /n:"http://Microsoft.ServiceModel.Samples,Microsoft.ServiceModel.Samples" http://localhost:8000/servicemodelsamples/service.svc/mex /l:vb /out:generatedClient.vb
    ```

    > [!NOTE]
    > 若要略過用戶端設定的產生，請新增 **/noConfig** 選項。

## <a name="see-also"></a>另請參閱

- [執行 Windows Communication Foundation 範例](running-the-samples.md)
- [ServiceModel 中繼資料公用程式工具 (Svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md)
