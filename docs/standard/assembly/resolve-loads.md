---
title: 解析組件負載
description: 本文描述 .NET AppDomain. System.appdomain.assemblyresolve 事件。 針對需要控制元件載入的應用程式，請使用此事件。
ms.date: 12/15/2020
helpviewer_keywords:
- assemblies [.NET], resolving loads
- application domains, loading assemblies
- resolving assembly loads
- assemblies [.NET], loading
- application domains, resolving assembly loads
ms.assetid: 5099e549-f4fd-49fb-a290-549edd456c6a
dev_langs:
- csharp
- vb
- cpp
ms.openlocfilehash: 63545db31a4290ce933da45c0957dfdb2a00701c
ms.sourcegitcommit: e301979e3049ce412d19b094c60ed95b316a8f8c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/16/2020
ms.locfileid: "97593860"
---
# <a name="resolve-assembly-loads"></a><span data-ttu-id="a1e0a-104">解析組件負載</span><span class="sxs-lookup"><span data-stu-id="a1e0a-104">Resolve assembly loads</span></span>

<span data-ttu-id="a1e0a-105">.NET <xref:System.AppDomain.AssemblyResolve?displayProperty=nameWithType> 為需要更充分掌控元件載入的應用程式提供事件。</span><span class="sxs-lookup"><span data-stu-id="a1e0a-105">.NET provides the <xref:System.AppDomain.AssemblyResolve?displayProperty=nameWithType> event for applications that require greater control over assembly loading.</span></span> <span data-ttu-id="a1e0a-106">藉由處理這個事件，您的應用程式可以將組件從一般探查路徑外部載入到載入內容、選取要載入的數個組件版本、發出動態組件，並傳回它，以此類推。</span><span class="sxs-lookup"><span data-stu-id="a1e0a-106">By handling this event, your application can load an assembly into the load context from outside the normal probing paths, select which of several assembly versions to load, emit a dynamic assembly and return it, and so on.</span></span> <span data-ttu-id="a1e0a-107">本主題提供處理 <xref:System.AppDomain.AssemblyResolve> 事件的指引。</span><span class="sxs-lookup"><span data-stu-id="a1e0a-107">This topic provides guidance for handling the <xref:System.AppDomain.AssemblyResolve> event.</span></span>

> [!NOTE]
> <span data-ttu-id="a1e0a-108">若要解析僅限反映內容中的組件載入，請改為使用 <xref:System.AppDomain.ReflectionOnlyAssemblyResolve?displayProperty=nameWithType> 事件。</span><span class="sxs-lookup"><span data-stu-id="a1e0a-108">For resolving assembly loads in the reflection-only context, use the <xref:System.AppDomain.ReflectionOnlyAssemblyResolve?displayProperty=nameWithType> event instead.</span></span>

## <a name="how-the-assemblyresolve-event-works"></a><span data-ttu-id="a1e0a-109">System.appdomain.assemblyresolve 事件的運作方式</span><span class="sxs-lookup"><span data-stu-id="a1e0a-109">How the AssemblyResolve event works</span></span>

<span data-ttu-id="a1e0a-110">當您註冊 <xref:System.AppDomain.AssemblyResolve> 事件的處理常式時，只要執行階段無法依名稱繫結至組件，就會叫用處理常式。</span><span class="sxs-lookup"><span data-stu-id="a1e0a-110">When you register a handler for the <xref:System.AppDomain.AssemblyResolve> event, the handler is invoked whenever the runtime fails to bind to an assembly by name.</span></span> <span data-ttu-id="a1e0a-111">例如，從使用者程式碼呼叫下列方法可能會引發 <xref:System.AppDomain.AssemblyResolve> 事件：</span><span class="sxs-lookup"><span data-stu-id="a1e0a-111">For example, calling the following methods from user code can cause the <xref:System.AppDomain.AssemblyResolve> event to be raised:</span></span>

