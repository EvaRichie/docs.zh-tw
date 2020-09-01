---
description: -resource (C# 編譯器選項)
title: -resource (C# 編譯器選項)
ms.date: 07/20/2015
f1_keywords:
- /resource
helpviewer_keywords:
- -resource compiler option [C#]
- /resource compiler option [C#]
- -res compiler option [C#]
- /res compiler option [C#]
- res compiler option [C#]
- resource compiler option [C#]
ms.assetid: 5212666e-98ab-47e4-a497-b5545ab15c7f
ms.openlocfilehash: 963004820f56272b4f1b1d92ccc4d0a60493a4a0
ms.sourcegitcommit: d579fb5e4b46745fd0f1f8874c94c6469ce58604
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2020
ms.locfileid: "89128695"
---
# <a name="-resource-c-compiler-options"></a>-resource (C# 編譯器選項)
將指定的資源內嵌到輸出檔。  
  
## <a name="syntax"></a>語法  
  
```console  
-resource:filename[,identifier[,accessibility-modifier]]  
```  
  
## <a name="arguments"></a>引數  
 `filename`  
 您想要內嵌到輸出檔的 .NET Framework 資源檔。  
  
 `identifier` (選擇性)  
 資源的邏輯名稱；用來載入資源的名稱。 預設值是檔案名稱。  
  
 `accessibility-modifier` (選擇性)  
 資源的存取範圍：公用或私用。 預設值是 public。  
  
## <a name="remarks"></a>備註  
 使用 [-linkresource](./linkresource-compiler-option.md) 將資源連結至組件，而不將資源檔新增至輸出檔案。  
  
 根據預設，使用 C# 編譯器建立資源時，這些資源在組件中為公用狀態。 若要將資源設為私用，可將 `private` 指定為存取範圍修飾詞。 不允許 `public` 或 `private` 以外的其他存取範圍。  
  
 例如，如果 `filename` 是由 [Resgen.exe](../../../framework/tools/resgen-exe-resource-file-generator.md) 或是在開發環境中所建立的 .NET Framework 資源檔，就可以使用 <xref:System.Resources> 命名空間中的成員進行存取。 如需詳細資訊，請參閱<xref:System.Resources.ResourceManager?displayProperty=nameWithType>。 對於其他所有資源，請使用 <xref:System.Reflection.Assembly> 類別中的 `GetManifestResource` 方法，以在執行階段存取資源。  
  
 **-res** 是 **-resource** 的簡短形式。  
  
 輸出檔中資源的順序是從命令列上指定的順序決定。  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>在 Visual Studio 開發環境中設定這個編譯器選項  
  
1. 將資源檔新增至專案。  
  
2. 選取您想要內嵌在方案總管**** 中的檔案。  
  
3. 在 [屬性]**** 視窗中，選取檔案的 [建置動作]****。  
  
4. 將 [建置動作]**** 設定為 [內嵌資源]****。  
  
 如需如何以程式設計方式設定這個編譯器選項的詳細資訊，請參閱 <xref:VSLangProj80.FileProperties2.BuildAction%2A>。  
  
## <a name="example"></a>範例  
 編譯 `in.cs`，並附加 `rf.resource` 資源檔：  
  
```console  
csc -resource:rf.resource in.cs  
```  
  
## <a name="see-also"></a>另請參閱

- [C # 編譯器選項](./index.md)
- [管理專案和方案屬性](/visualstudio/ide/managing-project-and-solution-properties)
