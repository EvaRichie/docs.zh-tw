---
title: 在 Managed 程式碼中建立原型
description: 在 .NET managed 程式碼中建立原型，讓您可以存取未受管理的函式，並使用在 managed 程式碼中標注方法定義的屬性欄位。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- prototypes in managed code
- COM interop, DLL functions
- unmanaged functions
- platform invoke, creating prototypes
- COM interop, platform invoke
- interoperation with unmanaged code, DLL functions
- interoperation with unmanaged code, platform invoke
- platform invoke, object fields
- DLL functions
- object fields in platform invoke
ms.assetid: ecdcf25d-cae3-4f07-a2b6-8397ac6dc42d
ms.openlocfilehash: e83979e5843c52fc3a446a5b669ae8822b32ddad
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90555584"
---
# <a name="creating-prototypes-in-managed-code"></a>在 Managed 程式碼中建立原型
本主題描述如何存取 Unmanaged 函式，並介紹數個以 Managed 程式碼來註解方法定義的屬性欄位。 如需示範如何建構要與平台叫用搭配使用之 .NET 型宣告的範例，請參閱[使用平台叫用封送處理資料](marshaling-data-with-platform-invoke.md)。  
  
 在您可以從 Managed 程式碼存取 Unmanaged DLL 函式之前，您需要知道函式的名稱，以及將它匯出的 DLL 名稱。 利用此資訊，您可以開始撰寫 Managed 定義給在 DLL 中實作的 Unmanaged 函式。 此外，您可以調整叫用平台建立函式和封送處理資料給予或來自函式的方式。  
  
> [!NOTE]
> 配置字串的 Windows API 函式可讓您使用下列方法釋放字串，例如 `LocalFree`。 平台叫用以不同方式處理這類參數。 為了平台叫用呼叫，將參數設定為 `IntPtr` 類型而非 `String` 類型。 使用 <xref:System.Runtime.InteropServices.Marshal?displayProperty=nameWithType> 類別所提供的方法來手動將類型轉換為字串，並手動釋放。  
  
## <a name="declaration-basics"></a>宣告的基本概念  
 Unmanaged 函式的 Managed 定義會依語言而異，您可以在下列範例中觀察到。 如需更完整的程式碼範例，請參閱[平台叫用範例](platform-invoke-examples.md)。  
  
```vb
Friend Class NativeMethods
    Friend Declare Auto Function MessageBox Lib "user32.dll" (
        ByVal hWnd As IntPtr,
        ByVal lpText As String,
        ByVal lpCaption As String,
        ByVal uType As UInteger) As Integer
End Class
```
  
 若要將 <xref:System.Runtime.InteropServices.DllImportAttribute.BestFitMapping?displayProperty=nameWithType>、<xref:System.Runtime.InteropServices.DllImportAttribute.CallingConvention?displayProperty=nameWithType>、<xref:System.Runtime.InteropServices.DllImportAttribute.ExactSpelling?displayProperty=nameWithType>、<xref:System.Runtime.InteropServices.DllImportAttribute.PreserveSig?displayProperty=nameWithType>、<xref:System.Runtime.InteropServices.DllImportAttribute.SetLastError?displayProperty=nameWithType> 或 <xref:System.Runtime.InteropServices.DllImportAttribute.ThrowOnUnmappableChar?displayProperty=nameWithType> 欄位套用至 Visual Basic 宣告，您必須使用 <xref:System.Runtime.InteropServices.DllImportAttribute> 屬性，而不是 `Declare` 陳述式。  
  
```vb
Imports System.Runtime.InteropServices

Friend Class NativeMethods
    <DllImport("user32.dll", CharSet:=CharSet.Auto)>
    Friend Shared Function MessageBox(
        ByVal hWnd As IntPtr,
        ByVal lpText As String,
        ByVal lpCaption As String,
        ByVal uType As UInteger) As Integer
    End Function
End Class
```
  
```csharp
using System;
using System.Runtime.InteropServices;

internal static class NativeMethods
{
    [DllImport("user32.dll")]
    internal static extern int MessageBox(
        IntPtr hWnd, string lpText, string lpCaption, uint uType);
}
```
  
```cpp
using namespace System;
using namespace System::Runtime::InteropServices;

[DllImport("user32.dll")]
extern "C" int MessageBox(
    IntPtr hWnd, String* lpText, String* lpCaption, unsigned int uType);
```
  
