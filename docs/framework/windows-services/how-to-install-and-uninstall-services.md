---
title: 如何：安裝和卸載 Windows 服務
description: 請參閱如何安裝和卸載 Windows 服務。 如果您是使用 .NET 開發 Windows 服務，您可以使用 InstallUtil.exe 或 PowerShell。
ms.date: 02/05/2019
helpviewer_keywords:
- Windows Service applications, deploying
- services, uninstalling
- services, installing
- installing Windows Services
- uninstalling applications, apps, Windows services
- installation, Windows services
- uninstalling Windows services
- installutil.exe tool
ms.assetid: c89c5169-f567-4305-9d62-db31a1de5481
author: ghogen
ms.openlocfilehash: 883b587a7ef60bc686d6f453c775f6651f0ccb7f
ms.sourcegitcommit: 7476c20d2f911a834a00b8a7f5e8926bae6804d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/11/2020
ms.locfileid: "88063818"
---
# <a name="how-to-install-and-uninstall-windows-services"></a>如何：安裝和卸載 Windows 服務

如果您要使用 .NET Framework 開發 Windows 服務，您可以使用[*InstallUtil.exe*](../tools/installutil-exe-installer-tool.md)命令列公用程式或[PowerShell](/powershell/scripting/overview)，快速安裝服務應用程式。 想要發行使用者可以安裝和卸載之 Windows 服務的開發人員，可以使用免費的[WiX 工具](https://wixtoolset.org/)組或商業工具（例如[Advanced Installer](https://www.advancedinstaller.com/)、 [InstallShield](https://www.revenera.com/install/products/installshield.html)或其他專案）。 如需詳細資訊，請參閱[ (Windows 桌面) 建立安裝程式套件](/visualstudio/deployment/deploying-applications-services-and-components#create-an-installer-package-windows-desktop)。

> [!WARNING]
> 如果您想要從電腦解除安裝服務，則不要遵循本文中的步驟。 請改為找出安裝服務的程式或軟體套件，然後在 [設定] 中選擇 [應用程式]**** 以解除安裝該程式。 請注意，許多服務都是 Windows 不可或缺的一部分；如果移除這些服務，可能會導致系統不穩定。

若要使用本文中的步驟，首先需要將服務安裝程式新增至 Windows 服務。 如需詳細資訊，請參閱[逐步解說：建立 Windows 服務應用程式](walkthrough-creating-a-windows-service-application-in-the-component-designer.md)。

您無法按下 F5，直接從 Visual Studio 開發環境中執行 Windows 服務專案。 您必須先安裝專案中的服務，才可以執行專案。

> [!TIP]
> 您可以使用 [伺服器總管]**** 來確認您已安裝或解除安裝服務。 如需詳細資訊，請參閱 [How to use Server Explorer in Visual Studio](https://support.microsoft.com/help/316649/how-to-use-the-server-explorer-in-visual-studio-net-and-visual-studio) (如何在 Visual Studio 中使用伺服器總管)。

### <a name="install-your-service-manually-using-installutilexe-utility"></a>使用 InstallUtil.exe 公用程式手動安裝您的服務

1. 在 [**開始**] 功能表中，選取 [ **Visual Studio \<*version*> ** ] 目錄，然後選取 [**針對 VS \<*version*> 開發人員命令提示字元**]。

     隨即顯示 Visual Studio 開發人員命令提示字元。

2. 存取您的專案已編譯之可執行檔所在的目錄。

3. 從命令提示字元，以您專案的可執行檔作為參數來執行 *InstallUtil.exe*：

    ```console
    installutil <yourproject>.exe
    ```

     如果您使用 Visual Studio 開發人員命令提示字元，*InstallUtil.exe* 應該位在系統路徑中。 否則，您可以將這個檔案新增至路徑，或使用完整路徑來叫用這個檔案。 此工具會與 *%WINDIR%\Microsoft.NET\Framework [64] \\<framework_version \> *中的 .NET Framework 一併安裝。

     例如：
     - 針對 32 位元版本的 .NET Framework 4 或 4.5 和更新版本，如果您的 Windows 安裝目錄是 *C:\Windows*，則預設路徑為 *C:\Windows\Microsoft.NET\Framework\v4.0.30319\InstallUtil.exe*。
     - 針對 64 位元版本的 .NET Framework 4 或 4.5 和更新版本，預設路徑為 *C:\Windows\Microsoft.NET\Framework64\v4.0.30319\InstallUtil.exe*。

### <a name="uninstall-your-service-manually-using-installutilexe-utility"></a>使用 InstallUtil.exe 公用程式手動卸載您的服務

1. 在 [**開始**] 功能表中，選取 [ **Visual Studio \<*version*> ** ] 目錄，然後選取 [**針對 VS \<*version*> 開發人員命令提示字元**]。

     隨即顯示 Visual Studio 開發人員命令提示字元。

2. 從命令提示字元，以您專案的輸出作為參數來執行 *InstallUtil.exe*：

    ```console
    installutil /u <yourproject>.exe
    ```

3. 刪除服務的可執行檔之後，服務可能還是會在登錄中。 如果是這種情況，請使用命令 [sc delete](/windows-server/administration/windows-commands/sc-delete) 來從登錄中移除服務項目。

### <a name="install-your-service-manually-using-powershell"></a>使用 PowerShell 手動安裝您的服務

1. 從 [**開始**] 功能表中，選取 [ **windows powershell** ] 目錄，然後選取 [ **windows powershell**]。

2. 存取您的專案已編譯之可執行檔所在的目錄。

3. 使用搭配專案的輸出和服務名稱作為參數，執行[**新的-Service**](/powershell/module/microsoft.powershell.management/new-service) Cmdlet：

    ```powershell
    New-Service -Name "YourServiceName" -BinaryPathName <yourproject>.exe
    ```

### <a name="uninstall-your-service-manually-using-powershell"></a>使用 PowerShell 手動卸載您的服務

1. 從 [**開始**] 功能表中，選取 [ **windows powershell** ] 目錄，然後選取 [ **windows powershell**]。

2. 使用您的服務名稱作為參數來執行[**Remove-Service**](/powershell/module/microsoft.powershell.management/remove-service) Cmdlet：

    ```powershell
    Remove-Service -Name "YourServiceName"
    ```

3. 刪除服務的可執行檔之後，服務可能還是會在登錄中。 如果是這種情況，請使用命令 [sc delete](/windows-server/administration/windows-commands/sc-delete) 來從登錄中移除服務項目。

    ```powershell
    sc.exe delete "YourServiceName"
    ```

## <a name="see-also"></a>另請參閱

- [Windows 服務應用程式簡介](introduction-to-windows-service-applications.md)
- [How to：建立 Windows 服務](how-to-create-windows-services.md)
- [如何：將安裝程式新增至您的服務應用程式](how-to-add-installers-to-your-service-application.md)
- [Installutil.exe (安裝程式工具)](../tools/installutil-exe-installer-tool.md)
