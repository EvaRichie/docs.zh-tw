---
title: bindingFailure MDA
description: 閱讀 bindingFailure managed 偵錯工具（MDA），這是當元件無法在 .NET 中載入時啟動的。
ms.date: 03/30/2017
helpviewer_keywords:
- binding failure
- binding, failures
- MDAs (managed debugging assistants), binding failures
- assemblies [.NET Framework], binding failures
- managed debugging assistants (MDAs), binding failures
- BindingFailure MDA
ms.assetid: 26ada5af-175c-4576-931a-9f07fa1723e9
ms.openlocfilehash: 98c7947c7e5d2a1f0af8c26744d3b292ed8cb4c4
ms.sourcegitcommit: a2c8b19e813a52b91facbb5d7e3c062c7188b457
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85415624"
---
# <a name="bindingfailure-mda"></a><span data-ttu-id="2398c-103">bindingFailure MDA</span><span class="sxs-lookup"><span data-stu-id="2398c-103">bindingFailure MDA</span></span>

<span data-ttu-id="2398c-104">無法載入組件時，會啟用 `bindingFailure` Managed 偵錯助理 (MDA)。</span><span class="sxs-lookup"><span data-stu-id="2398c-104">The `bindingFailure` managed debugging assistant (MDA) is activated when an assembly fails to load.</span></span>

## <a name="symptoms"></a><span data-ttu-id="2398c-105">徵狀</span><span class="sxs-lookup"><span data-stu-id="2398c-105">Symptoms</span></span>

<span data-ttu-id="2398c-106">程式碼已嘗試使用靜態參考或其中一個載入器方法 (例如 <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> 或 <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType>) 載入組件。</span><span class="sxs-lookup"><span data-stu-id="2398c-106">Code has attempted to load an assembly using a static reference or one of the loader methods, such as <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> or <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType>.</span></span> <span data-ttu-id="2398c-107">未載入組件，並擲回 <xref:System.IO.FileNotFoundException> 或 <xref:System.IO.FileLoadException> 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="2398c-107">The assembly is not loaded and a <xref:System.IO.FileNotFoundException> or <xref:System.IO.FileLoadException> exception is thrown.</span></span>

## <a name="cause"></a><span data-ttu-id="2398c-108">原因</span><span class="sxs-lookup"><span data-stu-id="2398c-108">Cause</span></span>

<span data-ttu-id="2398c-109">執行階段無法載入組件時，發生繫結失敗。</span><span class="sxs-lookup"><span data-stu-id="2398c-109">A binding failure occurs when the runtime is unable to load an assembly.</span></span> <span data-ttu-id="2398c-110">繫結失敗可能是下列其中一個情況所造成：</span><span class="sxs-lookup"><span data-stu-id="2398c-110">A binding failure might be the result of one of the following situations:</span></span>

- <span data-ttu-id="2398c-111">Common Language Runtime (CLR) 找不到要求的組件。</span><span class="sxs-lookup"><span data-stu-id="2398c-111">The common language runtime (CLR) cannot find the requested assembly.</span></span> <span data-ttu-id="2398c-112">有許多原因可能會發生這種情況，例如未安裝組件，或應用程式未正確地設定成尋找組件。</span><span class="sxs-lookup"><span data-stu-id="2398c-112">There are many reasons this can occur, such as the assembly not being installed or the application not being correctly configured to find the assembly.</span></span>

- <span data-ttu-id="2398c-113">常見問題案例是將類型傳遞給另一個應用程式定義域，而這需要 CLR 在另一個應用程式定義域中載入包含該類型的組件。</span><span class="sxs-lookup"><span data-stu-id="2398c-113">A common problem scenario is passing a type to another application domain, which requires the CLR to load the assembly containing that type in the other application domain.</span></span> <span data-ttu-id="2398c-114">如果另一個應用程式定義域與原始應用程式定義域的設定方式不同，則執行階段可能無法載入組件。</span><span class="sxs-lookup"><span data-stu-id="2398c-114">It may not be possible for the runtime to load the assembly if the other application domain is configured differently from the original application domain.</span></span> <span data-ttu-id="2398c-115">例如，兩個應用程式定義域可能會有不同的 <xref:System.AppDomain.BaseDirectory%2A> 屬性值。</span><span class="sxs-lookup"><span data-stu-id="2398c-115">For example, the two application domains might have different <xref:System.AppDomain.BaseDirectory%2A> property values.</span></span>

- <span data-ttu-id="2398c-116">所要求的組件損毀或不是組件。</span><span class="sxs-lookup"><span data-stu-id="2398c-116">The requested assembly is corrupted or is not an assembly.</span></span>

