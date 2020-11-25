---
title: 解析組件負載
description: 本文描述 .NET AppDomain. System.appdomain.assemblyresolve 事件。 針對需要控制元件載入的應用程式，請使用此事件。
ms.date: 08/20/2019
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
ms.openlocfilehash: edd101e57793668d71d44db08f191ae412c6d998
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95720902"
---
# <a name="resolve-assembly-loads"></a>解析組件負載

.NET <xref:System.AppDomain.AssemblyResolve?displayProperty=nameWithType> 為需要更充分掌控元件載入的應用程式提供事件。 藉由處理這個事件，您的應用程式可以將組件從一般探查路徑外部載入到載入內容、選取要載入的數個組件版本、發出動態組件，並傳回它，以此類推。 本主題提供處理 <xref:System.AppDomain.AssemblyResolve> 事件的指引。  
  
> [!NOTE]
> 若要解析僅限反映內容中的組件載入，請改為使用 <xref:System.AppDomain.ReflectionOnlyAssemblyResolve?displayProperty=nameWithType> 事件。  
  
## <a name="how-the-assemblyresolve-event-works"></a>System.appdomain.assemblyresolve 事件的運作方式  

 當您註冊 <xref:System.AppDomain.AssemblyResolve> 事件的處理常式時，只要執行階段無法依名稱繫結至組件，就會叫用處理常式。 例如，從使用者程式碼呼叫下列方法可能會引發 <xref:System.AppDomain.AssemblyResolve> 事件：  
  
- 第一個引數是字串的 <xref:System.AppDomain.Load%2A?displayProperty=nameWithType> 方法多載或 <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> 方法多載，可代表要載入之組件的顯示名稱 (即 <xref:System.Reflection.Assembly.FullName%2A?displayProperty=nameWithType> 屬性所傳回的字串)。  
  
- 第一個引數是 <xref:System.Reflection.AssemblyName> 物件的 <xref:System.AppDomain.Load%2A?displayProperty=nameWithType> 方法多載或 <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> 方法多載，可識別要載入的組件。  
  
- <xref:System.Reflection.Assembly.LoadWithPartialName%2A?displayProperty=nameWithType> 方法多載。  
  
- 執行個體化另一個應用程式定義域中物件的 <xref:System.AppDomain.CreateInstance%2A?displayProperty=nameWithType> 或 <xref:System.AppDomain.CreateInstanceAndUnwrap%2A?displayProperty=nameWithType> 方法多載。  
  