## <a name="adjusting-the-definition"></a>調整定義  
 不論您是否明確地設定它們，屬性欄位都會定義 Managed 程式碼的行為。 平台叫用操作根據以中繼資料的形式存在於組件中的各種欄位上所設定的預設值。 您可以藉由調整一或多個欄位的值來變更此預設行為。 在許多情況下，您會使用 <xref:System.Runtime.InteropServices.DllImportAttribute> 來設定該值。  
  
 下表列出一組平台叫用的完整屬性欄位。 在每個欄位裡，資料表包含預設值以及連結，關於如何使用這些欄位來定義 Unmanaged DLL 函式的詳細資訊。  
  
|欄位|說明|  
|-----------|-----------------|  
|<xref:System.Runtime.InteropServices.DllImportAttribute.BestFitMapping>|啟用或停用自動調整對應。|  
|<xref:System.Runtime.InteropServices.DllImportAttribute.CallingConvention>|指定用來傳遞方法引數的呼叫慣例。 預設值是 `WinAPI` ，它對應至適用於 32 位元 Intel 平台的 `__stdcall` 。|  
|<xref:System.Runtime.InteropServices.DllImportAttribute.CharSet>|控制項名稱的損害以及字串引數的方式應該封送處理至函式。 預設為 `CharSet.Ansi`。|  
|<xref:System.Runtime.InteropServices.DllImportAttribute.EntryPoint>|指定要呼叫 DLL 進入點。|  
|<xref:System.Runtime.InteropServices.DllImportAttribute.ExactSpelling>|控制是否應修改進入點以對應至字元集。 預設值依程式語言而異。|  
|<xref:System.Runtime.InteropServices.DllImportAttribute.PreserveSig>|控制是否應將 Managed 方法簽章轉換成 Unmanaged 簽章，其會傳回 HRESULT 且傳回值會有額外的 [out, retval] 引數。<br /><br /> 預設值是 `true` (簽章不應該轉換)。|  
|<xref:System.Runtime.InteropServices.DllImportAttribute.SetLastError>|可讓呼叫者使用 `Marshal.GetLastWin32Error` API 函式來判斷當執行此方法時是否發生錯誤。 在 Visual Basic 中，預設值是 `true`；在 C# 和 C++ 中，預設值是  `false`。|  
|<xref:System.Runtime.InteropServices.DllImportAttribute.ThrowOnUnmappableChar>|在無法對應 Unicode 字元的例外狀況中，控制項的擲回轉換成 ANSI "?" 字元。|  
  
 如需詳細參考資訊，請參閱 <xref:System.Runtime.InteropServices.DllImportAttribute>。  
  
## <a name="platform-invoke-security-considerations"></a>平台叫用安全性考量  
 <xref:System.Security.Permissions.SecurityAction> 列舉的 `Assert`、`Deny` 和 `PermitOnly` 成員稱為「堆疊查核修飾詞」**。 如果這些成員被做為平台叫用宣告式和 COM 介面定義語言 (IDL) 陳述式的宣告式屬性，就會忽略這些成員。  
  
### <a name="platform-invoke-examples"></a>平台叫用範例  
 本節中的平台叫用範例將說明如何使用具有堆疊查核行程修飾詞的  `RegistryPermission` 屬性。  
  
 在下列範例中，<xref:System.Security.Permissions.SecurityAction>`Assert`、`Deny` 和 `PermitOnly` 修飾詞會被忽略。  
  
```csharp  
[DllImport("MyClass.dll", EntryPoint = "CallRegistryPermission")]  
[RegistryPermission(SecurityAction.Assert, Unrestricted = true)]  
    private static extern bool CallRegistryPermissionAssert();  
  
[DllImport("MyClass.dll", EntryPoint = "CallRegistryPermission")]  
[RegistryPermission(SecurityAction.Deny, Unrestricted = true)]  
    private static extern bool CallRegistryPermissionDeny();  
  
[DllImport("MyClass.dll", EntryPoint = "CallRegistryPermission")]  
[RegistryPermission(SecurityAction.PermitOnly, Unrestricted = true)]  
    private static extern bool CallRegistryPermissionDeny();  
```  
  
 不過，`Demand` 修飾詞，在下列範例中會被接受。  
  
```csharp
[DllImport("MyClass.dll", EntryPoint = "CallRegistryPermission")]  
[RegistryPermission(SecurityAction.Demand, Unrestricted = true)]  
    private static extern bool CallRegistryPermissionDeny();  
```  
  
 如果它們被放在包含 (換行) 平台叫用呼叫的類別上，<xref:System.Security.Permissions.SecurityAction> 修飾詞會正常運作。  
  
