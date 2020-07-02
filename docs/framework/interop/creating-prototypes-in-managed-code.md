---
title: 在 Managed 程式碼中建立原型
description: 在 .NET managed 程式碼中建立原型，讓您可以存取非受控函式，並使用在 managed 程式碼中標注方法定義的屬性欄位。
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
ms.openlocfilehash: 76b1a87c4513fdee21c5c3d5eba533b11e022e3a
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85622155"
---
# <a name="creating-prototypes-in-managed-code"></a><span data-ttu-id="16516-103">在 Managed 程式碼中建立原型</span><span class="sxs-lookup"><span data-stu-id="16516-103">Creating Prototypes in Managed Code</span></span>
<span data-ttu-id="16516-104">本主題描述如何存取 Unmanaged 函式，並介紹數個以 Managed 程式碼來註解方法定義的屬性欄位。</span><span class="sxs-lookup"><span data-stu-id="16516-104">This topic describes how to access unmanaged functions and introduces several attribute fields that annotate method definition in managed code.</span></span> <span data-ttu-id="16516-105">如需示範如何建構要與平台叫用搭配使用之 .NET 型宣告的範例，請參閱[使用平台叫用封送處理資料](marshaling-data-with-platform-invoke.md)。</span><span class="sxs-lookup"><span data-stu-id="16516-105">For examples that demonstrate how to construct .NET-based declarations to be used with platform invoke, see [Marshaling Data with Platform Invoke](marshaling-data-with-platform-invoke.md).</span></span>  
  
 <span data-ttu-id="16516-106">在您可以從 Managed 程式碼存取 Unmanaged DLL 函式之前，您需要知道函式的名稱，以及將它匯出的 DLL 名稱。</span><span class="sxs-lookup"><span data-stu-id="16516-106">Before you can access an unmanaged DLL function from managed code, you need to know the name of the function and the name of the DLL that exports it.</span></span> <span data-ttu-id="16516-107">利用此資訊，您可以開始撰寫 Managed 定義給在 DLL 中實作的 Unmanaged 函式。</span><span class="sxs-lookup"><span data-stu-id="16516-107">With this information, you can begin to write the managed definition for an unmanaged function that is implemented in a DLL.</span></span> <span data-ttu-id="16516-108">此外，您可以調整叫用平台建立函式和封送處理資料給予或來自函式的方式。</span><span class="sxs-lookup"><span data-stu-id="16516-108">Furthermore, you can adjust the way that platform invoke creates the function and marshals data to and from the function.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="16516-109">配置字串的 Windows API 函式可讓您使用下列方法釋放字串，例如 `LocalFree`。</span><span class="sxs-lookup"><span data-stu-id="16516-109">Windows API functions that allocate a string enable you to free the string by using a method such as `LocalFree`.</span></span> <span data-ttu-id="16516-110">平台叫用以不同方式處理這類參數。</span><span class="sxs-lookup"><span data-stu-id="16516-110">Platform invoke handles such parameters differently.</span></span> <span data-ttu-id="16516-111">為了平台叫用呼叫，將參數設定為 `IntPtr` 類型而非 `String` 類型。</span><span class="sxs-lookup"><span data-stu-id="16516-111">For platform invoke calls, make the parameter an `IntPtr` type instead of a `String` type.</span></span> <span data-ttu-id="16516-112">使用 <xref:System.Runtime.InteropServices.Marshal?displayProperty=nameWithType> 類別所提供的方法來手動將類型轉換為字串，並手動釋放。</span><span class="sxs-lookup"><span data-stu-id="16516-112">Use methods that are provided by the <xref:System.Runtime.InteropServices.Marshal?displayProperty=nameWithType> class to convert the type to a string manually and free it manually.</span></span>  
  