- <span data-ttu-id="a1e0a-112">第一個引數是字串的 <xref:System.AppDomain.Load%2A?displayProperty=nameWithType> 方法多載或 <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> 方法多載，可代表要載入之組件的顯示名稱 (即 <xref:System.Reflection.Assembly.FullName%2A?displayProperty=nameWithType> 屬性所傳回的字串)。</span><span class="sxs-lookup"><span data-stu-id="a1e0a-112">An <xref:System.AppDomain.Load%2A?displayProperty=nameWithType> method overload or <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> method overload whose first argument is a string that represents the display name of the assembly to load (that is, the string returned by the <xref:System.Reflection.Assembly.FullName%2A?displayProperty=nameWithType> property).</span></span>

- <span data-ttu-id="a1e0a-113">第一個引數是 <xref:System.Reflection.AssemblyName> 物件的 <xref:System.AppDomain.Load%2A?displayProperty=nameWithType> 方法多載或 <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> 方法多載，可識別要載入的組件。</span><span class="sxs-lookup"><span data-stu-id="a1e0a-113">An <xref:System.AppDomain.Load%2A?displayProperty=nameWithType> method overload or <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> method overload whose first argument is an <xref:System.Reflection.AssemblyName> object that identifies the assembly to load.</span></span>

- <span data-ttu-id="a1e0a-114"><xref:System.Reflection.Assembly.LoadWithPartialName%2A?displayProperty=nameWithType> 方法多載。</span><span class="sxs-lookup"><span data-stu-id="a1e0a-114">An <xref:System.Reflection.Assembly.LoadWithPartialName%2A?displayProperty=nameWithType> method overload.</span></span>

- <span data-ttu-id="a1e0a-115">執行個體化另一個應用程式定義域中物件的 <xref:System.AppDomain.CreateInstance%2A?displayProperty=nameWithType> 或 <xref:System.AppDomain.CreateInstanceAndUnwrap%2A?displayProperty=nameWithType> 方法多載。</span><span class="sxs-lookup"><span data-stu-id="a1e0a-115">An <xref:System.AppDomain.CreateInstance%2A?displayProperty=nameWithType> or <xref:System.AppDomain.CreateInstanceAndUnwrap%2A?displayProperty=nameWithType> method overload that instantiates an object in another application domain.</span></span>

## <a name="what-the-event-handler-does"></a><span data-ttu-id="a1e0a-116">事件處理常式的作用</span><span class="sxs-lookup"><span data-stu-id="a1e0a-116">What the event handler does</span></span>

