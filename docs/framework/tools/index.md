---
title: .NET Framework 工具
description: 查看 .NET 工具清單，讓您更輕鬆地建立、部署及管理以 .NET 為目標的應用程式和元件。
ms.date: 03/30/2017
helpviewer_keywords:
- command line, .NET Framework tools
- .NET Framework, tools
- tools [.NET Framework]
- running .NET Framework tools
ms.assetid: a2ca532d-91f7-426a-9303-417c2ee1247c
ms.openlocfilehash: 0a5cbcd4fa60b819d3ab07a4f221e77ca106c321
ms.sourcegitcommit: 87cfeb69226fef01acb17c56c86f978f4f4a13db
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2020
ms.locfileid: "87166851"
---
# <a name="net-framework-tools"></a>.NET Framework 工具

.NET Framework 工具可讓您更輕鬆地建立、部署和管理以 .NET Framework 為目標的應用程式和元件。

本節提及的大部分 .NET Framework 工具會隨 Visual Studio 自動安裝  若要下載 Visual Studio，請前往 [Visual Studio 下載](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019)頁面。

您可以從命令列執行所有工具，但元件快取檢視器除外（*Shfusion.dll*）。 您必須從 [檔案瀏覽器] 存取*Shfusion.dll* 。
  
執行命令列工具的最佳方式，是使用 Visual Studio 的 [開發人員命令提示字元]。 這些公用程式可讓您輕鬆執行工具，而不必巡覽至安裝資料夾。 如需詳細資訊，請參閱[命令提示字元](developer-command-prompt-for-vs.md)。

> [!NOTE]
> 某些工具為 32 位元電腦或 64 位元電腦專用。 請務必執行電腦適用的工具版本。

## <a name="in-this-section"></a>本節內容

- [Al.exe （元件連結器）](al-exe-assembly-linker.md)  
從模組或資源檔中產生一個包含組件資訊清單的檔案。

- [Aximp.exe （Windows Forms ActiveX 控制項匯入工具）](aximp-exe-windows-forms-activex-control-importer.md)  
將 COM 類型程式庫中的類型定義轉換為 Windows Form 控制項中的 ActiveX 控制項。