- <span data-ttu-id="2398c-117">嘗試載入組件的程式碼沒有載入組件的正確程式碼存取安全性權限。</span><span class="sxs-lookup"><span data-stu-id="2398c-117">The code attempting to load the assembly does not have the correct code access security permissions to load assemblies.</span></span>

- <span data-ttu-id="2398c-118">使用者認證未提供讀取檔案的必要權限。</span><span class="sxs-lookup"><span data-stu-id="2398c-118">The user credentials do not provide the required permissions to read the file.</span></span>

## <a name="resolution"></a><span data-ttu-id="2398c-119">解決方案</span><span class="sxs-lookup"><span data-stu-id="2398c-119">Resolution</span></span>

<span data-ttu-id="2398c-120">第一個步驟是判斷 CLR 為什麼無法繫結至所要求的組件。</span><span class="sxs-lookup"><span data-stu-id="2398c-120">The first step is to determine why the CLR could not bind to the requested assembly.</span></span> <span data-ttu-id="2398c-121">有許多原因會找不到執行階段或無法載入所要求的組件，例如 [原因] 區段中列出的案例。</span><span class="sxs-lookup"><span data-stu-id="2398c-121">There are many reasons why the runtime might not have found or been able load the requested assembly, such as the scenarios listed in the Cause section.</span></span> <span data-ttu-id="2398c-122">若要消除繫結失敗的原因，建議使用下列動作：</span><span class="sxs-lookup"><span data-stu-id="2398c-122">The following actions are recommended to eliminate the cause of the binding failure:</span></span>

- <span data-ttu-id="2398c-123">使用 `bindingFailure` MDA 所提供的資料，來判斷原因：</span><span class="sxs-lookup"><span data-stu-id="2398c-123">Determine the cause by using the data provided by the `bindingFailure` MDA:</span></span>

  - <span data-ttu-id="2398c-124">執行 [Fuslogvw.exe (組件繫結記錄檔檢視器)](../tools/fuslogvw-exe-assembly-binding-log-viewer.md)，以讀取組件繫結器所產生的錯誤記錄檔。</span><span class="sxs-lookup"><span data-stu-id="2398c-124">Run the [Fuslogvw.exe (Assembly Binding Log Viewer)](../tools/fuslogvw-exe-assembly-binding-log-viewer.md) to read the error logs produced by the assembly binder.</span></span>

  - <span data-ttu-id="2398c-125">判斷組件是否位於要求的位置。</span><span class="sxs-lookup"><span data-stu-id="2398c-125">Determine if the assembly is at the location requested.</span></span> <span data-ttu-id="2398c-126">如果是 <xref:System.Reflection.Assembly.LoadFrom%2A> 和 <xref:System.Reflection.Assembly.LoadFile%2A> 方法，則可以輕鬆地判斷所要求的位置。</span><span class="sxs-lookup"><span data-stu-id="2398c-126">In the case of the <xref:System.Reflection.Assembly.LoadFrom%2A> and <xref:System.Reflection.Assembly.LoadFile%2A> methods, the requested location can be easily determined.</span></span> <span data-ttu-id="2398c-127">如果是使用組件身分識別繫結的 <xref:System.Reflection.Assembly.Load%2A> 方法，則您必須尋找符合應用程式定義域之 <xref:System.AppDomain.BaseDirectory%2A> 屬性探查路徑和全域組件快取中該身分識別的組件。</span><span class="sxs-lookup"><span data-stu-id="2398c-127">In the case of the <xref:System.Reflection.Assembly.Load%2A> method, which binds using the assembly identity, you must look for assemblies that match that identity in the application domain's <xref:System.AppDomain.BaseDirectory%2A> property probe path and the global assembly cache.</span></span>

