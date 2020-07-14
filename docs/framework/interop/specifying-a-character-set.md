---
title: 指定字元集
description: 瞭解如何指定使用窄 (ANSI) 或寬 (Unicode) 編碼的字元集。 您也可以指定自動執行時間選取。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- platform invoke, attribute fields
- attribute fields in platform invoke, CharSet
- CharSet field
ms.assetid: a8347eb1-295f-46b9-8a78-63331f9ecc50
ms.openlocfilehash: a4f18431d89343a77ccf2b920edac485e7dcfca3
ms.sourcegitcommit: 97ce5363efa88179dd76e09de0103a500ca9b659
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/13/2020
ms.locfileid: "86282121"
---
# <a name="specifying-a-character-set"></a><span data-ttu-id="a1056-104">指定字元集</span><span class="sxs-lookup"><span data-stu-id="a1056-104">Specifying a Character Set</span></span>
<span data-ttu-id="a1056-105"><xref:System.Runtime.InteropServices.DllImportAttribute.CharSet?displayProperty=nameWithType> 欄位控制字串封送處理，並決定平台叫用如何在 DLL 中尋找函式名稱。</span><span class="sxs-lookup"><span data-stu-id="a1056-105">The <xref:System.Runtime.InteropServices.DllImportAttribute.CharSet?displayProperty=nameWithType> field controls string marshaling and determines how platform invoke finds function names in a DLL.</span></span> <span data-ttu-id="a1056-106">這個主題將描述這兩種行為。</span><span class="sxs-lookup"><span data-stu-id="a1056-106">This topic describes both behaviors.</span></span>  
  
 <span data-ttu-id="a1056-107">某些 API 匯出兩個版本的函式，接受字串引數：窄 (ANSI) 和寬 (Unicode)。</span><span class="sxs-lookup"><span data-stu-id="a1056-107">Some APIs export two versions of functions that take string arguments: narrow (ANSI) and wide (Unicode).</span></span> <span data-ttu-id="a1056-108">例如，Win32 API 包括 **MessageBox** 函式的下列進入點名稱：</span><span class="sxs-lookup"><span data-stu-id="a1056-108">The Windows API, for instance, includes the following entry-point names for the **MessageBox** function:</span></span>  
  
- <span data-ttu-id="a1056-109">**MessageBoxA**</span><span class="sxs-lookup"><span data-stu-id="a1056-109">**MessageBoxA**</span></span>  
  
     <span data-ttu-id="a1056-110">提供 1 個位元組字元 ANSI 格式化，區別方式是在進入點名稱附加 "A"。</span><span class="sxs-lookup"><span data-stu-id="a1056-110">Provides 1-byte character ANSI formatting, distinguished by an "A" appended to the entry-point name.</span></span> <span data-ttu-id="a1056-111">**MessageBoxA** 呼叫一律以 ANSI 格式的字串封送處理。</span><span class="sxs-lookup"><span data-stu-id="a1056-111">Calls to **MessageBoxA** always marshal strings in ANSI format.</span></span>  
  
- <span data-ttu-id="a1056-112">**MessageBoxW**</span><span class="sxs-lookup"><span data-stu-id="a1056-112">**MessageBoxW**</span></span>  
  
     <span data-ttu-id="a1056-113">提供 2 個位元組字元 Unicode 格式化，區別方式是在進入點名稱附加 "W"。</span><span class="sxs-lookup"><span data-stu-id="a1056-113">Provides 2-byte character Unicode formatting, distinguished by a "W" appended to the entry-point name.</span></span> <span data-ttu-id="a1056-114">**MessageBoxW** 呼叫一律以 Unicode 格式的字串封送處理。</span><span class="sxs-lookup"><span data-stu-id="a1056-114">Calls to **MessageBoxW** always marshal strings in Unicode format.</span></span>  
  
## <a name="string-marshaling-and-name-matching"></a><span data-ttu-id="a1056-115">字串封送處理及名稱比對</span><span class="sxs-lookup"><span data-stu-id="a1056-115">String Marshaling and Name Matching</span></span>  
 <span data-ttu-id="a1056-116">`CharSet` 欄位可接受下列值：</span><span class="sxs-lookup"><span data-stu-id="a1056-116">The `CharSet` field accepts the following values:</span></span>  
  
 <span data-ttu-id="a1056-117"><xref:System.Runtime.InteropServices.CharSet.Ansi> (預設值)</span><span class="sxs-lookup"><span data-stu-id="a1056-117"><xref:System.Runtime.InteropServices.CharSet.Ansi> (default value)</span></span>  
  
