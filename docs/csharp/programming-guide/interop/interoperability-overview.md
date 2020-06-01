---
title: 互通性概觀 - C# 程式設計指南
ms.date: 07/20/2015
helpviewer_keywords:
- COM interop
- C# language, interoperability
- C++ Interop
- interoperability, about interoperability
- platform invoke
ms.assetid: c025b2e0-2357-4c27-8461-118f0090aeff
ms.openlocfilehash: 6546a379d6d851aafbced0931221dc19ca022a72
ms.sourcegitcommit: a241301495a84cc8c64fe972330d16edd619868b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/01/2020
ms.locfileid: "84241730"
---
# <a name="interoperability-overview-c-programming-guide"></a><span data-ttu-id="a93a6-102">互通性概觀 (C# 程式設計手冊)</span><span class="sxs-lookup"><span data-stu-id="a93a6-102">Interoperability Overview (C# Programming Guide)</span></span>
<span data-ttu-id="a93a6-103">本主題說明可在 C# Managed 程式碼和 Unmanaged 程式碼之間啟用互通性的方法。</span><span class="sxs-lookup"><span data-stu-id="a93a6-103">The topic describes methods to enable interoperability between C# managed code and unmanaged code.</span></span>  
  
## <a name="platform-invoke"></a><span data-ttu-id="a93a6-104">平台叫用</span><span class="sxs-lookup"><span data-stu-id="a93a6-104">Platform Invoke</span></span>  
 <span data-ttu-id="a93a6-105">*平台叫用*服務，可讓 Managed 程式碼呼叫 Unmanaged 函式在動態連結程式庫 (DLL) 中實作，例如 Microsoft Windows API 中。</span><span class="sxs-lookup"><span data-stu-id="a93a6-105">*Platform invoke* is a service that enables managed code to call unmanaged functions that are implemented in dynamic link libraries (DLLs), such as those in the Microsoft Windows API.</span></span> <span data-ttu-id="a93a6-106">它會找出並叫用匯出的函式，並且在需要的時候於交互操作界限之間封送處理其引數 (整數、 字串、 陣列、 結構和其他) 。</span><span class="sxs-lookup"><span data-stu-id="a93a6-106">It locates and invokes an exported function and marshals its arguments (integers, strings, arrays, structures, and so on) across the interoperation boundary as needed.</span></span>  
  
<span data-ttu-id="a93a6-107">如需詳細資訊，請參閱使用[非受控 DLL](../../../framework/interop/consuming-unmanaged-dll-functions.md)函式和[如何使用平台叫用來播放 WAV](./how-to-use-platform-invoke-to-play-a-wave-file.md)檔案。</span><span class="sxs-lookup"><span data-stu-id="a93a6-107">For more information, see [Consuming Unmanaged DLL Functions](../../../framework/interop/consuming-unmanaged-dll-functions.md) and [How to use platform invoke to play a WAV file](./how-to-use-platform-invoke-to-play-a-wave-file.md).</span></span>
  
> [!NOTE]
> <span data-ttu-id="a93a6-108">[Common Language Runtime](../../../standard/clr.md) (CLR) 管理對系統資源的存取。</span><span class="sxs-lookup"><span data-stu-id="a93a6-108">The [Common Language Runtime](../../../standard/clr.md) (CLR) manages access to system resources.</span></span> <span data-ttu-id="a93a6-109">在 CLR 外部呼叫 Unmanaged 程式碼會略過此安全性機制，因而造成安全性風險。</span><span class="sxs-lookup"><span data-stu-id="a93a6-109">Calling unmanaged code that is outside the CLR bypasses this security mechanism, and therefore presents a security risk.</span></span> <span data-ttu-id="a93a6-110">例如，Unmanaged 程式碼可能會直接呼叫 Unmanaged 程式碼中的資源，並略過 CLR 安全性機制。</span><span class="sxs-lookup"><span data-stu-id="a93a6-110">For example, unmanaged code might call resources in unmanaged code directly, bypassing CLR security mechanisms.</span></span> <span data-ttu-id="a93a6-111">如需詳細資訊，請參閱 [.NET 的安全性](../../../standard/security/index.md)。</span><span class="sxs-lookup"><span data-stu-id="a93a6-111">For more information, see [Security in .NET](../../../standard/security/index.md).</span></span>  
  
