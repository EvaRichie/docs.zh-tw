---
title: 部署 .NET Framework 和應用程式
description: 開始使用您的應用程式來部署 .NET。 .NET 預設會提供不影響的應用程式、私用元件、控制的程式碼共用等等。
ms.date: 03/30/2017
helpviewer_keywords:
- deploying applications [.NET Framework], packaging
- deploying applications [.NET Framework]
- deploying applications [.NET Framework], features
- deploying applications [.NET Framework], distribution
- .NET Framework, deploying
- .NET Framework application deployment
ms.assetid: 238d8284-6042-4a38-a7f6-1ee8efd719da
ms.openlocfilehash: cce888c962c9ab83c13cce4040eb9ba50270972d
ms.sourcegitcommit: c23d9666ec75b91741da43ee3d91c317d68c7327
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85803493"
---
# <a name="deploying-the-net-framework-and-applications"></a>部署 .NET Framework 和應用程式

本文將協助您開始在應用程式上部署 .NET Framework。 大部分資訊的目標對象是開發人員、OEM 和企業系統管理員。 想要在電腦上安裝 .NET Framework 的使用者應閱讀[安裝 .NET Framework](../install/index.md)。

## <a name="key-deployment-resources"></a>主要部署資源

使用下列連結連接至其他 MSDN 主題，了解有關 .NET Framework 部署和服務的特定資訊。

**安裝和部署**