## <a name="declaration-basics"></a><span data-ttu-id="16516-113">宣告的基本概念</span><span class="sxs-lookup"><span data-stu-id="16516-113">Declaration Basics</span></span>  
 <span data-ttu-id="16516-114">Unmanaged 函式的 Managed 定義會依語言而異，您可以在下列範例中觀察到。</span><span class="sxs-lookup"><span data-stu-id="16516-114">Managed definitions to unmanaged functions are language-dependent, as you can see in the following examples.</span></span> <span data-ttu-id="16516-115">如需更完整的程式碼範例，請參閱[平台叫用範例](platform-invoke-examples.md)。</span><span class="sxs-lookup"><span data-stu-id="16516-115">For more complete code examples, see [Platform Invoke Examples](platform-invoke-examples.md).</span></span>  
  
```vb
Friend Class NativeMethods
    Friend Declare Auto Function MessageBox Lib "user32.dll" (
        ByVal hWnd As IntPtr,
        ByVal lpText As String,
        ByVal lpCaption As String,
        ByVal uType As UInteger) As Integer
End Class
```
  
 <span data-ttu-id="16516-116">若要將 <xref:System.Runtime.InteropServices.DllImportAttribute.BestFitMapping?displayProperty=nameWithType>、<xref:System.Runtime.InteropServices.DllImportAttribute.CallingConvention?displayProperty=nameWithType>、<xref:System.Runtime.InteropServices.DllImportAttribute.ExactSpelling?displayProperty=nameWithType>、<xref:System.Runtime.InteropServices.DllImportAttribute.PreserveSig?displayProperty=nameWithType>、<xref:System.Runtime.InteropServices.DllImportAttribute.SetLastError?displayProperty=nameWithType> 或 <xref:System.Runtime.InteropServices.DllImportAttribute.ThrowOnUnmappableChar?displayProperty=nameWithType> 欄位套用至 Visual Basic 宣告，您必須使用 <xref:System.Runtime.InteropServices.DllImportAttribute> 屬性，而不是 `Declare` 陳述式。</span><span class="sxs-lookup"><span data-stu-id="16516-116">To apply the <xref:System.Runtime.InteropServices.DllImportAttribute.BestFitMapping?displayProperty=nameWithType>, <xref:System.Runtime.InteropServices.DllImportAttribute.CallingConvention?displayProperty=nameWithType>, <xref:System.Runtime.InteropServices.DllImportAttribute.ExactSpelling?displayProperty=nameWithType>, <xref:System.Runtime.InteropServices.DllImportAttribute.PreserveSig?displayProperty=nameWithType>, <xref:System.Runtime.InteropServices.DllImportAttribute.SetLastError?displayProperty=nameWithType>, or <xref:System.Runtime.InteropServices.DllImportAttribute.ThrowOnUnmappableChar?displayProperty=nameWithType> fields to a Visual Basic declaration, you must use the <xref:System.Runtime.InteropServices.DllImportAttribute> attribute instead of the `Declare` statement.</span></span>  
  
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
  
## <a name="adjusting-the-definition"></a><span data-ttu-id="16516-117">調整定義</span><span class="sxs-lookup"><span data-stu-id="16516-117">Adjusting the Definition</span></span>  
 <span data-ttu-id="16516-118">不論您是否明確地設定它們，屬性欄位都會定義 Managed 程式碼的行為。</span><span class="sxs-lookup"><span data-stu-id="16516-118">Whether you set them explicitly or not, attribute fields are at work defining the behavior of managed code.</span></span> <span data-ttu-id="16516-119">平台叫用操作根據以中繼資料的形式存在於組件中的各種欄位上所設定的預設值。</span><span class="sxs-lookup"><span data-stu-id="16516-119">Platform invoke operates according to the default values set on various fields that exist as metadata in an assembly.</span></span> <span data-ttu-id="16516-120">您可以藉由調整一或多個欄位的值來變更此預設行為。</span><span class="sxs-lookup"><span data-stu-id="16516-120">You can alter this default behavior by adjusting the values of one or more fields.</span></span> <span data-ttu-id="16516-121">在許多情況下，您會使用 <xref:System.Runtime.InteropServices.DllImportAttribute> 來設定該值。</span><span class="sxs-lookup"><span data-stu-id="16516-121">In many cases, you use the <xref:System.Runtime.InteropServices.DllImportAttribute> to set a value.</span></span>  
  
 <span data-ttu-id="16516-122">下表列出一組平台叫用的完整屬性欄位。</span><span class="sxs-lookup"><span data-stu-id="16516-122">The following table lists the complete set of attribute fields that pertain to platform invoke.</span></span> <span data-ttu-id="16516-123">在每個欄位裡，資料表包含預設值以及連結，關於如何使用這些欄位來定義 Unmanaged DLL 函式的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="16516-123">For each field, the table includes the default value and a link to information on how to use these fields to define unmanaged DLL functions.</span></span>  
  
