---
title: 如何：使用強式名稱簽署元件
description: 本文說明如何使用 [簽署] 索引標籤、元件連結器、元件屬性或編譯器選項，以強式名稱簽署 .NET 元件。
ms.date: 08/20/2019
helpviewer_keywords:
- strong-named assemblies, signing with strong names
- signing assemblies
- assemblies [.NET], signing
- assemblies [.NET], strong-named
ms.assetid: 2c30799a-a826-46b4-a25d-c584027a6c67
dev_langs:
- csharp
- vb
- cpp
ms.openlocfilehash: 5192f7f372b9ef7927930c3599aebc6fca9f1f0f
ms.sourcegitcommit: 279fb6e8d515df51676528a7424a1df2f0917116
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/27/2020
ms.locfileid: "92687657"
---
# <a name="how-to-sign-an-assembly-with-a-strong-name"></a>如何：使用強式名稱簽署元件

> [!NOTE]
> 雖然 .NET Core 支援強式名稱的元件，以及 .NET Core 程式庫中的所有元件都已簽署，但大部分的協力廠商元件都不需要強名稱。 如需詳細資訊，請參閱 GitHub 上的 [強式名稱簽署](https://github.com/dotnet/runtime/blob/master/docs/project/strong-name-signing.md) 。

以下是幾種以強式名稱簽署組件的方式：  
  
- 使用 Visual Studio 中，專案之 [ **屬性** ] 對話方塊中的 [ **簽署** ] 索引標籤。 這是最簡單、最方便以強式名稱簽署組件的方式。  
  
- 藉由使用 [元件連結器 ( # A0)](../../framework/tools/al-exe-assembly-linker.md) 將 .NET Framework 程式碼模組與金鑰檔) 連結 ( *.netmodule* 檔。  
  
- 使用組件屬性將強式名稱資訊插入您的程式碼。 您可以使用 <xref:System.Reflection.AssemblyKeyFileAttribute> 或 <xref:System.Reflection.AssemblyKeyNameAttribute> 屬性，視使用的金鑰檔所在位置而定。  
  
- 使用編譯器選項。  
  
 您必須使用密碼編譯金鑰組將組件簽署為強式名稱。 如需建立金鑰組的詳細資訊，請參閱 [如何：建立公開/私密金鑰](create-public-private-key-pair.md)組。  
  
## <a name="create-and-sign-an-assembly-with-a-strong-name-by-using-visual-studio"></a>使用 Visual Studio 建立元件並以強式名稱簽署元件  
  
1. 在  。  
  
2. 選擇 [ **簽署** ] 索引標籤。  
  
3. 選取 [簽署組件]  方塊。  
  
4. 在 [ **選擇強式名稱金鑰** 檔案] 方塊中，選擇 **[流覽]** ，然後流覽至金鑰檔案。 若要建立新的金鑰檔，請選擇 [ **新增** ]，然後在 [ **建立強式名稱金鑰** ] 對話方塊中輸入其名稱。  
  
> [!NOTE]
> 若要[延遲簽署組件](delay-sign.md)，請選擇公開金鑰檔案。  
  
### <a name="create-and-sign-an-assembly-with-a-strong-name-by-using-the-assembly-linker"></a>使用元件連結器建立元件並以強式名稱簽署元件  
  
在 [Visual Studio 的開發人員命令提示字元](../../framework/tools/developer-command-prompt-for-vs.md)上，輸入下列命令：  

**al** **/out：** \<*assemblyName*> *\<moduleName>* **/keyfile：**\<*keyfileName*>  

其中：  

- *assemblyName* 是強式簽署元件的名稱， ( *.dll* 或 *.Exe* 檔案，) 該元件連結器將發出。  
  
- *moduleName* 是 .NET Framework 程式碼模組的名稱， (包含一或多個類型的 *.netmodule* 檔案) 。 您可以使用 *.netmodule* `/target:module` c # 或 Visual Basic 中的參數來編譯您的程式碼，以建立 .netmodule 檔案。
  
- *keyfileName* 是包含金鑰組的容器或檔案名。 元件連結器會解讀相對於目前的目錄的相對路徑。  

下列範例會使用 *sgKey* 金鑰檔，以強式名稱簽署元件 *MyAssembly.dll* 。  

```console
al /out:MyAssembly.dll MyModule.netmodule /keyfile:sgKey.snk  
```  
  
如需這項工具的詳細資訊，請參閱 [組件連結器](../../framework/tools/al-exe-assembly-linker.md)。  
  
## <a name="sign-an-assembly-with-a-strong-name-by-using-attributes"></a>使用屬性以強式名稱簽署元件  
  
1. 將 <xref:System.Reflection.AssemblyKeyFileAttribute?displayProperty=nameWithType> 或 <xref:System.Reflection.AssemblyKeyNameAttribute> 屬性加入至您的原始程式碼檔，並指定容器或檔案名稱，其中包含以強式名稱簽署組件時所使用的金鑰組。  

2. 以一般方式編譯原始程式碼檔。  

   > [!NOTE]
   > C# 和 Visual Basic 編譯器在原始程式碼中遇到 <xref:System.Reflection.AssemblyKeyFileAttribute> 或 <xref:System.Reflection.AssemblyKeyNameAttribute> 屬性時，會發出編譯器警告 (分別為 CS1699 和 BC41008)。 您可以忽略這些警告。  

下列範例 <xref:System.Reflection.AssemblyKeyFileAttribute> 會使用具有金鑰檔的屬性，名為 *keyfile .snk* ，它位於編譯元件的目錄中。  

```cpp
[assembly:AssemblyKeyFileAttribute("keyfile.snk")];
```

```csharp
[assembly:AssemblyKeyFileAttribute("keyfile.snk")]
```

```vb
<Assembly:AssemblyKeyFileAttribute("keyfile.snk")>
```

您也可以在編譯原始程式檔時延遲簽署組件。 如需詳細資訊，請參閱 [延遲簽署元件](delay-sign.md)。  

## <a name="sign-an-assembly-with-a-strong-name-by-using-the-compiler"></a>使用編譯器以強式名稱簽署元件  

在 C# 和 Visual Basic 中使用 `/keyfile` 或 `/delaysign` 編譯器選項，或是在 C++ 中使用 `/KEYFILE` 或 `/DELAYSIGN` 連結器選項編譯原始程式碼檔。 在選項名稱後面加上冒號和金鑰檔的名稱。 使用命令列編譯器時，您可以將金鑰檔複製到包含您的原始程式碼檔的目錄中。  

如需延遲簽署的詳細資訊，請參閱 [延遲簽署元件](delay-sign.md)。  

下列範例會使用 c # 編譯器，並使用 SgKey *UtilityLibrary.dll* 的金鑰檔，以強式名稱簽署元件UtilityLibrary.dll *。*  

```cmd
csc /t:library UtilityLibrary.cs /keyfile:sgKey.snk  
```  

## <a name="see-also"></a>請參閱

- [建立和使用強式名稱的組件](create-use-strong-named.md)
- [如何：建立公開/私密金鑰組](create-public-private-key-pair.md)
- [Al.exe (元件連結器) ](../../framework/tools/al-exe-assembly-linker.md)
- [延遲簽署組件](delay-sign.md)
- [管理組件和資訊清單簽署](/visualstudio/ide/managing-assembly-and-manifest-signing)
- [專案設計工具、簽署頁](/visualstudio/ide/reference/signing-page-project-designer)
