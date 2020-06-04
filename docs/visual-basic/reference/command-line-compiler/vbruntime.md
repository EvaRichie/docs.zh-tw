---
title: -vbruntime
ms.date: 03/13/2018
f1_keywords:
- vbruntime
- -vbruntime
helpviewer_keywords:
- vbruntime compiler option [Visual Basic]
- -vbruntime compiler option [Visual Basic]
- /vbruntime compiler option [Visual Basic]
ms.assetid: 1aa0239e-511a-4c29-957d-fd72877b350a
ms.openlocfilehash: 31b719fb7e43cdd6ac44424b359999410dd608a5
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84403040"
---
# <a name="-vbruntime"></a>-vbruntime
指定編譯器在編譯時不應使用 Visual Basic 執行階段程式庫的參考，或應使用特定執行階段程式庫的參考。  
  
## <a name="syntax"></a>語法  
  
```console  
-vbruntime:{ - | + | * | path }  
```  
  
## <a name="arguments"></a>引數  
 \-  
 不使用 Visual Basic 執行時間程式庫的參考編譯。  
  
 \+  
 使用預設 Visual Basic 執行時間程式庫的參考進行編譯。  
  
 \*  
 不使用 Visual Basic 執行時間程式庫的參考進行編譯，並將 Visual Basic 執行時間程式庫中的核心功能內嵌至元件。  
  
 `path`  
 使用指定之程式庫（DLL）的參考進行編譯。  
  
## <a name="remarks"></a>備註  
 `-vbruntime`編譯器選項可讓您指定編譯器應該編譯，而不需要 Visual Basic 執行時間程式庫的參考。 如果您編譯時沒有 Visual Basic 執行時間程式庫的參考，則會將錯誤或警告記錄在產生呼叫 Visual Basic 執行時間 helper 的程式碼或語言結構上。 （ *Visual Basic 運行*時間協助程式是在執行時間呼叫的函式，可執行特定語言的語義）。  
  
 `-vbruntime+`如果未指定任何參數，選項會產生相同的行為 `-vbruntime` 。 您可以使用 `-vbruntime+` 選項來覆寫先前 `-vbruntime` 的參數。  
  
 `My`當您使用或選項時，大部分類型的物件都無法使用 `-vbruntime-` `-vbruntime:path` 。  
  
## <a name="embedding-visual-basic-runtime-core-functionality"></a>內嵌 Visual Basic 執行時間核心功能  
 `-vbruntime*`選項可讓您在沒有執行時間程式庫參考的情況下進行編譯。 相反地，Visual Basic 執行時間程式庫中的核心功能會內嵌在使用者元件中。 如果您的應用程式是在不包含 Visual Basic 執行時間的平臺上執行，您可以使用此選項。  
  
 下列是內嵌的執行時間成員：  
  
- <xref:Microsoft.VisualBasic.CompilerServices.Conversions> 類別  
  
- <xref:Microsoft.VisualBasic.Strings.AscW%28System.Char%29> 方法  
  
- <xref:Microsoft.VisualBasic.Strings.AscW%28System.String%29> 方法  
  
- <xref:Microsoft.VisualBasic.Strings.ChrW%28System.Int32%29> 方法  
  
- <xref:Microsoft.VisualBasic.Constants.vbBack>常數  
  
- <xref:Microsoft.VisualBasic.Constants.vbCr>常數  
  
- <xref:Microsoft.VisualBasic.Constants.vbCrLf>常數  
  
- <xref:Microsoft.VisualBasic.Constants.vbFormFeed>常數  
  
- <xref:Microsoft.VisualBasic.Constants.vbLf>常數  
  
- <xref:Microsoft.VisualBasic.Constants.vbNewLine>常數  
  
- <xref:Microsoft.VisualBasic.Constants.vbNullChar>常數  
  
- <xref:Microsoft.VisualBasic.Constants.vbNullString>常數  
  
- <xref:Microsoft.VisualBasic.Constants.vbTab>常數  
  
- <xref:Microsoft.VisualBasic.Constants.vbVerticalTab>常數  
  
- 類型的某些物件 `My`  
  
 如果您使用選項進行編譯， `-vbruntime*` 而您的程式碼參考的成員來自不是以核心功能內嵌的 Visual Basic 執行時間程式庫，則編譯器會傳回錯誤，指出該成員無法使用。  
  
## <a name="referencing-a-specified-library"></a>參考指定的程式庫  
 您可以使用 `path` 引數，以自訂執行時間程式庫的參考進行編譯，而不是預設的 Visual Basic 執行時間程式庫。  
  
 如果引數的值 `path` 是 DLL 的完整路徑，編譯器將會使用該檔案做為執行時間程式庫。 如果引數的值 `path` 不是 DLL 的完整路徑，Visual Basic 編譯器會先在目前的資料夾中搜尋已識別的 DLL。 然後，它會在您使用[-sdkpath](sdkpath.md)編譯器選項所指定的路徑中進行搜尋。 如果 `-sdkpath` 未使用編譯器選項，編譯器會在 .NET Framework 資料夾（）中搜尋已識別的 DLL `%systemroot%\Microsoft.NET\Framework\versionNumber` 。  
  
## <a name="example"></a>範例  
 下列範例顯示如何使用 `-vbruntime` 選項，以自訂程式庫的參考進行編譯。  
  
```console
vbc -vbruntime:C:\VBLibraries\CustomVBLibrary.dll  
```  
  
## <a name="see-also"></a>另請參閱

- [Visual Basic 核心– Visual Studio 2010 SP1 中的新編譯模式](https://devblogs.microsoft.com/vbteam/vb-core-new-compilation-mode-in-visual-studio-2010-sp1/)
- [Visual Basic 命令列編譯器](index.md)
- [編譯命令列的範例](sample-compilation-command-lines.md)
- [-sdkpath](sdkpath.md)