|<span data-ttu-id="16516-124">欄位</span><span class="sxs-lookup"><span data-stu-id="16516-124">Field</span></span>|<span data-ttu-id="16516-125">描述</span><span class="sxs-lookup"><span data-stu-id="16516-125">Description</span></span>|  
|-----------|-----------------|  
|<xref:System.Runtime.InteropServices.DllImportAttribute.BestFitMapping>|<span data-ttu-id="16516-126">啟用或停用自動調整對應。</span><span class="sxs-lookup"><span data-stu-id="16516-126">Enables or disables best-fit mapping.</span></span>|  
|<xref:System.Runtime.InteropServices.DllImportAttribute.CallingConvention>|<span data-ttu-id="16516-127">指定用來傳遞方法引數的呼叫慣例。</span><span class="sxs-lookup"><span data-stu-id="16516-127">Specifies the calling convention to use in passing method arguments.</span></span> <span data-ttu-id="16516-128">預設值是 `WinAPI` ，它對應至適用於 32 位元 Intel 平台的 `__stdcall` 。</span><span class="sxs-lookup"><span data-stu-id="16516-128">The default is `WinAPI`, which corresponds to `__stdcall` for the 32-bit Intel-based platforms.</span></span>|  
|<xref:System.Runtime.InteropServices.DllImportAttribute.CharSet>|<span data-ttu-id="16516-129">控制項名稱的損害以及字串引數的方式應該封送處理至函式。</span><span class="sxs-lookup"><span data-stu-id="16516-129">Controls name mangling and the way that string arguments should be marshaled to the function.</span></span> <span data-ttu-id="16516-130">預設值為 `CharSet.Ansi`。</span><span class="sxs-lookup"><span data-stu-id="16516-130">The default is `CharSet.Ansi`.</span></span>|  
|<xref:System.Runtime.InteropServices.DllImportAttribute.EntryPoint>|<span data-ttu-id="16516-131">指定要呼叫 DLL 進入點。</span><span class="sxs-lookup"><span data-stu-id="16516-131">Specifies the DLL entry point to be called.</span></span>|  
|<xref:System.Runtime.InteropServices.DllImportAttribute.ExactSpelling>|<span data-ttu-id="16516-132">控制是否應修改進入點以對應至字元集。</span><span class="sxs-lookup"><span data-stu-id="16516-132">Controls whether an entry point should be modified to correspond to the character set.</span></span> <span data-ttu-id="16516-133">預設值依程式語言而異。</span><span class="sxs-lookup"><span data-stu-id="16516-133">The default value varies by programming language.</span></span>|  
|<xref:System.Runtime.InteropServices.DllImportAttribute.PreserveSig>|<span data-ttu-id="16516-134">控制是否應將 Managed 方法簽章轉換成 Unmanaged 簽章，其會傳回 HRESULT 且傳回值會有額外的 [out, retval] 引數。</span><span class="sxs-lookup"><span data-stu-id="16516-134">Controls whether the managed method signature should be transformed into an unmanaged signature that returns an HRESULT and has an additional [out, retval] argument for the return value.</span></span><br /><br /> <span data-ttu-id="16516-135">預設值是 `true` (簽章不應該轉換)。</span><span class="sxs-lookup"><span data-stu-id="16516-135">The default is `true` (the signature should not be transformed).</span></span>|  
|<xref:System.Runtime.InteropServices.DllImportAttribute.SetLastError>|<span data-ttu-id="16516-136">可讓呼叫者使用 `Marshal.GetLastWin32Error` API 函式來判斷當執行此方法時是否發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="16516-136">Enables the caller to use the `Marshal.GetLastWin32Error` API function to determine whether an error occurred while executing the method.</span></span> <span data-ttu-id="16516-137">在 Visual Basic 中，預設值是 `true`；在 C# 和 C++ 中，預設值是  `false`。</span><span class="sxs-lookup"><span data-stu-id="16516-137">In Visual Basic, the default is `true`; in C# and C++, the default is `false`.</span></span>|  
|<xref:System.Runtime.InteropServices.DllImportAttribute.ThrowOnUnmappableChar>|<span data-ttu-id="16516-138">在無法對應 Unicode 字元的例外狀況中，控制項的擲回轉換成 ANSI "?" 字元。</span><span class="sxs-lookup"><span data-stu-id="16516-138">Controls throwing of an exception on an unmappable Unicode character that is converted to an ANSI "?" character.</span></span>|  
  
 <span data-ttu-id="16516-139">如需詳細參考資訊，請參閱 <xref:System.Runtime.InteropServices.DllImportAttribute>。</span><span class="sxs-lookup"><span data-stu-id="16516-139">For detailed reference information, see <xref:System.Runtime.InteropServices.DllImportAttribute>.</span></span>  
  