- <span data-ttu-id="2398c-128">根據先前的判斷來解決原因。</span><span class="sxs-lookup"><span data-stu-id="2398c-128">Resolve the cause based on the preceding determination.</span></span> <span data-ttu-id="2398c-129">可能的解決方式選項如下：</span><span class="sxs-lookup"><span data-stu-id="2398c-129">Possible resolution options are the following:</span></span>

  - <span data-ttu-id="2398c-130">在全域組件快取中安裝所要求的組件，並呼叫</span><span class="sxs-lookup"><span data-stu-id="2398c-130">Install the requested assembly in the global assembly cache and call the.</span></span> <span data-ttu-id="2398c-131"><xref:System.Reflection.Assembly.Load%2A> 方法，依身分識別載入組件。</span><span class="sxs-lookup"><span data-stu-id="2398c-131"><xref:System.Reflection.Assembly.Load%2A> method to load the assembly by identity.</span></span>

  - <span data-ttu-id="2398c-132">將所要求的組件複製至應用程式目錄，並呼叫 <xref:System.Reflection.Assembly.Load%2A> 方法，依身分識別載入組件。</span><span class="sxs-lookup"><span data-stu-id="2398c-132">Copy the requested assembly into the application directory and call the <xref:System.Reflection.Assembly.Load%2A> method to load the assembly by identity.</span></span>

  - <span data-ttu-id="2398c-133">變更 <xref:System.AppDomain.BaseDirectory%2A> 屬性，或新增私用探查路徑，以重新設定發生繫結失敗的應用程式定義域，來包含組件路徑。</span><span class="sxs-lookup"><span data-stu-id="2398c-133">Reconfigure the application domain in which the binding failure occurred to include the assembly path by either changing the <xref:System.AppDomain.BaseDirectory%2A> property or adding private probing paths.</span></span>

  - <span data-ttu-id="2398c-134">變更檔案的存取控制清單，讓已登入的使用者讀取檔案。</span><span class="sxs-lookup"><span data-stu-id="2398c-134">Change the access control list for the file to allow the logged-on user to read the file.</span></span>

## <a name="effect-on-the-runtime"></a><span data-ttu-id="2398c-135">對執行階段的影響</span><span class="sxs-lookup"><span data-stu-id="2398c-135">Effect on the Runtime</span></span>

<span data-ttu-id="2398c-136">此 MDA 對 CLR 沒有影響。</span><span class="sxs-lookup"><span data-stu-id="2398c-136">This MDA has no effect on the CLR.</span></span> <span data-ttu-id="2398c-137">它只會回報繫結失敗的資料。</span><span class="sxs-lookup"><span data-stu-id="2398c-137">It only reports data about binding failures.</span></span>

## <a name="output"></a><span data-ttu-id="2398c-138">輸出</span><span class="sxs-lookup"><span data-stu-id="2398c-138">Output</span></span>

<span data-ttu-id="2398c-139">MDA 回報無法載入的組件，包含要求的路徑和 (或) 顯示名稱、繫結內容、在其中要求載入的應用程式定義域，以及失敗原因。</span><span class="sxs-lookup"><span data-stu-id="2398c-139">The MDA reports the assembly that failed to load, including the requested path and/or display name, the binding context, the application domain in which the load was requested, and the reason for the failure.</span></span>

<span data-ttu-id="2398c-140">如果該資料無法用於 CLR，則顯示名稱或所要求的路徑可能空白。</span><span class="sxs-lookup"><span data-stu-id="2398c-140">The display name or requested path may be blank if that data was not available to the CLR.</span></span> <span data-ttu-id="2398c-141">如果失敗的呼叫是 <xref:System.Reflection.Assembly.Load%2A> 方法，則執行階段可能無法判斷組件的顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="2398c-141">If the call that failed was to the <xref:System.Reflection.Assembly.Load%2A> method, it is likely the runtime could not determine the display name for the assembly.</span></span>

## <a name="configuration"></a><span data-ttu-id="2398c-142">設定</span><span class="sxs-lookup"><span data-stu-id="2398c-142">Configuration</span></span>

```xml
<mdaConfig>
  <assistants>
    <bindingFailure />
  </assistants>
</mdaConfig>
```

## <a name="example"></a><span data-ttu-id="2398c-143">範例</span><span class="sxs-lookup"><span data-stu-id="2398c-143">Example</span></span>

<span data-ttu-id="2398c-144">下列程式碼範例示範可以啟動此 MDA 的情況：</span><span class="sxs-lookup"><span data-stu-id="2398c-144">The following code example demonstrates a situation that can activate this MDA:</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Text;
using System.Reflection;
namespace ConsoleApplication1
{
    class Program
    {
        static void Main(string[] args)
        {
            // This call attempts to load a nonexistent assembly.
            // The call will throw a System.IO.FileNotFound exception
            // and cause the activation of the bindingFailure MDA
            // if it is registered.
            Assembly.Load("NonExistentAssembly");
        }
    }
}
```

## <a name="see-also"></a><span data-ttu-id="2398c-145">另請參閱</span><span class="sxs-lookup"><span data-stu-id="2398c-145">See also</span></span>

- [<span data-ttu-id="2398c-146">使用 Managed 偵錯助理診斷錯誤</span><span class="sxs-lookup"><span data-stu-id="2398c-146">Diagnosing Errors with Managed Debugging Assistants</span></span>](diagnosing-errors-with-managed-debugging-assistants.md)
