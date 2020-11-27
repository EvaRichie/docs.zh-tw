---
title: 使用 Unmanaged DLL 函式
description: 使用平台叫用服務來取用非受控 DLL 函式，此服務可讓 managed 程式碼呼叫 DLL 程式庫中所執行的非受控函式。
ms.date: 03/30/2017
helpviewer_keywords:
- unmanaged functions, calling
- COM interop, DLL functions
- unmanaged functions
- COM interop, platform invoke
- platform invoke, about platform invoke
- DLL functions, consuming unmanaged
- interoperation with unmanaged code, DLL functions
- interoperation with unmanaged code, platform invoke
- platform invoke
- DLL functions
ms.assetid: eca7606e-ebfb-4f47-b8d9-289903fdc045
ms.openlocfilehash: ea4008db59e580fc9d68135618f292496e96fce9
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96282934"
---
# <a name="consuming-unmanaged-dll-functions"></a><span data-ttu-id="43ed4-103">使用 Unmanaged DLL 函式</span><span class="sxs-lookup"><span data-stu-id="43ed4-103">Consuming Unmanaged DLL Functions</span></span>

<span data-ttu-id="43ed4-104">平台叫用服務，可讓受控碼呼叫實作在動態連結程式庫 (DLL) 中的非受控函式，如 Windows API 中的函式。</span><span class="sxs-lookup"><span data-stu-id="43ed4-104">Platform invoke is a service that enables managed code to call unmanaged functions implemented in dynamic link libraries (DLLs), such as those in the Windows API.</span></span> <span data-ttu-id="43ed4-105">它會找出並叫用匯出的函式，並且在需要的時候於交互操作界限之間封送處理其引數 (整數、 字串、 陣列、 結構和其他) 。</span><span class="sxs-lookup"><span data-stu-id="43ed4-105">It locates and invokes an exported function and marshals its arguments (integers, strings, arrays, structures, and so on) across the interoperation boundary as needed.</span></span>  
  
 <span data-ttu-id="43ed4-106">本節將介紹與取用非受控 DLL 函式相關聯的工作，並提供關於平台叫用的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="43ed4-106">This section introduces tasks associated with consuming unmanaged DLL functions and provides more information about platform invoke.</span></span> <span data-ttu-id="43ed4-107">除了下列工作之外，還有一般考量以及提供其他資訊和範例的連結。</span><span class="sxs-lookup"><span data-stu-id="43ed4-107">In addition to the following tasks, there are general considerations and a link providing additional information and examples.</span></span>  
  
#### <a name="to-consume-exported-dll-functions"></a><span data-ttu-id="43ed4-108">使用匯出的 DLL 函式</span><span class="sxs-lookup"><span data-stu-id="43ed4-108">To consume exported DLL functions</span></span>  
  
1. <span data-ttu-id="43ed4-109">[識別 DLL 中的函式](identifying-functions-in-dlls.md)。</span><span class="sxs-lookup"><span data-stu-id="43ed4-109">[Identify functions in DLLs](identifying-functions-in-dlls.md).</span></span>  
  
     <span data-ttu-id="43ed4-110">至少，您必須指定函式的名稱以及包含該函式之 DLL 的名稱。</span><span class="sxs-lookup"><span data-stu-id="43ed4-110">Minimally, you must specify the name of the function and name of the DLL that contains it.</span></span>  
  
2. <span data-ttu-id="43ed4-111">[建立類別以包裝 DLL 函式](creating-a-class-to-hold-dll-functions.md)。</span><span class="sxs-lookup"><span data-stu-id="43ed4-111">[Create a class to hold DLL functions](creating-a-class-to-hold-dll-functions.md).</span></span>  
  
     <span data-ttu-id="43ed4-112">您可以使用現有的類別、為每個 Unmanaged 函式建立個別的類別、或建立一個類別，其中包含一組相關的 Unmanaged 函式。</span><span class="sxs-lookup"><span data-stu-id="43ed4-112">You can use an existing class, create an individual class for each unmanaged function, or create one class that contains a set of related unmanaged functions.</span></span>  
  
