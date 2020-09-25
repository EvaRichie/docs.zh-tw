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
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91193994"
---
# <a name="-nowin32manifest-c-compiler-options"></a><span data-ttu-id="29e07-103">-nowin32manifest (C# 編譯器選項)</span><span class="sxs-lookup"><span data-stu-id="29e07-103">-nowin32manifest (C# Compiler Options)</span></span>

<span data-ttu-id="29e07-104">使用 **-nowin32manifest** 選項指示編譯器不要將任何應用程式資訊清單內嵌在可執行檔中。</span><span class="sxs-lookup"><span data-stu-id="29e07-104">Use the **-nowin32manifest** option to instruct the compiler not to embed any application manifest into the executable file.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="29e07-105">語法</span><span class="sxs-lookup"><span data-stu-id="29e07-105">Syntax</span></span>  
  
```console  
-nowin32manifest  
```  
  
## <a name="remarks"></a><span data-ttu-id="29e07-106">備註</span><span class="sxs-lookup"><span data-stu-id="29e07-106">Remarks</span></span>  

 <span data-ttu-id="29e07-107">使用此選項時，應用程式在 Windows Vista 上會虛擬化，除非您在 Win32 資源檔案中或於更新版本組建步驟期間提供應用程式資訊清單。</span><span class="sxs-lookup"><span data-stu-id="29e07-107">When this option is used, the application will be subject to virtualization on Windows Vista unless you provide an application manifest in a Win32 Resource file or during a later build step.</span></span>  
  
 <span data-ttu-id="29e07-108">在 Visual Studio 中，選取 [資訊清單]\*\*\*\* 下拉式清單的 [建立無資訊清單應用程式]\*\*\*\* 選項，在 [Application Property] (應用程式屬性)\*\*\*\* 頁面中設定這個選項。</span><span class="sxs-lookup"><span data-stu-id="29e07-108">In Visual Studio, set this option in the **Application Property** page by selecting the **Create Application Without a Manifest** option in the **Manifest** drop down list.</span></span> <span data-ttu-id="29e07-109">如需詳細資訊，請參閱 [應用程式頁面、專案設計工具 (c # ) ](/visualstudio/ide/reference/application-page-project-designer-csharp)。</span><span class="sxs-lookup"><span data-stu-id="29e07-109">For more information, see [Application Page, Project Designer (C#)](/visualstudio/ide/reference/application-page-project-designer-csharp).</span></span>  
  
 <span data-ttu-id="29e07-110">如需建立資訊清單的詳細資訊，請參閱 [-win32manifest (C# 編譯器選項)](./win32manifest-compiler-option.md)。</span><span class="sxs-lookup"><span data-stu-id="29e07-110">For more information about manifest creation, see [-win32manifest (C# Compiler Options)](./win32manifest-compiler-option.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="29e07-111">另請參閱</span><span class="sxs-lookup"><span data-stu-id="29e07-111">See also</span></span>

- [<span data-ttu-id="29e07-112">C# 編譯器選項</span><span class="sxs-lookup"><span data-stu-id="29e07-112">C# Compiler Options</span></span>](./index.md)
- [<span data-ttu-id="29e07-113">管理專案和方案屬性</span><span class="sxs-lookup"><span data-stu-id="29e07-113">Managing Project and Solution Properties</span></span>](/visualstudio/ide/managing-project-and-solution-properties)