- [Caspol.exe （代碼啟用安全性原則工具）](caspol-exe-code-access-security-policy-tool.md)  
可讓您檢視和設定電腦原則層級、使用者原則層級和企業原則層級的安全性原則。 在 .NET Framework 4 和更新版本中，除非[ \<legacyCasPolicy> 元素](../configure-apps/file-schema/runtime/netfx40-legacysecuritypolicy-element.md)設定為，否則此工具不會影響代碼啟用安全性（CAS）原則 `true` 。 如需詳細資訊，請參閱[安全性變更](https://docs.microsoft.com/previous-versions/dotnet/framework/security/security-changes)。

- [Cert2spc.exe （軟體發行者憑證測試控管）](cert2spc-exe-software-publisher-certificate-test-tool.md)  
從一個或多個 X.509 憑證建立軟體發行者憑證 (SPC)。 這個工具僅供測試用。

- [Certmgr.exe （憑證管理員工具）](certmgr-exe-certificate-manager-tool.md)  
管理憑證、憑證信任清單 (CTL) 和憑證廢止清單 (CRL)。

- [Clrver.exe （CLR 版本工具）](clrver-exe-clr-version-tool.md)  
報告電腦上所有已安裝的 common language runtime （CLR）版本。

- [命令提示字元](developer-command-prompt-for-vs.md)  
可讓您更輕鬆地使用 .NET Framework 工具。 它是命令提示字元，可自動設定特定的環境變數。

- [CorFlags.exe （CorFlags 轉換工具）](corflags-exe-corflags-conversion-tool.md)  
可讓您設定可攜式執行檔 (PE) 影像之標頭的 CorFlags 區段。

- [Fuslogvw.exe （元件系結記錄檔檢視器）](fuslogvw-exe-assembly-binding-log-viewer.md)  
顯示有關組件繫結的資訊，可以協助您診斷 .NET Framework 為何不能在執行階段時找到組件。

- [Gacutil.exe （全域組件快取工具）](gacutil-exe-gac-tool.md)  
可讓您檢視和操作全域組件快取的內容並下載快取。

- [Ilasm.exe （IL 組譯工具）](ilasm-exe-il-assembler.md)  
從中繼語言 (IL) 中產生可攜式執行檔 (PE)。 您可以執行產生的可執行檔，來判斷 IL 是否如預期般地執行。

- [Ildasm.exe （IL 解譯器）](ildasm-exe-il-disassembler.md)  
使用包含中繼語言 (IL) 程式碼的可攜式執行檔 (PE)，並建立可以輸入至 IL 組譯工具 (Ilasm.exe) 的文字檔。

- [Installutil.exe （安裝程式工具）](installutil-exe-installer-tool.md)  
可讓您藉由執行所指定組件的 Installer 元件，來安裝和解除安裝伺服器資源  (使用 <xref:System.Configuration.Install> 命名空間中的類別)。

- [Lc.exe （授權編譯器）](lc-exe-license-compiler.md)  
讀取包含授權資訊的文字檔，並產生可以內嵌在 common language runtime 可執行檔中做為資源的*許可證*檔。

- [Mage.exe （資訊清單產生和編輯工具）](mage-exe-manifest-generation-and-editing-tool.md)  
可讓您建立、編輯和簽署應用程式以及部署資訊清單。 由於 *Mage.exe* 是命令列工具，因此可以從批次指令碼及其他 Windows 應用程式 (包括 ASP.NET 應用程式) 中執行。

- [MageUI.exe （資訊清單產生和編輯工具、圖形化用戶端）](mageui-exe-manifest-generation-and-editing-tool-graphical-client.md)  
支援與命令列工具 Mage.exe 相同的功能，但使用 Windows 架構使用者介面 (UI)。 支援與命令列工具*Mage.exe*相同的功能，但使用以 Windows 為基礎的使用者介面（UI）。

- [MDbg.exe （.NET Framework 命令列偵錯工具）](mdbg-exe.md)  
協助工具廠商和應用程式開發人員尋找並修復以 .NET Framework 通用語言執行平台為目標的程式中的 Bug。 這個工具使用執行階段偵錯 API 來提供偵錯服務。

- [Mgmtclassgen.exe （管理強型別類別產生器）](mgmtclassgen-exe.md)  
可讓您為指定的 Windows Management Instrumentation (WMI) 類別，產生早期繫結 Managed 類別。

- [Mpgo.exe （Managed 特性指引優化工具）](mpgo-exe-managed-profile-guided-optimization-tool.md)  
可讓您調整使用一般使用者情節的原生映像組件。 Mpgo.exe 可讓您使用應用程式開發人員選出的訓練情節，產生和使用原生映像應用程式組件 (不是 .NET Framework 組件) 的分析資料。

- [Ngen.exe （原生映射產生器）](ngen-exe-native-image-generator.md)  
透過使用原生影像 (含有已編譯之處理器特定機器碼的檔案)，改善 Managed 應用程式的效能。 執行階段就可以從快取中使用原生映像，而不是使用 Just-In-Time (JIT) 編譯器來編譯原始組件。

- [Peverify.exe （PEVerify 工具）](peverify-exe-peverify-tool.md)  
可以協助您驗證 Microsoft Intermediate Language (MSIL) 程式碼及相關的中繼資料是否符合類型安全需求。

- [Regasm.exe （元件註冊工具）](regasm-exe-assembly-registration-tool.md)  
讀取組件內的中繼資料，並將需要的項目加入登錄。 這可讓 COM 用戶端顯示為 .NET Framework 類別。

- [Regsvcs.exe （.NET 服務安裝工具）](regsvcs-exe-net-services-installation-tool.md)  
載入並註冊組件、產生並安裝類型程式庫至指定的 COM+ 1.0 版應用程式，以及設定您已利用程式設計方式加入至類別的服務。

- [Resgen.exe （資源檔產生器）](resgen-exe-resource-file-generator.md)  
將文字檔（*.txt*或 *. .restext*）和 XML 架構資源格式（*.resx*）檔案轉換為 common language runtime 二進位（*.resources*）檔案，這些檔案可以內嵌在執行時間二進位可執行檔中，或編譯成附屬元件。

- [SecAnnotate.exe （.NET Security Annotator Tool）](secannotate-exe-net-security-annotator-tool.md)  
識別組件的 `SecurityCritical` 和 `SecuritySafeCritical` 的部分。

- [SignTool.exe （簽署工具）](signtool-exe.md)  
數位簽署檔案、驗證檔案中的簽章，以及為檔案加上時間戳記。

- [Sn.exe （強式名稱工具）](sn-exe-strong-name-tool.md)  
幫助以強式名稱 (Strong Name) 建立組件。 這個工具提供了金鑰管理、簽章產生和簽章驗證的選項。

- [SOS.dll （SOS 調試延伸模組）](sos-dll-sos-debugging-extension.md)  
提供內部通用語言執行平台環境的相關資訊，以協助您在 WinDbg.exe 偵錯工具和 Visual Studio 中偵錯 Managed 程式。

- [SqlMetal.exe （程式碼產生工具）](sqlmetal-exe-code-generation-tool.md)  
為 .NET Framework 的 LINQ to SQL 元件產生程式碼和對應。

- [Storeadm.exe （隔離儲存區工具）](storeadm-exe-isolated-storage-tool.md)  
管理隔離儲存區 (Isolated Storage)，提供選項以列出使用者的存放區並加以刪除。

- [Tlbexp.exe （類型程式庫匯出工具）](tlbexp-exe-type-library-exporter.md)  
產生類型程式庫，類型程式庫會描述通用語言執行平台 (CLR) 組件中所定義的類型。

- [Tlbimp.exe （類型程式庫匯入工具）](tlbimp-exe-type-library-importer.md)  
將 COM 類型程式庫中找到的類型定義轉換為通用語言執行平台組件中的等效定義。

- [Winmdexp.exe （Windows 執行階段中繼資料匯出工具）](winmdexp-exe-windows-runtime-metadata-export-tool.md)  
將編譯為*winmdobj*檔案的 .NET Framework 元件匯出到 Windows 執行階段元件中，該元件會封裝為包含 Windows 執行階段中繼資料和執行資訊的*winmd*檔案。

- [Winres.exe （Windows Forms 資源編輯器）](winres-exe-windows-forms-resource-editor.md)  
協助您將 Windows Forms 所使用的使用者介面（UI）資源（*.resx*或 *.resources*檔案）當地語系化。 您可以解譯字串，然後調整大小、移動和隱藏控制項來容納當地語系化的字串。

## <a name="related-sections"></a>相關章節

- [WPF 工具](https://docs.microsoft.com/previous-versions/ms742404(v=vs.110))  
包括 isXPS Conformance 工具 (isXPS.exe) 和效能程式碼剖析工具這類工具。

- [Windows Communication Foundation 工具](../wcf/tools.md)  
包含多種工具，可以幫助您更輕鬆地建立、部署及管理 Windows Communication Foundation (WCF) 應用程式。
