---
description: -target:winmdobj (C# 編譯器選項)
title: -target:winmdobj (C# 編譯器選項)
ms.date: 07/20/2015
ms.assetid: 1819a045-659d-498a-9457-c466e902986f
ms.openlocfilehash: 66a4bddb34832705ad4779829e561afd9442be8f
ms.sourcegitcommit: d579fb5e4b46745fd0f1f8874c94c6469ce58604
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2020
ms.locfileid: "89139082"
---
# <a name="-targetwinmdobj-c-compiler-options"></a>-target:winmdobj (C# 編譯器選項)
如果您使用 **-target:winmdobj** 編譯器選項，編譯器會建立一個可轉換成 Windows 執行階段二進位檔案 (.winmd) 的中繼 .winmdobj 檔案。 除了 Managed 語言程式之外，JavaScript 和 C++ 程式也可以使用 .winmd 檔案。  
  
## <a name="syntax"></a>語法  
  
```console  
-target:winmdobj  
```  
  
## <a name="remarks"></a>備註  
 **winmdobj** 設定對編譯器發出訊號，表示需要中繼模組。 Visual Studio 將 C# 類別庫編譯為 .winmdobj 檔案，做為回應。 然後 .winmdobj 檔案可以透過 <xref:Microsoft.Build.Tasks.WinMDExp> 匯出工具產生 Windows 中繼資料 (.winmd) 檔案。 .winmd 檔案包含原始類別庫的程式碼，以及 JavaScript 或 C++ 和 Windows 執行階段所使用的 WinMD 中繼資料。  
  
 使用 **-target:winmdobj** 編譯器選項所編譯之檔案的輸出，其設計目的只作為 WimMDExp 匯出工具的輸入，並不能直接參考 .winmdobj 檔案本身。  
  
 除非您使用 [-out](./out-compiler-option.md) 選項指定輸出檔案名稱，否則輸出檔案名稱會採用第一個輸入檔案的名稱。 不需要 [Main](../../programming-guide/main-and-command-args/index.md) 方法。  
  
 如果您在命令提示字元指定 -target:winmdobj 選項，下一個 **-out** 或 [-target:module](./target-module-compiler-option.md) 選項之前的所有檔案都是用來建立 Windows 程式。  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-ide-for-a-windows-store-app"></a>若要在 Visual Studio IDE 中為 Windows 市集應用程式設定這個編譯器選項  
  
1. 在方案總管**** 中，開啟專案的捷徑功能表，然後選擇 [屬性]****。  
  
2. 選擇 [應用程式]**** 索引標籤。  
  
3. 在 [輸出類型]**** 清單中，選擇 [WinMD 檔案]****。  
  
     **WinMD**檔案選項僅適用于 Windows 8. x Store 應用程式範本。  
  
 如需如何以程式設計方式設定這個編譯器選項的詳細資訊，請參閱 <xref:VSLangProj80.ProjectProperties3.OutputType%2A>。  
  
## <a name="example"></a>範例  
 下列命令會將 `filename.cs` 編譯到中繼 .winmdobj 檔案。  
  
```console  
csc -target:winmdobj filename.cs  
```  
  
## <a name="see-also"></a>另請參閱

- [-目標 (c # 編譯器選項) ](./target-compiler-option.md)
- [C # 編譯器選項](./index.md)
