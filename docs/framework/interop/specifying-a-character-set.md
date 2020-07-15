---
title: 指定字元集
description: 瞭解如何指定使用窄（ANSI）或寬（Unicode）編碼的字元集。 您也可以指定自動執行時間選取。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- platform invoke, attribute fields
- attribute fields in platform invoke, CharSet
- CharSet field
ms.assetid: a8347eb1-295f-46b9-8a78-63331f9ecc50
ms.openlocfilehash: 789753742d8714e481f038e323407cbab0499f6c
ms.sourcegitcommit: 0fa2b7b658bf137e813a7f4d09589d64c148ebf5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/14/2020
ms.locfileid: "86309790"
---
# <a name="specify-a-character-set"></a>指定字元集

<xref:System.Runtime.InteropServices.DllImportAttribute.CharSet?displayProperty=nameWithType> 欄位控制字串封送處理，並決定平台叫用如何在 DLL 中尋找函式名稱。 這個主題將描述這兩種行為。  
  
 某些 API 匯出兩個版本的函式，接受字串引數：窄 (ANSI) 和寬 (Unicode)。 例如，Win32 API 包括 **MessageBox** 函式的下列進入點名稱：  
  
- **MessageBoxA**  
  
     提供 1 個位元組字元 ANSI 格式化，區別方式是在進入點名稱附加 "A"。 **MessageBoxA** 呼叫一律以 ANSI 格式的字串封送處理。  
  
- **MessageBoxW**  
  
     提供 2 個位元組字元 Unicode 格式化，區別方式是在進入點名稱附加 "W"。 **MessageBoxW** 呼叫一律以 Unicode 格式的字串封送處理。  
  
## <a name="string-marshaling-and-name-matching"></a>字串封送處理及名稱比對  
 `CharSet` 欄位可接受下列值：  
  
 <xref:System.Runtime.InteropServices.CharSet.Ansi> (預設值)  
  
- 字串封送處理  
  
     平台叫用會將字串從其受管理的格式 (Unicode) 封送處理為 ANSI 格式。  
  
- 名稱比對  
  
     當 <xref:System.Runtime.InteropServices.DllImportAttribute.ExactSpelling?displayProperty=nameWithType> 欄位是 `true` 時，如同 Visual Basic 中的預設值，平台叫用僅會搜尋您指定的名稱。 例如，如果您指定 **MessageBox**，平台叫用會搜尋 **MessageBox**，並在找不到正確的拼字時失敗。  
  
     當 `ExactSpelling` 欄位是 `false` 時，如同在 C++ 和 C# 中的預設值，平台叫用會先搜尋未損壞別名 (**MessageBox**)，然後如果找不到未損壞別名則搜尋損壞名稱 (**MessageBoxA**)。 請注意，ANSI 名稱比對行為不同於 Unicode 名稱比對行為。  
  
 <xref:System.Runtime.InteropServices.CharSet.Unicode>  
  
- 字串封送處理  
  
     平台叫用會將字串從其受管理的格式 (Unicode) 複製為 Unicode 格式。  
  
- 名稱比對  
  
     當 `ExactSpelling` 欄位是 `true` 時，如同 Visual Basic 中的預設值，平台叫用僅會搜尋您指定的名稱。 例如，如果您指定 **MessageBox**，則平台叫用會搜尋 **MessageBox**，並在找不到正確的拼字時失敗。  
  
     當 `ExactSpelling` 欄位是 `false` 時，如同在 C++ 和 C# 中的預設值，平台叫用會先搜尋損壞名稱 (**MessageBoxW**)，然後如果找不到損壞名稱則搜尋未損壞別名 (**MessageBox**)。 請注意，Unicode 名稱比對行為不同於 ANSI 名稱比對行為。  
  
 <xref:System.Runtime.InteropServices.CharSet.Auto>  
  
- 平台叫用會在執行階段，根據在目標平台，在 ANSI 和 Unicode 格式之間選擇。  
  
## <a name="specify-a-character-set-in-visual-basic"></a>在 Visual Basic 中指定字元集

