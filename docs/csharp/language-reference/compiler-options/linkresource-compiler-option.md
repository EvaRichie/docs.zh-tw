---
description: -linkresource (C# 編譯器選項)
title: -linkresource (C# 編譯器選項)
ms.date: 07/20/2015
f1_keywords:
- /linkresource
helpviewer_keywords:
- /linkresource compiler option [C#]
- linkres compiler option [C#]
- /linkres compiler option [C#]
- -linkres compiler option [C#]
- -linkresource compiler option [C#]
- linkresource compiler option [C#]
ms.assetid: 440c26c2-77c1-4811-a0a3-57cce3f5fc96
ms.openlocfilehash: 4efa0cbf286b40ad971bad66a7acce15e553eb39
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "91194098"
---
# <a name="-linkresource-c-compiler-options"></a>-linkresource (C# 編譯器選項)

在輸出檔中建立 .NET 資源的連結。 資源檔不會新增至輸出檔。 這點與 [-resource](./resource-compiler-option.md) 選項不同；後者會將資源檔內嵌在輸出檔案中。  
  
## <a name="syntax"></a>語法  
  
```console  
-linkresource:filename[,identifier[,accessibility-modifier]]  
```  
  
## <a name="arguments"></a>引數  

 `filename`  
 您要從元件連結的 .NET 資源檔。  
  
 `identifier` (選擇性)  
 資源的邏輯名稱；用來載入資源的名稱。 預設值是檔案的名稱。  
  
 `accessibility-modifier` (選擇性)  
 資源的存取範圍：公用或私用。 預設值是 public。  
  
## <a name="remarks"></a>備註  

 根據預設，使用 C# 編譯器建立連結資源時，這些資源在組件中為公用狀態。 若要將資源設為私用，可將 `private` 指定為存取範圍修飾詞。 您只能使用 `public` 或 `private` 修飾詞。  
  
 **-linkresource** 必須使用其中一個 [-target](./target-compiler-option.md) 選項 (**-target:module** 除外)。  
  
 如果 `filename` 是建立的 .net 資源檔（例如 [Resgen.exe](../../../framework/tools/resgen-exe-resource-file-generator.md) 或在開發環境中），則可以使用命名空間中的成員進行存取 <xref:System.Resources> 。 如需詳細資訊，請參閱<xref:System.Resources.ResourceManager?displayProperty=nameWithType>。 對於其他所有資源，請使用 <xref:System.Reflection.Assembly> 類別中的 `GetManifestResource` 方法，以在執行階段存取資源。  
  
 `filename` 中指定的檔案可以為任何格式。 例如，您可能需要產生組件的原生 DLL 部分，以便安裝到全域組件快取中，並從組件的 Managed 程式碼存取。 下方第二個範例顯示如何執行此操作。 您可以在組件連結器中執行相同的動作。 下方第三個範例顯示如何執行此操作。 如需詳細資訊，請參閱 [Al.exe (組件連結器)](../../../framework/tools/al-exe-assembly-linker.md) 和[使用組件和全域組件快取](../../../framework/app-domains/working-with-assemblies-and-the-gac.md)。  
  
 **-linkres** 是 **-linkresource** 的簡短形式。  
  
 Visual Studio 不提供這個編譯器選項，您亦無法以程式設計方式變更。  
  
## <a name="example"></a>範例  

 編譯 `in.cs` 並連結至 `rf.resource` 資源檔：  
  
```console  
csc -linkresource:rf.resource in.cs  
```  
  
## <a name="example"></a>範例  

 將 `A.cs` 編譯為 DLL，再連結至原生 DLL N.dll，並將輸出放入全域組件快取 (GAC) 中。 此範例的 A.dll 和 N.dll 都會位於 GAC 中。  
  
```console  
csc -linkresource:N.dll -t:library A.cs  
gacutil -i A.dll  
```  
  
## <a name="example"></a>範例  

 此範例會執行與上一個範例相同的動作，但改為使用組件連結器選項。  
  
```console  
csc -t:module A.cs  
al -out:A.dll A.netmodule -link:N.dll
gacutil -i A.dll  
```  
  
## <a name="see-also"></a>另請參閱

- [C# 編譯器選項](./index.md)
- [Al.exe (元件連結器) ](../../../framework/tools/al-exe-assembly-linker.md)
- [使用組件和全域組件快取](../../../framework/app-domains/working-with-assemblies-and-the-gac.md)
- [管理專案和方案屬性](/visualstudio/ide/managing-project-and-solution-properties)
