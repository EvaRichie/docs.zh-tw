---
title: 設定組件繫結重新導向
description: 請參閱如何使用應用程式佈建檔的 assemblyBinding 元素中的 appliesTo 屬性，在 .NET 中設定元件系結重新導向。
ms.date: 03/30/2017
helpviewer_keywords:
- side-by-side execution, assembly binding redirection
- assemblies [.NET Framework], binding redirection
ms.assetid: d266cbd8-bf91-41d1-baf0-afbc481a741f
ms.openlocfilehash: 8f3e2270d92e11ea467d6cefc2b19b4faff563b4
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85621726"
---
# <a name="configuring-assembly-binding-redirection"></a><span data-ttu-id="a7070-103">設定組件繫結重新導向</span><span class="sxs-lookup"><span data-stu-id="a7070-103">Configuring Assembly Binding Redirection</span></span>
<span data-ttu-id="a7070-104">根據預設，應用程式會使用執行階段版本 (用來編譯應用程式) 隨附的 .NET Framework 組件集。</span><span class="sxs-lookup"><span data-stu-id="a7070-104">By default, applications use the set of .NET Framework assemblies that shipped with the runtime version used to compile the application.</span></span> <span data-ttu-id="a7070-105">您可以在**appliesTo** [\<assemblyBinding>](../configure-apps/file-schema/runtime/assemblybinding-element-for-runtime.md) 應用程式佈建檔中的元素上使用 appliesTo 屬性，將元件系結參考重新導向至特定版本的 .NET Framework 元件。</span><span class="sxs-lookup"><span data-stu-id="a7070-105">You can use the **appliesTo** attribute on the [\<assemblyBinding>](../configure-apps/file-schema/runtime/assemblybinding-element-for-runtime.md) element in an application configuration file to redirect assembly binding references to a specific version of the .NET Framework assemblies.</span></span> <span data-ttu-id="a7070-106">這個選擇性屬性會使用 .NET Framework 版本號碼，以表示它會套用至哪一個版本。</span><span class="sxs-lookup"><span data-stu-id="a7070-106">This optional attribute uses a .NET Framework version number to indicate which version it applies to.</span></span> <span data-ttu-id="a7070-107">如果未指定**appliesTo**屬性，元素會 **\<assemblyBinding>** 套用至 .NET Framework 的所有版本。</span><span class="sxs-lookup"><span data-stu-id="a7070-107">If no **appliesTo** attribute is specified, the **\<assemblyBinding>** element applies to all versions of the .NET Framework.</span></span>  
  
 <span data-ttu-id="a7070-108">在 .NET Framework 1.1 版中引進了 **appliesTo** 屬性；而 .NET Framework 1.0 版則會忽略它。</span><span class="sxs-lookup"><span data-stu-id="a7070-108">The **appliesTo** attribute was introduced in the .NET Framework version 1.1; it is ignored by the .NET Framework version 1.0.</span></span> <span data-ttu-id="a7070-109">這表示 **\<assemblyBinding>** 使用 .NET Framework 版本1.0 時，即使指定了**appliesTo**屬性，還是會套用所有元素。</span><span class="sxs-lookup"><span data-stu-id="a7070-109">This means that all **\<assemblyBinding>** elements are applied when using the .NET Framework version 1.0, even if an **appliesTo** attribute is specified.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="a7070-110">使用 **appliesTo** 屬性來限制組件繫結重新導向至特定版本的執行階段。</span><span class="sxs-lookup"><span data-stu-id="a7070-110">Use the **appliesTo** attribute to limit assembly binding redirection to a specific version of the runtime.</span></span>  
  
 <span data-ttu-id="a7070-111">例如對於 .NET Framework 1.0 版組件，如果要重新導向組件繫結，您可在應用程式組態檔中包含下列 XML 程式碼。</span><span class="sxs-lookup"><span data-stu-id="a7070-111">For example, to redirect assembly binding for a .NET Framework version 1.0 assembly, you would include the following XML code in your application configuration file.</span></span>  
  
