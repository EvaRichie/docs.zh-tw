---
description: -target:winexe (C# 編譯器選項)
title: -target:winexe (C# 編譯器選項)
ms.date: 07/20/2015
f1_keywords:
- /target:winexe
helpviewer_keywords:
- /target compiler options [C#], /target:winexe
- -target compiler options [C#], /target:winexe
- target compiler options [C#], /target:winexe
ms.assetid: b5a0619c-8caa-46a5-a743-1cf68408ad7a
ms.openlocfilehash: 6e14a2aac427c7adfd69f66eaf624816b75f6ea2
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91168929"
---
# <a name="-targetwinexe-c-compiler-options"></a>-target:winexe (C# 編譯器選項)

**-target:winexe** 選項可讓編譯器建立可執行檔 (EXE)，其為一個 Windows 程式。  
  
## <a name="syntax"></a>語法  
  
```console  
-target:winexe  
```  
  
## <a name="remarks"></a>備註  

 將會建立副檔名為 .exe 的可執行檔。 Windows 程式是從 .NET 程式庫或 Windows Api 提供使用者介面的程式。  
  
 使用 [-target:exe](./target-exe-compiler-option.md) 建立主控台應用程式。  
  
 除非特別使用 [-out](./out-compiler-option.md) 選項指定輸出檔案名稱，否則輸出檔案名稱會採用包含 [Main](../../programming-guide/main-and-command-args/index.md) 方法的輸入檔案名稱。  
  
 指定於命令列時，下一個 **-out** 或 [-target](./target-compiler-option.md) 選項之前的所有檔案都是用來建立 Windows 程式。  
  
 編譯為 .exe 檔案的原始程式碼檔中只需要一個 **Main** 方法。 如果您的程式碼有多個具有 **Main** 方法的類別，則 [-main](./main-compiler-option.md) 選項可讓您指定哪個類別包含 **Main** 方法。  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>在 Visual Studio 開發環境中設定這個編譯器選項  
  
1. 開啟專案的 [屬性]**** 頁面。  
  
2. 按一下 [應用程式]**** 屬性頁。  
  
3. 修改 [輸出類型]**** 屬性。  
  
 如需如何以程式設計方式設定這個編譯器選項的資訊，請參閱 <xref:VSLangProj80.ProjectProperties3.OutputType%2A>。  
  
## <a name="example"></a>範例  

 將 `in.cs` 編譯為 Windows 程式︰  
  
```console  
csc -target:winexe in.cs  
```  
  
## <a name="see-also"></a>另請參閱

- [-目標 (c # 編譯器選項) ](./target-compiler-option.md)
- [C# 編譯器選項](./index.md)
