---
title: 發出動態方法和組件
description: 使用 System.object 發出動態方法和元件，此命名空間可讓編譯器或工具在執行時間發出中繼資料和 MSIL 程式碼。
ms.date: 08/30/2017
helpviewer_keywords:
- reflection emit
- dynamic assemblies
- metadata, emit interfaces
- reflection emit, overview
- assemblies [.NET Framework], emitting dynamic assemblies
ms.openlocfilehash: 76d2a83943d9df06cc66cf86c6869f18fac2a12c
ms.sourcegitcommit: cf5a800a33de64d0aad6d115ffcc935f32375164
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/20/2020
ms.locfileid: "86475043"
---
# <a name="emitting-dynamic-methods-and-assemblies"></a><span data-ttu-id="d75c0-103">發出動態方法和組件</span><span class="sxs-lookup"><span data-stu-id="d75c0-103">Emitting Dynamic Methods and Assemblies</span></span>

<span data-ttu-id="d75c0-104">本節說明 <xref:System.Reflection.Emit> 命名空間中的一組 Managed 類型，它可讓編譯器或工具在執行階段發出中繼資料和 Microsoft 中繼語言 (MSIL)，以及選擇性地在磁碟上產生可攜式執行檔 (PE)。</span><span class="sxs-lookup"><span data-stu-id="d75c0-104">This section describes a set of managed types in the <xref:System.Reflection.Emit> namespace that allow a compiler or tool to emit metadata and Microsoft intermediate language (MSIL) at run time and optionally generate a portable executable (PE) file on disk.</span></span> <span data-ttu-id="d75c0-105">指令碼引擎和編譯器是此命名空間的主要使用者。</span><span class="sxs-lookup"><span data-stu-id="d75c0-105">Script engines and compilers are the primary users of this namespace.</span></span> <span data-ttu-id="d75c0-106">在本節中，<xref:System.Reflection.Emit> 命名空間所提供的功能稱為反映發出。</span><span class="sxs-lookup"><span data-stu-id="d75c0-106">In this section, the functionality provided by the <xref:System.Reflection.Emit> namespace is referred to as reflection emit.</span></span>  
  
<span data-ttu-id="d75c0-107">反映發出提供下列功能：</span><span class="sxs-lookup"><span data-stu-id="d75c0-107">Reflection emit provides the following capabilities:</span></span>  
  
- <span data-ttu-id="d75c0-108">使用 <xref:System.Reflection.Emit.DynamicMethod> 類別，在執行階段定義輕量型全域方法，並使用委派加以執行。</span><span class="sxs-lookup"><span data-stu-id="d75c0-108">Define lightweight global methods at run time, using the <xref:System.Reflection.Emit.DynamicMethod> class, and execute them using delegates.</span></span>  
  
- <span data-ttu-id="d75c0-109">在執行階段定義組件，然後加以執行，並/或儲存至磁碟。</span><span class="sxs-lookup"><span data-stu-id="d75c0-109">Define assemblies at run time and then run them and/or save them to disk.</span></span>  
  
- <span data-ttu-id="d75c0-110">在執行階段定義組件、加以執行，然後將其卸載，並允許記憶體回收，以回收其資源。</span><span class="sxs-lookup"><span data-stu-id="d75c0-110">Define assemblies at run time, run them, and then unload them and allow garbage collection to reclaim their resources.</span></span>  
  
- <span data-ttu-id="d75c0-111">在執行階段定義新組件中的模組，然後加以執行，並/或儲存至磁碟。</span><span class="sxs-lookup"><span data-stu-id="d75c0-111">Define modules in new assemblies at run time and then run and/or save them to disk.</span></span>  
  
- <span data-ttu-id="d75c0-112">在執行階段定義模組中的類型、建立這些類型的執行個體，並叫用其方法。</span><span class="sxs-lookup"><span data-stu-id="d75c0-112">Define types in modules at run time, create instances of these types, and invoke their methods.</span></span>  
  
- <span data-ttu-id="d75c0-113">針對已定義的模組，定義可供工具 (例如偵錯工具和程式碼分析工具) 使用的符號資訊。</span><span class="sxs-lookup"><span data-stu-id="d75c0-113">Define symbolic information for defined modules that can be used by tools such as debuggers and code profilers.</span></span>  
  
<span data-ttu-id="d75c0-114">除了 <xref:System.Reflection.Emit> 命名空間中的 Managed 類型，還有[中繼資料介面](../unmanaged-api/metadata/metadata-interfaces.md)參考文件中說明的 Unmanaged 中繼資料介面。</span><span class="sxs-lookup"><span data-stu-id="d75c0-114">In addition to the managed types in the <xref:System.Reflection.Emit> namespace, there are unmanaged metadata interfaces which are described in the [Metadata Interfaces](../unmanaged-api/metadata/metadata-interfaces.md) reference documentation.</span></span> <span data-ttu-id="d75c0-115">相較於 Unmanaged 中繼資料介面，Managed 反映發出提供較強的語意錯誤檢查，以及抽象層級較高的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="d75c0-115">Managed reflection emit provides stronger semantic error checking and a higher level of abstraction of the metadata than the unmanaged metadata interfaces.</span></span>  
  