- <span data-ttu-id="a1056-118">字串封送處理</span><span class="sxs-lookup"><span data-stu-id="a1056-118">String marshaling</span></span>  
  
     <span data-ttu-id="a1056-119">平台叫用會將字串從其受管理的格式 (Unicode) 封送處理為 ANSI 格式。</span><span class="sxs-lookup"><span data-stu-id="a1056-119">Platform invoke marshals strings from their managed format (Unicode) to ANSI format.</span></span>  
  
- <span data-ttu-id="a1056-120">名稱比對</span><span class="sxs-lookup"><span data-stu-id="a1056-120">Name matching</span></span>  
  
     <span data-ttu-id="a1056-121">當 <xref:System.Runtime.InteropServices.DllImportAttribute.ExactSpelling?displayProperty=nameWithType> 欄位是 `true` 時，如同 Visual Basic 中的預設值，平台叫用僅會搜尋您指定的名稱。</span><span class="sxs-lookup"><span data-stu-id="a1056-121">When the <xref:System.Runtime.InteropServices.DllImportAttribute.ExactSpelling?displayProperty=nameWithType> field is `true`, as it is by default in Visual Basic, platform invoke searches only for the name you specify.</span></span> <span data-ttu-id="a1056-122">例如，如果您指定 **MessageBox**，平台叫用會搜尋 **MessageBox**，並在找不到正確的拼字時失敗。</span><span class="sxs-lookup"><span data-stu-id="a1056-122">For example, if you specify **MessageBox**, platform invoke searches for **MessageBox** and fails when it cannot locate the exact spelling.</span></span>  
  
     <span data-ttu-id="a1056-123">當 `ExactSpelling` 欄位是 `false` 時，如同在 C++ 和 C# 中的預設值，平台叫用會先搜尋未損壞別名 (**MessageBox**)，然後如果找不到未損壞別名則搜尋損壞名稱 (**MessageBoxA**)。</span><span class="sxs-lookup"><span data-stu-id="a1056-123">When the `ExactSpelling` field is `false`, as it is by default in C++ and C#, platform invoke searches for the unmangled alias first (**MessageBox**), then the mangled name (**MessageBoxA**) if the unmangled alias is not found.</span></span> <span data-ttu-id="a1056-124">請注意，ANSI 名稱比對行為不同於 Unicode 名稱比對行為。</span><span class="sxs-lookup"><span data-stu-id="a1056-124">Notice that ANSI name-matching behavior differs from Unicode name-matching behavior.</span></span>  
  
 <xref:System.Runtime.InteropServices.CharSet.Unicode>  
  
- <span data-ttu-id="a1056-125">字串封送處理</span><span class="sxs-lookup"><span data-stu-id="a1056-125">String marshaling</span></span>  
  
     <span data-ttu-id="a1056-126">平台叫用會將字串從其受管理的格式 (Unicode) 複製為 Unicode 格式。</span><span class="sxs-lookup"><span data-stu-id="a1056-126">Platform invoke copies strings from their managed format (Unicode) to Unicode format.</span></span>  
  