```xml  
<runtime>  
        <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1" appliesTo="v1.0.3705">  
            <dependentAssembly>
               * assembly information goes here *  
            </dependentAssembly>  
       </assemblyBinding>  
</runtime>  
```  
  
 <span data-ttu-id="a7070-112">專案 **\<assemblyBinding>** 會區分順序。</span><span class="sxs-lookup"><span data-stu-id="a7070-112">The **\<assemblyBinding>** elements are order-sensitive.</span></span> <span data-ttu-id="a7070-113">您應先輸入任何 .NET Framework 1.0 版組件的組件繫結重新導向資訊，然後才是任何 .NET Framework 1.1 版組件的組件繫結重新導向資訊。</span><span class="sxs-lookup"><span data-stu-id="a7070-113">You should enter assembly binding redirection information for any .NET Framework version 1.0 assemblies first, followed by assembly binding redirection information for any .NET Framework version 1.1 assemblies.</span></span> <span data-ttu-id="a7070-114">最後，請輸入不使用 **appliesTo** 屬性的任何 .NET Framework 組件重新導向之組件繫結重新導向資訊，如此一來會適用於所有版本的 .NET Framework。</span><span class="sxs-lookup"><span data-stu-id="a7070-114">Finally, enter assembly binding redirection information for any .NET Framework assembly redirection that does not use the **appliesTo** attribute and therefore applies to all versions of the .NET Framework.</span></span> <span data-ttu-id="a7070-115">若重新導向發生衝突，會使用組態檔中第一筆相符的重新導向陳述式。</span><span class="sxs-lookup"><span data-stu-id="a7070-115">In case of a conflict in redirection, the first matching redirection statement in the configuration file is used.</span></span>  
  
 <span data-ttu-id="a7070-116">例如，若要重新導向一個參考至 .NET Framework 1.0 版組件和另一個參考至 .NET Framework 1.1 版組件，則您可使用下列虛擬程式碼所示的模式。</span><span class="sxs-lookup"><span data-stu-id="a7070-116">For example, to redirect one reference to a .NET Framework version 1.0 assembly and another reference to a .NET Framework version 1.1 assembly, you would use the pattern shown in the following pseudocode.</span></span>  
  
```xml  
<assemblyBinding xmlns="..." appliesTo="v1.0.3705">
  <!-- .NET Framework version 1.0 redirects here. -->
</assemblyBinding>
  
<assemblyBinding xmlns="..." appliesTo="v1.1.4322">
  <!-- .NET Framework version 1.1 redirects here. -->
</assemblyBinding>
  
<assemblyBinding xmlns="...">
  <!-- Redirects meant for all versions of the .NET Framework. -->
</assemblyBinding>  
```  
  
## <a name="debugging-configuration-file-errors"></a><span data-ttu-id="a7070-117">偵錯組態檔錯誤</span><span class="sxs-lookup"><span data-stu-id="a7070-117">Debugging Configuration File Errors</span></span>  
 <span data-ttu-id="a7070-118">一旦建立應用程式定義域，並載入程式碼至應用程式定義域中，執行階段就會剖析組態檔。</span><span class="sxs-lookup"><span data-stu-id="a7070-118">The runtime parses configuration files once when an application domain is created, and loads code into that application domain.</span></span> <span data-ttu-id="a7070-119">Common Language Runtime 會忽略此項目，以處理組態檔中的錯誤。</span><span class="sxs-lookup"><span data-stu-id="a7070-119">The common language runtime handles errors in a configuration file by ignoring the entry.</span></span> <span data-ttu-id="a7070-120">如果它包含格式不正確的 XML，則執行階段會略過整個組態檔案。</span><span class="sxs-lookup"><span data-stu-id="a7070-120">The runtime ignores the entire configuration file if it contains malformed XML.</span></span> <span data-ttu-id="a7070-121">對於無效的 XML，則會忽略無效的區段。</span><span class="sxs-lookup"><span data-stu-id="a7070-121">For invalid XML, only the invalid sections are ignored.</span></span>  
  
 <span data-ttu-id="a7070-122">您可判斷組態檔是否用於決定正在進行組件繫結重新導向。</span><span class="sxs-lookup"><span data-stu-id="a7070-122">You can determine whether a configuration file is being used by determining whether assembly binding redirects are occurring.</span></span> <span data-ttu-id="a7070-123">使用[組件繫結記錄檔檢視器 (Fuslogvw.exe)](../tools/fuslogvw-exe-assembly-binding-log-viewer.md) 來查看正在載入哪些組件。</span><span class="sxs-lookup"><span data-stu-id="a7070-123">Use the [Assembly Binding Log Viewer (Fuslogvw.exe)](../tools/fuslogvw-exe-assembly-binding-log-viewer.md) to see which assemblies are being loaded.</span></span> <span data-ttu-id="a7070-124">若要查看所有組件繫結，您必須在登錄中設定 **ForceLog** 項目。</span><span class="sxs-lookup"><span data-stu-id="a7070-124">To see all assembly binds, you must set an entry for **ForceLog** in the registry.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="a7070-125">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a7070-125">See also</span></span>

- [<span data-ttu-id="a7070-126">作法：啟用和停用自動繫結重新導向</span><span class="sxs-lookup"><span data-stu-id="a7070-126">How to: Enable and Disable Automatic Binding Redirection</span></span>](../configure-apps/how-to-enable-and-disable-automatic-binding-redirection.md)
