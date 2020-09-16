---
title: 預設的封送處理行為
description: 瞭解 .NET 中的預設封送處理行為。 使用 interop 封送處理來檢查記憶體管理，並查看類別、委派和實數值型別的預設封送處理。
ms.date: 06/26/2018
dev_langs:
- csharp
- vb
helpviewer_keywords:
- interop marshaling, default
- interoperation with unmanaged code, marshaling
- marshaling behavior
ms.assetid: c0a9bcdf-3df8-4db3-b1b6-abbdb2af809a
ms.openlocfilehash: f2a508b87d2f4a9ad92bc0f27fc44d74d8e916d3
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90555272"
---
# <a name="default-marshaling-behavior"></a><span data-ttu-id="23688-104">預設的封送處理行為</span><span class="sxs-lookup"><span data-stu-id="23688-104">Default Marshaling Behavior</span></span>
<span data-ttu-id="23688-105">Interop 封送處理會依據規則作業，這些規則指定與方法參數關聯的資料在 Managed 和 Unmanaged 記憶體之間傳遞時的運作方式。</span><span class="sxs-lookup"><span data-stu-id="23688-105">Interop marshaling operates on rules that dictate how data associated with method parameters behaves as it passes between managed and unmanaged memory.</span></span> <span data-ttu-id="23688-106">這些內建規則會將這類封送處理活動當做資料類型轉換來控制；控制被呼叫者是否可以變更收到的資料，並將這些變更傳回給呼叫端；以及控制在哪些情況下，封送處理器會提供效能最佳化。</span><span class="sxs-lookup"><span data-stu-id="23688-106">These built-in rules control such marshaling activities as data type transformations, whether a callee can change data passed to it and return those changes to the caller, and under which circumstances the marshaler provides performance optimizations.</span></span>  
  
 <span data-ttu-id="23688-107">本節指出 Interop 封送處理服務的預設行為特性，</span><span class="sxs-lookup"><span data-stu-id="23688-107">This section identifies the default behavioral characteristics of the interop marshaling service.</span></span> <span data-ttu-id="23688-108">提供有關封送處理陣列、Boolean 類型、char 類型、委派、類別、物件、字串和結構的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="23688-108">It presents detailed information on marshaling arrays, Boolean types, char types, delegates, classes, objects, strings, and structures.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="23688-109">不支援封送處理泛型類型。</span><span class="sxs-lookup"><span data-stu-id="23688-109">Marshaling of generic types is not supported.</span></span> <span data-ttu-id="23688-110">如需詳細資訊，請參閱[使用泛型型別互通](/previous-versions/dotnet/netframework-4.0/ms229590(v=vs.100))。</span><span class="sxs-lookup"><span data-stu-id="23688-110">For more information see, [Interoperating Using Generic Types](/previous-versions/dotnet/netframework-4.0/ms229590(v=vs.100)).</span></span>  
  
## <a name="memory-management-with-the-interop-marshaler"></a><span data-ttu-id="23688-111">使用 Interop 封送處理器進行記憶體管理</span><span class="sxs-lookup"><span data-stu-id="23688-111">Memory management with the interop marshaler</span></span>  
 <span data-ttu-id="23688-112">Interop 封送處理器一律會嘗試釋放 Unmanaged 程式碼所配置的記憶體。</span><span class="sxs-lookup"><span data-stu-id="23688-112">The interop marshaler always attempts to free memory allocated by unmanaged code.</span></span> <span data-ttu-id="23688-113">這個行為使用 COM 記憶體管理規則進行編譯，但與管理原生 C++ 的規則不同。</span><span class="sxs-lookup"><span data-stu-id="23688-113">This behavior complies with COM memory management rules, but differs from the rules that govern native C++.</span></span>  
  
 <span data-ttu-id="23688-114">如果您使用平台叫用 (會自動釋放指標的記憶體) 時，預期原生 C++ 行為 (不釋放記憶體)，則會發生混淆。</span><span class="sxs-lookup"><span data-stu-id="23688-114">Confusion can arise if you anticipate native C++ behavior (no memory freeing) when using platform invoke, which automatically frees memory for pointers.</span></span> <span data-ttu-id="23688-115">例如，從 C++ DLL 呼叫下列 Unmanage 方法不會自動釋放任何記憶體。</span><span class="sxs-lookup"><span data-stu-id="23688-115">For example, calling the following unmanaged method from a C++ DLL does not automatically free any memory.</span></span>  
  
### <a name="unmanaged-signature"></a><span data-ttu-id="23688-116">Unmanaged 簽章</span><span class="sxs-lookup"><span data-stu-id="23688-116">Unmanaged signature</span></span>  
  
```cpp  
BSTR MethodOne (BSTR b) {  
     return b;  
}  
```  
  
 <span data-ttu-id="23688-117">不過，如果您將方法定義為平台叫用原型、將每個 **BSTR** 類型取代為 <xref:System.String> 類型，並呼叫 `MethodOne`，則 Common Language Runtime 會嘗試釋放 `b` 兩次。</span><span class="sxs-lookup"><span data-stu-id="23688-117">However, if you define the method as a platform invoke prototype, replace each **BSTR** type with a <xref:System.String> type, and call `MethodOne`, the common language runtime attempts to free `b` twice.</span></span> <span data-ttu-id="23688-118">您可以使用 <xref:System.IntPtr> 類型 (而不是 **String** 類型) 變更封送處理行為。</span><span class="sxs-lookup"><span data-stu-id="23688-118">You can change the marshaling behavior by using <xref:System.IntPtr> types rather than **String** types.</span></span>  
  
 <span data-ttu-id="23688-119">執行階段一律會使用 **CoTaskMemFree** 方法來釋放記憶體。</span><span class="sxs-lookup"><span data-stu-id="23688-119">The runtime always uses the **CoTaskMemFree** method to free memory.</span></span> <span data-ttu-id="23688-120">如果您正在使用的記憶體不是使用 **CoTaskMemAlloc** 方法配置，則必須使用 **IntPtr**，並使用適當方法手動釋放記憶體。</span><span class="sxs-lookup"><span data-stu-id="23688-120">If the memory you are working with was not allocated with the **CoTaskMemAlloc** method, you must use an **IntPtr** and free the memory manually using the appropriate method.</span></span> <span data-ttu-id="23688-121">同樣地，您可以在絕不應該釋放記憶體的情況下避免自動釋放記憶體；例如，從 Kernel32.dll 使用 **GetCommandLine** 函式，該函式會傳回核心記憶體的指標。</span><span class="sxs-lookup"><span data-stu-id="23688-121">Similarly, you can avoid automatic memory freeing in situations where memory should never be freed, such as when using the **GetCommandLine** function from Kernel32.dll, which returns a pointer to kernel memory.</span></span> <span data-ttu-id="23688-122">如需手動釋放記憶體的詳細資訊，請參閱[緩衝區範例](/previous-versions/dotnet/netframework-4.0/x3txb6xc(v=vs.100))。</span><span class="sxs-lookup"><span data-stu-id="23688-122">For details on manually freeing memory, see the [Buffers Sample](/previous-versions/dotnet/netframework-4.0/x3txb6xc(v=vs.100)).</span></span>  
  
