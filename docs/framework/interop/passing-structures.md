---
title: 傳遞結構
description: 瞭解如何將結構和類別傳遞給未受管理的函式。 瞭解用來定義格式化類型的 StructLayoutAttribute 屬性。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- platform invoke, calling unmanaged functions
ms.assetid: 9b92ac73-32b7-4e1b-862e-6d8d950cf169
ms.openlocfilehash: ece5db8fdf803ce2f450ebeaaad66a379cfbf992
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96268907"
---
# <a name="passing-structures"></a><span data-ttu-id="a899a-104">傳遞結構</span><span class="sxs-lookup"><span data-stu-id="a899a-104">Passing Structures</span></span>

<span data-ttu-id="a899a-105">許多 Unmanaged 函式都需要您將其傳遞為函式的參數、結構成員 (Visual Basic 中的使用者定義型別) 或使用 Managed 程式碼所定義類別的成員。</span><span class="sxs-lookup"><span data-stu-id="a899a-105">Many unmanaged functions expect you to pass, as a parameter to the function, members of structures (user-defined types in Visual Basic) or members of classes that are defined in managed code.</span></span> <span data-ttu-id="a899a-106">使用平台叫用將結構或類別傳遞至 Unmanaged 程式碼時，您必須提供其他資訊來保留原始配置和對齊方式。</span><span class="sxs-lookup"><span data-stu-id="a899a-106">When passing structures or classes to unmanaged code using platform invoke, you must provide additional information to preserve the original layout and alignment.</span></span> <span data-ttu-id="a899a-107">本主題介紹用來定義格式化類型的 <xref:System.Runtime.InteropServices.StructLayoutAttribute> 屬性。</span><span class="sxs-lookup"><span data-stu-id="a899a-107">This topic introduces the <xref:System.Runtime.InteropServices.StructLayoutAttribute> attribute, which you use to define formatted types.</span></span> <span data-ttu-id="a899a-108">針對 Managed 結構和類別，您可以從 **LayoutKind** 列舉所提供的數個可預測配置行為中進行選取。</span><span class="sxs-lookup"><span data-stu-id="a899a-108">For managed structures and classes, you can select from several predictable layout behaviors supplied by the **LayoutKind** enumeration.</span></span>  
  
 <span data-ttu-id="a899a-109">本主題中所呈現概念的中心是結構與類別類型之間的重要差異。</span><span class="sxs-lookup"><span data-stu-id="a899a-109">Central to the concepts presented in this topic is an important difference between structure and class types.</span></span> <span data-ttu-id="a899a-110">結構是實值型別，而類別是參考型別 - 類別一律會提供至少一層記憶體間接取值 (實值的指標)。</span><span class="sxs-lookup"><span data-stu-id="a899a-110">Structures are value types and classes are reference types — classes always provide at least one level of memory indirection (a pointer to a value).</span></span> <span data-ttu-id="a899a-111">這項差異十分重要，因為 Unmanaged 函式通常要求間接取值，如下表第一個資料行中的簽章所示。</span><span class="sxs-lookup"><span data-stu-id="a899a-111">This difference is important because unmanaged functions often demand indirection, as shown by the signatures in the first column of the following table.</span></span> <span data-ttu-id="a899a-112">其餘資料行中的 Managed 結構和類別宣告會顯示您可調整宣告中間接取值層級的目標程度。所提供的宣告同時適用於 Visual Basic 和 Visual C#。</span><span class="sxs-lookup"><span data-stu-id="a899a-112">The managed structure and class declarations in the remaining columns show the degree to which you can adjust the level of indirection in your declaration.Declarations are provided for both Visual Basic and Visual C#.</span></span>  
  