- <span data-ttu-id="a1056-127">名稱比對</span><span class="sxs-lookup"><span data-stu-id="a1056-127">Name matching</span></span>  
  
     <span data-ttu-id="a1056-128">當 `ExactSpelling` 欄位是 `true` 時，如同 Visual Basic 中的預設值，平台叫用僅會搜尋您指定的名稱。</span><span class="sxs-lookup"><span data-stu-id="a1056-128">When the `ExactSpelling` field is `true`, as it is by default in Visual Basic, platform invoke searches only for the name you specify.</span></span> <span data-ttu-id="a1056-129">例如，如果您指定 **MessageBox**，則平台叫用會搜尋 **MessageBox**，並在找不到正確的拼字時失敗。</span><span class="sxs-lookup"><span data-stu-id="a1056-129">For example, if you specify **MessageBox**, platform invoke searches for **MessageBox** and fails if it cannot locate the exact spelling.</span></span>  
  
     <span data-ttu-id="a1056-130">當 `ExactSpelling` 欄位是 `false` 時，如同在 C++ 和 C# 中的預設值，平台叫用會先搜尋損壞名稱 (**MessageBoxW**)，然後如果找不到損壞名稱則搜尋未損壞別名 (**MessageBox**)。</span><span class="sxs-lookup"><span data-stu-id="a1056-130">When the `ExactSpelling` field is `false`, as it is by default in C++ and C#, platform invoke searches for the mangled name first (**MessageBoxW**), then the unmangled alias (**MessageBox**) if the mangled name is not found.</span></span> <span data-ttu-id="a1056-131">請注意，Unicode 名稱比對行為不同於 ANSI 名稱比對行為。</span><span class="sxs-lookup"><span data-stu-id="a1056-131">Notice that Unicode name-matching behavior differs from ANSI name-matching behavior.</span></span>  
  
 <xref:System.Runtime.InteropServices.CharSet.Auto>  
  
- <span data-ttu-id="a1056-132">平台叫用會在執行階段，根據在目標平台，在 ANSI 和 Unicode 格式之間選擇。</span><span class="sxs-lookup"><span data-stu-id="a1056-132">Platform invoke chooses between ANSI and Unicode formats at run time, based on the target platform.</span></span>  
  
## <a name="specifying-a-character-set-in-visual-basic"></a><span data-ttu-id="a1056-133">在 Visual Basic 中指定字元集</span><span class="sxs-lookup"><span data-stu-id="a1056-133">Specifying a Character Set in Visual Basic</span></span>  
 <span data-ttu-id="a1056-134">下列範例會宣告 **MessageBox** 函式三次，每次都有不同的字元集行為。</span><span class="sxs-lookup"><span data-stu-id="a1056-134">The following example declares the **MessageBox** function three times, each time with different character-set behavior.</span></span> <span data-ttu-id="a1056-135">您可以在宣告陳述式新增 **Ansi**、**Unicode** 或 **Auto** 關鍵字，在 Visual Basic 中指定字元集行為。</span><span class="sxs-lookup"><span data-stu-id="a1056-135">You can specify character-set behavior in Visual Basic by adding the **Ansi**, **Unicode**, or **Auto** keyword to the declaration statement.</span></span>  
  
 <span data-ttu-id="a1056-136">如果您省略字元集關鍵字，如同您在第一個宣告陳述式的做法，<xref:System.Runtime.InteropServices.DllImportAttribute.CharSet?displayProperty=nameWithType> 欄位會預設為 ANSI 字元集。</span><span class="sxs-lookup"><span data-stu-id="a1056-136">If you omit the character-set keyword, as is done in the first declaration statement, the <xref:System.Runtime.InteropServices.DllImportAttribute.CharSet?displayProperty=nameWithType> field defaults to the ANSI character set.</span></span> <span data-ttu-id="a1056-137">在範例中的第二個和第三個陳述式，明確地以關鍵字指定字元集。</span><span class="sxs-lookup"><span data-stu-id="a1056-137">The second and third statements in the example explicitly specify a character set with a keyword.</span></span>  
  
```vb
Friend Class NativeMethods
    Friend Declare Function MessageBoxA Lib "user32.dll" (
        ByVal hWnd As IntPtr,
        ByVal lpText As String,
        ByVal lpCaption As String,
        ByVal uType As UInteger) As Integer

    Friend Declare Unicode Function MessageBoxW Lib "user32.dll" (
        ByVal hWnd As IntPtr,
        ByVal lpText As String,
        ByVal lpCaption As String,
        ByVal uType As UInteger) As Integer

    Friend Declare Auto Function MessageBox Lib "user32.dll" (
        ByVal hWnd As IntPtr,
        ByVal lpText As String,
        ByVal lpCaption As String,
        ByVal uType As UInteger) As Integer
End Class
```
  
