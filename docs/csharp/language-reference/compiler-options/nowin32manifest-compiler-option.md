---
description: -nowin32manifest (C# 編譯器選項)
title: -nowin32manifest (C# 編譯器選項)
ms.date: 07/20/2015
f1_keywords:
- /nowin32manifest
helpviewer_keywords:
- nowin32manifest compiler option [C#]
- -nowin32manifest compiler option [C#]
- /nowin32manifest compiler option [C#]
ms.assetid: 6f06365b-b87b-46a2-b187-b3bfeaf4862d
ms.openlocfilehash: 13bbee66901149d54632d9b164431f8898cdf52e
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "91193994"
---
# <a name="-nowin32manifest-c-compiler-options"></a>-nowin32manifest (C# 編譯器選項)

使用 **-nowin32manifest** 選項指示編譯器不要將任何應用程式資訊清單內嵌在可執行檔中。  
  
## <a name="syntax"></a>語法  
  
```console  
-nowin32manifest  
```  
  
## <a name="remarks"></a>備註  

 使用此選項時，應用程式在 Windows Vista 上會虛擬化，除非您在 Win32 資源檔案中或於更新版本組建步驟期間提供應用程式資訊清單。  
  
 在 Visual Studio 中，選取 [資訊清單] 下拉式清單的 [建立無資訊清單應用程式] 選項，在 [Application Property] (應用程式屬性) 頁面中設定這個選項。 如需詳細資訊，請參閱 [應用程式頁面、專案設計工具 (c # ) ](/visualstudio/ide/reference/application-page-project-designer-csharp)。  
  
 如需建立資訊清單的詳細資訊，請參閱 [-win32manifest (C# 編譯器選項)](./win32manifest-compiler-option.md)。  
  
## <a name="see-also"></a>另請參閱

- [C# 編譯器選項](./index.md)
- [管理專案和方案屬性](/visualstudio/ide/managing-project-and-solution-properties)