## <a name="platform-invoke-security-considerations"></a><span data-ttu-id="16516-140">平台叫用安全性考量</span><span class="sxs-lookup"><span data-stu-id="16516-140">Platform invoke security considerations</span></span>  
 <span data-ttu-id="16516-141"><xref:System.Security.Permissions.SecurityAction> 列舉的 `Assert`、`Deny` 和 `PermitOnly` 成員稱為「堆疊查核修飾詞」\*\*。</span><span class="sxs-lookup"><span data-stu-id="16516-141">The `Assert`, `Deny`, and `PermitOnly` members of the <xref:System.Security.Permissions.SecurityAction> enumeration are referred to as *stack walk modifiers*.</span></span> <span data-ttu-id="16516-142">如果這些成員被做為平台叫用宣告式和 COM 介面定義語言 (IDL) 陳述式的宣告式屬性，就會忽略這些成員。</span><span class="sxs-lookup"><span data-stu-id="16516-142">These members are ignored if they are used as declarative attributes on platform invoke declarations and COM Interface Definition Language (IDL) statements.</span></span>  
  
### <a name="platform-invoke-examples"></a><span data-ttu-id="16516-143">平台叫用範例</span><span class="sxs-lookup"><span data-stu-id="16516-143">Platform Invoke Examples</span></span>  
 <span data-ttu-id="16516-144">本節中的平台叫用範例將說明如何使用具有堆疊查核行程修飾詞的  `RegistryPermission` 屬性。</span><span class="sxs-lookup"><span data-stu-id="16516-144">The platform invoke samples in this section illustrate the use of the `RegistryPermission` attribute with the stack walk modifiers.</span></span>  
  
 <span data-ttu-id="16516-145">在下列範例中，<xref:System.Security.Permissions.SecurityAction>`Assert`、`Deny` 和 `PermitOnly` 修飾詞會被忽略。</span><span class="sxs-lookup"><span data-stu-id="16516-145">In the following example, the <xref:System.Security.Permissions.SecurityAction>`Assert`, `Deny`, and `PermitOnly` modifiers are ignored.</span></span>  
  
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
  
 <span data-ttu-id="16516-146">不過，`Demand` 修飾詞，在下列範例中會被接受。</span><span class="sxs-lookup"><span data-stu-id="16516-146">However, the `Demand` modifier in the following example is accepted.</span></span>  
  