<span data-ttu-id="a1e0a-117"><xref:System.AppDomain.AssemblyResolve> 事件的處理常式會在 <xref:System.ResolveEventArgs.Name%2A?displayProperty=nameWithType> 屬性中接收要載入之組件的顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="a1e0a-117">The handler for the <xref:System.AppDomain.AssemblyResolve> event receives the display name of the assembly to be loaded, in the <xref:System.ResolveEventArgs.Name%2A?displayProperty=nameWithType> property.</span></span> <span data-ttu-id="a1e0a-118">如果處理常式無法辨識元件名稱，則會傳回 `null` (c # ) 、 `Nothing` (Visual Basic) 或 (Visual C++) `nullptr` 。</span><span class="sxs-lookup"><span data-stu-id="a1e0a-118">If the handler does not recognize the assembly name, it returns `null` (C#), `Nothing` (Visual Basic), or `nullptr` (Visual C++).</span></span>

<span data-ttu-id="a1e0a-119">如果處理常式可辨識組件名稱，則可以載入並傳回滿足要求的組件。</span><span class="sxs-lookup"><span data-stu-id="a1e0a-119">If the handler recognizes the assembly name, it can load and return an assembly that satisfies the request.</span></span> <span data-ttu-id="a1e0a-120">下列清單描述一些範例情節。</span><span class="sxs-lookup"><span data-stu-id="a1e0a-120">The following list describes some sample scenarios.</span></span>

- <span data-ttu-id="a1e0a-121">如果處理常式知道組件版本的位置，則可以使用 <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType> 或 <xref:System.Reflection.Assembly.LoadFile%2A?displayProperty=nameWithType> 方法來載入組件，而且可以在成功時傳回載入的組件。</span><span class="sxs-lookup"><span data-stu-id="a1e0a-121">If the handler knows the location of a version of the assembly, it can load the assembly by using the <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType> or <xref:System.Reflection.Assembly.LoadFile%2A?displayProperty=nameWithType> method, and can return the loaded assembly if successful.</span></span>

- <span data-ttu-id="a1e0a-122">如果處理常式可以存取儲存為位元組陣列之組件的資料庫，則可以使用其中一個接受位元組陣列的 <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> 方法多載來載入位元組陣列。</span><span class="sxs-lookup"><span data-stu-id="a1e0a-122">If the handler has access to a database of assemblies stored as byte arrays, it can load a byte array by using one of the <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> method overloads that take a byte array.</span></span>

- <span data-ttu-id="a1e0a-123">處理常式可以產生動態組件，並將它傳回。</span><span class="sxs-lookup"><span data-stu-id="a1e0a-123">The handler can generate a dynamic assembly and return it.</span></span>

> [!NOTE]
> <span data-ttu-id="a1e0a-124">處理常式必須將元件載入至載入來源內容、載入內容或沒有內容。</span><span class="sxs-lookup"><span data-stu-id="a1e0a-124">The handler must load the assembly into the load-from context, into the load context, or without context.</span></span> <span data-ttu-id="a1e0a-125">如果處理常式使用或方法，將元件載入至僅限反映的內容 <xref:System.Reflection.Assembly.ReflectionOnlyLoad%2A?displayProperty=nameWithType> <xref:System.Reflection.Assembly.ReflectionOnlyLoadFrom%2A?displayProperty=nameWithType> ，則引發事件的載入嘗試 <xref:System.AppDomain.AssemblyResolve> 會失敗。</span><span class="sxs-lookup"><span data-stu-id="a1e0a-125">If the handler loads the assembly into the reflection-only context by using the <xref:System.Reflection.Assembly.ReflectionOnlyLoad%2A?displayProperty=nameWithType> or the <xref:System.Reflection.Assembly.ReflectionOnlyLoadFrom%2A?displayProperty=nameWithType> method, the load attempt that raised the <xref:System.AppDomain.AssemblyResolve> event fails.</span></span>

<span data-ttu-id="a1e0a-126">它負責讓事件處理常式傳回適當的組件。</span><span class="sxs-lookup"><span data-stu-id="a1e0a-126">It is the responsibility of the event handler to return a suitable assembly.</span></span> <span data-ttu-id="a1e0a-127">處理常式可以將 <xref:System.ResolveEventArgs.Name%2A?displayProperty=nameWithType> 屬性值傳遞給 <xref:System.Reflection.AssemblyName.%23ctor%28System.String%29> 建構函式，以剖析所要求組件的顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="a1e0a-127">The handler can parse the display name of the requested assembly by passing the <xref:System.ResolveEventArgs.Name%2A?displayProperty=nameWithType> property value to the <xref:System.Reflection.AssemblyName.%23ctor%28System.String%29> constructor.</span></span> <span data-ttu-id="a1e0a-128">從 .NET Framework 4 開始，處理常式可以使用 <xref:System.ResolveEventArgs.RequestingAssembly%2A?displayProperty=nameWithType> 屬性來判斷目前的要求是否為另一個組件的相依性。</span><span class="sxs-lookup"><span data-stu-id="a1e0a-128">Beginning with the .NET Framework 4, the handler can use the <xref:System.ResolveEventArgs.RequestingAssembly%2A?displayProperty=nameWithType> property to determine whether the current request is a dependency of another assembly.</span></span> <span data-ttu-id="a1e0a-129">這項資訊可以協助識別將符合相依性的組件。</span><span class="sxs-lookup"><span data-stu-id="a1e0a-129">This information can help identify an assembly that will satisfy the dependency.</span></span>

<span data-ttu-id="a1e0a-130">事件處理常式可以傳回的組件版本與所要求的版本不同。</span><span class="sxs-lookup"><span data-stu-id="a1e0a-130">The event handler can return a different version of the assembly than the version that was requested.</span></span>

<span data-ttu-id="a1e0a-131">在大部分情況下，處理常式所傳回的組件會出現在載入內容中，不論處理常式將它載入的內容為何。</span><span class="sxs-lookup"><span data-stu-id="a1e0a-131">In most cases, the assembly that is returned by the handler appears in the load context, regardless of the context the handler loads it into.</span></span> <span data-ttu-id="a1e0a-132">例如，如果處理常式使用 <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType> 方法將組件載入到載入來源內容，則在處理常式傳回載入內容時，組件就會出現在載入內容中。</span><span class="sxs-lookup"><span data-stu-id="a1e0a-132">For example, if the handler uses the <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType> method to load an assembly into the load-from context, the assembly appears in the load context when the handler returns it.</span></span> <span data-ttu-id="a1e0a-133">不過，在下列情況下，組件在處理常式傳回它時沒有內容：</span><span class="sxs-lookup"><span data-stu-id="a1e0a-133">However, in the following case the assembly appears without context when the handler returns it:</span></span>

- <span data-ttu-id="a1e0a-134">處理常式會載入沒有內容的組件。</span><span class="sxs-lookup"><span data-stu-id="a1e0a-134">The handler loads an assembly without context.</span></span>

- <span data-ttu-id="a1e0a-135"><xref:System.ResolveEventArgs.RequestingAssembly%2A?displayProperty=nameWithType> 屬性不是 Null。</span><span class="sxs-lookup"><span data-stu-id="a1e0a-135">The <xref:System.ResolveEventArgs.RequestingAssembly%2A?displayProperty=nameWithType> property is not null.</span></span>

- <span data-ttu-id="a1e0a-136">已載入發出要求的組件 (即 <xref:System.ResolveEventArgs.RequestingAssembly%2A?displayProperty=nameWithType> 屬性所傳回的組件)，但沒有內容。</span><span class="sxs-lookup"><span data-stu-id="a1e0a-136">The requesting assembly (that is, the assembly that is returned by the <xref:System.ResolveEventArgs.RequestingAssembly%2A?displayProperty=nameWithType> property) was loaded without context.</span></span>

<span data-ttu-id="a1e0a-137">如需內容的資訊，請參閱 <xref:System.Reflection.Assembly.LoadFrom%28System.String%29?displayProperty=nameWithType> 方法多載。</span><span class="sxs-lookup"><span data-stu-id="a1e0a-137">For information about contexts, see the <xref:System.Reflection.Assembly.LoadFrom%28System.String%29?displayProperty=nameWithType> method overload.</span></span>

<span data-ttu-id="a1e0a-138">相同組件的多個版本可以載入相同的應用程式定義域。</span><span class="sxs-lookup"><span data-stu-id="a1e0a-138">Multiple versions of the same assembly can be loaded into the same application domain.</span></span> <span data-ttu-id="a1e0a-139">不建議這種做法，因為它可能會導致類型指派問題。</span><span class="sxs-lookup"><span data-stu-id="a1e0a-139">This practice is not recommended, because it can lead to type assignment problems.</span></span> <span data-ttu-id="a1e0a-140">請參閱 [元件載入的最佳做法](../../framework/deployment/best-practices-for-assembly-loading.md)。</span><span class="sxs-lookup"><span data-stu-id="a1e0a-140">See [Best practices for assembly loading](../../framework/deployment/best-practices-for-assembly-loading.md).</span></span>

## <a name="what-the-event-handler-should-not-do"></a><span data-ttu-id="a1e0a-141">事件處理常式不應採取的動作</span><span class="sxs-lookup"><span data-stu-id="a1e0a-141">What the event handler should not do</span></span>

<span data-ttu-id="a1e0a-142">處理 <xref:System.AppDomain.AssemblyResolve> 事件的主要規則是您不應該嘗試傳回無法辨識的組件。</span><span class="sxs-lookup"><span data-stu-id="a1e0a-142">The primary rule for handling the <xref:System.AppDomain.AssemblyResolve> event is that you should not try to return an assembly you do not recognize.</span></span> <span data-ttu-id="a1e0a-143">當您撰寫處理常式時，應該知道哪些組件可能會引發此事件。</span><span class="sxs-lookup"><span data-stu-id="a1e0a-143">When you write the handler, you should know which assemblies might cause the event to be raised.</span></span> <span data-ttu-id="a1e0a-144">針對其他組件，您的處理常式應該傳回 Null。</span><span class="sxs-lookup"><span data-stu-id="a1e0a-144">Your handler should return null for other assemblies.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a1e0a-145">從 .NET Framework 4 開始，會針對附屬組件引發 <xref:System.AppDomain.AssemblyResolve> 事件。</span><span class="sxs-lookup"><span data-stu-id="a1e0a-145">Beginning with the .NET Framework 4, the <xref:System.AppDomain.AssemblyResolve> event is raised for satellite assemblies.</span></span> <span data-ttu-id="a1e0a-146">如果處理常式嘗試解析所有組件載入要求，則這項變更會影響針對舊版 .NET Framework 所撰寫的事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="a1e0a-146">This change affects an event handler that was written for an earlier version of the .NET Framework, if the handler tries to resolve all assembly load requests.</span></span> <span data-ttu-id="a1e0a-147">忽略無法辨識之元件的事件處理常式不會受到這項變更的影響：它們會傳回 `null` ，而且會遵循一般的恢復機制。</span><span class="sxs-lookup"><span data-stu-id="a1e0a-147">Event handlers that ignore assemblies they do not recognize are not affected by this change: They return `null`, and normal fallback mechanisms are followed.</span></span>

<span data-ttu-id="a1e0a-148">載入組件時，事件處理常式不得使用任何 <xref:System.AppDomain.Load%2A?displayProperty=nameWithType> 或 <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> 方法多載，而此方法多載可以遞迴引發 <xref:System.AppDomain.AssemblyResolve> 事件，因為這可能會導致堆疊溢位。</span><span class="sxs-lookup"><span data-stu-id="a1e0a-148">When loading an assembly, the event handler must not use any of the <xref:System.AppDomain.Load%2A?displayProperty=nameWithType> or <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> method overloads that can cause the <xref:System.AppDomain.AssemblyResolve> event to be raised recursively, because this can lead to a stack overflow.</span></span> <span data-ttu-id="a1e0a-149"> (請參閱本主題稍早提供的清單 ) 。即使您提供載入要求的例外狀況處理，還是會發生這種情況，因為在所有事件處理常式都傳回之前，不會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="a1e0a-149">(See the list provided earlier in this topic.) This happens even if you provide exception handling for the load request, because no exception is thrown until all event handlers have returned.</span></span> <span data-ttu-id="a1e0a-150">因此，如果找不到 `MyAssembly`，則下列程式碼會導致堆疊溢位：</span><span class="sxs-lookup"><span data-stu-id="a1e0a-150">Thus, the following code results in a stack overflow if `MyAssembly` is not found:</span></span>

```csharp
using System;
using System.Reflection;

class BadExample
{
    static void Main()
    {
        AppDomain ad = AppDomain.CreateDomain("Test");
        ad.AssemblyResolve += MyHandler;

        try
        {
            object obj = ad.CreateInstanceAndUnwrap(
                "MyAssembly, version=1.2.3.4, culture=neutral, publicKeyToken=null",
                "MyType");
        }
        catch (Exception ex)
        {
            Console.WriteLine(ex.Message);
        }
    }

    static Assembly MyHandler(object source, ResolveEventArgs e)
    {
        Console.WriteLine("Resolving {0}", e.Name);
        // DO NOT DO THIS: This causes a StackOverflowException
        return Assembly.Load(e.Name);
    }
}

/* This example produces output similar to the following:

Resolving MyAssembly, Version=1.2.3.4, Culture=neutral, PublicKeyToken=null
Resolving MyAssembly, Version=1.2.3.4, Culture=neutral, PublicKeyToken=null
...
Resolving MyAssembly, Version=1.2.3.4, Culture=neutral, PublicKeyToken=null
Resolving MyAssembly, Version=1.2.3.4, Culture=neutral, PublicKeyToken=null

Process is terminated due to StackOverflowException.
 */
```

```vb
Imports System.Reflection

Class BadExample

    Shared Sub Main()

        Dim ad As AppDomain = AppDomain.CreateDomain("Test")
        AddHandler ad.AssemblyResolve, AddressOf MyHandler

        Try
            Dim obj As object = ad.CreateInstanceAndUnwrap(
                "MyAssembly, version=1.2.3.4, culture=neutral, publicKeyToken=null",
                "MyType")
        Catch ex As Exception
            Console.WriteLine(ex.Message)
        End Try
    End Sub

    Shared Function MyHandler(ByVal source As Object, _
                              ByVal e As ResolveEventArgs) As Assembly
        Console.WriteLine("Resolving {0}", e.Name)
        // DO NOT DO THIS: This causes a StackOverflowException
        Return Assembly.Load(e.Name)
    End Function
End Class

' This example produces output similar to the following:
'
'Resolving MyAssembly, Version=1.2.3.4, Culture=neutral, PublicKeyToken=null
'Resolving MyAssembly, Version=1.2.3.4, Culture=neutral, PublicKeyToken=null
'...
'Resolving MyAssembly, Version=1.2.3.4, Culture=neutral, PublicKeyToken=null
'Resolving MyAssembly, Version=1.2.3.4, Culture=neutral, PublicKeyToken=null
'
'Process is terminated due to StackOverflowException.
```

```cpp
using namespace System;
using namespace System::Reflection;

ref class Example
{
internal:
    static Assembly^ MyHandler(Object^ source, ResolveEventArgs^ e)
    {
        Console::WriteLine("Resolving {0}", e->Name);
        // DO NOT DO THIS: This causes a StackOverflowException
        return Assembly::Load(e->Name);
    }
};

void main()
{
    AppDomain^ ad = AppDomain::CreateDomain("Test");
    ad->AssemblyResolve += gcnew ResolveEventHandler(&Example::MyHandler);

    try
    {
        Object^ obj = ad->CreateInstanceAndUnwrap(
            "MyAssembly, version=1.2.3.4, culture=neutral, publicKeyToken=null",
            "MyType");
    }
    catch (Exception^ ex)
    {
        Console::WriteLine(ex->Message);
    }
}

/* This example produces output similar to the following:

Resolving MyAssembly, Version=1.2.3.4, Culture=neutral, PublicKeyToken=null
Resolving MyAssembly, Version=1.2.3.4, Culture=neutral, PublicKeyToken=null
...
Resolving MyAssembly, Version=1.2.3.4, Culture=neutral, PublicKeyToken=null
Resolving MyAssembly, Version=1.2.3.4, Culture=neutral, PublicKeyToken=null

Process is terminated due to StackOverflowException.
*/
```

### <a name="the-correct-way-to-handle-assemblyresolve"></a><span data-ttu-id="a1e0a-151">處理 System.appdomain.assemblyresolve 的正確方式</span><span class="sxs-lookup"><span data-stu-id="a1e0a-151">The correct way to handle AssemblyResolve</span></span>

<span data-ttu-id="a1e0a-152">從 <xref:System.AppDomain.AssemblyResolve> 事件處理常式解析元件時， <xref:System.StackOverflowException> 如果處理常式使用 <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> 或方法呼叫，最終將會擲回 <xref:System.AppDomain.Load%2A?displayProperty=nameWithType> 。</span><span class="sxs-lookup"><span data-stu-id="a1e0a-152">When resolving assemblies from the <xref:System.AppDomain.AssemblyResolve> event handler, a <xref:System.StackOverflowException> will eventually be thrown if the handler uses the <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> or <xref:System.AppDomain.Load%2A?displayProperty=nameWithType> method calls.</span></span> <span data-ttu-id="a1e0a-153">請改用 <xref:System.Reflection.Assembly.LoadFile%2A> 或 <xref:System.Reflection.Assembly.LoadFrom%2A> 方法，因為它們不會引發 `AssemblyResolve` 事件。</span><span class="sxs-lookup"><span data-stu-id="a1e0a-153">Instead, use <xref:System.Reflection.Assembly.LoadFile%2A> or <xref:System.Reflection.Assembly.LoadFrom%2A> methods, as they do not raise the `AssemblyResolve` event.</span></span>

<span data-ttu-id="a1e0a-154">想像一下 `MyAssembly.dll` 位於執行中元件附近的已知位置中，可以使用 `Assembly.LoadFile` 指定的元件路徑來解決此問題。</span><span class="sxs-lookup"><span data-stu-id="a1e0a-154">Imagine that `MyAssembly.dll` is located near the executing assembly, in a known location, it can be resolved using `Assembly.LoadFile` given the path to the assembly.</span></span>

```csharp
using System;
using System.IO;
using System.Reflection;

class CorrectExample
{
    static void Main()
    {
        AppDomain ad = AppDomain.CreateDomain("Test");
        ad.AssemblyResolve += MyHandler;

        try
        {
            object obj = ad.CreateInstanceAndUnwrap(
                "MyAssembly, version=1.2.3.4, culture=neutral, publicKeyToken=null",
                "MyType");
        }
        catch (Exception ex)
        {
            Console.WriteLine(ex.Message);
        }
    }

    static Assembly MyHandler(object source, ResolveEventArgs e)
    {
        Console.WriteLine("Resolving {0}", e.Name);

        var path = Path.GetFullPath("../../MyAssembly.dll");
        return Assembly.LoadFile(path);
     }
}
```

```vb
Imports System.IO
Imports System.Reflection

Class CorrectExample

    Shared Sub Main()

        Dim ad As AppDomain = AppDomain.CreateDomain("Test")
        AddHandler ad.AssemblyResolve, AddressOf MyHandler

        Try
            Dim obj As Object = ad.CreateInstanceAndUnwrap(
                "MyAssembly, version=1.2.3.4, culture=neutral, publicKeyToken=null",
                "MyType")
        Catch ex As Exception
            Console.WriteLine(ex.Message)
        End Try
    End Sub

    Shared Function MyHandler(ByVal source As Object,
                              ByVal e As ResolveEventArgs) As Assembly
        Console.WriteLine("Resolving {0}", e.Name)

        Dim fullPath = Path.GetFullPath("../../MyAssembly.dll")
        Return Assembly.LoadFile(fullPath)
    End Function
End Class
```

```cpp
using namespace System;
using namespace System::IO;
using namespace System::Reflection;

ref class Example
{
internal:
    static Assembly^ MyHandler(Object^ source, ResolveEventArgs^ e)
    {
        Console::WriteLine("Resolving {0}", e->Name);

        String^ fullPath = Path::GetFullPath("../../MyAssembly.dll");
        return Assembly::LoadFile(fullPath);
    }
};

void main()
{
    AppDomain^ ad = AppDomain::CreateDomain("Test");
    ad->AssemblyResolve += gcnew ResolveEventHandler(&Example::MyHandler);

    try
    {
        Object^ obj = ad->CreateInstanceAndUnwrap(
            "MyAssembly, version=1.2.3.4, culture=neutral, publicKeyToken=null",
            "MyType");
    }
    catch (Exception^ ex)
    {
        Console::WriteLine(ex->Message);
    }
}
```

## <a name="see-also"></a><span data-ttu-id="a1e0a-155">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a1e0a-155">See also</span></span>

- [<span data-ttu-id="a1e0a-156">元件載入的最佳做法</span><span class="sxs-lookup"><span data-stu-id="a1e0a-156">Best practices for assembly loading</span></span>](../../framework/deployment/best-practices-for-assembly-loading.md)
- [<span data-ttu-id="a1e0a-157">使用應用程式域</span><span class="sxs-lookup"><span data-stu-id="a1e0a-157">Use application domains</span></span>](../../framework/app-domains/use.md)