您可以藉由在宣告語句中加入 `Ansi` 、或關鍵字，在 Visual Basic 中指定字元集行為 `Unicode` `Auto` 。 如果您省略 character set 關鍵字， <xref:System.Runtime.InteropServices.DllImportAttribute.CharSet?displayProperty=nameWithType> 欄位會預設為 ANSI 字元集。

下列範例會宣告 **MessageBox** 函式三次，每次都有不同的字元集行為。 第一個語句會省略 character set 關鍵字，因此字元集預設為 ANSI。 第二個和第三個語句使用關鍵字明確指定字元集。

```vb
Friend Class NativeMethods
    Friend Declare Function MessageBoxA Lib "user32.dll" (
        ByVal hWnd As IntPtr,
        ByVal lpText As String,
        ByVal lpCaption As String,
        ByVal uType As UInteger) As Integer

    Friend Declare Unicode Function MessageBoxW Lib "user32.dll" (
        ByVal hWnd As IntPtr,
        ByVal lpText As String,
        ByVal lpCaption As String,
        ByVal uType As UInteger) As Integer

    Friend Declare Auto Function MessageBox Lib "user32.dll" (
        ByVal hWnd As IntPtr,
        ByVal lpText As String,
        ByVal lpCaption As String,
        ByVal uType As UInteger) As Integer
End Class
```
  
## <a name="specify-a-character-set-in-c-and-c"></a>在 c # 和 c + + 中指定字元集

<xref:System.Runtime.InteropServices.DllImportAttribute.CharSet?displayProperty=nameWithType> 欄位將基礎字元集識別為 ANSI 或 Unicode。 字元集控制應該如何封送處理方法的字串引數。 您可以使用下列格式之一來表示字元集：  
  
```csharp
[DllImport("DllName", CharSet = CharSet.Ansi)]
[DllImport("DllName", CharSet = CharSet.Unicode)]
[DllImport("DllName", CharSet = CharSet.Auto)]
```
  
```cpp
[DllImport("DllName", CharSet = CharSet::Ansi)]
[DllImport("DllName", CharSet = CharSet::Unicode)]
[DllImport("DllName", CharSet = CharSet::Auto)]
```
  
 下列範例示範 **MessageBox** 函式的三個 Managed 定義，其已屬性化以指定字元集。 在第一個定義中，根據其省略，`CharSet` 欄位預設為 ANSI 字元集。  
  
```csharp  
using System;
using System.Runtime.InteropServices;

internal static class NativeMethods
{
    [DllImport("user32.dll")]
    internal static extern int MessageBoxA(
        IntPtr hWnd, string lpText, string lpCaption, uint uType);

    [DllImport("user32.dll", CharSet = CharSet.Unicode)]
    internal static extern int MessageBoxW(
        IntPtr hWnd, string lpText, string lpCaption, uint uType);

    [DllImport("user32.dll", CharSet = CharSet.Auto)]
    internal static extern int MessageBox(
        IntPtr hWnd, string lpText, string lpCaption, uint uType);
}
```  
  
```cpp
typedef void* HWND;

// Can use MessageBox or MessageBoxA.
[DllImport("user32")]
extern "C" int MessageBox(
    HWND hWnd, String* lpText, String* lpCaption, unsigned int uType);

// Can use MessageBox or MessageBoxW.
[DllImport("user32", CharSet = CharSet::Unicode)]
extern "C" int MessageBoxW(
    HWND hWnd, String* lpText, String* lpCaption, unsigned int uType);

// Must use MessageBox.
[DllImport("user32", CharSet = CharSet::Auto)]
extern "C" int MessageBox(
    HWND hWnd, String* lpText, String* lpCaption, unsigned int uType);
```
  
## <a name="see-also"></a>另請參閱

- <xref:System.Runtime.InteropServices.DllImportAttribute>
- [在 Managed 程式碼中建立原型](creating-prototypes-in-managed-code.md)
- [平台叫用範例](platform-invoke-examples.md)
- [使用平台叫用封送處理資料](marshaling-data-with-platform-invoke.md)