- 一般安裝程式和部署資訊：

  - 安裝程式選項：

    - [Web 安裝程式](../install/guide-for-developers.md#to-install-or-download-the-net-framework-redistributable)

    - [離線安裝程式](../install/guide-for-developers.md#to-install-or-download-the-net-framework-redistributable)

  - 安裝模式：

    - [無訊息安裝](deployment-guide-for-developers.md#chaining_custom)

    - [顯示 UI](deployment-guide-for-developers.md#chaining_default)

  - [在 .NET Framework 4.5 安裝期間減少系統重新啟動的次數](reducing-system-restarts.md)

  - [疑難排解 .NET Framework 安裝和解除安裝遭封鎖的問題](../install/troubleshoot-blocked-installations-and-uninstallations.md)

- 在用戶端應用程式上部署 .NET Framework (適用於開發人員)：

  - 在安裝和部署專案中[使用 InstallShield](deployment-guide-for-developers.md#installshield-deployment)

  - [使用 Visual Studio ClickOnce 應用程式](deployment-guide-for-developers.md#clickonce-deployment)

  - [建立 WiX 安裝套件](deployment-guide-for-developers.md#wix)

  - [使用自訂安裝程式](deployment-guide-for-developers.md#chaining)

  - 適用於開發人員的[其他資訊](deployment-guide-for-developers.md)

- 部署 .NET Framework (適用於 OEM 和系統管理員)：

  - [Windows 評定及部署套件 (ADK)](https://go.microsoft.com/fwlink/p/?LinkId=254976)

  - [系統管理員手冊](guide-for-administrators.md)

**服務**

- 如需一般資訊，請參閱[.NET Framework 的 blog](https://devblogs.microsoft.com/dotnet/)。

- [偵測版本](../migration-guide/how-to-determine-which-versions-are-installed.md)

- [偵測 Service Pack 和更新](../migration-guide/how-to-determine-which-net-framework-updates-are-installed.md)

## <a name="features-that-simplify-deployment"></a>簡化部署的功能

.NET Framework 提供了一些基本功能，讓部署應用程式更為容易：

- 不受影響的應用程式。

     這項功能提供應用程式隔離，並排除 DLL 衝突。 根據預設，元件不會影響其他應用程式。

- 預設為私用元件。

     根據預設，元件會部署到應用程式目錄，並且只有對包含的應用程式為可見的。

- 受控制的程式碼共用。

     程式碼共用需要您明確地將程式碼設定為共用，而不是使用預設行為。

- 並存版本。

     元件或應用程式的多個版本可以共存，您可以選擇要使用哪個版本，而且 Common Language Runtime 會強制執行版本原則。

- XCOPY 部署和複寫。

     自我描述和獨立的元件和應用程式不需登錄項目或相依性即可部署。

- 動態更新。

     系統管理員可以使用主應用程式 (例如 ASP.NET) 來更新程式 DLL，甚至是在遠端電腦上。

- 與 Windows Installer 整合

     部署您的應用程式時，通告、發行、修復和隨選安裝全部都可以使用。

- 企業部署。

     這項功能可讓您輕鬆散發軟體，包括使用 Active Directory。

- 下載和快取。

     累加下載會維持較小的下載，而且會隔離元件，僅供對部署影響較小的應用程式使用。

- 部分信任的程式碼

     識別的依據是程式碼而非使用者，而且不會出現憑證對話方塊。

## <a name="packaging-and-distributing-net-framework-applications"></a>封裝和散發 .NET Framework 應用程式

文件的其他章節將說明 .NET Framework 的一些封裝和部署資訊。 那些小節針對下列內容提供相關資訊：稱為[組件](../../standard/assembly/index.md)的自我描述單位 (不需要登錄項目)、[強式名稱的組件](../../standard/assembly/strong-named.md) (能確保名稱唯一性並防止名稱冒用)，以及[組件版本控制](../../standard/assembly/versioning.md) (能處理許多與 DLL 衝突相關的問題)。 下列章節提供封裝和散發 .NET Framework 應用程式的相關資訊。

### <a name="packaging"></a>包裝

.NET Framework 提供下列封裝應用程式的選項：

- 當做單一組件或組件集合。

     使用這個選項時，您會直接依建置時原狀使用 .dll 或 .exe 檔。

- 當做封包 (CAB) 檔案。

     使用這個選項時，您會將檔案壓縮成 .cab 檔，讓散發或下載較不費時。

- 當做 Windows Installer 套件或採用其他安裝程式的格式。

     使用這個選項時，您將會建立搭配 Windows Installer 使用的 .msi 檔，或封裝您的應用程式以搭配另一個安裝程式使用。

### <a name="distribution"></a>散發

.NET Framework 提供下列散發應用程式的選項：

- 使用 XCOPY 或 FTP。

     由於 Common Language Runtime 應用程式是自我描述且不需要登錄項目，因此您可以使用 XCOPY 或 FTP 直接將應用程式複製到適當的目錄。 接著便可從該目錄執行應用程式。

- 使用程式碼下載。

     如果您正在網際網路上或透過公司內部網路散發應用程式，您可以直接將程式碼下載到電腦，並在電腦上執行應用程式。

- 使用安裝程式，例如 Windows Installer 2.0。

     Windows Installer 2.0 可以在全域組件快取和私人目錄中安裝、修復或移除 .NET Framework 組件。

### <a name="installation-location"></a>安裝位置

若要決定應用程式的組件應該部署在哪裡，使執行階段能夠找到它們，請參閱[執行階段如何找出組件](how-the-runtime-locates-assemblies.md)。

安全性考量也可能影響您部署應用程式的方式。 在對 Managed 程式碼授與安全性權限時，依據的是程式碼的位置。 如果將應用程式或元件部署到信任度極低的位置 (例如網際網路)，應用程式或元件所能執行的工作則會受限。 如需部署和安全性考量的詳細資訊，請參閱[程式碼存取安全性的基本概念](../misc/code-access-security-basics.md)。

## <a name="related-topics"></a>相關主題

|Title|描述|
|-----------|-----------------|
|[執行階段如何找出組件](how-the-runtime-locates-assemblies.md)|描述 Common Language Runtime 如何決定要用哪個組件來實現繫結要求。|
|[組件載入的最佳做法](best-practices-for-assembly-loading.md)|討論如何避免發生可能造成 <xref:System.InvalidCastException>、<xref:System.MissingMethodException> 和其他錯誤之類型識別的問題。|
|[減少 .NET Framework 4.5 安裝期間的系統重新開機](reducing-system-restarts.md)|描述可防止在任何可能的情況下重新開機的重新啟動管理員，並說明安裝 .NET Framework 的應用程式如何利用 .NET Framework。|
|[系統管理員部署手冊](guide-for-administrators.md)|說明系統管理員如何使用 Microsoft 端點 Configuration Manager，在網路上部署 .NET Framework 及其系統相依性。|
|[開發人員部署手冊](deployment-guide-for-developers.md)|說明開發人員如何將 .NET Framework 隨使用者的應用程式安裝在其電腦上。|
|[部署應用程式、服務和元件](/visualstudio/deployment/deploying-applications-services-and-components)|討論 Visual Studio 中的部署選項，包括使用 ClickOnce 和 Windows Installer 技術發行應用程式的指示。|
|[發行 ClickOnce 應用程式](/visualstudio/deployment/publishing-clickonce-applications)|描述如何封裝 Windows Forms 應用程式，並使用 ClickOnce 將它部署到網路上的用戶端電腦。|
|[封裝和部署資源](../resources/packaging-and-deploying-resources-in-desktop-apps.md)|描述 .NET Framework 用來封裝及部署資源的中樞和輪輻模型；內容涵蓋資源命名慣例、後援程序和封裝替代方式。|
|[部署 Interop 應用程式](../interop/deploying-an-interop-application.md)|描述如何交付及安裝 Interop 應用程式，這類應用程式通常包含 .NET Framework 用戶端組件、代表各種不同 COM 類型程式庫的一或多個 Interop 組件，以及一或多個已註冊的 COM 元件。|
|[如何：取得 .NET Framework 4.5 安裝程式的進度](how-to-get-progress-from-the-dotnet-installer.md)|描述如何以無訊息模式啟動並追蹤 .NET Framework 安裝程序，並同時顯示您自己的安裝進度檢視。|

## <a name="see-also"></a>另請參閱

- [開發指南](../development-guide.md)