## <a name="default-marshaling-for-classes"></a><span data-ttu-id="23688-123">類別的預設封送處理</span><span class="sxs-lookup"><span data-stu-id="23688-123">Default marshaling for classes</span></span>  
 <span data-ttu-id="23688-124">類別只能由 COM Interop 封送處理，並且一律會封送處理為介面。</span><span class="sxs-lookup"><span data-stu-id="23688-124">Classes can be marshaled only by COM interop and are always marshaled as interfaces.</span></span> <span data-ttu-id="23688-125">在某些情況下，用來封送處理類別的介面就是所謂的類別介面。</span><span class="sxs-lookup"><span data-stu-id="23688-125">In some cases the interface used to marshal the class is known as the class interface.</span></span> <span data-ttu-id="23688-126">如需以您選擇的介面來覆寫類別介面的相關資訊，請參閱 [類別介面簡介](../../standard/native-interop/com-callable-wrapper.md#introducing-the-class-interface)。</span><span class="sxs-lookup"><span data-stu-id="23688-126">For information about overriding the class interface with an interface of your choice, see [Introducing the class interface](../../standard/native-interop/com-callable-wrapper.md#introducing-the-class-interface).</span></span>  
  
### <a name="passing-classes-to-com"></a><span data-ttu-id="23688-127">將類別傳遞給 COM</span><span class="sxs-lookup"><span data-stu-id="23688-127">Passing Classes to COM</span></span>  
 <span data-ttu-id="23688-128">將 Managed 類別傳遞給 COM 時，Interop 封送處理器會自動使用 COM Proxy 來包裝類別，並將 Proxy 產生的類別介面傳遞給 COM 方法呼叫。</span><span class="sxs-lookup"><span data-stu-id="23688-128">When a managed class is passed to COM, the interop marshaler automatically wraps the class with a COM proxy and passes the class interface produced by the proxy to the COM method call.</span></span> <span data-ttu-id="23688-129">Proxy 接著會將類別介面上的所有呼叫重新委派給 Managed 物件。</span><span class="sxs-lookup"><span data-stu-id="23688-129">The proxy then delegates all calls on the class interface back to the managed object.</span></span> <span data-ttu-id="23688-130">Proxy 也會公開類別未明確實作的其他介面。</span><span class="sxs-lookup"><span data-stu-id="23688-130">The proxy also exposes other interfaces that are not explicitly implemented by the class.</span></span> <span data-ttu-id="23688-131">Proxy 會代表類別自動實作 **IUnknown** 和 **IDispatch** 這類介面。</span><span class="sxs-lookup"><span data-stu-id="23688-131">The proxy automatically implements interfaces such as **IUnknown** and **IDispatch** on behalf of the class.</span></span>  
  
### <a name="passing-classes-to-net-code"></a><span data-ttu-id="23688-132">將類別傳遞給 .NET 程式碼</span><span class="sxs-lookup"><span data-stu-id="23688-132">Passing Classes to .NET Code</span></span>  
 <span data-ttu-id="23688-133">一般而言，Coclass 在 COM 中不會做為方法引數，</span><span class="sxs-lookup"><span data-stu-id="23688-133">Coclasses are not typically used as method arguments in COM.</span></span> <span data-ttu-id="23688-134">通常會以預設介面代替 Coclass 傳遞。</span><span class="sxs-lookup"><span data-stu-id="23688-134">Instead, a default interface is usually passed in place of the coclass.</span></span>  
  
 <span data-ttu-id="23688-135">在將介面傳遞至 Managed 程式碼中之後，Interop 封送處理器會負責以適當的包裝函式來包裝介面，並將包裝函式傳遞給 Managed 方法。</span><span class="sxs-lookup"><span data-stu-id="23688-135">When an interface is passed into managed code, the interop marshaler is responsible for wrapping the interface with the proper wrapper and passing the wrapper to the managed method.</span></span> <span data-ttu-id="23688-136">您可能很難決定要使用哪個包裝函式。</span><span class="sxs-lookup"><span data-stu-id="23688-136">Determining which wrapper to use can be difficult.</span></span> <span data-ttu-id="23688-137">不論物件實作多少個介面，COM 物件的每個執行個體都只會有一個包裝函式。</span><span class="sxs-lookup"><span data-stu-id="23688-137">Every instance of a COM object has a single, unique wrapper, no matter how many interfaces the object implements.</span></span> <span data-ttu-id="23688-138">例如，實作五個不同介面的單一 COM 物件只會有一個包裝函式。</span><span class="sxs-lookup"><span data-stu-id="23688-138">For example, a single COM object that implements five distinct interfaces has only one wrapper.</span></span> <span data-ttu-id="23688-139">同一個包裝函式會公開所有五個介面。</span><span class="sxs-lookup"><span data-stu-id="23688-139">The same wrapper exposes all five interfaces.</span></span> <span data-ttu-id="23688-140">如果建立 COM 物件的兩個執行個體，則會建立包裝函式的兩個執行個體。</span><span class="sxs-lookup"><span data-stu-id="23688-140">If two instances of the COM object are created, then two instances of the wrapper are created.</span></span>  
  
 <span data-ttu-id="23688-141">為了讓包裝函式在整個存留期間保持同一個類型，當第一次透過 Interop 封送處理器傳遞物件所公開的介面時，封送處理器必須識別正確的包裝函式。</span><span class="sxs-lookup"><span data-stu-id="23688-141">For the wrapper to maintain the same type throughout its lifetime, the interop marshaler must identify the correct wrapper the first time an interface exposed by the object is passed through the marshaler.</span></span> <span data-ttu-id="23688-142">封送處理器會透過查看物件所實作的其中一個介面，來識別物件。</span><span class="sxs-lookup"><span data-stu-id="23688-142">The marshaler identifies the object by looking at one of the interfaces the object implements.</span></span>  
  
 <span data-ttu-id="23688-143">例如，封送處理器會決定應該使用類別包裝函式來包裝已傳遞至 Managed 程式碼中的介面。</span><span class="sxs-lookup"><span data-stu-id="23688-143">For example, the marshaler determines that the class wrapper should be used to wrap the interface that was passed into managed code.</span></span> <span data-ttu-id="23688-144">當透過封送處理器第一次傳遞介面時，封送處理器會檢查介面是否來自已知的物件。</span><span class="sxs-lookup"><span data-stu-id="23688-144">When the interface is first passed through the marshaler, the marshaler checks whether the interface is coming from a known object.</span></span> <span data-ttu-id="23688-145">這項檢查會發生於下列兩種情況：</span><span class="sxs-lookup"><span data-stu-id="23688-145">This check occurs in two situations:</span></span>  
  
- <span data-ttu-id="23688-146">另一個已傳遞至其他位置之 COM 的 Managed 物件正在實作介面。</span><span class="sxs-lookup"><span data-stu-id="23688-146">An interface is being implemented by another managed object that was passed to COM elsewhere.</span></span> <span data-ttu-id="23688-147">封送處理器能夠立即識別 Managed 物件所公開的介面，而且能夠以提供實作的 Managed 物件來比對介面。</span><span class="sxs-lookup"><span data-stu-id="23688-147">The marshaler can readily identify interfaces exposed by managed objects and is able to match the interface with the managed object that provides the implementation.</span></span> <span data-ttu-id="23688-148">接著 Managed 物件會傳遞給方法，並且不需要任何包裝函式。</span><span class="sxs-lookup"><span data-stu-id="23688-148">The managed object is then passed to the method and no wrapper is needed.</span></span>  
  
- <span data-ttu-id="23688-149">已包裝的物件正在實作介面。</span><span class="sxs-lookup"><span data-stu-id="23688-149">An object that has already been wrapped is implementing the interface.</span></span> <span data-ttu-id="23688-150">為了判斷是否為這種情況，封送處理器會查詢物件是否有 **IUnknown** 介面，並且將傳回的介面與其他已包裝之物件的介面進行比較。</span><span class="sxs-lookup"><span data-stu-id="23688-150">To determine whether this is the case, the marshaler queries the object for its **IUnknown** interface and compares the returned interface to the interfaces of other objects that are already wrapped.</span></span> <span data-ttu-id="23688-151">如果該介面與其他包裝函式的介面相同，則物件會有相同的識別，因此會將現有的包裝函式傳遞給方法。</span><span class="sxs-lookup"><span data-stu-id="23688-151">If the interface is the same as that of another wrapper, the objects have the same identity and the existing wrapper is passed to the method.</span></span>  
  
 <span data-ttu-id="23688-152">如果介面不是來自已知的物件，則封送處理器會執行下列作業：</span><span class="sxs-lookup"><span data-stu-id="23688-152">If an interface is not from a known object, the marshaler does the following:</span></span>  
  
1. <span data-ttu-id="23688-153">封送處理器會查詢物件是否有 **IProvideClassInfo2** 介面。</span><span class="sxs-lookup"><span data-stu-id="23688-153">The marshaler queries the object for the **IProvideClassInfo2** interface.</span></span> <span data-ttu-id="23688-154">如果有的話，封送處理器會使用從 **IProvideClassInfo2.GetGUID** 傳回的 CLSID 來識別提供介面的 coclass。</span><span class="sxs-lookup"><span data-stu-id="23688-154">If provided, the marshaler uses the CLSID returned from **IProvideClassInfo2.GetGUID** to identify the coclass providing the interface.</span></span> <span data-ttu-id="23688-155">如果先前已註冊組件，封送處理器就可以使用 CLSID 從登錄中找出包裝函式。</span><span class="sxs-lookup"><span data-stu-id="23688-155">With the CLSID, the marshaler can locate the wrapper from the registry if the assembly has previously been registered.</span></span>  
  
2. <span data-ttu-id="23688-156">封送處理器會查詢介面是否有 **IProvideClassInfo** 介面。</span><span class="sxs-lookup"><span data-stu-id="23688-156">The marshaler queries the interface for the **IProvideClassInfo** interface.</span></span> <span data-ttu-id="23688-157">如果有的話，封送處理器會使用從 **IProvideClassInfo.GetClassinfo** 傳回的 **ITypeInfo** 來判斷公開介面之類別的 CLSID。</span><span class="sxs-lookup"><span data-stu-id="23688-157">If provided, the marshaler uses the **ITypeInfo** returned from **IProvideClassInfo.GetClassinfo** to determine the CLSID of the class exposing the interface.</span></span> <span data-ttu-id="23688-158">封送處理器可以使用 CLSID 來找出包裝函式的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="23688-158">The marshaler can use the CLSID to locate the metadata for the wrapper.</span></span>  
  
3. <span data-ttu-id="23688-159">如果封送處理器仍然無法識別類別，則會以稱為 **System.__ComObject** 的泛型包裝函式類別來包裝介面。</span><span class="sxs-lookup"><span data-stu-id="23688-159">If the marshaler still cannot identify the class, it wraps the interface with a generic wrapper class called **System.__ComObject**.</span></span>  
  
## <a name="default-marshaling-for-delegates"></a><span data-ttu-id="23688-160">委派的預設封送處理</span><span class="sxs-lookup"><span data-stu-id="23688-160">Default marshaling for delegates</span></span>  
 <span data-ttu-id="23688-161">根據呼叫的機制，Managed 委派會封送處理為 COM 介面或函式指標：</span><span class="sxs-lookup"><span data-stu-id="23688-161">A managed delegate is marshaled as a COM interface or as a function pointer, based on the calling mechanism:</span></span>  
  
- <span data-ttu-id="23688-162">若為平台叫用，委派預設會封送處理為 Unmanaged 函式指標。</span><span class="sxs-lookup"><span data-stu-id="23688-162">For platform invoke, a delegate is marshaled as an unmanaged function pointer by default.</span></span>  
  
- <span data-ttu-id="23688-163">若為 COM Interop，委派預設會封送處理為 **_Delegate** 類型的 COM 介面。</span><span class="sxs-lookup"><span data-stu-id="23688-163">For COM interop, a delegate is marshaled as a COM interface of type **_Delegate** by default.</span></span> <span data-ttu-id="23688-164">**_Delegate** 介面是在 Mscorlib.tlb 型別程式庫中定義，並且包含 <xref:System.Delegate.DynamicInvoke%2A?displayProperty=nameWithType> 方法，可讓您呼叫委派所參考的方法。</span><span class="sxs-lookup"><span data-stu-id="23688-164">The **_Delegate** interface is defined in the Mscorlib.tlb type library and contains the <xref:System.Delegate.DynamicInvoke%2A?displayProperty=nameWithType> method, which enables you to call the method that the delegate references.</span></span>  
  
 <span data-ttu-id="23688-165">下表顯示 Managed 委派資料類型的封送處理選項。</span><span class="sxs-lookup"><span data-stu-id="23688-165">The following table shows the marshaling options for the managed delegate data type.</span></span> <span data-ttu-id="23688-166"><xref:System.Runtime.InteropServices.MarshalAsAttribute> 屬性提供幾種 <xref:System.Runtime.InteropServices.UnmanagedType> 列舉值來封送處理委派。</span><span class="sxs-lookup"><span data-stu-id="23688-166">The <xref:System.Runtime.InteropServices.MarshalAsAttribute> attribute provides several <xref:System.Runtime.InteropServices.UnmanagedType> enumeration values to marshal delegates.</span></span>  
  
|<span data-ttu-id="23688-167">列舉類型</span><span class="sxs-lookup"><span data-stu-id="23688-167">Enumeration type</span></span>|<span data-ttu-id="23688-168">Unmanaged 格式的描述</span><span class="sxs-lookup"><span data-stu-id="23688-168">Description of unmanaged format</span></span>|  
|----------------------|-------------------------------------|  
|<span data-ttu-id="23688-169">**UnmanagedType.FunctionPtr**</span><span class="sxs-lookup"><span data-stu-id="23688-169">**UnmanagedType.FunctionPtr**</span></span>|<span data-ttu-id="23688-170">Unmanaged 函式指標。</span><span class="sxs-lookup"><span data-stu-id="23688-170">An unmanaged function pointer.</span></span>|  
|<span data-ttu-id="23688-171">**UnmanagedType.Interface**</span><span class="sxs-lookup"><span data-stu-id="23688-171">**UnmanagedType.Interface**</span></span>|<span data-ttu-id="23688-172">**_Delegate** 類型的介面，如 Mscorlib.tlb 中所定義。</span><span class="sxs-lookup"><span data-stu-id="23688-172">An interface of type **_Delegate**, as defined in Mscorlib.tlb.</span></span>|  
  
 <span data-ttu-id="23688-173">請考慮以下的範例程式碼，其中 `DelegateTestInterface` 的方法是匯出至 COM 類型程式庫。</span><span class="sxs-lookup"><span data-stu-id="23688-173">Consider the following example code in which the methods of `DelegateTestInterface` are exported to a COM type library.</span></span> <span data-ttu-id="23688-174">請注意，只有標記為 **ref** (或 **ByRef**) 關鍵字的委派才會傳遞為 In/Out 參數。</span><span class="sxs-lookup"><span data-stu-id="23688-174">Notice that only delegates marked with the **ref** (or **ByRef**) keyword are passed as In/Out parameters.</span></span>  
  
```csharp  
using System;  
using System.Runtime.InteropServices;  
  
public interface DelegateTest {  
void m1(Delegate d);  
void m2([MarshalAs(UnmanagedType.Interface)] Delegate d);
void m3([MarshalAs(UnmanagedType.Interface)] ref Delegate d);
void m4([MarshalAs(UnmanagedType.FunctionPtr)] Delegate d);
void m5([MarshalAs(UnmanagedType.FunctionPtr)] ref Delegate d);
}  
```  
  
### <a name="type-library-representation"></a><span data-ttu-id="23688-175">類型程式庫表示</span><span class="sxs-lookup"><span data-stu-id="23688-175">Type library representation</span></span>  
  
```cpp  
importlib("mscorlib.tlb");  
interface DelegateTest : IDispatch {  
[id(…)] HRESULT m1([in] _Delegate* d);  
[id(…)] HRESULT m2([in] _Delegate* d);  
[id(…)] HRESULT m3([in, out] _Delegate** d);  
[id()] HRESULT m4([in] int d);  
[id()] HRESULT m5([in, out] int *d);  
   };  
```  
  
 <span data-ttu-id="23688-176">函式指標和其他任何 Unmanaged 函式指標一樣，都可以解除參考。</span><span class="sxs-lookup"><span data-stu-id="23688-176">A function pointer can be dereferenced, just as any other unmanaged function pointer can be dereferenced.</span></span>  

<span data-ttu-id="23688-177">在此範例中，當兩個委派封送處理成 <xref:System.Runtime.InteropServices.UnmanagedType.FunctionPtr?displayProperty=nameWithType> 時，結果就是 `int` 和 `int` 的指標。</span><span class="sxs-lookup"><span data-stu-id="23688-177">In this example, when the two delegates are marshaled as <xref:System.Runtime.InteropServices.UnmanagedType.FunctionPtr?displayProperty=nameWithType>, the result is an `int` and a pointer to an `int`.</span></span> <span data-ttu-id="23688-178">因為正在封送處理委派型別，所以這裡的 `int` 代表 void (`void*`) 的指標，這是記憶體中的委派位址。</span><span class="sxs-lookup"><span data-stu-id="23688-178">Because delegate types are being marshaled, `int` here represents a pointer to a void (`void*`), which is the address of the delegate in memory.</span></span> <span data-ttu-id="23688-179">換句話說，此結果是 32 位元 Windows 系統所特有，因為這裡的 `int` 代表函式指標的大小。</span><span class="sxs-lookup"><span data-stu-id="23688-179">In other words, this result is specific to 32-bit Windows systems, since `int` here represents the size of the function pointer.</span></span>

> [!NOTE]
> <span data-ttu-id="23688-180">Unmanaged 程式碼所持有之 Managed 委派的函式指標參考，無法防止 Common Language Runtime 在 Managed 物件上執行記憶體回收。</span><span class="sxs-lookup"><span data-stu-id="23688-180">A reference to the function pointer to a managed delegate held by unmanaged code does not prevent the common language runtime from performing garbage collection on the managed object.</span></span>  
  
 <span data-ttu-id="23688-181">例如，下列程式碼不正確，因為傳遞給 `SetChangeHandler` 方法的 `cb` 物件參考無法使 `cb` 在過了 `Test` 方法的存留期後仍保持運作。</span><span class="sxs-lookup"><span data-stu-id="23688-181">For example, the following code is incorrect because the reference to the `cb` object, passed to the `SetChangeHandler` method, does not keep `cb` alive beyond the life of the `Test` method.</span></span> <span data-ttu-id="23688-182">一旦 `cb` 物件的記憶體被回收，傳遞給 `SetChangeHandler` 的函式指標便不再有效。</span><span class="sxs-lookup"><span data-stu-id="23688-182">Once the `cb` object is garbage collected, the function pointer passed to `SetChangeHandler` is no longer valid.</span></span>  
  
```csharp  
public class ExternalAPI {  
   [DllImport("External.dll")]  
   public static extern void SetChangeHandler(  
      [MarshalAs(UnmanagedType.FunctionPtr)]ChangeDelegate d);  
}  
public delegate bool ChangeDelegate([MarshalAs(UnmanagedType.LPWStr) string S);  
public class CallBackClass {  
   public bool OnChange(string S){ return true;}  
}  
internal class DelegateTest {  
   public static void Test() {  
      CallBackClass cb = new CallBackClass();  
      // Caution: The following reference on the cb object does not keep the
      // object from being garbage collected after the Main method
      // executes.  
      ExternalAPI.SetChangeHandler(new ChangeDelegate(cb.OnChange));
   }  
}  
```  
  
 <span data-ttu-id="23688-183">為了彌補未預期的記憶體回收，呼叫端必須確保只要 Unmanaged 函式指標正在使用中，`cb` 物件就會保持運作。</span><span class="sxs-lookup"><span data-stu-id="23688-183">To compensate for unexpected garbage collection, the caller must ensure that the `cb` object is kept alive as long as the unmanaged function pointer is in use.</span></span> <span data-ttu-id="23688-184">您可以選擇性地讓 Unmanaged 程式碼通知 Managed 程式碼已不再需要函式指標，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="23688-184">Optionally, you can have the unmanaged code notify the managed code when the function pointer is no longer needed, as the following example shows.</span></span>  
  
```csharp  
internal class DelegateTest {  
   CallBackClass cb;  
   // Called before ever using the callback function.  
   public static void SetChangeHandler() {  
      cb = new CallBackClass();  
      ExternalAPI.SetChangeHandler(new ChangeDelegate(cb.OnChange));  
   }  
   // Called after using the callback function for the last time.  
   public static void RemoveChangeHandler() {  
      // The cb object can be collected now. The unmanaged code is
      // finished with the callback function.  
      cb = null;  
   }  
}  
```  
  
## <a name="default-marshaling-for-value-types"></a><span data-ttu-id="23688-185">實值類型的預設封送處理</span><span class="sxs-lookup"><span data-stu-id="23688-185">Default marshaling for value types</span></span>  
 <span data-ttu-id="23688-186">大部分的實值型別 (例如整數和浮點數) 都是 [Blittable](blittable-and-non-blittable-types.md)，而且不需要封送處理。</span><span class="sxs-lookup"><span data-stu-id="23688-186">Most value types, such as integers and floating-point numbers, are [blittable](blittable-and-non-blittable-types.md) and do not require marshaling.</span></span> <span data-ttu-id="23688-187">其他[非 Blittable](blittable-and-non-blittable-types.md) 類型在 Managed 和 Unmanaged 記憶體中有不同的表示，而且需要封送處理。</span><span class="sxs-lookup"><span data-stu-id="23688-187">Other [non-blittable](blittable-and-non-blittable-types.md) types have dissimilar representations in managed and unmanaged memory and do require marshaling.</span></span> <span data-ttu-id="23688-188">但其他類型需要跨互通界限進行明確格式化。</span><span class="sxs-lookup"><span data-stu-id="23688-188">Still other types require explicit formatting across the interoperation boundary.</span></span>  
  
 <span data-ttu-id="23688-189">本節提供下列格式化實值型別的相關資訊：</span><span class="sxs-lookup"><span data-stu-id="23688-189">This section provides information on the following formatted value types:</span></span>  
  
- [<span data-ttu-id="23688-190">在平台叫用中使用的實值型別</span><span class="sxs-lookup"><span data-stu-id="23688-190">Value Types Used in Platform Invoke</span></span>](#value-types-used-in-platform-invoke)  
  
- [<span data-ttu-id="23688-191">在 COM Interop 中使用的實值類型</span><span class="sxs-lookup"><span data-stu-id="23688-191">Value Types Used in COM Interop</span></span>](#value-types-used-in-com-interop)  
  
 <span data-ttu-id="23688-192">本主題除了描述格式化類型之外，還指出具有獨特封送處理行為的[系統實值型別](#system-value-types)。</span><span class="sxs-lookup"><span data-stu-id="23688-192">In addition to describing formatted types, this topic identifies [System Value Types](#system-value-types) that have unusual marshaling behavior.</span></span>  
  
 <span data-ttu-id="23688-193">格式化類型是複雜類型，其中包含在記憶體中明確控制其成員配置的資訊。</span><span class="sxs-lookup"><span data-stu-id="23688-193">A formatted type is a complex type that contains information that explicitly controls the layout of its members in memory.</span></span> <span data-ttu-id="23688-194">這項成員配置資訊會透過 <xref:System.Runtime.InteropServices.StructLayoutAttribute> 屬性來提供。</span><span class="sxs-lookup"><span data-stu-id="23688-194">The member layout information is provided using the <xref:System.Runtime.InteropServices.StructLayoutAttribute> attribute.</span></span> <span data-ttu-id="23688-195">配置可以是下列其中一個 <xref:System.Runtime.InteropServices.LayoutKind> 列舉值：</span><span class="sxs-lookup"><span data-stu-id="23688-195">The layout can be one of the following <xref:System.Runtime.InteropServices.LayoutKind> enumeration values:</span></span>  
  
- <span data-ttu-id="23688-196">**Layoutkind.sequential 標示。 Auto**</span><span class="sxs-lookup"><span data-stu-id="23688-196">**LayoutKind.Auto**</span></span>  
  
     <span data-ttu-id="23688-197">表示 Common Language Runtime 可以為了更高的效率隨意重新排列類型的成員。</span><span class="sxs-lookup"><span data-stu-id="23688-197">Indicates that the common language runtime is free to reorder the members of the type for efficiency.</span></span> <span data-ttu-id="23688-198">不過，當實值類型傳遞至 Unmanaged 程式碼時，成員的配置是可以預測的。</span><span class="sxs-lookup"><span data-stu-id="23688-198">However, when a value type is passed to unmanaged code, the layout of the members is predictable.</span></span> <span data-ttu-id="23688-199">嘗試封送處理這類結構會自動造成例外狀況。</span><span class="sxs-lookup"><span data-stu-id="23688-199">An attempt to marshal such a structure automatically causes an exception.</span></span>  
  
- <span data-ttu-id="23688-200">**LayoutKind.Sequential**</span><span class="sxs-lookup"><span data-stu-id="23688-200">**LayoutKind.Sequential**</span></span>  
  
     <span data-ttu-id="23688-201">表示類型的成員可以透過它們出現在 Managed 類型定義中的相同順序來配置於 Unmanaged 記憶體中。</span><span class="sxs-lookup"><span data-stu-id="23688-201">Indicates that the members of the type are to be laid out in unmanaged memory in the same order in which they appear in the managed type definition.</span></span>  
  
- <span data-ttu-id="23688-202">**LayoutKind.Explicit**</span><span class="sxs-lookup"><span data-stu-id="23688-202">**LayoutKind.Explicit**</span></span>  
  
     <span data-ttu-id="23688-203">表示根據每個欄位提供的 <xref:System.Runtime.InteropServices.FieldOffsetAttribute> 來配置成員。</span><span class="sxs-lookup"><span data-stu-id="23688-203">Indicates that the members are laid out according to the <xref:System.Runtime.InteropServices.FieldOffsetAttribute> supplied with each field.</span></span>  
  
### <a name="value-types-used-in-platform-invoke"></a><span data-ttu-id="23688-204">在平台叫用中使用的實值類型</span><span class="sxs-lookup"><span data-stu-id="23688-204">Value Types Used in Platform Invoke</span></span>  
 <span data-ttu-id="23688-205">在下列範例中，`Point` 和 `Rect` 類型使用 **StructLayoutAttribute** 提供成員配置資訊。</span><span class="sxs-lookup"><span data-stu-id="23688-205">In the following example the `Point` and `Rect` types provide member layout information using the **StructLayoutAttribute**.</span></span>  
  
```vb  
Imports System.Runtime.InteropServices  
<StructLayout(LayoutKind.Sequential)> Public Structure Point  
   Public x As Integer  
   Public y As Integer  
End Structure  
<StructLayout(LayoutKind.Explicit)> Public Structure Rect  
   <FieldOffset(0)> Public left As Integer  
   <FieldOffset(4)> Public top As Integer  
   <FieldOffset(8)> Public right As Integer  
   <FieldOffset(12)> Public bottom As Integer  
End Structure  
```  
  
```csharp  
using System.Runtime.InteropServices;  
[StructLayout(LayoutKind.Sequential)]  
public struct Point {  
   public int x;  
   public int y;  
}
  
[StructLayout(LayoutKind.Explicit)]  
public struct Rect {  
   [FieldOffset(0)] public int left;  
   [FieldOffset(4)] public int top;  
   [FieldOffset(8)] public int right;  
   [FieldOffset(12)] public int bottom;  
}  
```  
  
 <span data-ttu-id="23688-206">當封送處理至 Unmanaged 程式碼時，這些格式化類型會封送處理為 C 樣式結構。</span><span class="sxs-lookup"><span data-stu-id="23688-206">When marshaled to unmanaged code, these formatted types are marshaled as C-style structures.</span></span> <span data-ttu-id="23688-207">如此可讓您輕鬆地呼叫具有結構引數的 Unmanaged 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="23688-207">This provides an easy way of calling an unmanaged API that has structure arguments.</span></span> <span data-ttu-id="23688-208">例如，`POINT` 和 `RECT` 結構可以傳遞至 Microsoft Windows API **PtInRect** 函式，如下所示：</span><span class="sxs-lookup"><span data-stu-id="23688-208">For example, the `POINT` and `RECT` structures can be passed to the Microsoft Windows API **PtInRect** function as follows:</span></span>  
  
```cpp  
BOOL PtInRect(const RECT *lprc, POINT pt);  
```  
  
 <span data-ttu-id="23688-209">您可以使用以下的平台叫用定義來傳遞結構：</span><span class="sxs-lookup"><span data-stu-id="23688-209">You can pass structures using the following platform invoke definition:</span></span>  
  
```vb
Friend Class NativeMethods
    Friend Declare Auto Function PtInRect Lib "User32.dll" (
        ByRef r As Rect, p As Point) As Boolean
End Class
```
  
```csharp
internal static class NativeMethods
{
   [DllImport("User32.dll")]
   internal static extern bool PtInRect(ref Rect r, Point p);
}
```
  
 <span data-ttu-id="23688-210">`Rect` 實值類型必須以傳址方式傳遞，因為 Unmanaged 應用程式開發介面必須將 `RECT` 的指標傳遞至函式。</span><span class="sxs-lookup"><span data-stu-id="23688-210">The `Rect` value type must be passed by reference because the unmanaged API is expecting a pointer to a `RECT` to be passed to the function.</span></span> <span data-ttu-id="23688-211">`Point` 實值類型必須以傳值方式傳遞，因為 Unmanaged 應用程式開發介面必須在堆疊上傳遞 `POINT`。</span><span class="sxs-lookup"><span data-stu-id="23688-211">The `Point` value type is passed by value because the unmanaged API expects the `POINT` to be passed on the stack.</span></span> <span data-ttu-id="23688-212">這種微妙的差異是非常重要的。</span><span class="sxs-lookup"><span data-stu-id="23688-212">This subtle difference is very important.</span></span> <span data-ttu-id="23688-213">參考會當做指標傳遞至 Unmanaged 程式碼，</span><span class="sxs-lookup"><span data-stu-id="23688-213">References are passed to unmanaged code as pointers.</span></span> <span data-ttu-id="23688-214">而值會在堆疊上傳遞至 Unmanaged 程式碼。</span><span class="sxs-lookup"><span data-stu-id="23688-214">Values are passed to unmanaged code on the stack.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="23688-215">當格式化類型封送處理為結構時，只能存取類型內的欄位。</span><span class="sxs-lookup"><span data-stu-id="23688-215">When a formatted type is marshaled as a structure, only the fields within the type are accessible.</span></span> <span data-ttu-id="23688-216">如果類型具有方法、屬性或事件，您無法從 Unmanaged 程式碼存取這些項目。</span><span class="sxs-lookup"><span data-stu-id="23688-216">If the type has methods, properties, or events, they are inaccessible from unmanaged code.</span></span>  
  
 <span data-ttu-id="23688-217">只要類別有固定成員配置，也可以當做 C 樣式結構封送處理至 Unmanaged 程式碼。</span><span class="sxs-lookup"><span data-stu-id="23688-217">Classes can also be marshaled to unmanaged code as C-style structures, provided they have fixed member layout.</span></span> <span data-ttu-id="23688-218"><xref:System.Runtime.InteropServices.StructLayoutAttribute> 屬性也會提供類別的成員配置資訊。</span><span class="sxs-lookup"><span data-stu-id="23688-218">The member layout information for a class is also provided with the <xref:System.Runtime.InteropServices.StructLayoutAttribute> attribute.</span></span> <span data-ttu-id="23688-219">具有固定配置的實值類型和具有固定配置的類別之間的主要差異在於，將其封送處理至 Unmanaged 程式碼的方式不同。</span><span class="sxs-lookup"><span data-stu-id="23688-219">The main difference between value types with fixed layout and classes with fixed layout is the way in which they are marshaled to unmanaged code.</span></span> <span data-ttu-id="23688-220">實值類型是以傳值方式 (在堆疊上) 傳遞，因此呼叫端不會看到被呼叫端對類型的成員所做的任何變更。</span><span class="sxs-lookup"><span data-stu-id="23688-220">Value types are passed by value (on the stack) and consequently any changes made to the members of the type by the callee are not seen by the caller.</span></span> <span data-ttu-id="23688-221">參考類型是以傳址方式 (在堆疊上傳遞類型的參考) 傳遞，因此呼叫端會看到被呼叫端對類型的 Blittable 類型成員所做的所有變更。</span><span class="sxs-lookup"><span data-stu-id="23688-221">Reference types are passed by reference (a reference to the type is passed on the stack); consequently, all changes made to blittable-type members of a type by the callee are seen by the caller.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="23688-222">如果參考類型具有非 Blittable 類型的成員，則需要轉換兩次：第一次是在將引數傳遞至 Unmanaged 端時，第二次是從呼叫傳回時。</span><span class="sxs-lookup"><span data-stu-id="23688-222">If a reference type has members of non-blittable types, conversion is required twice: the first time when an argument is passed to the unmanaged side and the second time on return from the call.</span></span> <span data-ttu-id="23688-223">由於這會增加額外負荷，因此如果呼叫端想要看到被呼叫端所做的變更，就必須將 In/Out 參數明確套用至引數。</span><span class="sxs-lookup"><span data-stu-id="23688-223">Due to this added overhead, In/Out parameters must be explicitly applied to an argument if the caller wants to see changes made by the callee.</span></span>  
  
 <span data-ttu-id="23688-224">在下列範例中，`SystemTime` 類別具有循序成員配置，可以傳遞至 Windows API **GetSystemTime** 函式。</span><span class="sxs-lookup"><span data-stu-id="23688-224">In the following example, the `SystemTime` class has sequential member layout and can be passed to the Windows API **GetSystemTime** function.</span></span>  
  
```vb  
<StructLayout(LayoutKind.Sequential)> Public Class SystemTime  
   Public wYear As System.UInt16  
   Public wMonth As System.UInt16  
   Public wDayOfWeek As System.UInt16  
   Public wDay As System.UInt16  
   Public wHour As System.UInt16  
   Public wMinute As System.UInt16  
   Public wSecond As System.UInt16  
   Public wMilliseconds As System.UInt16  
End Class  
```  
  
```csharp  
[StructLayout(LayoutKind.Sequential)]  
   public class SystemTime {  
   public ushort wYear;
   public ushort wMonth;  
   public ushort wDayOfWeek;
   public ushort wDay;
   public ushort wHour;
   public ushort wMinute;
   public ushort wSecond;
   public ushort wMilliseconds;
}  
```  
  
 <span data-ttu-id="23688-225">**GetSystemTime** 函式的定義如下：</span><span class="sxs-lookup"><span data-stu-id="23688-225">The **GetSystemTime** function is defined as follows:</span></span>  
  
```cpp  
void GetSystemTime(SYSTEMTIME* SystemTime);  
```  
  
 <span data-ttu-id="23688-226">**GetSystemTime** 的對等平台叫用定義如下：</span><span class="sxs-lookup"><span data-stu-id="23688-226">The equivalent platform invoke definition for **GetSystemTime** is as follows:</span></span>  
  
```vb
Friend Class NativeMethods
    Friend Declare Auto Sub GetSystemTime Lib "Kernel32.dll" (
        ByVal sysTime As SystemTime)
End Class
```
  
```csharp
internal static class NativeMethods
{
   [DllImport("Kernel32.dll", CharSet = CharSet.Auto)]
   internal static extern void GetSystemTime(SystemTime st);
}
```
  
 <span data-ttu-id="23688-227">請注意，`SystemTime` 引數未當做參考引數輸入，因為 `SystemTime` 是類別，不是實值類型。</span><span class="sxs-lookup"><span data-stu-id="23688-227">Notice that the `SystemTime` argument is not typed as a reference argument because `SystemTime` is a class, not a value type.</span></span> <span data-ttu-id="23688-228">不同於實值類型，類別永遠會以傳址方式傳遞。</span><span class="sxs-lookup"><span data-stu-id="23688-228">Unlike value types, classes are always passed by reference.</span></span>  
  
 <span data-ttu-id="23688-229">下列程式碼範例顯示具有 `SetXY` 方法的不同 `Point` 類別。</span><span class="sxs-lookup"><span data-stu-id="23688-229">The following code example shows a different `Point` class that has a method called `SetXY`.</span></span> <span data-ttu-id="23688-230">由於類型具有循序配置，因此可傳遞至 Unmanaged 程式碼，並封送處理為結構。</span><span class="sxs-lookup"><span data-stu-id="23688-230">Because the type has sequential layout, it can be passed to unmanaged code and marshaled as a structure.</span></span> <span data-ttu-id="23688-231">不過，即使物件是以傳址方式傳遞，還是無法從 Unmanaged 程式碼中呼叫 `SetXY` 成員。</span><span class="sxs-lookup"><span data-stu-id="23688-231">However, the `SetXY` member is not callable from unmanaged code, even though the object is passed by reference.</span></span>  
  
```vb  
<StructLayout(LayoutKind.Sequential)> Public Class Point  
   Private x, y As Integer  
   Public Sub SetXY(x As Integer, y As Integer)  
      Me.x = x  
      Me.y = y  
   End Sub  
End Class  
```  
  
```csharp  
[StructLayout(LayoutKind.Sequential)]  
public class Point {  
   int x, y;  
   public void SetXY(int x, int y){
      this.x = x;  
      this.y = y;  
   }  
}  
```  
  
### <a name="value-types-used-in-com-interop"></a><span data-ttu-id="23688-232">在 COM Interop 中使用的實值類型</span><span class="sxs-lookup"><span data-stu-id="23688-232">Value Types Used in COM Interop</span></span>  
 <span data-ttu-id="23688-233">格式化類型也可以傳遞至 COM Interop 方法呼叫。</span><span class="sxs-lookup"><span data-stu-id="23688-233">Formatted types can also be passed to COM interop method calls.</span></span> <span data-ttu-id="23688-234">事實上，當匯出至類型程式庫時，實值類型會自動轉換成結構。</span><span class="sxs-lookup"><span data-stu-id="23688-234">In fact, when exported to a type library, value types are automatically converted to structures.</span></span> <span data-ttu-id="23688-235">如下列範例所示，`Point` 實值類型會變成名為 `Point` 的類型定義 (typedef)。</span><span class="sxs-lookup"><span data-stu-id="23688-235">As the following example shows, the `Point` value type becomes a type definition (typedef) with the name `Point`.</span></span> <span data-ttu-id="23688-236">`Point` typedef 會取代在類型程式庫中的所有 `Point` 實值類型的參考。</span><span class="sxs-lookup"><span data-stu-id="23688-236">All references to the `Point` value type elsewhere in the type library are replaced with the `Point` typedef.</span></span>  
  
 <span data-ttu-id="23688-237">**型別程式庫呈現**</span><span class="sxs-lookup"><span data-stu-id="23688-237">**Type library representation**</span></span>  
  
```cpp  
typedef struct tagPoint {  
   int x;  
   int y;  
} Point;  
interface _Graphics {  
   …  
   HRESULT SetPoint ([in] Point p)  
   HRESULT SetPointRef ([in,out] Point *p)  
   HRESULT GetPoint ([out,retval] Point *p)  
}  
```  
  
 <span data-ttu-id="23688-238">當透過 COM 介面進行封送處理時，會使用與封送處理平台叫用呼叫的值和參考時相同的規則。</span><span class="sxs-lookup"><span data-stu-id="23688-238">The same rules used to marshal values and references to platform invoke calls are used when marshaling through COM interfaces.</span></span> <span data-ttu-id="23688-239">例如，將 `Point` 實值類型的執行個體從 .NET Framework 傳遞至 COM 時，會以傳值方式傳遞 `Point`。</span><span class="sxs-lookup"><span data-stu-id="23688-239">For example, when an instance of the `Point` value type is passed from the .NET Framework to COM, the `Point` is passed by value.</span></span> <span data-ttu-id="23688-240">如果以傳址方式傳遞 `Point` 實值類型，則會在堆疊上傳遞 `Point` 的指標。</span><span class="sxs-lookup"><span data-stu-id="23688-240">If the `Point` value type is passed by reference, a pointer to a `Point` is passed on the stack.</span></span> <span data-ttu-id="23688-241">Interop 封送處理器不支援任一方向中更高層級的間接取值 (**Point** \*\*)。</span><span class="sxs-lookup"><span data-stu-id="23688-241">The interop marshaler does not support higher levels of indirection (**Point** \*\*) in either direction.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="23688-242">由於匯出的型別程式庫無法表示明確的配置，因此不可在 COM Interop 中使用將 <xref:System.Runtime.InteropServices.LayoutKind> 列舉值設定為 [明確]\*\*\*\* 的結構。</span><span class="sxs-lookup"><span data-stu-id="23688-242">Structures having the <xref:System.Runtime.InteropServices.LayoutKind> enumeration value set to **Explicit** cannot be used in COM interop because the exported type library cannot express an explicit layout.</span></span>  
  
### <a name="system-value-types"></a><span data-ttu-id="23688-243">系統實值類型</span><span class="sxs-lookup"><span data-stu-id="23688-243">System Value Types</span></span>  
 <span data-ttu-id="23688-244"><xref:System> 命名空間具有數個實值類型，代表執行階段基本類型的 Boxed 格式。</span><span class="sxs-lookup"><span data-stu-id="23688-244">The <xref:System> namespace has several value types that represent the boxed form of the runtime primitive types.</span></span> <span data-ttu-id="23688-245">例如，實值型別 <xref:System.Int32?displayProperty=nameWithType> 結構代表 **ELEMENT_TYPE_I4** 的 Boxed 格式。</span><span class="sxs-lookup"><span data-stu-id="23688-245">For example, the value type <xref:System.Int32?displayProperty=nameWithType> structure represents the boxed form of **ELEMENT_TYPE_I4**.</span></span> <span data-ttu-id="23688-246">如同其他格式化類型，封送處理這些類型的方式與這些類型 Box 處理基本類型的方式相同，而不是將其封送處理為結構。</span><span class="sxs-lookup"><span data-stu-id="23688-246">Instead of marshaling these types as structures, as other formatted types are, you marshal them in the same way as the primitive types they box.</span></span> <span data-ttu-id="23688-247">因此會將 **System.Int32** 封送處理為 **ELEMENT_TYPE_I4**，而不是封送處理為包含 **long** 類型之單一成員的結構。</span><span class="sxs-lookup"><span data-stu-id="23688-247">**System.Int32** is therefore marshaled as **ELEMENT_TYPE_I4** instead of as a structure containing a single member of type **long**.</span></span> <span data-ttu-id="23688-248">下表包含 **System** 命名空間中的實值型別清單，這些類型是基本類型的 Boxed 表示。</span><span class="sxs-lookup"><span data-stu-id="23688-248">The following table contains a list of the value types in the **System** namespace that are boxed representations of primitive types.</span></span>  
  
|<span data-ttu-id="23688-249">系統實值類型</span><span class="sxs-lookup"><span data-stu-id="23688-249">System value type</span></span>|<span data-ttu-id="23688-250">項目類型</span><span class="sxs-lookup"><span data-stu-id="23688-250">Element type</span></span>|  
|-----------------------|------------------|  
|<xref:System.Boolean?displayProperty=nameWithType>|<span data-ttu-id="23688-251">**ELEMENT_TYPE_BOOLEAN**</span><span class="sxs-lookup"><span data-stu-id="23688-251">**ELEMENT_TYPE_BOOLEAN**</span></span>|  
|<xref:System.SByte?displayProperty=nameWithType>|<span data-ttu-id="23688-252">**ELEMENT_TYPE_I1**</span><span class="sxs-lookup"><span data-stu-id="23688-252">**ELEMENT_TYPE_I1**</span></span>|  
|<xref:System.Byte?displayProperty=nameWithType>|<span data-ttu-id="23688-253">**ELEMENT_TYPE_UI1**</span><span class="sxs-lookup"><span data-stu-id="23688-253">**ELEMENT_TYPE_UI1**</span></span>|  
|<xref:System.Char?displayProperty=nameWithType>|<span data-ttu-id="23688-254">**ELEMENT_TYPE_CHAR**</span><span class="sxs-lookup"><span data-stu-id="23688-254">**ELEMENT_TYPE_CHAR**</span></span>|  
|<xref:System.Int16?displayProperty=nameWithType>|<span data-ttu-id="23688-255">**ELEMENT_TYPE_I2**</span><span class="sxs-lookup"><span data-stu-id="23688-255">**ELEMENT_TYPE_I2**</span></span>|  
|<xref:System.UInt16?displayProperty=nameWithType>|<span data-ttu-id="23688-256">**ELEMENT_TYPE_U2**</span><span class="sxs-lookup"><span data-stu-id="23688-256">**ELEMENT_TYPE_U2**</span></span>|  
|<xref:System.Int32?displayProperty=nameWithType>|<span data-ttu-id="23688-257">**ELEMENT_TYPE_I4**</span><span class="sxs-lookup"><span data-stu-id="23688-257">**ELEMENT_TYPE_I4**</span></span>|  
|<xref:System.UInt32?displayProperty=nameWithType>|<span data-ttu-id="23688-258">**ELEMENT_TYPE_U4**</span><span class="sxs-lookup"><span data-stu-id="23688-258">**ELEMENT_TYPE_U4**</span></span>|  
|<xref:System.Int64?displayProperty=nameWithType>|<span data-ttu-id="23688-259">**ELEMENT_TYPE_I8**</span><span class="sxs-lookup"><span data-stu-id="23688-259">**ELEMENT_TYPE_I8**</span></span>|  
|<xref:System.UInt64?displayProperty=nameWithType>|<span data-ttu-id="23688-260">**ELEMENT_TYPE_U8**</span><span class="sxs-lookup"><span data-stu-id="23688-260">**ELEMENT_TYPE_U8**</span></span>|  
|<xref:System.Single?displayProperty=nameWithType>|<span data-ttu-id="23688-261">**ELEMENT_TYPE_R4**</span><span class="sxs-lookup"><span data-stu-id="23688-261">**ELEMENT_TYPE_R4**</span></span>|  
|<xref:System.Double?displayProperty=nameWithType>|<span data-ttu-id="23688-262">**ELEMENT_TYPE_R8**</span><span class="sxs-lookup"><span data-stu-id="23688-262">**ELEMENT_TYPE_R8**</span></span>|  
|<xref:System.String?displayProperty=nameWithType>|<span data-ttu-id="23688-263">**ELEMENT_TYPE_STRING**</span><span class="sxs-lookup"><span data-stu-id="23688-263">**ELEMENT_TYPE_STRING**</span></span>|  
|<xref:System.IntPtr?displayProperty=nameWithType>|<span data-ttu-id="23688-264">**ELEMENT_TYPE_I**</span><span class="sxs-lookup"><span data-stu-id="23688-264">**ELEMENT_TYPE_I**</span></span>|  
|<xref:System.UIntPtr?displayProperty=nameWithType>|<span data-ttu-id="23688-265">**ELEMENT_TYPE_U**</span><span class="sxs-lookup"><span data-stu-id="23688-265">**ELEMENT_TYPE_U**</span></span>|  
  
 <span data-ttu-id="23688-266">**System** 命名空間中的其他一些實值型別會以不同方式處理。</span><span class="sxs-lookup"><span data-stu-id="23688-266">Some other value types in the **System** namespace are handled differently.</span></span> <span data-ttu-id="23688-267">由於 Unmanaged 程式碼已經有這些類型的確立格式，因此封送處理器針對這些類型有特殊的封送處理方式。</span><span class="sxs-lookup"><span data-stu-id="23688-267">Because the unmanaged code already has well-established formats for these types, the marshaler has special rules for marshaling them.</span></span> <span data-ttu-id="23688-268">下表列出 **System** 命名空間中的特殊實值型別，以及要封送處理的目標 Unmanaged 類型。</span><span class="sxs-lookup"><span data-stu-id="23688-268">The following table lists the special value types in the **System** namespace, as well as the unmanaged type they are marshaled to.</span></span>  
  
|<span data-ttu-id="23688-269">系統實值類型</span><span class="sxs-lookup"><span data-stu-id="23688-269">System value type</span></span>|<span data-ttu-id="23688-270">IDL 類型</span><span class="sxs-lookup"><span data-stu-id="23688-270">IDL type</span></span>|  
|-----------------------|--------------|  
|<xref:System.DateTime?displayProperty=nameWithType>|<span data-ttu-id="23688-271">**DATE**</span><span class="sxs-lookup"><span data-stu-id="23688-271">**DATE**</span></span>|  
|<xref:System.Decimal?displayProperty=nameWithType>|<span data-ttu-id="23688-272">**DECIMAL**</span><span class="sxs-lookup"><span data-stu-id="23688-272">**DECIMAL**</span></span>|  
|<xref:System.Guid?displayProperty=nameWithType>|<span data-ttu-id="23688-273">**GUID**</span><span class="sxs-lookup"><span data-stu-id="23688-273">**GUID**</span></span>|  
|<xref:System.Drawing.Color?displayProperty=nameWithType>|<span data-ttu-id="23688-274">**OLE_COLOR**</span><span class="sxs-lookup"><span data-stu-id="23688-274">**OLE_COLOR**</span></span>|  
  
 <span data-ttu-id="23688-275">下列程式碼示範 Stdole2 型別程式庫中 Unmanaged 類型 **DATE**、**GUID**、**DECIMAL** 和 **OLE_COLOR** 的定義。</span><span class="sxs-lookup"><span data-stu-id="23688-275">The following code shows the definition of the unmanaged types **DATE**, **GUID**, **DECIMAL**, and **OLE_COLOR** in the Stdole2 type library.</span></span>  
  
#### <a name="type-library-representation"></a><span data-ttu-id="23688-276">類型程式庫表示</span><span class="sxs-lookup"><span data-stu-id="23688-276">Type library representation</span></span>  
  
```cpp  
typedef double DATE;  
typedef DWORD OLE_COLOR;  
  
typedef struct tagDEC {  
    USHORT    wReserved;  
    BYTE      scale;  
    BYTE      sign;  
    ULONG     Hi32;  
    ULONGLONG Lo64;  
} DECIMAL;  
  
typedef struct tagGUID {  
    DWORD Data1;  
    WORD  Data2;  
    WORD  Data3;  
    BYTE  Data4[ 8 ];  
} GUID;  
```  
  
 <span data-ttu-id="23688-277">下列程式碼顯示 Managed `IValueTypes` 介面中的對應定義。</span><span class="sxs-lookup"><span data-stu-id="23688-277">The following code shows the corresponding definitions in the managed `IValueTypes` interface.</span></span>  
  
```vb  
Public Interface IValueTypes  
   Sub M1(d As System.DateTime)  
   Sub M2(d As System.Guid)  
   Sub M3(d As System.Decimal)  
   Sub M4(d As System.Drawing.Color)  
End Interface  
```  
  
```csharp  
public interface IValueTypes {  
   void M1(System.DateTime d);  
   void M2(System.Guid d);  
   void M3(System.Decimal d);  
   void M4(System.Drawing.Color d);  
}  
```  
  
#### <a name="type-library-representation"></a><span data-ttu-id="23688-278">類型程式庫表示</span><span class="sxs-lookup"><span data-stu-id="23688-278">Type library representation</span></span>  
  
```cpp  
[…]  
interface IValueTypes : IDispatch {  
   HRESULT M1([in] DATE d);  
   HRESULT M2([in] GUID d);  
   HRESULT M3([in] DECIMAL d);  
   HRESULT M4([in] OLE_COLOR d);  
};  
```  
  
## <a name="see-also"></a><span data-ttu-id="23688-279">另請參閱</span><span class="sxs-lookup"><span data-stu-id="23688-279">See also</span></span>

- [<span data-ttu-id="23688-280">Blittable 和非 Blittable 類型</span><span class="sxs-lookup"><span data-stu-id="23688-280">Blittable and Non-Blittable Types</span></span>](blittable-and-non-blittable-types.md)
- [<span data-ttu-id="23688-281">複製和 Pin</span><span class="sxs-lookup"><span data-stu-id="23688-281">Copying and Pinning</span></span>](copying-and-pinning.md)
- [<span data-ttu-id="23688-282">陣列的預設封送處理</span><span class="sxs-lookup"><span data-stu-id="23688-282">Default Marshaling for Arrays</span></span>](default-marshaling-for-arrays.md)
- [<span data-ttu-id="23688-283">物件的預設封送處理</span><span class="sxs-lookup"><span data-stu-id="23688-283">Default Marshaling for Objects</span></span>](default-marshaling-for-objects.md)
- [<span data-ttu-id="23688-284">字串的預設封送處理</span><span class="sxs-lookup"><span data-stu-id="23688-284">Default Marshaling for Strings</span></span>](default-marshaling-for-strings.md)
