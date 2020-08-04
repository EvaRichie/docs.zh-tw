---
title: Winmdexp.exe (Windows 執行階段中繼資料匯出工具)
description: 瞭解 Winmdexp.exe，Windows 執行階段中繼資料匯出工具。 此工具會將 .NET 模組轉換成包含 Windows 執行階段中繼資料的檔案。
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Runtime Metadata Export Tool
- Winmdexp.exe
ms.assetid: d2ce0683-343d-403e-bb8d-209186f7a19d
ms.openlocfilehash: 10626e00eb340d84653419da18a0b219ef1d197e
ms.sourcegitcommit: b4f8849c47c1a7145eb26ce68bc9f9976e0dbec3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2020
ms.locfileid: "87517018"
---
# <a name="winmdexpexe-windows-runtime-metadata-export-tool"></a>Winmdexp.exe (Windows 執行階段中繼資料匯出工具)
Windows 執行階段中繼資料匯出工具 (Winmdexp.exe) 會將 .NET Framework 模組轉換為包含 Windows 執行階段中繼資料的檔案。 雖然 .NET Framework 組件和 Windows 執行階段中繼資料檔案使用相同的實體格式，但是中繼資料資料表的內容有些差異，也就是說，.NET Framework 組件不會自動作為 Windows 執行階段元件使用。 將 .NET Framework 模組轉換為 Windows 執行階段元件的程序稱為「匯出」**。 在 .NET Framework 4.5 和 .NET Framework 4.5.1 中，產生的 Windows 中繼資料 (.winmd) 檔案同時包含中繼資料和實作。  
  
 當您使用 [Windows 執行階段元件]**** 範本時 (在 Visual Studio 2013 或 Visual Studio 2012 中位於 C# 和 Visual Basic 的 [Windows 市集]**** 底下)，編譯器目標是 .winmdobj 檔案，而後續建置步驟會呼叫 Winmdexp.exe 將 .winmdobj 檔案匯出到 .winmd 檔案。 這是建置 Windows 執行階段元件的建議方式。 如果您想要更充分掌控建置流程，超越 Visual Studio 所提供的範圍，請直接使用 Winmdexp.exe。  
  
 此工具會自動與 Visual Studio 一起安裝。 若要執行這項工具，請使用 [Visual Studio 開發人員命令提示字元] (或 Windows 7 中的 [Visual Studio 命令提示字元])。 如需詳細資訊，請參閱[命令提示字元](developer-command-prompt-for-vs.md)。  
  
 在命令提示字元中，請輸入下列項目：  
  
## <a name="syntax"></a>語法  
  
```console  
winmdexp [options] winmdmodule  
```  
  
## <a name="parameters"></a>參數  
  
|引數或選項|說明|  
|------------------------|-----------------|  
|`winmdmodule`|指定要匯出的模組 (.winmdobj)。 只允許一個模組。 若要建立這個模組，請使用 `/target` 編譯器選項搭配 `winmdobj` 目標。 請參閱[-target： winmdobj （c # 編譯器選項）](../../csharp/language-reference/compiler-options/target-winmdobj-compiler-option.md)或[-target （Visual Basic）](../../visual-basic/reference/command-line-compiler/target.md)。|  
|`/docfile:` `docfile`<br /><br /> `/d:` `docfile`|指定 Winmdexp.exe 將產生的輸出 XML 文件檔。 在 .NET Framework 4.5 中，輸出檔案基本上與輸入 XML 文件檔相同。|  
|`/moduledoc:` `docfile`<br /><br /> `/md:` `docfile`|指定編譯器使用 `winmdmodule` 所產生的 XML 文件檔名稱。|  
|`/modulepdb:` `symbolfile`<br /><br /> `/mp:` `symbolfile`|指定式資料庫 (PDB) 檔名稱，該檔案包含 `winmdmodule` 的符號。|  
|`/nowarn:` `warning`|隱藏指定的警告編號。 對於 *warning*，僅提供錯誤碼的數字部分，不包含前置零。|  
|`/out:` `file`<br /><br /> `/o:` `file`|指定輸出 Windows 中繼資料 (.winmd) 檔的名稱。|  
|`/pdb:` `symbolfile`<br /><br /> `/p:` `symbolfile`|指定將包含所匯出 Windows 中繼資料 (.winmd) 檔之符號的輸出程式資料庫 (PDB) 檔 (PDB) 名稱。|  
|`/reference:` `winmd`<br /><br /> `/r:` `winmd`|指定匯出期間參考的中繼資料檔 (.winmd 或組件)。 如果您使用位於 "\Program Files (x86)\Reference Assemblies\Microsoft\Framework\\.NETCore\v4.5" 的參考組件 (在 32 位元電腦上位於 "\Program Files\\...")，請同時包含 System.Runtime.dll 和 mscorlib.dll 的參考。|  
|`/utf8output`|指定應該採用 UTF-8 編碼的輸出訊息。|  
|`/warnaserror+`|指定應該將所有警告視為錯誤。|  
|**@** `responsefile`|指定包含選項的回應檔 (.rsp) (以及選擇性的 `winmdmodule`)。 `responsefile` 中的每一行都應該包含單一引數或選項。|  
  
## <a name="remarks"></a>備註  
 Winmdexp.exe 的設計並不是將任意 .NET Framework 組件轉換成 .winmd 檔案。 它需要的是使用 `/target:winmdobj` 選項編譯的模組，並且適用其他限制。 這些限制中最重要的是，組件的 API 介面中公開的所有型別都必須是 Windows 執行階段型別。 如需詳細資訊，請參閱在[c # 中建立 Windows 執行階段元件和 Visual Basic](https://docs.microsoft.com/previous-versions/br230301(v=vs.110))一文中的「在 Windows 執行階段元件中宣告類型」一節。
  
 當您使用 c # 或 Visual Basic 撰寫 Windows 8.x 存放應用程式或 Windows 執行階段元件時，.NET Framework 會提供支援，讓 Windows 執行階段更自然地進行程式設計。 這會在[適用於 Windows 市集應用程式和 Windows 執行階段的 .NET Framework 支援](../../standard/cross-platform/support-for-windows-store-apps-and-windows-runtime.md)文章中討論。 在過程中，有些常用的 Windows 執行階段型別會對應至 .NET Framework 型別。 Winmdexp.exe 會將這個過程反轉，並產生 API 介面來使用對應的 Windows 執行階段型別。 例如，從介面所建立的類型會 <xref:System.Collections.Generic.IList%601> 對應至從 Windows 執行階段介面所結構化的類型 <xref:Windows.Foundation.Collections.IVector%601> 。  
  
## <a name="see-also"></a>另請參閱

- [適用於 Windows 市集應用程式和 Windows 執行階段的 .NET Framework 支援](../../standard/cross-platform/support-for-windows-store-apps-and-windows-runtime.md)
- [在 C++ 和 Visual Basic 中建立 Windows 執行階段元件](https://docs.microsoft.com/previous-versions/br230301(v=vs.110))
- [Winmdexp.exe 錯誤訊息](winmdexp-exe-error-messages.md)
- [建置、部署及組態工具 (.NET Framework)](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/dd233108(v=vs.100))
