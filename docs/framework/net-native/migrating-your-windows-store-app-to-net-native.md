---
title: 將您的 Windows 市集應用程式移轉至 .NET Native
ms.date: 03/30/2017
ms.assetid: 4153aa18-6f56-4a0a-865b-d3da743a1d05
ms.openlocfilehash: cef985200efaf2ed7488d5e99394a5f01cc38594
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90556924"
---
# <a name="migrate-your-windows-store-app-to-net-native"></a><span data-ttu-id="0871e-102">將您的 Windows Store 應用程式遷移至 .NET Native</span><span class="sxs-lookup"><span data-stu-id="0871e-102">Migrate Your Windows Store App to .NET Native</span></span>

<span data-ttu-id="0871e-103">.NET Native 在 Windows Store 或開發人員的電腦上提供應用程式的靜態編譯。</span><span class="sxs-lookup"><span data-stu-id="0871e-103">.NET Native provides static compilation of apps in the Windows Store or on the developer's computer.</span></span> <span data-ttu-id="0871e-104">這不同於 just-in-time (JIT) 編譯器或裝置上的 [原生映像產生器 (Ngen.exe)](../tools/ngen-exe-native-image-generator.md) 為 Windows 市集應用程式執行的動態編譯。</span><span class="sxs-lookup"><span data-stu-id="0871e-104">This differs from the dynamic compilation performed for Windows Store apps by the just-in-time (JIT) compiler or the [Native Image Generator (Ngen.exe)](../tools/ngen-exe-native-image-generator.md) on the device.</span></span> <span data-ttu-id="0871e-105">儘管有差異，.NET Native 還是會嘗試維持與 [適用于 Windows Store 應用程式的 .net](/previous-versions/windows/apps/br230302(v=vs.140))的相容性。</span><span class="sxs-lookup"><span data-stu-id="0871e-105">Despite the differences, .NET Native tries to maintain compatibility with the [.NET for Windows Store apps](/previous-versions/windows/apps/br230302(v=vs.140)).</span></span> <span data-ttu-id="0871e-106">大部分的情況下，在適用于 Windows Store 應用程式的 .NET 上運作的專案也適用于 .NET Native。</span><span class="sxs-lookup"><span data-stu-id="0871e-106">For the most part, things that work on the .NET for Windows Store apps also work with .NET Native.</span></span>  <span data-ttu-id="0871e-107">不過，在某些情況下，您可能會遇到行為上的變更。</span><span class="sxs-lookup"><span data-stu-id="0871e-107">However, in some cases, you may encounter behavioral changes.</span></span> <span data-ttu-id="0871e-108">本檔討論適用于 Windows Store 應用程式的標準 .NET 與下欄區域 .NET Native 之間的差異：</span><span class="sxs-lookup"><span data-stu-id="0871e-108">This document discusses these differences between the standard .NET for Windows Store apps and .NET Native in the following areas:</span></span>