|<span data-ttu-id="a899a-113">Unmanaged 簽章</span><span class="sxs-lookup"><span data-stu-id="a899a-113">Unmanaged signature</span></span>|<span data-ttu-id="a899a-114">Managed 宣告：</span><span class="sxs-lookup"><span data-stu-id="a899a-114">Managed declaration:</span></span> <br /><span data-ttu-id="a899a-115">無間接取值</span><span class="sxs-lookup"><span data-stu-id="a899a-115">no indirection</span></span><br />`Structure MyType`<br />`struct MyType;`|<span data-ttu-id="a899a-116">Managed 宣告：</span><span class="sxs-lookup"><span data-stu-id="a899a-116">Managed declaration:</span></span> <br /><span data-ttu-id="a899a-117">一層間接取值</span><span class="sxs-lookup"><span data-stu-id="a899a-117">one level of indirection</span></span><br />`Class MyType`<br />`class MyType;`|  
|-------------------------|---------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|  
|`DoWork(MyType x);`<br /><br /> <span data-ttu-id="a899a-118">要求零層間接取值。</span><span class="sxs-lookup"><span data-stu-id="a899a-118">Demands zero levels of indirection.</span></span>|`DoWork(ByVal x As MyType)` <br /> `DoWork(MyType x)`<br /><br /> <span data-ttu-id="a899a-119">兩層間接取值。</span><span class="sxs-lookup"><span data-stu-id="a899a-119">Adds zero levels of indirection.</span></span>|<span data-ttu-id="a899a-120">無法進行，因為已有一層間接取值。</span><span class="sxs-lookup"><span data-stu-id="a899a-120">Not possible because there is already one level of indirection.</span></span>|  
|`DoWork(MyType* x);`<br /><br /> <span data-ttu-id="a899a-121">要求一層間接取值。</span><span class="sxs-lookup"><span data-stu-id="a899a-121">Demands one level of indirection.</span></span>|`DoWork(ByRef x As MyType)` <br /> `DoWork(ref MyType x)`<br /><br /> <span data-ttu-id="a899a-122">新增一層間接取值。</span><span class="sxs-lookup"><span data-stu-id="a899a-122">Adds one level of indirection.</span></span>|`DoWork(ByVal x As MyType)` <br /> `DoWork(MyType x)`<br /><br /> <span data-ttu-id="a899a-123">兩層間接取值。</span><span class="sxs-lookup"><span data-stu-id="a899a-123">Adds zero levels of indirection.</span></span>|  
|`DoWork(MyType** x);`<br /><br /> <span data-ttu-id="a899a-124">要求兩層間接取值。</span><span class="sxs-lookup"><span data-stu-id="a899a-124">Demands two levels of indirection.</span></span>|<span data-ttu-id="a899a-125">不可行，因為無法使用 **ByRef** **ByRef** 或 `ref` `ref`。</span><span class="sxs-lookup"><span data-stu-id="a899a-125">Not possible because **ByRef** **ByRef** or `ref` `ref` cannot be used.</span></span>|`DoWork(ByRef x As MyType)` <br /> `DoWork(ref MyType x)`<br /><br /> <span data-ttu-id="a899a-126">新增一層間接取值。</span><span class="sxs-lookup"><span data-stu-id="a899a-126">Adds one level of indirection.</span></span>|  
  
 <span data-ttu-id="a899a-127">此表格描述下列平台叫用宣告方針：</span><span class="sxs-lookup"><span data-stu-id="a899a-127">The table describes the following guidelines for platform invoke declarations:</span></span>  
  
- <span data-ttu-id="a899a-128">Unmanaged 函式未要求間接取值時，請使用以傳值方式傳遞的結構。</span><span class="sxs-lookup"><span data-stu-id="a899a-128">Use a structure passed by value when the unmanaged function demands no indirection.</span></span>  
  
- <span data-ttu-id="a899a-129">Unmanaged 函式要求一層間接取值時，請使用以傳址方式傳遞的結構或以傳值方式傳遞的類別。</span><span class="sxs-lookup"><span data-stu-id="a899a-129">Use either a structure passed by reference or a class passed by value when the unmanaged function demands one level of indirection.</span></span>  
  
- <span data-ttu-id="a899a-130">Unmanaged 函式要求兩層間接取值時，請使用以傳址方式傳遞的類別。</span><span class="sxs-lookup"><span data-stu-id="a899a-130">Use a class passed by reference when the unmanaged function demands two levels of indirection.</span></span>  
  
## <a name="declaring-and-passing-structures"></a><span data-ttu-id="a899a-131">宣告和傳遞結構</span><span class="sxs-lookup"><span data-stu-id="a899a-131">Declaring and Passing Structures</span></span>  

 <span data-ttu-id="a899a-132">下列範例示範如何使用 Managed 程式碼定義 `Point` 和 `Rect` 結構，並將類型當成參數傳遞至 User32.dll 檔案中的 **PtInRect** 函式。</span><span class="sxs-lookup"><span data-stu-id="a899a-132">The following example shows how to define the `Point` and `Rect` structures in managed code, and pass the types as parameter to the **PtInRect** function in the User32.dll file.</span></span> <span data-ttu-id="a899a-133">**PtInRect** 具有下列 Unmanaged 簽章：</span><span class="sxs-lookup"><span data-stu-id="a899a-133">**PtInRect** has the following unmanaged signature:</span></span>  
  
```cpp
BOOL PtInRect(const RECT *lprc, POINT pt);  
```  
  
 <span data-ttu-id="a899a-134">請注意，您必須以傳址方式傳遞 Rect 結構，因為此函式需要有 RECT 類型的指標。</span><span class="sxs-lookup"><span data-stu-id="a899a-134">Notice that you must pass the Rect structure by reference, since the function expects a pointer to a RECT type.</span></span>  
  
```vb  
Imports System.Runtime.InteropServices  
  
<StructLayout(LayoutKind.Sequential)> Public Structure Point  
    Public x As Integer  
    Public y As Integer  
End Structure  
  
Public Structure <StructLayout(LayoutKind.Explicit)> Rect  
    <FieldOffset(0)> Public left As Integer  
    <FieldOffset(4)> Public top As Integer  
    <FieldOffset(8)> Public right As Integer  
    <FieldOffset(12)> Public bottom As Integer  
End Structure  
  
Friend Class NativeMethods
    Friend Declare Auto Function PtInRect Lib "user32.dll" (
        ByRef r As Rect, p As Point) As Boolean  
End Class  
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
  
internal static class NativeMethods
{  
    [DllImport("User32.dll")]  
    internal static extern bool PtInRect(ref Rect r, Point p);  
}  
```  
  