## <a name="c-interop"></a><span data-ttu-id="a93a6-112">C++ Interop</span><span class="sxs-lookup"><span data-stu-id="a93a6-112">C++ Interop</span></span>  
 <span data-ttu-id="a93a6-113">您可以使用 c + + interop （也稱為 Works （IJW））包裝原生 c + + 類別，使其可供以 c # 或其他 .NET 語言撰寫的程式碼使用。</span><span class="sxs-lookup"><span data-stu-id="a93a6-113">You can use C++ interop, also known as It Just Works (IJW), to wrap a native C++ class so that it can be consumed by code that is authored in C# or another .NET language.</span></span> <span data-ttu-id="a93a6-114">若要這樣做，您可以撰寫 C++ 程式碼來包裝原生 DLL 或 COM 元件。</span><span class="sxs-lookup"><span data-stu-id="a93a6-114">To do this, you write C++ code to wrap a native DLL or COM component.</span></span> <span data-ttu-id="a93a6-115">不同于其他 .NET 語言，Visual C++ 具有互通性支援，可讓受控和非受控程式碼位於相同的應用程式中，甚至在同一個檔案中。</span><span class="sxs-lookup"><span data-stu-id="a93a6-115">Unlike other .NET languages, Visual C++ has interoperability support that enables managed and unmanaged code to be located in the same application and even in the same file.</span></span> <span data-ttu-id="a93a6-116">您接著可使用 **/clr** 編譯器參數建立 C++ 程式碼，以產生 Managed 組件。</span><span class="sxs-lookup"><span data-stu-id="a93a6-116">You then build the C++ code by using the **/clr** compiler switch to produce a managed assembly.</span></span> <span data-ttu-id="a93a6-117">最後，您可以在 C# 專案中新增組件的參考，並使用包裝的物件，就像是使用其他 Managed 類別一樣。</span><span class="sxs-lookup"><span data-stu-id="a93a6-117">Finally, you add a reference to the assembly in your C# project and use the wrapped objects just as you would use other managed classes.</span></span>  
  
## <a name="exposing-com-components-to-c"></a><span data-ttu-id="a93a6-118">將 COM 元件公開給 C\#</span><span class="sxs-lookup"><span data-stu-id="a93a6-118">Exposing COM Components to C\#</span></span>
 <span data-ttu-id="a93a6-119">您可以從 C# 專案取用 COM 元件。</span><span class="sxs-lookup"><span data-stu-id="a93a6-119">You can consume a COM component from a C# project.</span></span> <span data-ttu-id="a93a6-120">一般步驟如下所示：</span><span class="sxs-lookup"><span data-stu-id="a93a6-120">The general steps are as follows:</span></span>  
  
1. <span data-ttu-id="a93a6-121">找出並註冊所要使用的 COM 元件。</span><span class="sxs-lookup"><span data-stu-id="a93a6-121">Locate a COM component to use and register it.</span></span> <span data-ttu-id="a93a6-122">使用 regsvr32.exe 註冊或取消註冊 COM DLL。</span><span class="sxs-lookup"><span data-stu-id="a93a6-122">Use regsvr32.exe to register or un–register a COM DLL.</span></span>  
  
