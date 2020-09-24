---
description: -addmodule (C# 編譯器選項)
title: -addmodule (C# 編譯器選項)
ms.date: 07/20/2015
f1_keywords:
- /addmodule
helpviewer_keywords:
- /addmodule compiler option [C#]
- -addmodule compiler option [C#]
- addmodule compiler option [C#]
ms.assetid: ed604546-0dc2-4bd4-9a3e-610a8d973e58
ms.openlocfilehash: ec72fc76b3d550029b1286f64b8f86e69e721468
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91150566"
---
# <a name="-addmodule-c-compiler-options"></a>-addmodule (C# 編譯器選項)

此選項會將使用 target:module 參數所建立的模組新增至目前的編譯。  
  
## <a name="syntax"></a>語法  
  
```console  
-addmodule:file[;file2]  
```  
  
## <a name="arguments"></a>引數  

 `file`, `file2`  
 包含中繼資料的輸出檔案。 檔案不能包含組件資訊清單。 若要匯入多個檔案，請以逗號或分號分隔檔案名稱。  
  
## <a name="remarks"></a>備註  

 所有加上 **-addmodule** 的模組都必須和執行階段的輸出檔案位於相同的目錄中。 也就是說，您可以在編譯時間指定任一目錄中的模組，但該模組於執行階段必須位在應用程式目錄中。 如果模組於執行階段不在應用程式目錄中，您就會有 <xref:System.TypeLoadException>。  
  
 `file` 不包含組件。 例如，如果輸出檔案是使用 [-target:module](./target-module-compiler-option.md) 所建立，則其中繼資料可以使用 **-addmodule** 匯入。  
  
 如果輸出檔案是使用 **-target** 選項而不是使用 **-target:module** 所建立，則其中繼資料無法使用 **-addmodule** 進行匯入，但可以使用 [-reference](./reference-compiler-option.md) 進行匯入。  
  
 Visual Studio 不提供這個編譯器選項，專案無法參考模組。 此外，這個編譯器選項也不能以程式設計方式變更。  
  
## <a name="example"></a>範例  

 編譯來源檔案 `input.cs` 並從 `metad1.netmodule` 和 `metad2.netmodule` 新增中繼資料，以產生 `out.exe`：  
  
```console  
csc -addmodule:metad1.netmodule;metad2.netmodule -out:out.exe input.cs  
```  
  
## <a name="see-also"></a>另請參閱

- [C# 編譯器選項](./index.md)
- [管理專案和方案屬性](/visualstudio/ide/managing-project-and-solution-properties)
- [多檔案元件](../../../framework/app-domains/multifile-assemblies.md)
- [如何：建立多檔案元件](../../../framework/app-domains/build-multifile-assembly.md)