## <a name="declaring-and-passing-classes"></a><span data-ttu-id="a899a-135">宣告和傳遞類別</span><span class="sxs-lookup"><span data-stu-id="a899a-135">Declaring and Passing Classes</span></span>  

 <span data-ttu-id="a899a-136">只要類別具有固定成員配置，您就可以將類別的成員傳遞至 Unmanaged DLL 函式。</span><span class="sxs-lookup"><span data-stu-id="a899a-136">You can pass members of a class to an unmanaged DLL function, as long as the class has a fixed member layout.</span></span> <span data-ttu-id="a899a-137">下列範例示範如何以定義的循序順序將 `MySystemTime` 類別成員傳遞至 User32.dll 檔案中的 **GetSystemTime**。</span><span class="sxs-lookup"><span data-stu-id="a899a-137">The following example demonstrates how to pass members of the `MySystemTime` class, which are defined in sequential order, to the **GetSystemTime** in the User32.dll file.</span></span> <span data-ttu-id="a899a-138">**GetSystemTime** 具有下列 Unmanaged 簽章：</span><span class="sxs-lookup"><span data-stu-id="a899a-138">**GetSystemTime** has the following unmanaged signature:</span></span>  
  
```cpp
void GetSystemTime(SYSTEMTIME* SystemTime);  
```  
  
 <span data-ttu-id="a899a-139">與實值型別不同，類別一律會有至少一層間接取值。</span><span class="sxs-lookup"><span data-stu-id="a899a-139">Unlike value types, classes always have at least one level of indirection.</span></span>  
  
```vb  
Imports System.Runtime.InteropServices  
  
<StructLayout(LayoutKind.Sequential)> Public Class MySystemTime  
    Public wYear As Short  
    Public wMonth As Short  
    Public wDayOfWeek As Short
    Public wDay As Short  
    Public wHour As Short  
    Public wMinute As Short  
    Public wSecond As Short  
    Public wMiliseconds As Short  
End Class  
  
Friend Class NativeMethods  
    Friend Declare Auto Sub GetSystemTime Lib "Kernel32.dll" (
        sysTime As MySystemTime)  
    Friend Declare Auto Function MessageBox Lib "User32.dll" (
        hWnd As IntPtr, lpText As String, lpCaption As String, uType As UInteger) As Integer  
End Class  
  
Public Class TestPlatformInvoke
    Public Shared Sub Main()  
        Dim sysTime As New MySystemTime()  
        NativeMethods.GetSystemTime(sysTime)  
  
        Dim dt As String  
        dt = "System time is:" & ControlChars.CrLf & _  
              "Year: " & sysTime.wYear & _  
              ControlChars.CrLf & "Month: " & sysTime.wMonth & _  
              ControlChars.CrLf & "DayOfWeek: " & sysTime.wDayOfWeek & _  
              ControlChars.CrLf & "Day: " & sysTime.wDay  
        NativeMethods.MessageBox(IntPtr.Zero, dt, "Platform Invoke Sample", 0)
    End Sub  
End Class  
```  
  
```csharp  
[StructLayout(LayoutKind.Sequential)]  
public class MySystemTime {  
    public ushort wYear;
    public ushort wMonth;  
    public ushort wDayOfWeek;
    public ushort wDay;
    public ushort wHour;
    public ushort wMinute;
    public ushort wSecond;
    public ushort wMilliseconds;
}  
internal static class NativeMethods
{  
    [DllImport("Kernel32.dll")]  
    internal static extern void GetSystemTime(MySystemTime st);  
  
    [DllImport("user32.dll", CharSet = CharSet.Auto)]  
    internal static extern int MessageBox(
        IntPtr hWnd, string lpText, string lpCaption, uint uType);  
}  
  
public class TestPlatformInvoke  
{  
    public static void Main()  
    {  
        MySystemTime sysTime = new MySystemTime();  
        NativeMethods.GetSystemTime(sysTime);  
  
        string dt;  
        dt = "System time is: \n" +  
              "Year: " + sysTime.wYear + "\n" +  
              "Month: " + sysTime.wMonth + "\n" +  
              "DayOfWeek: " + sysTime.wDayOfWeek + "\n" +  
              "Day: " + sysTime.wDay;  
        NativeMethods.MessageBox(IntPtr.Zero, dt, "Platform Invoke Sample", 0);  
    }  
}  
```  
  
## <a name="see-also"></a><span data-ttu-id="a899a-140">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a899a-140">See also</span></span>

- [<span data-ttu-id="a899a-141">呼叫 DLL 函式</span><span class="sxs-lookup"><span data-stu-id="a899a-141">Calling a DLL Function</span></span>](calling-a-dll-function.md)
- <xref:System.Runtime.InteropServices.StructLayoutAttribute>
- <xref:System.Runtime.InteropServices.FieldOffsetAttribute>