2. <span data-ttu-id="a93a6-123">將 COM 元件或型別程式庫的參考新增至專案。</span><span class="sxs-lookup"><span data-stu-id="a93a6-123">Add to the project a reference to the COM component or type library.</span></span>  
  
     <span data-ttu-id="a93a6-124">當您新增參考時，Visual Studio 會使用[tlbimp.exe （類型程式庫匯入工具）](../../../framework/tools/tlbimp-exe-type-library-importer.md)，其採用型別程式庫做為輸入，以輸出 .net interop 元件。</span><span class="sxs-lookup"><span data-stu-id="a93a6-124">When you add the reference, Visual Studio uses the [Tlbimp.exe (Type Library Importer)](../../../framework/tools/tlbimp-exe-type-library-importer.md), which takes a type library as input, to output a .NET interop assembly.</span></span> <span data-ttu-id="a93a6-125">此組件 (也稱為執行階段可呼叫包裝函式 (RCW)) 包含 Managed 類別和介面，以包裝型別程式庫中的 COM 類別和介面。</span><span class="sxs-lookup"><span data-stu-id="a93a6-125">The assembly, also named a runtime callable wrapper (RCW), contains managed classes and interfaces that wrap the COM classes and interfaces that are in the type library.</span></span> <span data-ttu-id="a93a6-126">Visual Studio 會將產生的組件參考新增至專案。</span><span class="sxs-lookup"><span data-stu-id="a93a6-126">Visual Studio adds to the project a reference to the generated assembly.</span></span>  
  
3. <span data-ttu-id="a93a6-127">建立定義於 RCW 之類別的執行個體。</span><span class="sxs-lookup"><span data-stu-id="a93a6-127">Create an instance of a class that is defined in the RCW.</span></span> <span data-ttu-id="a93a6-128">這會接著建立 COM 物件的執行個體。</span><span class="sxs-lookup"><span data-stu-id="a93a6-128">This, in turn, creates an instance of the COM object.</span></span>  
  
4. <span data-ttu-id="a93a6-129">就像是使用其他 Managed 物件一樣來使用此物件。</span><span class="sxs-lookup"><span data-stu-id="a93a6-129">Use the object just as you use other managed objects.</span></span> <span data-ttu-id="a93a6-130">當記憶體回收將物件回收時，也會從記憶體釋放 COM 物件的執行個體。</span><span class="sxs-lookup"><span data-stu-id="a93a6-130">When the object is reclaimed by garbage collection, the instance of the COM object is also released from memory.</span></span>  
  
 <span data-ttu-id="a93a6-131">如需詳細資訊，請參閱[將 COM 元件公開給 .NET Framework](../../../framework/interop/exposing-com-components.md)。</span><span class="sxs-lookup"><span data-stu-id="a93a6-131">For more information, see [Exposing COM Components to the .NET Framework](../../../framework/interop/exposing-com-components.md).</span></span>  
  
## <a name="exposing-c-to-com"></a><span data-ttu-id="a93a6-132">將 C# 公開給 COM</span><span class="sxs-lookup"><span data-stu-id="a93a6-132">Exposing C# to COM</span></span>  
 <span data-ttu-id="a93a6-133">COM 用戶端可取用已正確公開的 C# 類型。</span><span class="sxs-lookup"><span data-stu-id="a93a6-133">COM clients can consume C# types that have been correctly exposed.</span></span> <span data-ttu-id="a93a6-134">公開 C# 類型的基本步驟如下所示：</span><span class="sxs-lookup"><span data-stu-id="a93a6-134">The basic steps to expose C# types are as follows:</span></span>  
  
1. <span data-ttu-id="a93a6-135">在 C# 專案中新增 Interop 屬性。</span><span class="sxs-lookup"><span data-stu-id="a93a6-135">Add interop attributes in the C# project.</span></span>  
  
     <span data-ttu-id="a93a6-136">您可以藉由修改 Visual C# 專案屬性來顯示組件 COM。</span><span class="sxs-lookup"><span data-stu-id="a93a6-136">You can make an assembly COM visible by modifying Visual C# project properties.</span></span> <span data-ttu-id="a93a6-137">如需詳細資訊，請參閱[組件資訊對話方塊](/visualstudio/ide/reference/assembly-information-dialog-box)。</span><span class="sxs-lookup"><span data-stu-id="a93a6-137">For more information, see [Assembly Information Dialog Box](/visualstudio/ide/reference/assembly-information-dialog-box).</span></span>  
  