<span data-ttu-id="d75c0-116">另一項適用於中繼資料和 MSIL 的有用資源，是通用語言基礎結構 (CLI) 文件，尤其是＜第二部分：中繼資料定義和語意＞以及＜第三部分：CIL 指令集＞。</span><span class="sxs-lookup"><span data-stu-id="d75c0-116">Another useful resource for working with metadata and MSIL is the Common Language Infrastructure (CLI) documentation, especially "Partition II: Metadata Definition and Semantics" and "Partition III: CIL Instruction Set".</span></span> <span data-ttu-id="d75c0-117">您可以從[Ecma 網站](https://www.ecma-international.org/publications/standards/Ecma-335.htm)線上取得檔。</span><span class="sxs-lookup"><span data-stu-id="d75c0-117">The documentation is available online at the [Ecma Web site](https://www.ecma-international.org/publications/standards/Ecma-335.htm).</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="d75c0-118">本節內容</span><span class="sxs-lookup"><span data-stu-id="d75c0-118">In This Section</span></span>
  
[<span data-ttu-id="d75c0-119">反映發出中的安全性問題</span><span class="sxs-lookup"><span data-stu-id="d75c0-119">Security issues in reflection emit</span></span>](security-issues-in-reflection-emit.md)  
<span data-ttu-id="d75c0-120">說明有關使用反映發出來建立動態組件的安全性問題。</span><span class="sxs-lookup"><span data-stu-id="d75c0-120">Describes security issues related to creating dynamic assemblies using reflection emit.</span></span>  

<span data-ttu-id="d75c0-121">[如何：定義和執行動態方法](how-to-define-and-execute-dynamic-methods.md)顯示如何執行簡單的動態方法，以及系結至類別實例的動態方法。</span><span class="sxs-lookup"><span data-stu-id="d75c0-121">[How to: Define and execute dynamic methods](how-to-define-and-execute-dynamic-methods.md) Shows how to execute a simple dynamic method and a dynamic method bound to an instance of a class.</span></span>

<span data-ttu-id="d75c0-122">[如何：使用反映發出定義泛型型別](how-to-define-a-generic-type-with-reflection-emit.md)示範如何建立具有兩個型別參數的簡單泛型型別、如何將類別、介面和特殊條件約束套用至型別參數，以及如何建立成員，以使用類別的型別參數做為參數類型和傳回型別。</span><span class="sxs-lookup"><span data-stu-id="d75c0-122">[How to: Define a generic type with reflection emit](how-to-define-a-generic-type-with-reflection-emit.md) Shows how to create a simple generic type with two type parameters, how to apply class, interface, and special constraints to the type parameters, and how to create members that use the type parameters of the class as parameter types and return types.</span></span>

<span data-ttu-id="d75c0-123">[如何：使用反映發出定義泛型方法](how-to-define-a-generic-method-with-reflection-emit.md)說明如何建立、發出和叫用簡單的泛型方法。</span><span class="sxs-lookup"><span data-stu-id="d75c0-123">[How to: Define a generic method with reflection emit](how-to-define-a-generic-method-with-reflection-emit.md) Shows how to create, emit, and invoke a simple generic method.</span></span>

<span data-ttu-id="d75c0-124">[動態類型產生的可回收元件](collectible-assemblies.md)引進了可回收元件，這是動態元件，不需要卸載其建立所在的應用程式域即可加以卸載。</span><span class="sxs-lookup"><span data-stu-id="d75c0-124">[Collectible assemblies for dynamic type generation](collectible-assemblies.md) Introduces collectible assemblies, which are dynamic assemblies that can be unloaded without unloading the application domain in which they were created.</span></span>
  
## <a name="reference"></a><span data-ttu-id="d75c0-125">參考</span><span class="sxs-lookup"><span data-stu-id="d75c0-125">Reference</span></span>  

<xref:System.Reflection.Emit.OpCodes>  
<span data-ttu-id="d75c0-126">將可用來建置方法主體的 MSIL 指令碼編製目錄。</span><span class="sxs-lookup"><span data-stu-id="d75c0-126">Catalogs the MSIL instruction codes you can use to build method bodies.</span></span>  
  
<xref:System.Reflection.Emit>  
<span data-ttu-id="d75c0-127">包含用來發出動態方法、組件和類型的 Managed 類別。</span><span class="sxs-lookup"><span data-stu-id="d75c0-127">Contains managed classes used to emit dynamic methods, assemblies, and types.</span></span>  
  
<xref:System.Type>  
<span data-ttu-id="d75c0-128">說明 <xref:System.Type> 類別，其代表 Managed 反映和反映發出中的類型，且其為使用這些技術的關鍵。</span><span class="sxs-lookup"><span data-stu-id="d75c0-128">Describes the <xref:System.Type> class, which represents types in managed reflection and reflection emit, and which is key to the use of these technologies.</span></span>  
  
<xref:System.Reflection>  
<span data-ttu-id="d75c0-129">包含用來探索中繼資料和 Managed 程式碼的 Managed 類別。</span><span class="sxs-lookup"><span data-stu-id="d75c0-129">Contains managed classes used to explore metadata and managed code.</span></span>  
  
## <a name="related-sections"></a><span data-ttu-id="d75c0-130">相關章節</span><span class="sxs-lookup"><span data-stu-id="d75c0-130">Related Sections</span></span>  

[<span data-ttu-id="d75c0-131">反射</span><span class="sxs-lookup"><span data-stu-id="d75c0-131">Reflection</span></span>](reflection.md)  
<span data-ttu-id="d75c0-132">說明如何探索中繼資料和 Managed 程式碼。</span><span class="sxs-lookup"><span data-stu-id="d75c0-132">Explains how to explore metadata and managed code.</span></span>  
  
[<span data-ttu-id="d75c0-133">.NET 中的組件</span><span class="sxs-lookup"><span data-stu-id="d75c0-133">Assemblies in .NET</span></span>](../../standard/assembly/index.md)  
<span data-ttu-id="d75c0-134">提供 .NET 實作中組件的概觀。</span><span class="sxs-lookup"><span data-stu-id="d75c0-134">Provides an overview of assemblies in .NET implementations.</span></span>