```cpp  
      [RegistryPermission(SecurityAction.Demand, Unrestricted = true)]  
public ref class PInvokeWrapper  
{  
public:  
[DllImport("MyClass.dll", EntryPoint = "CallRegistryPermission")]  
    private static extern bool CallRegistryPermissionDeny();  
};  
```  
  
```csharp  
[RegistryPermission(SecurityAction.Demand, Unrestricted = true)]  
class PInvokeWrapper  
{  
[DllImport("MyClass.dll", EntryPoint = "CallRegistryPermission")]  
    private static extern bool CallRegistryPermissionDeny();  
}  
```  
  
 <xref:System.Security.Permissions.SecurityAction> 修飾詞也會正確運作於巢狀案例中，其中它們被放在平台叫用呼叫的呼叫者上：  
  
```cpp  
      {  
public ref class PInvokeWrapper  
public:  
    [DllImport("MyClass.dll", EntryPoint = "CallRegistryPermission")]  
    private static extern bool CallRegistryPermissionDeny();  
  
    [RegistryPermission(SecurityAction.Demand, Unrestricted = true)]  
    public static bool CallRegistryPermission()  
    {  
     return CallRegistryPermissionInternal();  
    }  
};  
```  
  
```csharp  
class PInvokeScenario  
{  
    [DllImport("MyClass.dll", EntryPoint = "CallRegistryPermission")]  
    private static extern bool CallRegistryPermissionInternal();  
  
    [RegistryPermission(SecurityAction.Assert, Unrestricted = true)]  
    public static bool CallRegistryPermission()  
    {  
     return CallRegistryPermissionInternal();  
    }  
}  
```  
  
#### <a name="com-interop-examples"></a>COM Interop 範例  
 本節中的 COM Interop 範例說明使用具有堆疊查核行程修飾詞的 `RegistryPermission` 屬性。  
  
 下列 COM Interop 介面宣告忽略 `Assert` 、 `Deny` 和 `PermitOnly` 修飾詞，類似於先前章節中的平台叫用範例。  
  
```csharp
[ComImport, Guid("12345678-43E6-43c9-9A13-47F40B338DE0")]  
interface IAssertStubsItf  
{  
[RegistryPermission(SecurityAction.Assert, Unrestricted = true)]  
    bool CallRegistryPermission();  
[FileIOPermission(SecurityAction.Assert, Unrestricted = true)]  
    bool CallFileIoPermission();  
}  
  
[ComImport, Guid("12345678-43E6-43c9-9A13-47F40B338DE0")]  
interface IDenyStubsItf  
{  
[RegistryPermission(SecurityAction.Deny, Unrestricted = true)]  
    bool CallRegistryPermission();  
[FileIOPermission(SecurityAction.Deny, Unrestricted = true)]  
    bool CallFileIoPermission();  
}  
  
[ComImport, Guid("12345678-43E6-43c9-9A13-47F40B338DE0")]  
interface IAssertStubsItf  
{  
[RegistryPermission(SecurityAction.PermitOnly, Unrestricted = true)]  
    bool CallRegistryPermission();  
[FileIOPermission(SecurityAction.PermitOnly, Unrestricted = true)]  
    bool CallFileIoPermission();  
}  
```  
  
 此外，如下列範例所示，在 COM Interop 介面宣告的情況下，不接受 `Demand` 修飾詞。  
  
```csharp  
[ComImport, Guid("12345678-43E6-43c9-9A13-47F40B338DE0")]  
interface IDemandStubsItf  
{  
[RegistryPermission(SecurityAction.Demand, Unrestricted = true)]  
    bool CallRegistryPermission();  
[FileIOPermission(SecurityAction.Demand, Unrestricted = true)]  
    bool CallFileIoPermission();  
}  
```  
  
## <a name="see-also"></a>另請參閱

- [使用 Unmanaged DLL 函式](consuming-unmanaged-dll-functions.md)
- [指定進入點](specifying-an-entry-point.md)
- [指定字元集](specifying-a-character-set.md)
- [平台叫用範例](platform-invoke-examples.md)
- [平台叫用安全性考量](/previous-versions/dotnet/netframework-4.0/bb397754(v=vs.100))
- [識別 DLL 中的函式](identifying-functions-in-dlls.md)
- [建立類別以包裝 DLL 函式](creating-a-class-to-hold-dll-functions.md)
- [呼叫 DLL 函式](calling-a-dll-function.md)