## <a name="specifying-a-character-set-in-c-and-c"></a><span data-ttu-id="a1056-138">在 C# 和 C++ 指定字元集</span><span class="sxs-lookup"><span data-stu-id="a1056-138">Specifying a Character Set in C# and C++</span></span>  
 <span data-ttu-id="a1056-139"><xref:System.Runtime.InteropServices.DllImportAttribute.CharSet?displayProperty=nameWithType> 欄位將基礎字元集識別為 ANSI 或 Unicode。</span><span class="sxs-lookup"><span data-stu-id="a1056-139">The <xref:System.Runtime.InteropServices.DllImportAttribute.CharSet?displayProperty=nameWithType> field identifies the underlying character set as ANSI or Unicode.</span></span> <span data-ttu-id="a1056-140">字元集控制應該如何封送處理方法的字串引數。</span><span class="sxs-lookup"><span data-stu-id="a1056-140">The character set controls how string arguments to a method should be marshaled.</span></span> <span data-ttu-id="a1056-141">您可以使用下列格式之一來表示字元集：</span><span class="sxs-lookup"><span data-stu-id="a1056-141">Use one of the following forms to indicate the character set:</span></span>  
  
```csharp
[DllImport("DllName", CharSet = CharSet.Ansi)]
[DllImport("DllName", CharSet = CharSet.Unicode)]
[DllImport("DllName", CharSet = CharSet.Auto)]
```
  
```cpp
[DllImport("DllName", CharSet = CharSet::Ansi)]
[DllImport("DllName", CharSet = CharSet::Unicode)]
[DllImport("DllName", CharSet = CharSet::Auto)]
```
  
 <span data-ttu-id="a1056-142">下列範例示範 **MessageBox** 函式的三個 Managed 定義，其已屬性化以指定字元集。</span><span class="sxs-lookup"><span data-stu-id="a1056-142">The following example shows three managed definitions of the **MessageBox** function attributed to specify a character set.</span></span> <span data-ttu-id="a1056-143">在第一個定義中，根據其省略，`CharSet` 欄位預設為 ANSI 字元集。</span><span class="sxs-lookup"><span data-stu-id="a1056-143">In the first definition, by its omission, the `CharSet` field defaults to the ANSI character set.</span></span>  
  
```csharp  
using System;
using System.Runtime.InteropServices;

internal static class NativeMethods
{
    [DllImport("user32.dll")]
    internal static extern int MessageBoxA(
        IntPtr hWnd, string lpText, string lpCaption, uint uType);

    [DllImport("user32.dll", CharSet = CharSet.Unicode)]
    internal static extern int MessageBoxW(
        IntPtr hWnd, string lpText, string lpCaption, uint uType);

    [DllImport("user32.dll", CharSet = CharSet.Auto)]
    internal static extern int MessageBox(
        IntPtr hWnd, string lpText, string lpCaption, uint uType);
}
```  
  
```cpp
typedef void* HWND;

// Can use MessageBox or MessageBoxA.
[DllImport("user32")]
extern "C" int MessageBox(
    HWND hWnd, String* lpText, String* lpCaption, unsigned int uType);

// Can use MessageBox or MessageBoxW.
[DllImport("user32", CharSet = CharSet::Unicode)]
extern "C" int MessageBoxW(
    HWND hWnd, String* lpText, String* lpCaption, unsigned int uType);

// Must use MessageBox.
[DllImport("user32", CharSet = CharSet::Auto)]
extern "C" int MessageBox(
    HWND hWnd, String* lpText, String* lpCaption, unsigned int uType);
```
  
## <a name="see-also"></a><span data-ttu-id="a1056-144">請參閱</span><span class="sxs-lookup"><span data-stu-id="a1056-144">See also</span></span>

- <xref:System.Runtime.InteropServices.DllImportAttribute>
- [<span data-ttu-id="a1056-145">在 Managed 程式碼中建立原型</span><span class="sxs-lookup"><span data-stu-id="a1056-145">Creating Prototypes in Managed Code</span></span>](creating-prototypes-in-managed-code.md)
- [<span data-ttu-id="a1056-146">平台叫用範例</span><span class="sxs-lookup"><span data-stu-id="a1056-146">Platform Invoke Examples</span></span>](platform-invoke-examples.md)
- [<span data-ttu-id="a1056-147">使用平台叫用封送處理資料</span><span class="sxs-lookup"><span data-stu-id="a1056-147">Marshaling Data with Platform Invoke</span></span>](marshaling-data-with-platform-invoke.md)