3. <span data-ttu-id="43ed4-113">[在 Managed 程式碼中建立原型](creating-prototypes-in-managed-code.md).</span><span class="sxs-lookup"><span data-stu-id="43ed4-113">[Create prototypes in managed code](creating-prototypes-in-managed-code.md).</span></span>  
  
     <span data-ttu-id="43ed4-114">[Visual Basic] 搭配使用 **宣告** 陳述式與 **函式** 和 **Lib** 關鍵字。</span><span class="sxs-lookup"><span data-stu-id="43ed4-114">[Visual Basic] Use the **Declare** statement with the **Function** and **Lib** keywords.</span></span> <span data-ttu-id="43ed4-115">在某些罕見的情況下，您可以搭配使用 **DllImportAttribute** 與 **共用函式** 關鍵字。</span><span class="sxs-lookup"><span data-stu-id="43ed4-115">In some rare cases, you can use the **DllImportAttribute** with the **Shared Function** keywords.</span></span> <span data-ttu-id="43ed4-116">關於這種情況本節會於稍後加以說明。</span><span class="sxs-lookup"><span data-stu-id="43ed4-116">These cases are explained later in this section.</span></span>  
  
     <span data-ttu-id="43ed4-117">**使用DllImportAttribute** 來識別 DLL 和函式。</span><span class="sxs-lookup"><span data-stu-id="43ed4-117">[C#] Use the **DllImportAttribute** to identify the DLL and function.</span></span> <span data-ttu-id="43ed4-118">以 **靜態** 和 **外部** 修飾詞來標記方法。</span><span class="sxs-lookup"><span data-stu-id="43ed4-118">Mark the method with the **static** and **extern** modifiers.</span></span>  
  
     <span data-ttu-id="43ed4-119">[C#] 使用 **DllImportAttribute** 來識別 DLL 和函式。</span><span class="sxs-lookup"><span data-stu-id="43ed4-119">[C++] Use the **DllImportAttribute** to identify the DLL and function.</span></span> <span data-ttu-id="43ed4-120">以 **外部 "C"** 來標記包裝函式方法或函式。</span><span class="sxs-lookup"><span data-stu-id="43ed4-120">Mark the wrapper method or function with **extern "C"**.</span></span>  
  
4. <span data-ttu-id="43ed4-121">[呼叫 DLL 函式](calling-a-dll-function.md)。</span><span class="sxs-lookup"><span data-stu-id="43ed4-121">[Call a DLL function](calling-a-dll-function.md).</span></span>  
  
     <span data-ttu-id="43ed4-122">在您的 Managed 類別上呼叫方法，如同您呼叫任何其他 Managed 方法。</span><span class="sxs-lookup"><span data-stu-id="43ed4-122">Call the method on your managed class as you would any other managed method.</span></span> <span data-ttu-id="43ed4-123">[傳遞結構](passing-structures.md)和[實作回呼函式](callback-functions.md)為特殊案例。</span><span class="sxs-lookup"><span data-stu-id="43ed4-123">[Passing structures](passing-structures.md) and [implementing callback functions](callback-functions.md) are special cases.</span></span>  
  
 <span data-ttu-id="43ed4-124">如需示範如何建構要與平台叫用搭配使用之 .NET 型宣告的範例，請參閱[使用平台叫用封送處理資料](marshaling-data-with-platform-invoke.md)。</span><span class="sxs-lookup"><span data-stu-id="43ed4-124">For examples that demonstrate how to construct .NET-based declarations to be used with platform invoke, see [Marshaling Data with Platform Invoke](marshaling-data-with-platform-invoke.md).</span></span>  
  
## <a name="a-closer-look-at-platform-invoke"></a><span data-ttu-id="43ed4-125">進一步了解平台叫用</span><span class="sxs-lookup"><span data-stu-id="43ed4-125">A closer look at platform invoke</span></span>  

 <span data-ttu-id="43ed4-126">平台叫用依賴中繼資料來找出被匯出的函式，並在執行階段封送處理其引數。</span><span class="sxs-lookup"><span data-stu-id="43ed4-126">Platform invoke relies on metadata to locate exported functions and marshal their arguments at run time.</span></span> <span data-ttu-id="43ed4-127">下圖顯示這項程序。</span><span class="sxs-lookup"><span data-stu-id="43ed4-127">The following illustration shows this process.</span></span>  
  
 ![顯示平台叫用呼叫的圖表。](./media/consuming-unmanaged-dll-functions/platform-invoke-call.gif)  
  
 <span data-ttu-id="43ed4-129">當平台叫用呼叫 Unmanaged 函式時，它會依序執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="43ed4-129">When platform invoke calls an unmanaged function, it performs the following sequence of actions:</span></span>  
  
1. <span data-ttu-id="43ed4-130">找出包含該函式的 DLL。</span><span class="sxs-lookup"><span data-stu-id="43ed4-130">Locates the DLL containing the function.</span></span>  
  
2. <span data-ttu-id="43ed4-131">將 DLL 載入到記憶體中。</span><span class="sxs-lookup"><span data-stu-id="43ed4-131">Loads the DLL into memory.</span></span>  
  
3. <span data-ttu-id="43ed4-132">在記憶體中找出函式的位址，並將其引數推送至堆疊中，視需要封送處理資料。</span><span class="sxs-lookup"><span data-stu-id="43ed4-132">Locates the address of the function in memory and pushes its arguments onto the stack, marshaling data as required.</span></span>  
  
    > [!NOTE]
    > <span data-ttu-id="43ed4-133">僅在首次呼叫函式時尋找和載入 DLL，且尋找記憶體中的函式位址。</span><span class="sxs-lookup"><span data-stu-id="43ed4-133">Locating and loading the DLL, and locating the address of the function in memory occur only on the first call to the function.</span></span>  
  
4. <span data-ttu-id="43ed4-134">將控制項傳輸至 Unmanaged 函式。</span><span class="sxs-lookup"><span data-stu-id="43ed4-134">Transfers control to the unmanaged function.</span></span>  
  
 <span data-ttu-id="43ed4-135">平台叫用會擲回由 Unmanaged 函式產生的例外狀況給 Managed 呼叫端。</span><span class="sxs-lookup"><span data-stu-id="43ed4-135">Platform invoke throws exceptions generated by the unmanaged function to the managed caller.</span></span>

## <a name="see-also"></a><span data-ttu-id="43ed4-136">另請參閱</span><span class="sxs-lookup"><span data-stu-id="43ed4-136">See also</span></span>

- [<span data-ttu-id="43ed4-137">與 Unmanaged 程式碼互通</span><span class="sxs-lookup"><span data-stu-id="43ed4-137">Interoperating with Unmanaged Code</span></span>](index.md)
- [<span data-ttu-id="43ed4-138">平台叫用範例</span><span class="sxs-lookup"><span data-stu-id="43ed4-138">Platform Invoke Examples</span></span>](platform-invoke-examples.md)
- [<span data-ttu-id="43ed4-139">Interop 封送處理</span><span class="sxs-lookup"><span data-stu-id="43ed4-139">Interop Marshaling</span></span>](interop-marshaling.md)