2. <span data-ttu-id="a93a6-138">產生 COM 型別程式庫並註冊供 COM 使用。</span><span class="sxs-lookup"><span data-stu-id="a93a6-138">Generate a COM type library and register it for COM usage.</span></span>  
  
     <span data-ttu-id="a93a6-139">您可以修改 Visual C# 專案屬性，以自動為 COM Interop 註冊 C# 組件。</span><span class="sxs-lookup"><span data-stu-id="a93a6-139">You can modify Visual C# project properties to automatically register the C# assembly for COM interop.</span></span> <span data-ttu-id="a93a6-140">Visual Studio 使用 [Regasm.exe (組件登錄工具)](../../../framework/tools/regasm-exe-assembly-registration-tool.md)，並使用接受受控組件作為輸入的 `/tlb` 命令列參數，以產生型別程式庫。</span><span class="sxs-lookup"><span data-stu-id="a93a6-140">Visual Studio uses the [Regasm.exe (Assembly Registration Tool)](../../../framework/tools/regasm-exe-assembly-registration-tool.md), using the `/tlb` command-line switch, which takes a managed assembly as input, to generate a type library.</span></span> <span data-ttu-id="a93a6-141">此型別程式庫描述組件中的 `public` 類型，並新增登錄項目，讓 COM 用戶端可以建立 Managed 類別。</span><span class="sxs-lookup"><span data-stu-id="a93a6-141">This type library describes the `public` types in the assembly and adds registry entries so that COM clients can create managed classes.</span></span>  
  
 <span data-ttu-id="a93a6-142">如需詳細資訊，請參閱[將 .NET Framework 元件公開給 COM](../../../framework/interop/exposing-dotnet-components-to-com.md) 和[範例 COM 類別](./example-com-class.md)。</span><span class="sxs-lookup"><span data-stu-id="a93a6-142">For more information, see [Exposing .NET Framework Components to COM](../../../framework/interop/exposing-dotnet-components-to-com.md) and [Example COM Class](./example-com-class.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="a93a6-143">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a93a6-143">See also</span></span>

- [<span data-ttu-id="a93a6-144">提升 Interop 效能</span><span class="sxs-lookup"><span data-stu-id="a93a6-144">Improving Interop Performance</span></span>](https://docs.microsoft.com/previous-versions/msp-n-p/ff647812%28v=pandp.10%29)
- [<span data-ttu-id="a93a6-145">COM 和.NET 之間的互通性簡介</span><span class="sxs-lookup"><span data-stu-id="a93a6-145">Introduction to Interoperability between COM and .NET</span></span>](/office/client-developer/outlook/pia/introduction-to-interoperability-between-com-and-net)
- [<span data-ttu-id="a93a6-146">Visual Basic 中的 COM Interop 簡介</span><span class="sxs-lookup"><span data-stu-id="a93a6-146">Introduction to COM Interop in Visual Basic</span></span>](../../../visual-basic/programming-guide/com-interop/introduction-to-com-interop.md)
- [<span data-ttu-id="a93a6-147">在受控碼和非受控碼之間進行封送處理</span><span class="sxs-lookup"><span data-stu-id="a93a6-147">Marshaling between Managed and Unmanaged Code</span></span>](../../../framework/interop/interop-marshaling.md)
- [<span data-ttu-id="a93a6-148">與 Unmanaged 程式碼互通</span><span class="sxs-lookup"><span data-stu-id="a93a6-148">Interoperating with Unmanaged Code</span></span>](../../../framework/interop/index.md)
- [<span data-ttu-id="a93a6-149">C # 程式設計指南</span><span class="sxs-lookup"><span data-stu-id="a93a6-149">C# Programming Guide</span></span>](../index.md)