- [<span data-ttu-id="0871e-109">一般執行階段的差異</span><span class="sxs-lookup"><span data-stu-id="0871e-109">General runtime differences</span></span>](#Runtime)

- [<span data-ttu-id="0871e-110">動態程式設計的差異</span><span class="sxs-lookup"><span data-stu-id="0871e-110">Dynamic programming differences</span></span>](#Dynamic)

- [<span data-ttu-id="0871e-111">其他與反映相關的差異</span><span class="sxs-lookup"><span data-stu-id="0871e-111">Other reflection-related differences</span></span>](#Reflection)

- [<span data-ttu-id="0871e-112">不支援的案例和 API</span><span class="sxs-lookup"><span data-stu-id="0871e-112">Unsupported scenarios and APIs</span></span>](#Unsupported)

- [<span data-ttu-id="0871e-113">Visual Studio 的差異</span><span class="sxs-lookup"><span data-stu-id="0871e-113">Visual Studio differences</span></span>](#VS)

<a name="Runtime"></a>

## <a name="general-runtime-differences"></a><span data-ttu-id="0871e-114">一般執行階段的差異</span><span class="sxs-lookup"><span data-stu-id="0871e-114">General runtime differences</span></span>

- <span data-ttu-id="0871e-115"><xref:System.TypeLoadException>當應用程式在 common language runtime (CLR) 上執行時，JIT 編譯程式所擲回的例外狀況，通常會在 .NET Native 處理時導致編譯時期錯誤。</span><span class="sxs-lookup"><span data-stu-id="0871e-115">Exceptions, such as <xref:System.TypeLoadException>, that are thrown by the JIT compiler when an app runs on the common language runtime (CLR) generally result in compile-time errors when processed by .NET Native.</span></span>

- <span data-ttu-id="0871e-116">請勿從應用程式的 UI 執行緒呼叫 <xref:System.GC.WaitForPendingFinalizers%2A?displayProperty=nameWithType> 方法。</span><span class="sxs-lookup"><span data-stu-id="0871e-116">Don't call the <xref:System.GC.WaitForPendingFinalizers%2A?displayProperty=nameWithType> method from an app's UI thread.</span></span> <span data-ttu-id="0871e-117">這可能會導致 .NET Native 鎖死。</span><span class="sxs-lookup"><span data-stu-id="0871e-117">This can result in a deadlock on .NET Native.</span></span>

- <span data-ttu-id="0871e-118">請不要依賴靜態類別建構函式引動過程順序。</span><span class="sxs-lookup"><span data-stu-id="0871e-118">Don't rely on static class constructor invocation ordering.</span></span> <span data-ttu-id="0871e-119">在 .NET Native 中，調用順序與標準執行時間的順序不同。</span><span class="sxs-lookup"><span data-stu-id="0871e-119">In .NET Native, the invocation order is different from the order on the standard runtime.</span></span> <span data-ttu-id="0871e-120">(即使是使用標準執行階段，也不應該依賴靜態類別建構函式的執行順序。)</span><span class="sxs-lookup"><span data-stu-id="0871e-120">(Even with the standard runtime, you shouldn't rely on the order of execution of static class constructors.)</span></span>

- <span data-ttu-id="0871e-121">在任何執行緒上無限迴圈，而不進行呼叫 (例如 `while(true);`) 可能會導致應用程式中止。</span><span class="sxs-lookup"><span data-stu-id="0871e-121">Infinite looping without making a call (for example, `while(true);`) on any thread may bring the app to a halt.</span></span> <span data-ttu-id="0871e-122">同樣地，長時間或無限等待可能也會導致應用程式中止。</span><span class="sxs-lookup"><span data-stu-id="0871e-122">Similarly, large or infinite waits may bring the app to a halt.</span></span>

- <span data-ttu-id="0871e-123">某些泛型初始化迴圈不會在 .NET Native 中擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="0871e-123">Certain generic initialization cycles don't throw exceptions in .NET Native.</span></span> <span data-ttu-id="0871e-124">例如，下列程式碼會在標準 CLR 上擲回 <xref:System.TypeLoadException> 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="0871e-124">For example, the following code throws a <xref:System.TypeLoadException> exception on the standard CLR.</span></span> <span data-ttu-id="0871e-125">在 .NET Native 中，它不是。</span><span class="sxs-lookup"><span data-stu-id="0871e-125">In .NET Native, it doesn't.</span></span>

  [!code-csharp[ProjectN#8](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/compat1.cs#8)]

- <span data-ttu-id="0871e-126">在某些情況下，.NET Native 提供 .NET Framework 類別庫的不同執行。</span><span class="sxs-lookup"><span data-stu-id="0871e-126">In some cases, .NET Native provides different implementations of .NET Framework class libraries.</span></span> <span data-ttu-id="0871e-127">從方法傳回的物件一律會實作傳回類型的成員。</span><span class="sxs-lookup"><span data-stu-id="0871e-127">An object returned from a method will always implement the members of the returned type.</span></span> <span data-ttu-id="0871e-128">不過，由於其支援實作不同，所以您可能無法將其轉換成像在其他 .NET Framework 平台上轉換的相同類型集。</span><span class="sxs-lookup"><span data-stu-id="0871e-128">However, since its backing implementation is different, you may not be able to cast it to the same set of types as you could on other .NET Framework platforms.</span></span> <span data-ttu-id="0871e-129">例如，在某些情況下，您可能無法將 <xref:System.Collections.Generic.IEnumerable%601> 或 <xref:System.Reflection.TypeInfo.DeclaredMembers%2A?displayProperty=nameWithType> 這類方法傳回的 <xref:System.Reflection.TypeInfo.DeclaredProperties%2A?displayProperty=nameWithType> 介面物件轉換成 `T[]`。</span><span class="sxs-lookup"><span data-stu-id="0871e-129">For example, in some cases, you may not be able to cast the <xref:System.Collections.Generic.IEnumerable%601> interface object returned by methods such as <xref:System.Reflection.TypeInfo.DeclaredMembers%2A?displayProperty=nameWithType> or <xref:System.Reflection.TypeInfo.DeclaredProperties%2A?displayProperty=nameWithType> to `T[]`.</span></span>

- <span data-ttu-id="0871e-130">在 Windows Store 應用程式的 .NET 上預設不會啟用 WinInet 快取，但它是在 .NET Native 上。</span><span class="sxs-lookup"><span data-stu-id="0871e-130">The WinInet cache isn't enabled by default on .NET for Windows Store apps, but it is on .NET Native.</span></span> <span data-ttu-id="0871e-131">這可以改善效能，但有工作集含意。</span><span class="sxs-lookup"><span data-stu-id="0871e-131">This improves performance but has working set implications.</span></span> <span data-ttu-id="0871e-132">開發人員不需任何動作。</span><span class="sxs-lookup"><span data-stu-id="0871e-132">No developer action is necessary.</span></span>

<a name="Dynamic"></a>

## <a name="dynamic-programming-differences"></a><span data-ttu-id="0871e-133">動態程式設計的差異</span><span class="sxs-lookup"><span data-stu-id="0871e-133">Dynamic programming differences</span></span>

<span data-ttu-id="0871e-134">.NET Native .NET Framework 程式碼中的靜態連結，讓程式碼應用程式在本機取得最大效能。</span><span class="sxs-lookup"><span data-stu-id="0871e-134">.NET Native statically links in code from the .NET Framework to make the code app-local for maximum performance.</span></span> <span data-ttu-id="0871e-135">不過，二進位大小必須維持在較小的狀態，這樣才不會將整個 .NET Framework 帶進來。</span><span class="sxs-lookup"><span data-stu-id="0871e-135">However, binary sizes have to remain small, so the entire .NET Framework can't be brought in.</span></span> <span data-ttu-id="0871e-136">.NET Native 編譯器會使用移除未使用程式碼參考的相依性歸納器來解決這項限制。</span><span class="sxs-lookup"><span data-stu-id="0871e-136">The .NET Native compiler resolves this limitation by using a dependency reducer that removes references to unused code.</span></span> <span data-ttu-id="0871e-137">不過，當無法在編譯時期以靜態方式推斷資訊時，.NET Native 可能不會維護或產生某些類型資訊和程式碼，而是在執行時間以動態方式進行取出。</span><span class="sxs-lookup"><span data-stu-id="0871e-137">However, .NET Native might not maintain or generate some type information and code when that information can't be inferred statically at compile time, but instead is retrieved dynamically at runtime.</span></span>

<span data-ttu-id="0871e-138">.NET Native 確實會啟用反映和動態程式設計。</span><span class="sxs-lookup"><span data-stu-id="0871e-138">.NET Native does enable reflection and dynamic programming.</span></span> <span data-ttu-id="0871e-139">不過，並非所有類型都可以標記來進行反映，因為這樣會使所產生的程式碼大小過大 (尤其是因為可支援在 .NET Framework 中的公用 API 上反映)。</span><span class="sxs-lookup"><span data-stu-id="0871e-139">However, not all types can be marked for reflection, because this would make the generated code size too large (especially because reflecting on public APIs in the .NET Framework is supported).</span></span> <span data-ttu-id="0871e-140">.NET Native 編譯器會針對哪些型別提供支援反映的智慧型選擇，並保留中繼資料並只產生這些型別的程式碼。</span><span class="sxs-lookup"><span data-stu-id="0871e-140">The .NET Native compiler makes smart choices about which types should support reflection, and it keeps the metadata and generates code only for those types.</span></span>

<span data-ttu-id="0871e-141">例如，資料繫結會要求應用程式能夠將屬性名稱對應至函式。</span><span class="sxs-lookup"><span data-stu-id="0871e-141">For example, data binding requires an app to be able to map property names to functions.</span></span> <span data-ttu-id="0871e-142">在適用於 Windows 市集應用程式的 .NET 中，通用語言執行平台會自動使用反映來提供這項功能給 Managed 類型和可公開取得的原生類型。</span><span class="sxs-lookup"><span data-stu-id="0871e-142">In .NET for Windows Store apps, the common language runtime automatically uses reflection to provide this capability for managed types and publicly available native types.</span></span> <span data-ttu-id="0871e-143">在 .NET Native 中，編譯器會自動為您系結資料的類型加入中繼資料。</span><span class="sxs-lookup"><span data-stu-id="0871e-143">In .NET Native, the compiler automatically includes metadata for types to which you bind data.</span></span>

<span data-ttu-id="0871e-144">.NET Native 編譯器也可以處理常用的泛型型別（例如 <xref:System.Collections.Generic.List%601> 和 <xref:System.Collections.Generic.Dictionary%602> ），而不需要任何提示或指示詞。</span><span class="sxs-lookup"><span data-stu-id="0871e-144">The .NET Native compiler can also handle commonly used generic types such as <xref:System.Collections.Generic.List%601> and <xref:System.Collections.Generic.Dictionary%602>, which work without requiring any hints or directives.</span></span> <span data-ttu-id="0871e-145">在某些限制下，也可支援 [動態](../../csharp/language-reference/builtin-types/reference-types.md#the-dynamic-type) 關鍵字。</span><span class="sxs-lookup"><span data-stu-id="0871e-145">The [dynamic](../../csharp/language-reference/builtin-types/reference-types.md#the-dynamic-type) keyword is also supported within certain limits.</span></span>

> [!NOTE]
> <span data-ttu-id="0871e-146">將您的應用程式移植到 .NET Native 時，您應該徹底地測試所有動態程式碼路徑。</span><span class="sxs-lookup"><span data-stu-id="0871e-146">You should test all dynamic code paths thoroughly when porting your app to .NET Native.</span></span>

<span data-ttu-id="0871e-147">.NET Native 的預設設定對大部分的開發人員都已足夠，但某些開發人員可能會想要使用執行時間指示詞（ ( # A0) 檔）來微調其設定。</span><span class="sxs-lookup"><span data-stu-id="0871e-147">The default configuration for .NET Native is sufficient for most developers, but some developers might want to fine- tune their configurations by using a runtime directives (.rd.xml) file.</span></span> <span data-ttu-id="0871e-148">此外，在某些情況下，.NET Native 編譯器無法判斷哪些中繼資料必須可用於反映，而且依賴提示，特別是在下列情況中：</span><span class="sxs-lookup"><span data-stu-id="0871e-148">In addition, in some cases, the .NET Native compiler is unable to determine which metadata must be available for reflection and relies on hints, particularly in the following cases:</span></span>

- <span data-ttu-id="0871e-149">無法以靜態方式判斷某些結構，例如 <xref:System.Type.MakeGenericType%2A?displayProperty=nameWithType> 和 <xref:System.Reflection.MethodInfo.MakeGenericMethod%2A?displayProperty=nameWithType> 。</span><span class="sxs-lookup"><span data-stu-id="0871e-149">Some constructs like <xref:System.Type.MakeGenericType%2A?displayProperty=nameWithType> and <xref:System.Reflection.MethodInfo.MakeGenericMethod%2A?displayProperty=nameWithType> can't be determined statically.</span></span>

- <span data-ttu-id="0871e-150">由於編譯器無法判斷具現化，所以必須以執行階段指示詞來指定您想要反映的泛型類型。</span><span class="sxs-lookup"><span data-stu-id="0871e-150">Because the compiler can't determine the instantiations, a generic type that you want to reflect on has to be specified by runtime directives.</span></span> <span data-ttu-id="0871e-151">這不只是因為所有的程式碼必須包含在內，也因為反映在泛型類型上會形成無限循環 (例如，在泛型類型上叫用泛型方法時)。</span><span class="sxs-lookup"><span data-stu-id="0871e-151">This isn't just because all code must be included, but because reflection on generic types can form an infinite cycle (for example, when a generic method is invoked on a generic type).</span></span>

> [!NOTE]
> <span data-ttu-id="0871e-152">執行階段指示詞中定義在執行階段指示詞 (.rd.xml) 檔案中。</span><span class="sxs-lookup"><span data-stu-id="0871e-152">Runtime directives are defined in a runtime directives (.rd.xml) file.</span></span> <span data-ttu-id="0871e-153">如需使用此檔案的一般資訊，請參閱[使用者入門](getting-started-with-net-native.md)。</span><span class="sxs-lookup"><span data-stu-id="0871e-153">For general information about using this file, see [Getting Started](getting-started-with-net-native.md).</span></span> <span data-ttu-id="0871e-154">如需執行階段指示詞的詳細資訊，請參閱 [Runtime Directives (rd.xml) Configuration File Reference](runtime-directives-rd-xml-configuration-file-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="0871e-154">For information about the runtime directives, see [Runtime Directives (rd.xml) Configuration File Reference](runtime-directives-rd-xml-configuration-file-reference.md).</span></span>

<span data-ttu-id="0871e-155">.NET Native 也包含分析工具，可協助開發人員判斷預設集合以外的哪些類型應該支援反映。</span><span class="sxs-lookup"><span data-stu-id="0871e-155">.NET Native also includes profiling tools that help the developer determine which types outside the default set should support reflection.</span></span>

<a name="Reflection"></a>

## <a name="other-reflection-related-differences"></a><span data-ttu-id="0871e-156">其他與反映相關的差異</span><span class="sxs-lookup"><span data-stu-id="0871e-156">Other reflection-related differences</span></span>

<span data-ttu-id="0871e-157">在適用于 Windows Store 應用程式的 .NET 與 .NET Native 之間，有許多其他個別反映相關的行為差異。</span><span class="sxs-lookup"><span data-stu-id="0871e-157">There are a number of other individual reflection-related differences in behavior between the .NET for Windows Store apps and .NET Native.</span></span>

<span data-ttu-id="0871e-158">在 .NET Native：</span><span class="sxs-lookup"><span data-stu-id="0871e-158">In .NET Native:</span></span>

- <span data-ttu-id="0871e-159">不支援 .NET Framework 類別庫中，透過類型和成員的私用反映。</span><span class="sxs-lookup"><span data-stu-id="0871e-159">Private reflection over types and members in the .NET Framework class library is not supported.</span></span> <span data-ttu-id="0871e-160">不過，您可以透過自己的私用類型和成員，以及協力廠商程式庫中的類型和成員來進行反映。</span><span class="sxs-lookup"><span data-stu-id="0871e-160">You can, however, reflect over your own private types and members, as well as types and members in third-party libraries.</span></span>

- <span data-ttu-id="0871e-161"><xref:System.Reflection.ParameterInfo.HasDefaultValue%2A?displayProperty=nameWithType> 屬性針對表示傳回值的 `false` 物件，正確地傳回 <xref:System.Reflection.ParameterInfo> 。</span><span class="sxs-lookup"><span data-stu-id="0871e-161">The <xref:System.Reflection.ParameterInfo.HasDefaultValue%2A?displayProperty=nameWithType> property correctly returns `false` for a <xref:System.Reflection.ParameterInfo> object that represents a return value.</span></span> <span data-ttu-id="0871e-162">在適用於 Windows 市集應用程式的 .NET 中，它會傳回 `true`。</span><span class="sxs-lookup"><span data-stu-id="0871e-162">In the .NET for Windows Store apps, it returns `true`.</span></span> <span data-ttu-id="0871e-163">中繼語言 (IL) 不會直接支援這種情況，而轉譯會留給語言。</span><span class="sxs-lookup"><span data-stu-id="0871e-163">Intermediate language (IL) doesn't support this directly, and interpretation is left to the language.</span></span>

- <span data-ttu-id="0871e-164">不支援 <xref:System.RuntimeFieldHandle> 和 <xref:System.RuntimeMethodHandle> 結構上的公用成員。</span><span class="sxs-lookup"><span data-stu-id="0871e-164">Public members on the <xref:System.RuntimeFieldHandle> and <xref:System.RuntimeMethodHandle> structures aren't supported.</span></span> <span data-ttu-id="0871e-165">只有針對 LINQ、運算式樹狀架構和靜態陣列初始設定，才會支援這些類型。</span><span class="sxs-lookup"><span data-stu-id="0871e-165">These types are supported only for LINQ, expression trees, and static array initialization.</span></span>

- <span data-ttu-id="0871e-166"><xref:System.Reflection.RuntimeReflectionExtensions.GetRuntimeProperties%2A?displayProperty=nameWithType> 和 <xref:System.Reflection.RuntimeReflectionExtensions.GetRuntimeEvents%2A?displayProperty=nameWithType> 將隱藏的成員包含基底類別中，因此可能會在非明確覆寫的情況下被覆寫。</span><span class="sxs-lookup"><span data-stu-id="0871e-166"><xref:System.Reflection.RuntimeReflectionExtensions.GetRuntimeProperties%2A?displayProperty=nameWithType> and <xref:System.Reflection.RuntimeReflectionExtensions.GetRuntimeEvents%2A?displayProperty=nameWithType> include hidden members in base classes and thus may be overridden without explicit overrides.</span></span> <span data-ttu-id="0871e-167">針對其他 [RuntimeReflectionExtensions.GetRuntime\*](xref:System.Reflection.RuntimeReflectionExtensions) 方法也是如此。</span><span class="sxs-lookup"><span data-stu-id="0871e-167">This is also true of other [RuntimeReflectionExtensions.GetRuntime\*](xref:System.Reflection.RuntimeReflectionExtensions) methods.</span></span>

- <span data-ttu-id="0871e-168"><xref:System.Type.MakeArrayType%2A?displayProperty=nameWithType><xref:System.Type.MakeByRefType%2A?displayProperty=nameWithType>當您嘗試建立特定組合時，不會失敗 (例如， `byref`) 的物件陣列。</span><span class="sxs-lookup"><span data-stu-id="0871e-168"><xref:System.Type.MakeArrayType%2A?displayProperty=nameWithType> and <xref:System.Type.MakeByRefType%2A?displayProperty=nameWithType> don't fail when you try to create certain combinations (for example, an array of `byref` objects).</span></span>

- <span data-ttu-id="0871e-169">您不能使用反映來叫用具有指標參數的成員。</span><span class="sxs-lookup"><span data-stu-id="0871e-169">You can't use reflection to invoke members that have pointer parameters.</span></span>

- <span data-ttu-id="0871e-170">您不能使用反映來取得或設定指標欄位。</span><span class="sxs-lookup"><span data-stu-id="0871e-170">You can't use reflection to get or set a pointer field.</span></span>

- <span data-ttu-id="0871e-171">當引數計數錯誤且其中一個引數的類型不正確時，.NET Native 會擲回， <xref:System.ArgumentException> 而不是 <xref:System.Reflection.TargetParameterCountException> 。</span><span class="sxs-lookup"><span data-stu-id="0871e-171">When the argument count is wrong and the type of one of the arguments is incorrect, .NET Native throws an <xref:System.ArgumentException> instead of a <xref:System.Reflection.TargetParameterCountException>.</span></span>

- <span data-ttu-id="0871e-172">通常不支援例外狀況的二進位序列化。</span><span class="sxs-lookup"><span data-stu-id="0871e-172">Binary serialization of exceptions is generally not supported.</span></span> <span data-ttu-id="0871e-173">因此，可以將不可序列化的物件加入 <xref:System.Exception.Data%2A?displayProperty=nameWithType> 字典。</span><span class="sxs-lookup"><span data-stu-id="0871e-173">As a result, non-serializable objects can be added to the <xref:System.Exception.Data%2A?displayProperty=nameWithType> dictionary.</span></span>

<a name="Unsupported"></a>

## <a name="unsupported-scenarios-and-apis"></a><span data-ttu-id="0871e-174">不支援的案例和 API</span><span class="sxs-lookup"><span data-stu-id="0871e-174">Unsupported scenarios and APIs</span></span>

<span data-ttu-id="0871e-175">下列各節會針對一般開發、interop 以及 HTTPClient 和 Windows Communication Foundation (WCF) 等技術，列出不支援的案例和 API：</span><span class="sxs-lookup"><span data-stu-id="0871e-175">The following sections list unsupported scenarios and APIs for general development, interop, and technologies such as HTTPClient and Windows Communication Foundation (WCF):</span></span>

- [<span data-ttu-id="0871e-176">一般開發</span><span class="sxs-lookup"><span data-stu-id="0871e-176">General development</span></span>](#General)

- [<span data-ttu-id="0871e-177">HttpClient</span><span class="sxs-lookup"><span data-stu-id="0871e-177">HttpClient</span></span>](#HttpClient)

- [<span data-ttu-id="0871e-178">Interop</span><span class="sxs-lookup"><span data-stu-id="0871e-178">Interop</span></span>](#Interop)

- [<span data-ttu-id="0871e-179">不支援的 API</span><span class="sxs-lookup"><span data-stu-id="0871e-179">Unsupported APIs</span></span>](#APIs)

<a name="General"></a>

### <a name="general-development-differences"></a><span data-ttu-id="0871e-180">一般開發的差異</span><span class="sxs-lookup"><span data-stu-id="0871e-180">General development differences</span></span>

<span data-ttu-id="0871e-181">**值類型**</span><span class="sxs-lookup"><span data-stu-id="0871e-181">**Value types**</span></span>

- <span data-ttu-id="0871e-182">如果您覆寫 <xref:System.ValueType.Equals%2A?displayProperty=nameWithType> 和 <xref:System.ValueType.GetHashCode%2A?displayProperty=nameWithType> 方法的值類型，請勿呼叫基底類別實作。</span><span class="sxs-lookup"><span data-stu-id="0871e-182">If you override the <xref:System.ValueType.Equals%2A?displayProperty=nameWithType> and <xref:System.ValueType.GetHashCode%2A?displayProperty=nameWithType> methods for a value type, don't call the base class implementations.</span></span> <span data-ttu-id="0871e-183">在適用於 Windows 市集應用程式的 .NET 中，這些方法會依賴反映。</span><span class="sxs-lookup"><span data-stu-id="0871e-183">In .NET for Windows Store apps, these methods rely on reflection.</span></span> <span data-ttu-id="0871e-184">在編譯時期，.NET Native 會產生不依賴執行時間反映的實作為。</span><span class="sxs-lookup"><span data-stu-id="0871e-184">At compile time, .NET Native generates an implementation that doesn't rely on runtime reflection.</span></span> <span data-ttu-id="0871e-185">這表示，如果您未覆寫這兩個方法，這些方法將會如預期般運作，因為 .NET Native 會在編譯時期產生執行。</span><span class="sxs-lookup"><span data-stu-id="0871e-185">This means that if you don't override these two methods, they will work as expected, because .NET Native generates the implementation at compile time.</span></span> <span data-ttu-id="0871e-186">不過，覆寫這些方法，但又呼叫基底類別實作，將會導致例外狀況。</span><span class="sxs-lookup"><span data-stu-id="0871e-186">However, overriding these methods but calling the base class implementation results in an exception.</span></span>

- <span data-ttu-id="0871e-187">不支援大於 1 mb 的實數值型別。</span><span class="sxs-lookup"><span data-stu-id="0871e-187">Value types larger than 1 megabyte aren't supported.</span></span>

- <span data-ttu-id="0871e-188">實數值型別在 .NET Native 中不能有無參數的函式。</span><span class="sxs-lookup"><span data-stu-id="0871e-188">Value types can't have a parameterless constructor in .NET Native.</span></span> <span data-ttu-id="0871e-189"> (c # 和 Visual Basic 禁止在實數值型別上有參數的函式。</span><span class="sxs-lookup"><span data-stu-id="0871e-189">(C# and Visual Basic prohibit parameterless constructors on value types.</span></span> <span data-ttu-id="0871e-190">不過，可以在 IL 中建立這些預設建構函式)。</span><span class="sxs-lookup"><span data-stu-id="0871e-190">However, these can be created in IL.)</span></span>

<span data-ttu-id="0871e-191">**陣列**</span><span class="sxs-lookup"><span data-stu-id="0871e-191">**Arrays**</span></span>

- <span data-ttu-id="0871e-192">不支援下限不是零的陣列。</span><span class="sxs-lookup"><span data-stu-id="0871e-192">Arrays with a lower bound other than zero aren't supported.</span></span> <span data-ttu-id="0871e-193">一般而言，可以呼叫 <xref:System.Array.CreateInstance%28System.Type%2CSystem.Int32%5B%5D%2CSystem.Int32%5B%5D%29?displayProperty=nameWithType> 多載來建立這些陣列。</span><span class="sxs-lookup"><span data-stu-id="0871e-193">Typically, these arrays are created by calling the <xref:System.Array.CreateInstance%28System.Type%2CSystem.Int32%5B%5D%2CSystem.Int32%5B%5D%29?displayProperty=nameWithType> overload.</span></span>

- <span data-ttu-id="0871e-194">不支援動態建立多維陣列。</span><span class="sxs-lookup"><span data-stu-id="0871e-194">Dynamic creation of multidimensional arrays isn't supported.</span></span> <span data-ttu-id="0871e-195">這類陣列的建立，通常是藉由呼叫包含 <xref:System.Array.CreateInstance%2A?displayProperty=nameWithType> 參數之 `lengths` 方法的多載，或是呼叫 <xref:System.Type.MakeArrayType%28System.Int32%29?displayProperty=nameWithType> 方法。</span><span class="sxs-lookup"><span data-stu-id="0871e-195">Such arrays are typically created by calling an overload of the <xref:System.Array.CreateInstance%2A?displayProperty=nameWithType> method that includes a `lengths` parameter, or by calling the <xref:System.Type.MakeArrayType%28System.Int32%29?displayProperty=nameWithType> method.</span></span>

- <span data-ttu-id="0871e-196">不支援具有 4 個 (含) 以上維度的多維陣列，意即，其 <xref:System.Array.Rank%2A?displayProperty=nameWithType> 屬性值為 4 (含) 以上。</span><span class="sxs-lookup"><span data-stu-id="0871e-196">Multidimensional arrays that have four or more dimensions aren't supported; that is, their <xref:System.Array.Rank%2A?displayProperty=nameWithType> property value is four or greater.</span></span> <span data-ttu-id="0871e-197">請改用 [不規則陣列](../../csharp/programming-guide/arrays/jagged-arrays.md) (陣列的陣列)。</span><span class="sxs-lookup"><span data-stu-id="0871e-197">Use [jagged arrays](../../csharp/programming-guide/arrays/jagged-arrays.md) (an array of arrays) instead.</span></span> <span data-ttu-id="0871e-198">例如， `array[x,y,z]` 無效，但 `array[x][y][z]` 有效。</span><span class="sxs-lookup"><span data-stu-id="0871e-198">For example, `array[x,y,z]` is invalid, but `array[x][y][z]` isn't.</span></span>

- <span data-ttu-id="0871e-199">不支援多維陣列的變異數，它會在執行階段導致 <xref:System.InvalidCastException> 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="0871e-199">Variance for multidimensional arrays isn't supported and causes an <xref:System.InvalidCastException> exception at run time.</span></span>

<span data-ttu-id="0871e-200">**泛型**</span><span class="sxs-lookup"><span data-stu-id="0871e-200">**Generics**</span></span>

- <span data-ttu-id="0871e-201">無限的泛型類型擴充會導致編譯器錯誤。</span><span class="sxs-lookup"><span data-stu-id="0871e-201">Infinite generic type expansion results in a compiler error.</span></span> <span data-ttu-id="0871e-202">例如，此程式碼無法編譯：</span><span class="sxs-lookup"><span data-stu-id="0871e-202">For example, this code fails to compile:</span></span>

  [!code-csharp[ProjectN#9](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/compat2.cs#9)]

<span data-ttu-id="0871e-203">**指標**</span><span class="sxs-lookup"><span data-stu-id="0871e-203">**Pointers**</span></span>

- <span data-ttu-id="0871e-204">不支援指標的陣列。</span><span class="sxs-lookup"><span data-stu-id="0871e-204">Arrays of pointers aren't supported.</span></span>

- <span data-ttu-id="0871e-205">您不能使用反映來取得或設定指標欄位。</span><span class="sxs-lookup"><span data-stu-id="0871e-205">You can't use reflection to get or set a pointer field.</span></span>

<span data-ttu-id="0871e-206">**序列化**</span><span class="sxs-lookup"><span data-stu-id="0871e-206">**Serialization**</span></span>

<span data-ttu-id="0871e-207">不支援 <xref:System.Runtime.Serialization.KnownTypeAttribute.%23ctor%28System.String%29> 屬性。</span><span class="sxs-lookup"><span data-stu-id="0871e-207">The <xref:System.Runtime.Serialization.KnownTypeAttribute.%23ctor%28System.String%29> attribute isn't supported.</span></span> <span data-ttu-id="0871e-208">請改用 <xref:System.Runtime.Serialization.KnownTypeAttribute.%23ctor%28System.Type%29> 屬性。</span><span class="sxs-lookup"><span data-stu-id="0871e-208">Use the <xref:System.Runtime.Serialization.KnownTypeAttribute.%23ctor%28System.Type%29> attribute instead.</span></span>

<span data-ttu-id="0871e-209">**資源**</span><span class="sxs-lookup"><span data-stu-id="0871e-209">**Resources**</span></span>

<span data-ttu-id="0871e-210">不支援將當地語系化的資源與 <xref:System.Diagnostics.Tracing.EventSource> 類別搭配使用。</span><span class="sxs-lookup"><span data-stu-id="0871e-210">The use of localized resources with the <xref:System.Diagnostics.Tracing.EventSource> class isn't supported.</span></span> <span data-ttu-id="0871e-211"><xref:System.Diagnostics.Tracing.EventSourceAttribute.LocalizationResources%2A?displayProperty=nameWithType> 屬性不會定義當地語系化的資源。</span><span class="sxs-lookup"><span data-stu-id="0871e-211">The <xref:System.Diagnostics.Tracing.EventSourceAttribute.LocalizationResources%2A?displayProperty=nameWithType> property doesn't define localized resources.</span></span>

<span data-ttu-id="0871e-212">**委派**</span><span class="sxs-lookup"><span data-stu-id="0871e-212">**Delegates**</span></span>

<span data-ttu-id="0871e-213">不支援`Delegate.BeginInvoke` 和 `Delegate.EndInvoke` 。</span><span class="sxs-lookup"><span data-stu-id="0871e-213">`Delegate.BeginInvoke` and `Delegate.EndInvoke` aren't supported.</span></span>

<span data-ttu-id="0871e-214">**其他 API**</span><span class="sxs-lookup"><span data-stu-id="0871e-214">**Miscellaneous APIs**</span></span>

- <span data-ttu-id="0871e-215">[TypeInfo.GUID](xref:System.Type.GUID) <xref:System.PlatformNotSupportedException> 如果 <xref:System.Runtime.InteropServices.GuidAttribute> 屬性未套用至類型，TypeInfo GUID 屬性會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="0871e-215">The [TypeInfo.GUID](xref:System.Type.GUID) property throws a <xref:System.PlatformNotSupportedException> exception if a <xref:System.Runtime.InteropServices.GuidAttribute> attribute isn't applied to the type.</span></span> <span data-ttu-id="0871e-216">GUID 主要用於 COM 支援。</span><span class="sxs-lookup"><span data-stu-id="0871e-216">The GUID is used primarily for COM support.</span></span>

- <span data-ttu-id="0871e-217"><xref:System.DateTime.Parse%2A?displayProperty=nameWithType>方法會正確地剖析包含 .NET Native 中簡短日期的字串。</span><span class="sxs-lookup"><span data-stu-id="0871e-217">The <xref:System.DateTime.Parse%2A?displayProperty=nameWithType> method correctly parses strings that contain short dates in .NET Native.</span></span> <span data-ttu-id="0871e-218">不過，它不會維護 Microsoft 知識庫文章 [KB2803771](https://support.microsoft.com/kb/2803771) 和 [KB2803755](https://support.microsoft.com/kb/2803755)中描述之日期和時間剖析變更的相容性。</span><span class="sxs-lookup"><span data-stu-id="0871e-218">However, it doesn't maintain compatibility with the changes in date and time parsing described in the Microsoft Knowledge Base articles [KB2803771](https://support.microsoft.com/kb/2803771) and [KB2803755](https://support.microsoft.com/kb/2803755).</span></span>

- <span data-ttu-id="0871e-219"><xref:System.Numerics.BigInteger.ToString%2A?displayProperty=nameWithType>`("E")`在 .NET Native 中已正確四捨五入。</span><span class="sxs-lookup"><span data-stu-id="0871e-219"><xref:System.Numerics.BigInteger.ToString%2A?displayProperty=nameWithType> `("E")` is correctly rounded in .NET Native.</span></span> <span data-ttu-id="0871e-220">在某些版本的 CLR 中，會將結果字串無條件捨去，而不是四捨五入。</span><span class="sxs-lookup"><span data-stu-id="0871e-220">In some versions of the CLR, the result string is truncated instead of rounded.</span></span>

<a name="HttpClient"></a>

### <a name="httpclient-differences"></a><span data-ttu-id="0871e-221">HttpClient 差異</span><span class="sxs-lookup"><span data-stu-id="0871e-221">HttpClient differences</span></span>

<span data-ttu-id="0871e-222">在 .NET Native 中， <xref:System.Net.Http.HttpClientHandler> 類別會在內部使用 WinINet (透過 <xref:Windows.Web.Http.Filters.HttpBaseProtocolFilter> 類別) ，而不是 <xref:System.Net.WebRequest> <xref:System.Net.WebResponse> 在適用于 Windows Store 應用程式的標準 .net 中使用的和類別。</span><span class="sxs-lookup"><span data-stu-id="0871e-222">In .NET Native, the <xref:System.Net.Http.HttpClientHandler> class internally uses WinINet (through the <xref:Windows.Web.Http.Filters.HttpBaseProtocolFilter> class) instead of the <xref:System.Net.WebRequest> and <xref:System.Net.WebResponse> classes used in the standard .NET for Windows Store apps.</span></span>  <span data-ttu-id="0871e-223">WinINet 並未支援 <xref:System.Net.Http.HttpClientHandler> 類別支援的所有組態選項。</span><span class="sxs-lookup"><span data-stu-id="0871e-223">WinINet doesn't support all the configuration options that the <xref:System.Net.Http.HttpClientHandler> class supports.</span></span>  <span data-ttu-id="0871e-224">因此：</span><span class="sxs-lookup"><span data-stu-id="0871e-224">As a result:</span></span>

- <span data-ttu-id="0871e-225">某些功能屬性會在 .NET Native 上傳回 <xref:System.Net.Http.HttpClientHandler> `false` ，而這些屬性會 `true` 在適用于 Windows Store 應用程式的標準 .net 中返回。</span><span class="sxs-lookup"><span data-stu-id="0871e-225">Some of the capability properties on <xref:System.Net.Http.HttpClientHandler> return `false` on .NET Native, whereas they return `true` in the standard .NET for Windows Store apps.</span></span>

- <span data-ttu-id="0871e-226">某些 `get` 設定屬性存取子在 .NET Native 上一律會傳回固定的值，此值與 Windows Store 應用程式的 .net 中預設可設定的值不同。</span><span class="sxs-lookup"><span data-stu-id="0871e-226">Some of the configuration property `get` accessors always return a fixed value on .NET Native that is different than the default configurable value in .NET for Windows Store apps.</span></span>

<span data-ttu-id="0871e-227">下列各小節會說明一些其他的行為差異。</span><span class="sxs-lookup"><span data-stu-id="0871e-227">Some additional behavior differences are covered in the following subsections.</span></span>

<span data-ttu-id="0871e-228">**Proxy**</span><span class="sxs-lookup"><span data-stu-id="0871e-228">**Proxy**</span></span>

<span data-ttu-id="0871e-229"><xref:Windows.Web.Http.Filters.HttpBaseProtocolFilter>類別不支援以每個要求為基礎來設定或覆寫 proxy。</span><span class="sxs-lookup"><span data-stu-id="0871e-229">The <xref:Windows.Web.Http.Filters.HttpBaseProtocolFilter> class doesn't support configuring or overriding the proxy on a per-request basis.</span></span>  <span data-ttu-id="0871e-230">這表示 .NET Native 上的所有要求都會使用系統設定的 proxy 伺服器或無 proxy 伺服器（視屬性的值而定） <xref:System.Net.Http.HttpClientHandler.UseProxy%2A?displayProperty=nameWithType> 。</span><span class="sxs-lookup"><span data-stu-id="0871e-230">This means that all requests on .NET Native use the system-configured proxy server or no proxy server, depending on the value of the <xref:System.Net.Http.HttpClientHandler.UseProxy%2A?displayProperty=nameWithType> property.</span></span>  <span data-ttu-id="0871e-231">在適用於 Windows 市集應用程式的 .NET 中，是由 <xref:System.Net.Http.HttpClientHandler.Proxy%2A?displayProperty=nameWithType> 屬性來定義 Proxy 伺服器。</span><span class="sxs-lookup"><span data-stu-id="0871e-231">In .NET for Windows Store apps, the proxy server is defined by the <xref:System.Net.Http.HttpClientHandler.Proxy%2A?displayProperty=nameWithType> property.</span></span>  <span data-ttu-id="0871e-232">在 .NET Native 上，將設定為以外的值會擲回 <xref:System.Net.Http.HttpClientHandler.Proxy%2A?displayProperty=nameWithType> 例外狀況 `null` <xref:System.PlatformNotSupportedException> 。</span><span class="sxs-lookup"><span data-stu-id="0871e-232">On .NET Native, setting the <xref:System.Net.Http.HttpClientHandler.Proxy%2A?displayProperty=nameWithType> to a value other than `null` throws a <xref:System.PlatformNotSupportedException> exception.</span></span>  <span data-ttu-id="0871e-233"><xref:System.Net.Http.HttpClientHandler.SupportsProxy%2A?displayProperty=nameWithType>屬性 `false` 會在 .NET Native 上傳回，而會 `true` 在 Windows Store 應用程式的標準 .NET Framework 中返回。</span><span class="sxs-lookup"><span data-stu-id="0871e-233">The <xref:System.Net.Http.HttpClientHandler.SupportsProxy%2A?displayProperty=nameWithType> property returns `false` on .NET Native, whereas it returns `true` in the standard .NET Framework for Windows Store apps.</span></span>

<span data-ttu-id="0871e-234">**自動重新導向**</span><span class="sxs-lookup"><span data-stu-id="0871e-234">**Automatic redirection**</span></span>

<span data-ttu-id="0871e-235"><xref:Windows.Web.Http.Filters.HttpBaseProtocolFilter>類別不允許設定自動重新導向的數目上限。</span><span class="sxs-lookup"><span data-stu-id="0871e-235">The <xref:Windows.Web.Http.Filters.HttpBaseProtocolFilter> class doesn't allow the maximum number of automatic redirections to be configured.</span></span>  <span data-ttu-id="0871e-236">在適用於 Windows 市集應用程式的標準 .NET 中， <xref:System.Net.Http.HttpClientHandler.MaxAutomaticRedirections%2A?displayProperty=nameWithType> 屬性的值預設為 50，而且可以修改。</span><span class="sxs-lookup"><span data-stu-id="0871e-236">The value of the <xref:System.Net.Http.HttpClientHandler.MaxAutomaticRedirections%2A?displayProperty=nameWithType> property is 50 by default in the standard .NET for Windows Store apps and can be modified.</span></span> <span data-ttu-id="0871e-237">在 .NET Native 上，這個屬性的值是10，而且嘗試修改它會擲回 <xref:System.PlatformNotSupportedException> 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="0871e-237">On .NET Native, the value of this property is 10, and trying to modify it throws a <xref:System.PlatformNotSupportedException> exception.</span></span>  <span data-ttu-id="0871e-238"><xref:System.Net.Http.HttpClientHandler.SupportsRedirectConfiguration%2A?displayProperty=nameWithType>屬性 `false` 會在 .NET Native 上傳回，而會 `true` 在 .Net 中針對 Windows Store 應用程式傳回。</span><span class="sxs-lookup"><span data-stu-id="0871e-238">The <xref:System.Net.Http.HttpClientHandler.SupportsRedirectConfiguration%2A?displayProperty=nameWithType> property returns `false` on .NET Native, whereas it returns `true` in .NET for Windows Store apps.</span></span>

<span data-ttu-id="0871e-239">**自動解壓縮**</span><span class="sxs-lookup"><span data-stu-id="0871e-239">**Automatic decompression**</span></span>

<span data-ttu-id="0871e-240">適用於 Windows 市集應用程式的 .NET 可讓您將 <xref:System.Net.Http.HttpClientHandler.AutomaticDecompression%2A?displayProperty=nameWithType> 屬性設為 <xref:System.Net.DecompressionMethods.Deflate>、 <xref:System.Net.DecompressionMethods.GZip>、 <xref:System.Net.DecompressionMethods.Deflate> 和 <xref:System.Net.DecompressionMethods.GZip>同時設定，或是設為 <xref:System.Net.DecompressionMethods.None>。</span><span class="sxs-lookup"><span data-stu-id="0871e-240">.NET for Windows Store apps allows you to set the <xref:System.Net.Http.HttpClientHandler.AutomaticDecompression%2A?displayProperty=nameWithType> property to <xref:System.Net.DecompressionMethods.Deflate>, <xref:System.Net.DecompressionMethods.GZip>, both <xref:System.Net.DecompressionMethods.Deflate> and <xref:System.Net.DecompressionMethods.GZip>, or <xref:System.Net.DecompressionMethods.None>.</span></span>  <span data-ttu-id="0871e-241">.NET Native 僅支援 <xref:System.Net.DecompressionMethods.Deflate> 搭配 <xref:System.Net.DecompressionMethods.GZip> 、或 <xref:System.Net.DecompressionMethods.None> 。</span><span class="sxs-lookup"><span data-stu-id="0871e-241">.NET Native only supports <xref:System.Net.DecompressionMethods.Deflate> together with <xref:System.Net.DecompressionMethods.GZip>, or <xref:System.Net.DecompressionMethods.None>.</span></span>  <span data-ttu-id="0871e-242">嘗試以無訊息模式將 <xref:System.Net.Http.HttpClientHandler.AutomaticDecompression%2A> 屬性單獨設為 <xref:System.Net.DecompressionMethods.Deflate> 或 <xref:System.Net.DecompressionMethods.GZip> ，會將其設為同時使用 <xref:System.Net.DecompressionMethods.Deflate> 和 <xref:System.Net.DecompressionMethods.GZip>。</span><span class="sxs-lookup"><span data-stu-id="0871e-242">Trying to set the <xref:System.Net.Http.HttpClientHandler.AutomaticDecompression%2A> property to either <xref:System.Net.DecompressionMethods.Deflate> or <xref:System.Net.DecompressionMethods.GZip> alone silently sets it to both <xref:System.Net.DecompressionMethods.Deflate> and <xref:System.Net.DecompressionMethods.GZip>.</span></span>

<span data-ttu-id="0871e-243">**餅乾**</span><span class="sxs-lookup"><span data-stu-id="0871e-243">**Cookies**</span></span>

<span data-ttu-id="0871e-244"><xref:System.Net.Http.HttpClient> 和 WinINet 會同時執行 Cookie 處理作業。</span><span class="sxs-lookup"><span data-stu-id="0871e-244">Cookie handling is performed simultaneously by <xref:System.Net.Http.HttpClient> and WinINet.</span></span>  <span data-ttu-id="0871e-245"><xref:System.Net.CookieContainer> 所產生的 Cookie 會與 WinINet Cookie 快取中的 Cookie 合併。</span><span class="sxs-lookup"><span data-stu-id="0871e-245">Cookies from the <xref:System.Net.CookieContainer> are combined with cookies in the WinINet cookie cache.</span></span>  <span data-ttu-id="0871e-246">從 <xref:System.Net.CookieContainer> 移除 Cookie 會防止 <xref:System.Net.Http.HttpClient> 傳送 Cookie，但如果 WinINet 已經看到 Cookie，而且使用者沒有刪除 Cookie，WinINet 就會加以傳送。</span><span class="sxs-lookup"><span data-stu-id="0871e-246">Removing a cookie from <xref:System.Net.CookieContainer> prevents <xref:System.Net.Http.HttpClient> from sending the cookie, but if the cookie was already seen by WinINet, and cookies weren't deleted by the user, WinINet sends it.</span></span>  <span data-ttu-id="0871e-247">若要使用 <xref:System.Net.Http.HttpClient>, <xref:System.Net.Http.HttpClientHandler>或 <xref:System.Net.CookieContainer> API，以程式設計方式將 Cookie 從 WinINet 移除是不可能的。</span><span class="sxs-lookup"><span data-stu-id="0871e-247">It isn't possible to programmatically remove a cookie from WinINet by using the <xref:System.Net.Http.HttpClient>, <xref:System.Net.Http.HttpClientHandler>, or <xref:System.Net.CookieContainer> API.</span></span>  <span data-ttu-id="0871e-248">將 <xref:System.Net.Http.HttpClientHandler.UseCookies%2A?displayProperty=nameWithType> 屬性設為 `false` 只會導致 <xref:System.Net.Http.HttpClient> 停止傳送 Cookie，WinINet 還是會在要求中包含其 Cookie。</span><span class="sxs-lookup"><span data-stu-id="0871e-248">Setting the <xref:System.Net.Http.HttpClientHandler.UseCookies%2A?displayProperty=nameWithType> property to `false` causes only <xref:System.Net.Http.HttpClient> to stop sending cookies; WinINet might still include its cookies in the request.</span></span>

<span data-ttu-id="0871e-249">**認證**</span><span class="sxs-lookup"><span data-stu-id="0871e-249">**Credentials**</span></span>

<span data-ttu-id="0871e-250">在適用於 Windows 市集應用程式的 .NET 中， <xref:System.Net.Http.HttpClientHandler.UseDefaultCredentials%2A?displayProperty=nameWithType> 和 <xref:System.Net.Http.HttpClientHandler.Credentials%2A?displayProperty=nameWithType> 屬性會獨立運作。</span><span class="sxs-lookup"><span data-stu-id="0871e-250">In .NET for Windows Store apps, the <xref:System.Net.Http.HttpClientHandler.UseDefaultCredentials%2A?displayProperty=nameWithType> and <xref:System.Net.Http.HttpClientHandler.Credentials%2A?displayProperty=nameWithType> properties work independently.</span></span>  <span data-ttu-id="0871e-251">此外， <xref:System.Net.Http.HttpClientHandler.Credentials%2A> 屬性會接受實作 <xref:System.Net.ICredentials> 介面的任何物件。</span><span class="sxs-lookup"><span data-stu-id="0871e-251">Additionally, the <xref:System.Net.Http.HttpClientHandler.Credentials%2A> property accepts any object that implements the <xref:System.Net.ICredentials> interface.</span></span>  <span data-ttu-id="0871e-252">在 .NET Native 中，將 <xref:System.Net.Http.HttpClientHandler.UseDefaultCredentials%2A> 屬性設定為 `true` 會使 <xref:System.Net.Http.HttpClientHandler.Credentials%2A> 屬性成為 `null` 。</span><span class="sxs-lookup"><span data-stu-id="0871e-252">In .NET Native, setting the <xref:System.Net.Http.HttpClientHandler.UseDefaultCredentials%2A> property to `true` causes the <xref:System.Net.Http.HttpClientHandler.Credentials%2A> property to become `null`.</span></span>  <span data-ttu-id="0871e-253">此外， <xref:System.Net.Http.HttpClientHandler.Credentials%2A> 屬性只能設為 `null`、 <xref:System.Net.CredentialCache.DefaultCredentials%2A>，或是 <xref:System.Net.NetworkCredential>類型的物件。</span><span class="sxs-lookup"><span data-stu-id="0871e-253">In addition, the <xref:System.Net.Http.HttpClientHandler.Credentials%2A> property can be set only to `null`, <xref:System.Net.CredentialCache.DefaultCredentials%2A>, or an object of type <xref:System.Net.NetworkCredential>.</span></span>  <span data-ttu-id="0871e-254">將任何其他 <xref:System.Net.ICredentials> 物件 (最常用的是 <xref:System.Net.CredentialCache>) 指派給 <xref:System.Net.Http.HttpClientHandler.Credentials%2A> 屬性會擲回 <xref:System.PlatformNotSupportedException>。</span><span class="sxs-lookup"><span data-stu-id="0871e-254">Assigning any other <xref:System.Net.ICredentials> object, the most popular of which is <xref:System.Net.CredentialCache>, to the <xref:System.Net.Http.HttpClientHandler.Credentials%2A> property throws a <xref:System.PlatformNotSupportedException>.</span></span>

<span data-ttu-id="0871e-255">**其他不受支援或不可設定的功能**</span><span class="sxs-lookup"><span data-stu-id="0871e-255">**Other unsupported or unconfigurable features**</span></span>

<span data-ttu-id="0871e-256">在 .NET Native：</span><span class="sxs-lookup"><span data-stu-id="0871e-256">In .NET Native:</span></span>

- <span data-ttu-id="0871e-257"><xref:System.Net.Http.HttpClientHandler.ClientCertificateOptions%2A?displayProperty=nameWithType> 屬性的值一律為 <xref:System.Net.Http.ClientCertificateOption.Automatic>。</span><span class="sxs-lookup"><span data-stu-id="0871e-257">The value of the <xref:System.Net.Http.HttpClientHandler.ClientCertificateOptions%2A?displayProperty=nameWithType> property is always <xref:System.Net.Http.ClientCertificateOption.Automatic>.</span></span>  <span data-ttu-id="0871e-258">在適用於 Windows 市集應用程式的 .NET 中，預設值為 <xref:System.Net.Http.ClientCertificateOption.Manual>。</span><span class="sxs-lookup"><span data-stu-id="0871e-258">In .NET for Windows Store apps, the default is <xref:System.Net.Http.ClientCertificateOption.Manual>.</span></span>

- <span data-ttu-id="0871e-259"><xref:System.Net.Http.HttpClientHandler.MaxRequestContentBufferSize%2A?displayProperty=nameWithType> 屬性不可設定。</span><span class="sxs-lookup"><span data-stu-id="0871e-259">The <xref:System.Net.Http.HttpClientHandler.MaxRequestContentBufferSize%2A?displayProperty=nameWithType> property isn't configurable.</span></span>

- <span data-ttu-id="0871e-260"><xref:System.Net.Http.HttpClientHandler.PreAuthenticate%2A?displayProperty=nameWithType> 屬性一律為 `true`。</span><span class="sxs-lookup"><span data-stu-id="0871e-260">The <xref:System.Net.Http.HttpClientHandler.PreAuthenticate%2A?displayProperty=nameWithType> property is always `true`.</span></span>  <span data-ttu-id="0871e-261">在適用於 Windows 市集應用程式的 .NET 中，預設值為 `false`。</span><span class="sxs-lookup"><span data-stu-id="0871e-261">In .NET for Windows Store apps, the default is `false`.</span></span>

- <span data-ttu-id="0871e-262">系統會將回應中的 `SetCookie2` 標頭視為過時而將它忽略。</span><span class="sxs-lookup"><span data-stu-id="0871e-262">The `SetCookie2` header in responses is ignored as obsolete.</span></span>

<a name="Interop"></a>
### <a name="interop-differences"></a><span data-ttu-id="0871e-263">Interop 的差異</span><span class="sxs-lookup"><span data-stu-id="0871e-263">Interop differences</span></span>
 <span data-ttu-id="0871e-264">**已被取代的 API**</span><span class="sxs-lookup"><span data-stu-id="0871e-264">**Deprecated APIs**</span></span>

 <span data-ttu-id="0871e-265">有些與 Managed 程式碼交互操作的不常用 API 已被取代。</span><span class="sxs-lookup"><span data-stu-id="0871e-265">A number of infrequently used APIs for interoperability with managed code have been deprecated.</span></span> <span data-ttu-id="0871e-266">搭配 .NET Native 使用時，這些 Api 可能會擲回 <xref:System.NotImplementedException> 或 <xref:System.PlatformNotSupportedException> 例外狀況，或導致編譯器錯誤。</span><span class="sxs-lookup"><span data-stu-id="0871e-266">When used with .NET Native, these APIs may throw a <xref:System.NotImplementedException> or <xref:System.PlatformNotSupportedException> exception, or result in a compiler error.</span></span> <span data-ttu-id="0871e-267">在適用於 Windows 市集應用程式的 .NET 中，這些 API 會標示為已過時，但是呼叫這些 API 會產生編譯器警告，而不是編譯器錯誤。</span><span class="sxs-lookup"><span data-stu-id="0871e-267">In .NET for Windows Store apps, these APIs are marked as obsolete, although calling them generates a compiler warning rather than a compiler error.</span></span>

 <span data-ttu-id="0871e-268">封送處理已淘汰的 Api `VARIANT` 包括：</span><span class="sxs-lookup"><span data-stu-id="0871e-268">Deprecated APIs for `VARIANT` marshaling include:</span></span>

- <xref:System.Runtime.InteropServices.BStrWrapper?displayProperty=nameWithType>
- <xref:System.Runtime.InteropServices.CurrencyWrapper?displayProperty=nameWithType>
- <xref:System.Runtime.InteropServices.DispatchWrapper?displayProperty=nameWithType>
- <xref:System.Runtime.InteropServices.ErrorWrapper?displayProperty=nameWithType>
- <xref:System.Runtime.InteropServices.UnknownWrapper?displayProperty=nameWithType>
- <xref:System.Runtime.InteropServices.VariantWrapper?displayProperty=nameWithType>
- <xref:System.Runtime.InteropServices.UnmanagedType.IDispatch?displayProperty=nameWithType>
- <xref:System.Runtime.InteropServices.UnmanagedType.SafeArray?displayProperty=nameWithType>
- <xref:System.Runtime.InteropServices.VarEnum?displayProperty=nameWithType>

 <span data-ttu-id="0871e-269"><xref:System.Runtime.InteropServices.UnmanagedType.Struct?displayProperty=nameWithType> 受到支援，但在某些情況下會擲回例外狀況，例如搭配 [IDispatch](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch) 或 variant 使用時 `byref` 。</span><span class="sxs-lookup"><span data-stu-id="0871e-269"><xref:System.Runtime.InteropServices.UnmanagedType.Struct?displayProperty=nameWithType> is supported, but it throws an exception in some scenarios, such as when it is used with [IDispatch](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch) or `byref` variants.</span></span>

 <span data-ttu-id="0871e-270">[IDispatch](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch)支援的已淘汰 api 包括：</span><span class="sxs-lookup"><span data-stu-id="0871e-270">Deprecated APIs for [IDispatch](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch) support include:</span></span>

- <xref:System.Runtime.InteropServices.ClassInterfaceType.AutoDispatch?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.ClassInterfaceType.AutoDual?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.ComDefaultInterfaceAttribute?displayProperty=nameWithType>

<span data-ttu-id="0871e-271">傳統 COM 事件的已淘汰 Api 包括：</span><span class="sxs-lookup"><span data-stu-id="0871e-271">Deprecated APIs for classic COM events include:</span></span>

- <xref:System.Runtime.InteropServices.ComEventsHelper?displayProperty=nameWithType>
- <xref:System.Runtime.InteropServices.ComSourceInterfacesAttribute>

<span data-ttu-id="0871e-272">介面中的已淘汰 Api <xref:System.Runtime.InteropServices.ICustomQueryInterface?displayProperty=nameWithType> （.NET Native 中不支援）包括：</span><span class="sxs-lookup"><span data-stu-id="0871e-272">Deprecated APIs in the <xref:System.Runtime.InteropServices.ICustomQueryInterface?displayProperty=nameWithType> interface, which isn't supported in .NET Native, include:</span></span>

- <span data-ttu-id="0871e-273"><xref:System.Runtime.InteropServices.ICustomQueryInterface?displayProperty=nameWithType> (所有成員) </span><span class="sxs-lookup"><span data-stu-id="0871e-273"><xref:System.Runtime.InteropServices.ICustomQueryInterface?displayProperty=nameWithType> (all members)</span></span>
- <span data-ttu-id="0871e-274"><xref:System.Runtime.InteropServices.CustomQueryInterfaceMode?displayProperty=nameWithType> (所有成員) </span><span class="sxs-lookup"><span data-stu-id="0871e-274"><xref:System.Runtime.InteropServices.CustomQueryInterfaceMode?displayProperty=nameWithType> (all members)</span></span>
- <span data-ttu-id="0871e-275"><xref:System.Runtime.InteropServices.CustomQueryInterfaceResult?displayProperty=nameWithType> (所有成員) </span><span class="sxs-lookup"><span data-stu-id="0871e-275"><xref:System.Runtime.InteropServices.CustomQueryInterfaceResult?displayProperty=nameWithType> (all members)</span></span>
- <xref:System.Runtime.InteropServices.Marshal.GetComInterfaceForObject%28System.Object%2CSystem.Type%2CSystem.Runtime.InteropServices.CustomQueryInterfaceMode%29?displayProperty=fullName>

<span data-ttu-id="0871e-276">其他不支援的 interop 功能包括：</span><span class="sxs-lookup"><span data-stu-id="0871e-276">Other unsupported interop features include:</span></span>

- <span data-ttu-id="0871e-277"><xref:System.Runtime.InteropServices.ICustomAdapter?displayProperty=nameWithType> (所有成員) </span><span class="sxs-lookup"><span data-stu-id="0871e-277"><xref:System.Runtime.InteropServices.ICustomAdapter?displayProperty=nameWithType> (all members)</span></span>
- <span data-ttu-id="0871e-278"><xref:System.Runtime.InteropServices.SafeBuffer?displayProperty=nameWithType> (所有成員) </span><span class="sxs-lookup"><span data-stu-id="0871e-278"><xref:System.Runtime.InteropServices.SafeBuffer?displayProperty=nameWithType> (all members)</span></span>
- <xref:System.Runtime.InteropServices.UnmanagedType.Currency?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.UnmanagedType.VBByRefStr?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.UnmanagedType.AnsiBStr?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.UnmanagedType.AsAny?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.UnmanagedType.CustomMarshaler?displayProperty=fullName>

 <span data-ttu-id="0871e-279">很少使用的封送處理 Api：</span><span class="sxs-lookup"><span data-stu-id="0871e-279">Rarely used marshaling APIs:</span></span>

- <xref:System.Runtime.InteropServices.Marshal.ReadByte%28System.Object%2CSystem.Int32%29?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.Marshal.ReadInt16%28System.Object%2CSystem.Int32%29?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.Marshal.ReadInt32%28System.Object%2CSystem.Int32%29?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.Marshal.ReadInt64%28System.Object%2CSystem.Int32%29?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.Marshal.ReadIntPtr%28System.Object%2CSystem.Int32%29?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.Marshal.WriteByte%28System.Object%2CSystem.Int32%2CSystem.Byte%29?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.Marshal.WriteInt16%28System.Object%2CSystem.Int32%2CSystem.Int16%29?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.Marshal.WriteInt32%28System.Object%2CSystem.Int32%2CSystem.Int32%29?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.Marshal.WriteInt64%28System.Object%2CSystem.Int32%2CSystem.Int64%29?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.Marshal.WriteIntPtr%28System.Object%2CSystem.Int32%2CSystem.IntPtr%29?displayProperty=fullName>

 <span data-ttu-id="0871e-280">**平台叫用和 COM interop 相容性**</span><span class="sxs-lookup"><span data-stu-id="0871e-280">**Platform invoke and COM interop compatibility**</span></span>

 <span data-ttu-id="0871e-281">.NET Native 中仍支援大部分的平台叫用和 COM interop 案例。</span><span class="sxs-lookup"><span data-stu-id="0871e-281">Most platform invoke and COM interop scenarios are still supported in .NET Native.</span></span> <span data-ttu-id="0871e-282">特別是仍支援與 Windows 執行階段 (WinRT) API 的所有交互操作性，以及 Windows 執行階段需要的所有封送處理。</span><span class="sxs-lookup"><span data-stu-id="0871e-282">In particular, all interoperability with Windows Runtime (WinRT) APIs and all marshaling required for the Windows Runtime is supported.</span></span> <span data-ttu-id="0871e-283">其中包括對下列項目的封送處理支援：</span><span class="sxs-lookup"><span data-stu-id="0871e-283">This includes marshaling support for:</span></span>

- <span data-ttu-id="0871e-284">陣列 (包括 <xref:System.Runtime.InteropServices.UnmanagedType.ByValArray?displayProperty=nameWithType>)</span><span class="sxs-lookup"><span data-stu-id="0871e-284">Arrays (including <xref:System.Runtime.InteropServices.UnmanagedType.ByValArray?displayProperty=nameWithType>)</span></span>

- `BStr`

- <span data-ttu-id="0871e-285">委派</span><span class="sxs-lookup"><span data-stu-id="0871e-285">Delegates</span></span>

- <span data-ttu-id="0871e-286">Unicode、ANSI 和 HSTRING (字串) </span><span class="sxs-lookup"><span data-stu-id="0871e-286">Strings (Unicode, ANSI, and HSTRING)</span></span>

- <span data-ttu-id="0871e-287">結構 (`byref` 和 `byval`)</span><span class="sxs-lookup"><span data-stu-id="0871e-287">Structs (`byref` and `byval`)</span></span>

- <span data-ttu-id="0871e-288">等位</span><span class="sxs-lookup"><span data-stu-id="0871e-288">Unions</span></span>

- <span data-ttu-id="0871e-289">Win32 控制代碼</span><span class="sxs-lookup"><span data-stu-id="0871e-289">Win32 handles</span></span>

- <span data-ttu-id="0871e-290">所有 WinRT 結構</span><span class="sxs-lookup"><span data-stu-id="0871e-290">All WinRT constructs</span></span>

- <span data-ttu-id="0871e-291">部分支援封送處理變異數類型。</span><span class="sxs-lookup"><span data-stu-id="0871e-291">Partial support for marshaling variant types.</span></span> <span data-ttu-id="0871e-292">支援下列功能：</span><span class="sxs-lookup"><span data-stu-id="0871e-292">The following are supported:</span></span>

  - <xref:System.Boolean>

  - <xref:System.Byte>

  - <xref:System.Decimal>

  - <xref:System.Double>

  - <xref:System.Int16>

  - <xref:System.Int32>

  - <xref:System.Int64>

  - <xref:System.SByte>

  - <xref:System.Single>

  - <xref:System.UInt16>

  - <xref:System.UInt32>

  - <xref:System.UInt64>

  - `BStr`

  - [<span data-ttu-id="0871e-293">IUnknown</span><span class="sxs-lookup"><span data-stu-id="0871e-293">IUnknown</span></span>](/windows/desktop/api/unknwn/nn-unknwn-iunknown)

<span data-ttu-id="0871e-294">不過，.NET Native 不支援下列各項：</span><span class="sxs-lookup"><span data-stu-id="0871e-294">However, .NET Native doesn't support the following:</span></span>

- <span data-ttu-id="0871e-295">使用傳統 COM 事件</span><span class="sxs-lookup"><span data-stu-id="0871e-295">Using classic COM events</span></span>

- <span data-ttu-id="0871e-296">在 Managed 類型上實作 <xref:System.Runtime.InteropServices.ICustomQueryInterface?displayProperty=nameWithType> 介面</span><span class="sxs-lookup"><span data-stu-id="0871e-296">Implementing the <xref:System.Runtime.InteropServices.ICustomQueryInterface?displayProperty=nameWithType> interface on a managed type</span></span>

- <span data-ttu-id="0871e-297">透過 [屬性，在 Managed 類型上實作](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch) IDispatch <xref:System.Runtime.InteropServices.ComDefaultInterfaceAttribute?displayProperty=nameWithType> 介面。</span><span class="sxs-lookup"><span data-stu-id="0871e-297">Implementing the [IDispatch](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch) interface on a managed type through the <xref:System.Runtime.InteropServices.ComDefaultInterfaceAttribute?displayProperty=nameWithType> attribute.</span></span> <span data-ttu-id="0871e-298">不過，您無法透過呼叫 COM 物件 `IDispatch` ，而且您的 managed 物件無法執行 `IDispatch` 。</span><span class="sxs-lookup"><span data-stu-id="0871e-298">However, you can't call COM objects through `IDispatch`, and your managed object can't implement `IDispatch`.</span></span>

<span data-ttu-id="0871e-299">不支援使用反映來叫用平台叫用方法。</span><span class="sxs-lookup"><span data-stu-id="0871e-299">Using reflection to invoke a platform invoke method isn't supported.</span></span> <span data-ttu-id="0871e-300">若要解除決這項限制，您可以將此方法呼叫包裝在另一個方法中，並改用反映來呼叫包裝函式。</span><span class="sxs-lookup"><span data-stu-id="0871e-300">You can work around this limitation by wrapping the method call in another method and using reflection to call the wrapper instead.</span></span>

<a name="APIs"></a>

### <a name="other-differences-from-net-apis-for-windows-store-apps"></a><span data-ttu-id="0871e-301">其他與適用於 Windows 市集應用程式的 .NET API 的差異</span><span class="sxs-lookup"><span data-stu-id="0871e-301">Other differences from .NET APIs for Windows Store apps</span></span>

<span data-ttu-id="0871e-302">本節列出 .NET Native 中不支援的其餘 Api。</span><span class="sxs-lookup"><span data-stu-id="0871e-302">This section lists the remaining APIs that aren't supported in .NET Native.</span></span> <span data-ttu-id="0871e-303">最大的不支援 Api 集合是 Windows Communication Foundation (WCF) Api。</span><span class="sxs-lookup"><span data-stu-id="0871e-303">The largest set of the unsupported APIs is the Windows Communication Foundation (WCF) APIs.</span></span>

<span data-ttu-id="0871e-304">**DataAnnotations (System.ComponentModel.DataAnnotations)**</span><span class="sxs-lookup"><span data-stu-id="0871e-304">**DataAnnotations (System.ComponentModel.DataAnnotations)**</span></span>

<span data-ttu-id="0871e-305"><xref:System.ComponentModel.DataAnnotations> <xref:System.ComponentModel.DataAnnotations.Schema> .NET Native 中不支援和命名空間中的類型。</span><span class="sxs-lookup"><span data-stu-id="0871e-305">The types in the <xref:System.ComponentModel.DataAnnotations> and <xref:System.ComponentModel.DataAnnotations.Schema> namespaces aren't supported in .NET Native.</span></span> <span data-ttu-id="0871e-306">這些類型包括適用于適用于 Windows 8 之 Windows Store 應用程式的 .NET 中的下列型別：</span><span class="sxs-lookup"><span data-stu-id="0871e-306">These include the following types that are present in .NET for Windows Store apps for Windows 8:</span></span>

- <xref:System.ComponentModel.DataAnnotations.AssociationAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.ConcurrencyCheckAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.CustomValidationAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.DataType?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.DataTypeAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.DisplayAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.DisplayColumnAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.DisplayFormatAttribute>
- <xref:System.ComponentModel.DataAnnotations.EditableAttribute>
- <xref:System.ComponentModel.DataAnnotations.EnumDataTypeAttribute>
- <xref:System.ComponentModel.DataAnnotations.FilterUIHintAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.KeyAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.RangeAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.RegularExpressionAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.RequiredAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.StringLengthAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.TimestampAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.UIHintAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.ValidationAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.ValidationContext?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.ValidationException?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.ValidationResult?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.Validator?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.Schema.DatabaseGeneratedAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.Schema.DatabaseGeneratedOption?displayProperty=nameWithType>

 <span data-ttu-id="0871e-307">**Visual Basic**</span><span class="sxs-lookup"><span data-stu-id="0871e-307">**Visual Basic**</span></span>

<span data-ttu-id="0871e-308">.NET Native 目前不支援 Visual Basic。</span><span class="sxs-lookup"><span data-stu-id="0871e-308">Visual Basic isn't currently supported in .NET Native.</span></span> <span data-ttu-id="0871e-309">和命名空間中的下列類型在 <xref:Microsoft.VisualBasic> <xref:Microsoft.VisualBasic.CompilerServices> .NET Native 中無法使用：</span><span class="sxs-lookup"><span data-stu-id="0871e-309">The following types in the <xref:Microsoft.VisualBasic> and <xref:Microsoft.VisualBasic.CompilerServices> namespaces aren't available in .NET Native:</span></span>

- <xref:Microsoft.VisualBasic.CallType?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Constants?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.HideModuleNameAttribute?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Strings?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.Conversions?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.DesignerGeneratedAttribute?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.IncompleteInitialization?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.NewLateBinding?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.ObjectFlowControl?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.ObjectFlowControl.ForLoopControl?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.Operators?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.OptionCompareAttribute?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.OptionTextAttribute?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.ProjectData?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.StandardModuleAttribute?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.StaticLocalInitFlag?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.Utils?displayProperty=nameWithType>

<span data-ttu-id="0871e-310">**反映內容 (System.Reflection.Context 命名空間)**</span><span class="sxs-lookup"><span data-stu-id="0871e-310">**Reflection Context (System.Reflection.Context namespace)**</span></span>

<span data-ttu-id="0871e-311"><xref:System.Reflection.Context.CustomReflectionContext?displayProperty=nameWithType>.NET Native 中不支援類別。</span><span class="sxs-lookup"><span data-stu-id="0871e-311">The <xref:System.Reflection.Context.CustomReflectionContext?displayProperty=nameWithType> class isn't supported in .NET Native.</span></span>

<span data-ttu-id="0871e-312">**RTC (System.Net.Http.Rtc)**</span><span class="sxs-lookup"><span data-stu-id="0871e-312">**RTC (System.Net.Http.Rtc)**</span></span>

<span data-ttu-id="0871e-313">`System.Net.Http.RtcRequestFactory`.NET Native 中不支援類別。</span><span class="sxs-lookup"><span data-stu-id="0871e-313">The `System.Net.Http.RtcRequestFactory` class isn't supported in .NET Native.</span></span>

<span data-ttu-id="0871e-314">**Windows Communication Foundation (WCF) (System.ServiceModel.\*)**</span><span class="sxs-lookup"><span data-stu-id="0871e-314">**Windows Communication Foundation (WCF) (System.ServiceModel.\*)**</span></span>

<span data-ttu-id="0871e-315">.NET Native 中不支援 [system.servicemodel. \* 命名空間](xref:System.ServiceModel) 中的類型。</span><span class="sxs-lookup"><span data-stu-id="0871e-315">The types in the [System.ServiceModel.\* namespaces](xref:System.ServiceModel) aren't supported in .NET Native.</span></span> <span data-ttu-id="0871e-316">其中包括下列類型：</span><span class="sxs-lookup"><span data-stu-id="0871e-316">These include the following types:</span></span>

- <xref:System.ServiceModel.ActionNotSupportedException?displayProperty=nameWithType>
- <xref:System.ServiceModel.BasicHttpBinding?displayProperty=nameWithType>
- <xref:System.ServiceModel.BasicHttpMessageCredentialType?displayProperty=nameWithType>
- <xref:System.ServiceModel.BasicHttpSecurity?displayProperty=nameWithType>
- <xref:System.ServiceModel.BasicHttpSecurityMode?displayProperty=nameWithType>
- <xref:System.ServiceModel.CallbackBehaviorAttribute?displayProperty=nameWithType>
- <xref:System.ServiceModel.ChannelFactory?displayProperty=nameWithType>
- <xref:System.ServiceModel.ChannelFactory%601?displayProperty=nameWithType>
- <xref:System.ServiceModel.ClientBase%601?displayProperty=nameWithType>
- <xref:System.ServiceModel.ClientBase%601.BeginOperationDelegate?displayProperty=nameWithType>
- <xref:System.ServiceModel.ClientBase%601.ChannelBase%601?displayProperty=nameWithType>
- <xref:System.ServiceModel.ClientBase%601.EndOperationDelegate?displayProperty=nameWithType>
- <xref:System.ServiceModel.ClientBase%601.InvokeAsyncCompletedEventArgs?displayProperty=nameWithType>
- <xref:System.ServiceModel.CommunicationException?displayProperty=nameWithType>
- <xref:System.ServiceModel.CommunicationObjectAbortedException?displayProperty=nameWithType>
- <xref:System.ServiceModel.CommunicationObjectFaultedException?displayProperty=nameWithType>
- <xref:System.ServiceModel.CommunicationState?displayProperty=nameWithType>
- <xref:System.ServiceModel.DataContractFormatAttribute?displayProperty=nameWithType>
- <xref:System.ServiceModel.DnsEndpointIdentity?displayProperty=nameWithType>
- <xref:System.ServiceModel.DuplexChannelFactory%601?displayProperty=nameWithType>
- <xref:System.ServiceModel.DuplexClientBase%601?displayProperty=nameWithType>
- <xref:System.ServiceModel.EndpointAddress?displayProperty=nameWithType>
- <xref:System.ServiceModel.EndpointAddressBuilder?displayProperty=nameWithType>
- <xref:System.ServiceModel.EndpointIdentity?displayProperty=nameWithType>
- <xref:System.ServiceModel.EndpointNotFoundException?displayProperty=nameWithType>
- <xref:System.ServiceModel.EnvelopeVersion?displayProperty=nameWithType>
- <xref:System.ServiceModel.ExceptionDetail?displayProperty=nameWithType>
- <xref:System.ServiceModel.FaultCode?displayProperty=nameWithType>
- <xref:System.ServiceModel.FaultContractAttribute?displayProperty=nameWithType>
- <xref:System.ServiceModel.FaultException?displayProperty=nameWithType>
- <xref:System.ServiceModel.FaultException%601?displayProperty=nameWithType>
- <xref:System.ServiceModel.FaultReason?displayProperty=nameWithType>
- <xref:System.ServiceModel.FaultReasonText?displayProperty=nameWithType>
- <xref:System.ServiceModel.HttpBindingBase?displayProperty=nameWithType>
- <xref:System.ServiceModel.HttpClientCredentialType?displayProperty=nameWithType>
- <xref:System.ServiceModel.HttpTransportSecurity?displayProperty=nameWithType>
- <xref:System.ServiceModel.IClientChannel?displayProperty=nameWithType>
- <xref:System.ServiceModel.ICommunicationObject?displayProperty=nameWithType>
- <xref:System.ServiceModel.IContextChannel?displayProperty=nameWithType>
- <xref:System.ServiceModel.IDefaultCommunicationTimeouts?displayProperty=nameWithType>
- <xref:System.ServiceModel.IExtensibleObject%601?displayProperty=nameWithType>
- <xref:System.ServiceModel.IExtension%601?displayProperty=nameWithType>
- <xref:System.ServiceModel.IExtensionCollection%601?displayProperty=nameWithType>
- <xref:System.ServiceModel.InstanceContext?displayProperty=nameWithType>
- <xref:System.ServiceModel.InvalidMessageContractException?displayProperty=nameWithType>
- <xref:System.ServiceModel.MessageBodyMemberAttribute?displayProperty=nameWithType>
- <xref:System.ServiceModel.MessageContractAttribute?displayProperty=nameWithType>
- <xref:System.ServiceModel.MessageContractMemberAttribute?displayProperty=nameWithType>
- <xref:System.ServiceModel.MessageCredentialType?displayProperty=nameWithType>
- <xref:System.ServiceModel.MessageHeader%601?displayProperty=nameWithType>
- <xref:System.ServiceModel.MessageHeaderException?displayProperty=nameWithType>
- <xref:System.ServiceModel.MessageParameterAttribute?displayProperty=nameWithType>
- <xref:System.ServiceModel.MessageSecurityOverTcp?displayProperty=nameWithType>
- <xref:System.ServiceModel.MessageSecurityVersion?displayProperty=nameWithType>
- <xref:System.ServiceModel.NetHttpBinding?displayProperty=nameWithType>
- <xref:System.ServiceModel.NetHttpMessageEncoding?displayProperty=nameWithType>
- <xref:System.ServiceModel.NetTcpBinding?displayProperty=nameWithType>
- <xref:System.ServiceModel.NetTcpSecurity?displayProperty=nameWithType>
- <xref:System.ServiceModel.OperationContext?displayProperty=nameWithType>
- <xref:System.ServiceModel.OperationContextScope?displayProperty=nameWithType>
- <xref:System.ServiceModel.OperationContractAttribute?displayProperty=nameWithType>
- <xref:System.ServiceModel.OperationFormatStyle?displayProperty=nameWithType>
- <xref:System.ServiceModel.ProtocolException?displayProperty=nameWithType>
- <xref:System.ServiceModel.QuotaExceededException?displayProperty=nameWithType>
- <xref:System.ServiceModel.SecurityMode?displayProperty=nameWithType>
- <xref:System.ServiceModel.ServerTooBusyException?displayProperty=nameWithType>
- <xref:System.ServiceModel.ServiceActivationException?displayProperty=nameWithType>
- <xref:System.ServiceModel.ServiceContractAttribute?displayProperty=nameWithType>
- <xref:System.ServiceModel.ServiceKnownTypeAttribute?displayProperty=nameWithType>
- <xref:System.ServiceModel.SpnEndpointIdentity?displayProperty=nameWithType>
- <xref:System.ServiceModel.TcpClientCredentialType?displayProperty=nameWithType>
- <xref:System.ServiceModel.TcpTransportSecurity?displayProperty=nameWithType>
- <xref:System.ServiceModel.TransferMode?displayProperty=nameWithType>
- <xref:System.ServiceModel.UnknownMessageReceivedEventArgs?displayProperty=nameWithType>
- <xref:System.ServiceModel.UpnEndpointIdentity?displayProperty=nameWithType>
- <xref:System.ServiceModel.XmlSerializerFormatAttribute?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.AddressHeader?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.AddressHeaderCollection?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.AddressingVersion?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.ChannelManagerBase?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.ChannelParameterCollection?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.CommunicationObject?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.CompressionFormat?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.ConnectionOrientedTransportBindingElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.CustomBinding?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.FaultConverter?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.HttpRequestMessageProperty?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.HttpResponseMessageProperty?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.HttpsTransportBindingElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.HttpTransportBindingElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IChannel?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IChannelFactory?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IChannelFactory%601?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IDuplexChannel?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IDuplexSession?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IDuplexSessionChannel?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IHttpCookieContainerManager?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IInputChannel?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IInputSession?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IInputSessionChannel?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IMessageProperty?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IOutputChannel?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IOutputSession?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IOutputSessionChannel?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IRequestChannel?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IRequestSessionChannel?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.ISession?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.ISessionChannel%601?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.LocalClientSecuritySettings?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.Message?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.MessageBuffer?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.MessageEncoder?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.MessageEncoderFactory?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.MessageEncodingBindingElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.MessageFault?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.MessageHeader?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.MessageHeaderInfo?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.MessageHeaders?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.MessageProperties?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.MessageState?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.MessageVersion?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.RequestContext?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.SecurityBindingElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.SecurityHeaderLayout?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.SslStreamSecurityBindingElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.TcpConnectionPoolSettings?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.TcpTransportBindingElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.TransportBindingElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.TransportSecurityBindingElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.WebSocketTransportSettings?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.WebSocketTransportUsage?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.WindowsStreamSecurityBindingElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.ClientCredentials?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.ContractDescription?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.FaultDescription?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.FaultDescriptionCollection?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.IContractBehavior?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.IEndpointBehavior?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.IOperationBehavior?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.MessageBodyDescription?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.MessageDescription?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.MessageDescriptionCollection?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.MessageDirection?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.MessageHeaderDescription?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.MessageHeaderDescriptionCollection?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.MessagePartDescription?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.MessagePartDescriptionCollection?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.MessagePropertyDescription?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.MessagePropertyDescriptionCollection?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.OperationDescription?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.OperationDescriptionCollection?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.ServiceEndpoint?displayProperty=nameWithType>
- <xref:System.ServiceModel.Dispatcher.ClientOperation?displayProperty=nameWithType>
- <xref:System.ServiceModel.Dispatcher.ClientRuntime?displayProperty=nameWithType>
- <xref:System.ServiceModel.Dispatcher.DispatchOperation?displayProperty=nameWithType>
- <xref:System.ServiceModel.Dispatcher.DispatchRuntime?displayProperty=nameWithType>
- <xref:System.ServiceModel.Dispatcher.EndpointDispatcher?displayProperty=nameWithType>
- <xref:System.ServiceModel.Dispatcher.IClientMessageFormatter?displayProperty=nameWithType>
- <xref:System.ServiceModel.Dispatcher.IClientMessageInspector?displayProperty=nameWithType>
- <xref:System.ServiceModel.Dispatcher.IClientOperationSelector?displayProperty=nameWithType>
- <xref:System.ServiceModel.Dispatcher.IParameterInspector?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.BasicSecurityProfileVersion?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.HttpDigestClientCredential?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.MessageSecurityException?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.SecureConversationVersion?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.SecurityAccessDeniedException?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.SecurityPolicyVersion?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.SecurityVersion?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.TrustVersion?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.UserNamePasswordClientCredential?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.WindowsClientCredential?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.Tokens.SecureConversationSecurityTokenParameters?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.Tokens.SecurityTokenParameters?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.Tokens.SupportingTokenParameters?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.Tokens.UserNameSecurityTokenParameters?displayProperty=nameWithType>

### <a name="differences-in-serializers"></a><span data-ttu-id="0871e-317">序列化程式的差異</span><span class="sxs-lookup"><span data-stu-id="0871e-317">Differences in serializers</span></span>

<span data-ttu-id="0871e-318">下列差異與使用 <xref:System.Runtime.Serialization.DataContractSerializer>、 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>和 <xref:System.Xml.Serialization.XmlSerializer> 類別來進行序列化和還原序列化有關。</span><span class="sxs-lookup"><span data-stu-id="0871e-318">The following differences concern serialization and deserialization with the <xref:System.Runtime.Serialization.DataContractSerializer>, <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>, and <xref:System.Xml.Serialization.XmlSerializer> classes:</span></span>

- <span data-ttu-id="0871e-319">在 .NET Native 中， <xref:System.Runtime.Serialization.DataContractSerializer> 並 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> 無法序列化或還原序列化具有基類成員（其類型不是根序列化類型）的衍生類別。</span><span class="sxs-lookup"><span data-stu-id="0871e-319">In .NET Native, <xref:System.Runtime.Serialization.DataContractSerializer> and <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> fail to serialize or deserialize a derived class that has a base class member whose type isn't a root serialization type.</span></span> <span data-ttu-id="0871e-320">例如，在下列程式碼中，嘗試序列化或還原序列化 `Y` 會產生錯誤：</span><span class="sxs-lookup"><span data-stu-id="0871e-320">For example, in the following code, trying to serialize or deserialize `Y` results in an error:</span></span>

  [!code-csharp[ProjectN#10](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/compat3.cs#10)]

  <span data-ttu-id="0871e-321">序列化程式無法識別 `InnerType` 類型，因為在序列化期間，並未周遊基底類別的成員。</span><span class="sxs-lookup"><span data-stu-id="0871e-321">Type `InnerType` isn't known to the serializer, because the members of the base class aren't traversed during serialization.</span></span>

- <span data-ttu-id="0871e-322"><xref:System.Runtime.Serialization.DataContractSerializer> 和 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> 無法將實作 <xref:System.Collections.Generic.IEnumerable%601> 介面的類別或結構序列化。</span><span class="sxs-lookup"><span data-stu-id="0871e-322"><xref:System.Runtime.Serialization.DataContractSerializer> and <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> fail to serialize a class or structure that implements the <xref:System.Collections.Generic.IEnumerable%601> interface.</span></span> <span data-ttu-id="0871e-323">例如，下列的類型無法序列化或還原序列化：</span><span class="sxs-lookup"><span data-stu-id="0871e-323">For example, the following types fail to serialize or deserialize:</span></span>

- <span data-ttu-id="0871e-324"><xref:System.Xml.Serialization.XmlSerializer> 無法將下列物件值序列化，因為它不知道要序列化之物件的確切類型：</span><span class="sxs-lookup"><span data-stu-id="0871e-324"><xref:System.Xml.Serialization.XmlSerializer> fails to serialize the following object value, because it doesn't know the exact type of the object to be serialized:</span></span>

- <span data-ttu-id="0871e-325">如果已序列化物件的類型是<xref:System.Xml.Serialization.XmlSerializer> ，則 <xref:System.Xml.XmlQualifiedName>無法序列化或還原序列化。</span><span class="sxs-lookup"><span data-stu-id="0871e-325"><xref:System.Xml.Serialization.XmlSerializer> fails to serialize or deserialize if the type of the serialized object is <xref:System.Xml.XmlQualifiedName>.</span></span>

- <span data-ttu-id="0871e-326">所有序列化程式 (<xref:System.Runtime.Serialization.DataContractSerializer>、 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>和 <xref:System.Xml.Serialization.XmlSerializer>) 都無法為 <xref:System.Xml.Linq.XElement?displayProperty=nameWithType> 類型或是包含 <xref:System.Xml.Linq.XElement>的類型產生序列化程式碼，</span><span class="sxs-lookup"><span data-stu-id="0871e-326">All serializers (<xref:System.Runtime.Serialization.DataContractSerializer>, <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>, and <xref:System.Xml.Serialization.XmlSerializer>) fail to generate serialization code for type <xref:System.Xml.Linq.XElement?displayProperty=nameWithType> or for a type that contains <xref:System.Xml.Linq.XElement>.</span></span> <span data-ttu-id="0871e-327">而會顯示建置時間錯誤。</span><span class="sxs-lookup"><span data-stu-id="0871e-327">They display build-time errors instead.</span></span>

- <span data-ttu-id="0871e-328">無法保證序列化類型的下列建構函式能夠如預期般運作：</span><span class="sxs-lookup"><span data-stu-id="0871e-328">The following constructors of the serialization types aren't guaranteed to work as expected:</span></span>

  - <xref:System.Runtime.Serialization.DataContractSerializer.%23ctor%28System.Type%2CSystem.Collections.Generic.IEnumerable%7BSystem.Type%7D%29>

  - <xref:System.Runtime.Serialization.DataContractSerializer.%23ctor%28System.Type%2CSystem.Runtime.Serialization.DataContractSerializerSettings%29>

  - <xref:System.Runtime.Serialization.DataContractSerializer.%23ctor%28System.Type%2CSystem.String%2CSystem.String%2CSystem.Collections.Generic.IEnumerable%7BSystem.Type%7D%29>

  - <xref:System.Runtime.Serialization.DataContractSerializer.%23ctor%28System.Type%2CSystem.Xml.XmlDictionaryString%2CSystem.Xml.XmlDictionaryString%2CSystem.Collections.Generic.IEnumerable%7BSystem.Type%7D%29>

  - <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer.%23ctor%28System.Type%2CSystem.Runtime.Serialization.Json.DataContractJsonSerializerSettings%29>

  - <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer.%23ctor%28System.Type%2CSystem.Collections.Generic.IEnumerable%7BSystem.Type%7D%29>

  - <xref:System.Xml.Serialization.XmlSerializer.%23ctor%28System.Type%2CSystem.String%29>

  - <xref:System.Xml.Serialization.XmlSerializer.%23ctor%28System.Type%2CSystem.Type%5B%5D%29>

  - <xref:System.Xml.Serialization.XmlSerializer.%23ctor%28System.Type%2CSystem.Xml.Serialization.XmlAttributeOverrides%29>

  - <xref:System.Xml.Serialization.XmlSerializer.%23ctor%28System.Type%2CSystem.Xml.Serialization.XmlRootAttribute%29>

  - <xref:System.Xml.Serialization.XmlSerializer.%23ctor%28System.Type%2CSystem.Xml.Serialization.XmlAttributeOverrides%2CSystem.Type%5B%5D%2CSystem.Xml.Serialization.XmlRootAttribute%2CSystem.String%29>

- <span data-ttu-id="0871e-329">如果類型中有使用下列任何屬性的方法，則<xref:System.Xml.Serialization.XmlSerializer> 無法為該類型產生程式碼：</span><span class="sxs-lookup"><span data-stu-id="0871e-329"><xref:System.Xml.Serialization.XmlSerializer> fails to generate code for a type that has methods attributed with any of the following attributes:</span></span>

  - <xref:System.Runtime.Serialization.OnSerializingAttribute>

  - <xref:System.Runtime.Serialization.OnSerializedAttribute>

  - <xref:System.Runtime.Serialization.OnDeserializingAttribute>

  - <xref:System.Runtime.Serialization.OnDeserializedAttribute>

- <span data-ttu-id="0871e-330"><xref:System.Xml.Serialization.XmlSerializer> 不接受 <xref:System.Xml.Serialization.IXmlSerializable> 自訂序列化介面。</span><span class="sxs-lookup"><span data-stu-id="0871e-330"><xref:System.Xml.Serialization.XmlSerializer> doesn't honor the <xref:System.Xml.Serialization.IXmlSerializable> custom serialization interface.</span></span> <span data-ttu-id="0871e-331">如果您有實作這個介面的類別， <xref:System.Xml.Serialization.XmlSerializer> 會將該類型視為簡單的 CLR 物件 (POCO) 類型，並且只將其公開屬性序列化。</span><span class="sxs-lookup"><span data-stu-id="0871e-331">If you have a class that implements this interface, <xref:System.Xml.Serialization.XmlSerializer> considers the type a plain old CLR object (POCO) type and serializes only its public properties.</span></span>

- <span data-ttu-id="0871e-332">將純文字 <xref:System.Exception> 物件序列化無法與和搭配使用 <xref:System.Runtime.Serialization.DataContractSerializer> <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> 。</span><span class="sxs-lookup"><span data-stu-id="0871e-332">Serializing a plain <xref:System.Exception> object doesn't work well with <xref:System.Runtime.Serialization.DataContractSerializer> and <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>.</span></span>

<a name="VS"></a>

## <a name="visual-studio-differences"></a><span data-ttu-id="0871e-333">Visual Studio 的差異</span><span class="sxs-lookup"><span data-stu-id="0871e-333">Visual Studio differences</span></span>

<span data-ttu-id="0871e-334">**例外狀況和偵錯**</span><span class="sxs-lookup"><span data-stu-id="0871e-334">**Exceptions and debugging**</span></span>

<span data-ttu-id="0871e-335">當您在偵錯工具中執行使用 .NET Native 編譯的應用程式時，會針對下列例外狀況類型啟用第一個可能發生的例外狀況：</span><span class="sxs-lookup"><span data-stu-id="0871e-335">When you're running apps compiled by using .NET Native in the debugger, first-chance exceptions are enabled for the following exception types:</span></span>

- <xref:System.MemberAccessException>

- <xref:System.TypeAccessException>

<span data-ttu-id="0871e-336">**建置應用程式**</span><span class="sxs-lookup"><span data-stu-id="0871e-336">**Building apps**</span></span>

<span data-ttu-id="0871e-337">使用 Visual Studio 預設使用的 x86 建置工具。</span><span class="sxs-lookup"><span data-stu-id="0871e-337">Use the x86 build tools that are used by default by Visual Studio.</span></span> <span data-ttu-id="0871e-338">我們不建議使用 AMD64 MSBuild 工具 (可以在 C:\Program Files (x86)\MSBuild\12.0\bin\amd64 中找到)；這些工具可能會造成組建問題。</span><span class="sxs-lookup"><span data-stu-id="0871e-338">We don't recommend using the AMD64 MSBuild tools, which are found in C:\Program Files (x86)\MSBuild\12.0\bin\amd64; these may create build problems.</span></span>

<span data-ttu-id="0871e-339">**分析工具**</span><span class="sxs-lookup"><span data-stu-id="0871e-339">**Profilers**</span></span>

- <span data-ttu-id="0871e-340">Visual Studio CPU 分析工具和 XAML 記憶體分析工具不會正確顯示 Just-My-Code。</span><span class="sxs-lookup"><span data-stu-id="0871e-340">The Visual Studio CPU Profiler and XAML Memory Profiler don't display Just-My-Code correctly.</span></span>

- <span data-ttu-id="0871e-341">XAML 記憶體分析工具不會準確地顯示 Managed 堆積資料。</span><span class="sxs-lookup"><span data-stu-id="0871e-341">The XAML Memory Profiler doesn't accurately display managed heap data.</span></span>

- <span data-ttu-id="0871e-342">CPU 分析工具不會正確地識別模組，並且會顯示具有前置詞的函式名稱。</span><span class="sxs-lookup"><span data-stu-id="0871e-342">The CPU Profiler doesn't correctly identify modules, and displays prefixed function names.</span></span>

<span data-ttu-id="0871e-343">**單元測試程式庫專案**</span><span class="sxs-lookup"><span data-stu-id="0871e-343">**Unit Test Library projects**</span></span>

<span data-ttu-id="0871e-344">不支援在 Windows Store 應用程式專案的單元測試程式庫上啟用 .NET Native，並且會導致專案無法建立。</span><span class="sxs-lookup"><span data-stu-id="0871e-344">Enabling .NET Native on a Unit Test Library for a Windows Store apps project isn't supported and causes the project to fail to build.</span></span>

## <a name="see-also"></a><span data-ttu-id="0871e-345">另請參閱</span><span class="sxs-lookup"><span data-stu-id="0871e-345">See also</span></span>

- [<span data-ttu-id="0871e-346">快速入門</span><span class="sxs-lookup"><span data-stu-id="0871e-346">Getting Started</span></span>](getting-started-with-net-native.md)
- [<span data-ttu-id="0871e-347">執行階段指示詞 (rd.xml) 組態檔參考</span><span class="sxs-lookup"><span data-stu-id="0871e-347">Runtime Directives (rd.xml) Configuration File Reference</span></span>](runtime-directives-rd-xml-configuration-file-reference.md)
- <span data-ttu-id="0871e-348">[適用于 Windows Store 應用程式的 .NET 總覽](/previous-versions/windows/apps/br230302(v=vs.140))</span><span class="sxs-lookup"><span data-stu-id="0871e-348">[.NET For Windows Store apps overview](/previous-versions/windows/apps/br230302(v=vs.140))</span></span>
- [<span data-ttu-id="0871e-349">適用於 Windows 市集應用程式和 Windows 執行階段的 .NET Framework 支援</span><span class="sxs-lookup"><span data-stu-id="0871e-349">.NET Framework Support for Windows Store Apps and Windows Runtime</span></span>](../../standard/cross-platform/support-for-windows-store-apps-and-windows-runtime.md)
