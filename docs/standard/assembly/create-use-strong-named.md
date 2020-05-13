---
title: 建立和使用強式名稱的組件
description: 本文說明如何在 .NET 中使用強式名稱簽署元件，並于稍後依該名稱參考它。
ms.date: 08/19/2019
helpviewer_keywords:
- strong-name bypass feature
- strong-named assemblies, about strong-named assemblies
- strong-named assemblies
- signing assemblies
- assemblies [.NET Framework], signing
- strong-named assemblies, scenarios
- assemblies [.NET Framework], strong-named
- strong-named assemblies, loading into trusted application domains
- assembly binding, strong-named
ms.assetid: ffbf6d9e-4a88-4a8a-9645-4ce0ee1ee5f9
ms.openlocfilehash: 79c8cf2c21210fd80392a8aacf92840c11a36e43
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/13/2020
ms.locfileid: "83378525"
---
# <a name="create-and-use-strong-named-assemblies"></a>建立和使用強式名稱的組件

強式名稱 (Strong Name) 是由組件的識別 (Identity)，也就是其簡單文字名稱、版本號碼及文化特性資訊 (如果有提供)，加上公開金鑰和數位簽章所組成的。 這是使用對應的私密金鑰，從組件檔案所產生  (組件檔案包含附屬組件資訊清單，而資訊清單則包含組件中所有檔案的名稱和雜湊)。

> [!WARNING]
> 請勿依賴強式名稱提供安全性。 強式名稱僅提供唯一識別。

強式名稱的組件只可使用來自其他強式名稱組件的類型。 否則，強式名稱組件的完整性會受到危害。

> [!NOTE]
> 雖然 .NET Core 支援強式名稱的元件，而且 .NET Core 程式庫中的所有元件都已簽署，但大部分的協力廠商元件都不需要強名稱。 如需詳細資訊，請參閱 GitHub 上的[強式名稱簽署](https://github.com/dotnet/runtime/blob/master/docs/project/strong-name-signing.md)。

## <a name="strong-name-scenario"></a>強式名稱案例

下列案例概述處理序如何使用強式名稱簽署組件，然後再使用該名稱參考該組件。

1. 組件 A 是以下列方法之一，使用強式名稱所建立：

    - 使用支援建立強式名稱的開發環境，例如 Visual Studio。

    - 使用[強式名稱工具 (Sn.exe)](../../framework/tools/sn-exe-strong-name-tool.md) 建立密碼編譯金鑰組，並使用命令列編譯器或[組件連結器 (Al.exe)](../../framework/tools/al-exe-assembly-linker.md) 將該金鑰組指派給組件。 Windows SDK 提供 Sn.exe 與 Al.exe。

2. 開發環境或工具會使用開發人員的私密金鑰簽署檔案雜湊，而該檔案中包含組件的資訊清單。 此數位簽章儲存在可攜式執行檔 (PE) 中，而該檔案包含組件 A 的 資訊清單。

3. 組件 B 是組件 A 的消費者。組件 B 的資訊清單參考區段包含代表組件 A 公開金鑰的語彙基元。 語彙基元是完整公開金鑰的一部分，會取代金鑰本身來節省空間。

4. 當組件放在全域組件快取時，Common Language Runtime 會驗證強式名稱簽草章。 Common Language Runtime 在執行階段以強式名稱繫結時，會比較儲存在組件 B 資訊清單的金鑰，以及用來產生組件 A 強式名稱的金鑰。若 .NET Framework 通過安全性檢查且繫結成功，組件 B 就能保證組件 A 的位元未被修改，而且確實來自組件 A 的開發人員。

> [!NOTE]
> 此案例無法解決信任問題。 除了強式名稱之外，組件能夠包含完整的 Microsoft Authenticode 簽章。 Authenticode 簽章包含建立信任的憑證。 請務必注意，強式名稱不會要求程式碼以這種方式簽署。 強式名稱僅提供唯一身分識別。

## <a name="bypass-signature-verification-of-trusted-assemblies"></a>略過信任組件的簽章驗證

從 .NET Framework 3.5 Service Pack 1 開始，當組件載入到完全信任的應用程式網域 (例如適用於 `MyComputer` 區域的預設應用程式網域) 時，不會驗證強式名稱簽章。 這是指強式名稱略過功能。 在完全信任環境中，不論簽章為何，已簽署、完全信任的組件要求 <xref:System.Security.Permissions.StrongNameIdentityPermission> 一律會成功。 強式名稱略過功能可以避免在這種狀況中不必要的額外負荷，也就是完全信任組件的強式名稱簽章驗證，讓組件能夠更快載入。

略過功能適用於任何以強式名稱簽署並具有下列特性的組件：

- 完全信任而不具有 <xref:System.Security.Policy.StrongName> 辨識項 (例如具有 `MyComputer` 區域辨識項)。

- 載入到完全信任的 <xref:System.AppDomain>。

- 從 <xref:System.AppDomain> 的 <xref:System.AppDomainSetup.ApplicationBase%2A> 屬性下的位置載入。

- 不延遲簽署。

個別應用程式或電腦可停用此功能。 請參閱[如何：停用強式名稱略過功能](disable-strong-name-bypass-feature.md)。

## <a name="related-topics"></a>相關主題

|Title|描述|
|-----------|-----------------|
|[如何：建立公開/私密金鑰組](create-public-private-key-pair.md)|描述如何建立簽署組件的密碼編譯金鑰組。|
|[如何：使用強式名稱簽署元件](sign-strong-name.md)|描述如何建立強式名稱組件。|
|[增強的強式命名](enhanced-strong-naming.md)|描述 .NET Framework 4.5 中強式名稱的增強項目。|
|[如何：參考強式名稱的元件](reference-strong-named.md)|描述如何在編譯或執行階段期間，參考以強式名稱命名之組件中的類型或資源。|
|[如何：停用強式名稱略過功能](disable-strong-name-bypass-feature.md)|描述如何停用會略過強式名稱簽章驗證的功能。 所有應用程式皆可停用此功能，也可以只停用特定應用程式中的此功能。|
|[建立組件](create.md)|提供單一檔案和多檔案組件的概觀。|
|[如何在 Visual Studio 中延遲簽署元件](/visualstudio/ide/managing-assembly-and-manifest-signing#how-to-sign-an-assembly-in-visual-studio)|說明如何在建立組件之後，使用強式名稱簽署組件。|
|[Sn.exe （強式名稱工具）](../../framework/tools/sn-exe-strong-name-tool.md)|描述 .NET Framework 中可協助使用強式名稱來建立組件的工具。 這個工具提供了金鑰管理、簽章產生和簽章驗證的選項。|
|[Al.exe (組件連接器)](../../framework/tools/al-exe-assembly-linker.md)|描述 .NET Framework 中可產生檔案的工具，而該檔案具有來自模組或資源檔案組件的資訊清單。|