### <a name="what-the-event-handler-does"></a>事件處理常式的作用  

 <xref:System.AppDomain.AssemblyResolve> 事件的處理常式會在 <xref:System.ResolveEventArgs.Name%2A?displayProperty=nameWithType> 屬性中接收要載入之組件的顯示名稱。 如果處理常式無法辨識元件名稱，則會傳回 `null` (c # ) 、 `Nothing` (Visual Basic) 或 (Visual C++) `nullptr` 。  
  
 如果處理常式可辨識組件名稱，則可以載入並傳回滿足要求的組件。 下列清單描述一些範例情節。  
  
- 如果處理常式知道組件版本的位置，則可以使用 <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType> 或 <xref:System.Reflection.Assembly.LoadFile%2A?displayProperty=nameWithType> 方法來載入組件，而且可以在成功時傳回載入的組件。  
  
- 如果處理常式可以存取儲存為位元組陣列之組件的資料庫，則可以使用其中一個接受位元組陣列的 <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> 方法多載來載入位元組陣列。  
  
- 處理常式可以產生動態組件，並將它傳回。  
  
> [!NOTE]
> 此處理常式必須將組件載入到載入來源內容、到載入內容，或沒有內容。如果此處理常式使用 <xref:System.Reflection.Assembly.ReflectionOnlyLoad%2A?displayProperty=nameWithType> 或 <xref:System.Reflection.Assembly.ReflectionOnlyLoadFrom%2A?displayProperty=nameWithType> 方法以將組件載入僅限反映的內容，則引發 <xref:System.AppDomain.AssemblyResolve> 事件的載入嘗試會失敗。  
  
 它負責讓事件處理常式傳回適當的組件。 處理常式可以將 <xref:System.ResolveEventArgs.Name%2A?displayProperty=nameWithType> 屬性值傳遞給 <xref:System.Reflection.AssemblyName.%23ctor%28System.String%29> 建構函式，以剖析所要求組件的顯示名稱。 從 .NET Framework 4 開始，處理常式可以使用 <xref:System.ResolveEventArgs.RequestingAssembly%2A?displayProperty=nameWithType> 屬性來判斷目前的要求是否為另一個組件的相依性。 這項資訊可以協助識別將符合相依性的組件。  
  
 事件處理常式可以傳回的組件版本與所要求的版本不同。  
  
 在大部分情況下，處理常式所傳回的組件會出現在載入內容中，不論處理常式將它載入的內容為何。 例如，如果處理常式使用 <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType> 方法將組件載入到載入來源內容，則在處理常式傳回載入內容時，組件就會出現在載入內容中。 不過，在下列情況下，組件在處理常式傳回它時沒有內容：  
  
- 處理常式會載入沒有內容的組件。  
  
- <xref:System.ResolveEventArgs.RequestingAssembly%2A?displayProperty=nameWithType> 屬性不是 Null。  
  
- 已載入發出要求的組件 (即 <xref:System.ResolveEventArgs.RequestingAssembly%2A?displayProperty=nameWithType> 屬性所傳回的組件)，但沒有內容。  
  
 如需內容的資訊，請參閱 <xref:System.Reflection.Assembly.LoadFrom%28System.String%29?displayProperty=nameWithType> 方法多載。  
  
 相同組件的多個版本可以載入相同的應用程式定義域。 不建議這種做法，因為它可能會導致類型指派問題。 請參閱 [元件載入的最佳做法](../../framework/deployment/best-practices-for-assembly-loading.md)。  
  
### <a name="what-the-event-handler-should-not-do"></a>事件處理常式不應採取的動作  

處理 <xref:System.AppDomain.AssemblyResolve> 事件的主要規則是您不應該嘗試傳回無法辨識的組件。 當您撰寫處理常式時，應該知道哪些組件可能會引發此事件。 針對其他組件，您的處理常式應該傳回 Null。  

> [!IMPORTANT]
> 從 .NET Framework 4 開始，會針對附屬組件引發 <xref:System.AppDomain.AssemblyResolve> 事件。 如果處理常式嘗試解析所有組件載入要求，則這項變更會影響針對舊版 .NET Framework 所撰寫的事件處理常式。 略過無法辨識之組件的事件處理常式不會受到這項變更的影響：它們會傳回 Null，並遵循正常後援機制。  

載入組件時，事件處理常式不得使用任何 <xref:System.AppDomain.Load%2A?displayProperty=nameWithType> 或 <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> 方法多載，而此方法多載可以遞迴引發 <xref:System.AppDomain.AssemblyResolve> 事件，因為這可能會導致堆疊溢位。  (請參閱本主題稍早提供的清單 ) 。即使您提供載入要求的例外狀況處理，還是會發生這種情況，因為在所有事件處理常式都傳回之前，不會擲回例外狀況。 因此，如果找不到 `MyAssembly`，則下列程式碼會導致堆疊溢位：  

```cpp
using namespace System;
using namespace System::Reflection;

ref class Example
{
internal:
    static Assembly^ MyHandler(Object^ source, ResolveEventArgs^ e)
    {
        Console::WriteLine("Resolving {0}", e->Name);
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

## <a name="see-also"></a>另請參閱

- [元件載入的最佳做法](../../framework/deployment/best-practices-for-assembly-loading.md)
- [使用應用程式域](../../framework/app-domains/use.md)