```csharp
[DllImport("MyClass.dll", EntryPoint = "CallRegistryPermission")]  
[RegistryPermission(SecurityAction.Demand, Unrestricted = true)]  
    private static extern bool CallRegistryPermissionDeny();  
```  
  
 <span data-ttu-id="16516-147">如果它們被放在包含 (換行) 平台叫用呼叫的類別上，<xref:System.Security.Permissions.SecurityAction> 修飾詞會正常運作。</span><span class="sxs-lookup"><span data-stu-id="16516-147"><xref:System.Security.Permissions.SecurityAction> modifiers do work correctly if they are placed on a class that contains (wraps) the platform invoke call.</span></span>  
  
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
  
 <span data-ttu-id="16516-148"><xref:System.Security.Permissions.SecurityAction> 修飾詞也會正確運作於巢狀案例中，其中它們被放在平台叫用呼叫的呼叫者上：</span><span class="sxs-lookup"><span data-stu-id="16516-148"><xref:System.Security.Permissions.SecurityAction> modifiers also work correctly in a nested scenario where they are placed on the caller of the platform invoke call:</span></span>  
  
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
  
#### <a name="com-interop-examples"></a><span data-ttu-id="16516-149">COM Interop 範例</span><span class="sxs-lookup"><span data-stu-id="16516-149">COM Interop Examples</span></span>  
 <span data-ttu-id="16516-150">本節中的 COM Interop 範例說明使用具有堆疊查核行程修飾詞的 `RegistryPermission` 屬性。</span><span class="sxs-lookup"><span data-stu-id="16516-150">The COM interop samples in this section illustrate the use of the `RegistryPermission` attribute with the stack walk modifiers.</span></span>  
  
 <span data-ttu-id="16516-151">下列 COM Interop 介面宣告忽略 `Assert` 、 `Deny` 和 `PermitOnly` 修飾詞，類似於先前章節中的平台叫用範例。</span><span class="sxs-lookup"><span data-stu-id="16516-151">The following COM interop interface declarations ignore the `Assert`, `Deny`, and `PermitOnly` modifiers, similarly to the platform invoke examples in the previous section.</span></span>  
  
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
  
 <span data-ttu-id="16516-152">此外，如下列範例所示，在 COM Interop 介面宣告的情況下，不接受 `Demand` 修飾詞。</span><span class="sxs-lookup"><span data-stu-id="16516-152">Additionally, the `Demand` modifier is not accepted in COM interop interface declaration scenarios, as shown in the following example.</span></span>  
  
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
  
## <a name="see-also"></a><span data-ttu-id="16516-153">另請參閱</span><span class="sxs-lookup"><span data-stu-id="16516-153">See also</span></span>

- [<span data-ttu-id="16516-154">使用 Unmanaged DLL 函式</span><span class="sxs-lookup"><span data-stu-id="16516-154">Consuming Unmanaged DLL Functions</span></span>](consuming-unmanaged-dll-functions.md)
- [<span data-ttu-id="16516-155">指定進入點</span><span class="sxs-lookup"><span data-stu-id="16516-155">Specifying an Entry Point</span></span>](specifying-an-entry-point.md)
- [<span data-ttu-id="16516-156">指定字元集</span><span class="sxs-lookup"><span data-stu-id="16516-156">Specifying a Character Set</span></span>](specifying-a-character-set.md)
- [<span data-ttu-id="16516-157">平台叫用範例</span><span class="sxs-lookup"><span data-stu-id="16516-157">Platform Invoke Examples</span></span>](platform-invoke-examples.md)
- <span data-ttu-id="16516-158">[平台叫用安全性考量](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb397754(v=vs.100))</span><span class="sxs-lookup"><span data-stu-id="16516-158">[Platform Invoke Security Considerations](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb397754(v=vs.100))</span></span>
- [<span data-ttu-id="16516-159">識別 DLL 中的函式</span><span class="sxs-lookup"><span data-stu-id="16516-159">Identifying Functions in DLLs</span></span>](identifying-functions-in-dlls.md)
- [<span data-ttu-id="16516-160">建立類別以包裝 DLL 函式</span><span class="sxs-lookup"><span data-stu-id="16516-160">Creating a Class to Hold DLL Functions</span></span>](creating-a-class-to-hold-dll-functions.md)
- [<span data-ttu-id="16516-161">呼叫 DLL 函式</span><span class="sxs-lookup"><span data-stu-id="16516-161">Calling a DLL Function</span></span>](calling-a-dll-function.md)
