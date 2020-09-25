---
description: -bugreport (C# 編譯器選項)
title: -bugreport (C# 編譯器選項)
ms.date: 07/20/2015
f1_keywords:
- /bugreport
helpviewer_keywords:
- /bugreport compiler option [C#]
- -bugreport compiler option [C#]
- bugreport compiler option [C#]
ms.assetid: f39665e3-4f6f-4357-88a2-3274c7bec0c1
ms.openlocfilehash: 2afab44eec0c7bcc9809b458be0348093cb6dd07
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91196815"
---
# <a name="-bugreport-c-compiler-options"></a>-bugreport (C# 編譯器選項)

指定偵錯資訊應該置於檔案以供稍後分析。  
  
## <a name="syntax"></a>語法  
  
```console  
-bugreport:file  
```  
  
## <a name="arguments"></a>引數  

 `file`  
 您要包含錯誤報告的檔案名稱。  
  
## <a name="remarks"></a>備註  

 **-bugreport** 選項會指定下列資訊應該置於 `file`：  
  
- 編譯中所有原始程式碼檔的複本。  
  
- 編譯中使用的編譯器選項清單。  
  
- 您的編譯器、執行階段和作業系統的版本資訊。  
  
- 除了隨附於 .NET Framework 和 SDK 的組件之外，還包括參考組件和模組 (儲存為十六進位數字)。  
  
- 編譯器輸出 (如果有的話)。  
  
- 問題的描述，會提示您操作指示。  
  
- 您認為問題該如何解決的描述，會提示您操作指示。  
  
 如果這個選項與 **-errorreport:prompt** 或 **-errorreport:send** 搭配使用，則會將檔案中的資訊傳送給 Microsoft Corporation。  
  
 由於 `file`中放置所有原始程式碼檔的複本，您可能想要以最短的可能程式重現 (可疑的) 程式碼缺失。  
  
 Visual Studio 不提供這個編譯器選項，您亦無法以程式設計方式變更。  
  
 請注意，所產生檔案的內容會公開原始程式碼，而這可能會不慎洩漏資訊。  
  
## <a name="see-also"></a>另請參閱

- [C# 編譯器選項](./index.md)
- [-errorreport (c # 編譯器選項) ](./errorreport-compiler-option.md)
- [管理專案和方案屬性](/visualstudio/ide/managing-project-and-solution-properties)
