---
description: -link (C# 編譯器選項)
title: -link (C# 編譯器選項)
ms.date: 07/20/2015
helpviewer_keywords:
- /l compiler option [C#]
- /link compiler option [C#]
- -l compiler option [C#]
- EmbedInteropTypes
- l compiler option [C#]
- embed interop types [COM Interop]
- -link compiler option [C#]
- link compiler option [C#]
ms.assetid: 00da70c6-9ea1-43c2-86f2-aa7f26c03475
ms.openlocfilehash: 0f6927fd240f3f8535478d163be615fc74dad8d2
ms.sourcegitcommit: d579fb5e4b46745fd0f1f8874c94c6469ce58604
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2020
ms.locfileid: "89125393"
---
# <a name="-link-c-compiler-options"></a><span data-ttu-id="666ad-103">-link (C# 編譯器選項)</span><span class="sxs-lookup"><span data-stu-id="666ad-103">-link (C# Compiler Options)</span></span>
<span data-ttu-id="666ad-104">讓編譯器將所指定組件的 COM 類型資訊全部提供給您目前編譯的專案。</span><span class="sxs-lookup"><span data-stu-id="666ad-104">Causes the compiler to make COM type information in the specified assemblies available to the project that you are currently compiling.</span></span>

## <a name="syntax"></a><span data-ttu-id="666ad-105">語法</span><span class="sxs-lookup"><span data-stu-id="666ad-105">Syntax</span></span>

```console
-link:fileList
// -or-
-l:fileList
```

## <a name="arguments"></a><span data-ttu-id="666ad-106">引數</span><span class="sxs-lookup"><span data-stu-id="666ad-106">Arguments</span></span>
 `fileList`  
 <span data-ttu-id="666ad-107">必要。</span><span class="sxs-lookup"><span data-stu-id="666ad-107">Required.</span></span> <span data-ttu-id="666ad-108">以逗號分隔的組件檔案名稱清單。</span><span class="sxs-lookup"><span data-stu-id="666ad-108">Comma-delimited list of assembly file names.</span></span> <span data-ttu-id="666ad-109">如果檔案名稱包含空格，請用引號括住名稱。</span><span class="sxs-lookup"><span data-stu-id="666ad-109">If the file name contains a space, enclose the name in quotation marks.</span></span>

## <a name="remarks"></a><span data-ttu-id="666ad-110">備註</span><span class="sxs-lookup"><span data-stu-id="666ad-110">Remarks</span></span>
 <span data-ttu-id="666ad-111">`-link` 選項可讓您部署具有內嵌類型資訊的應用程式。</span><span class="sxs-lookup"><span data-stu-id="666ad-111">The `-link` option enables you to deploy an application that has embedded type information.</span></span> <span data-ttu-id="666ad-112">應用程式接著可以使用執行階段組件中實作內嵌類型資訊的類型，而不需要參考執行階段組件。</span><span class="sxs-lookup"><span data-stu-id="666ad-112">The application can then use types in a runtime assembly that implement the embedded type information without requiring a reference to the runtime assembly.</span></span> <span data-ttu-id="666ad-113">如果執行階段組件有許多發行版本，包含內嵌類型資訊的應用程式不需要重新編譯，就可以搭配各種版本使用。</span><span class="sxs-lookup"><span data-stu-id="666ad-113">If various versions of the runtime assembly are published, the application that contains the embedded type information can work with the various versions without having to be recompiled.</span></span> <span data-ttu-id="666ad-114">如需範例，請參閱 [Walkthrough: Embedding Types from Managed Assemblies](../../../standard/assembly/embed-types-visual-studio.md) (逐步解說：從 Managed 組件內嵌類型)。</span><span class="sxs-lookup"><span data-stu-id="666ad-114">For an example, see [Walkthrough: Embedding Types from Managed Assemblies](../../../standard/assembly/embed-types-visual-studio.md).</span></span>

 <span data-ttu-id="666ad-115">如果您正在使用 COM Interop，使用 `-link` 選項會特別有用。</span><span class="sxs-lookup"><span data-stu-id="666ad-115">Using the `-link` option is especially useful when you are working with COM interop.</span></span> <span data-ttu-id="666ad-116">您可以內嵌 COM 類型，如此一來您的應用程式就不會再要求目標電腦上必須有主要 Interop 組件 (PIA)。</span><span class="sxs-lookup"><span data-stu-id="666ad-116">You can embed COM types so that your application no longer requires a primary interop assembly (PIA) on the target computer.</span></span> <span data-ttu-id="666ad-117">`-link` 選項會指示編譯器將所參考 Interop 組件的 COM 類型資訊嵌入編譯產生的程式碼。</span><span class="sxs-lookup"><span data-stu-id="666ad-117">The `-link` option instructs the compiler to embed the COM type information from the referenced interop assembly into the resulting compiled code.</span></span> <span data-ttu-id="666ad-118">COM 類型是由 CLSID (GUID) 值來識別。</span><span class="sxs-lookup"><span data-stu-id="666ad-118">The COM type is identified by the CLSID (GUID) value.</span></span> <span data-ttu-id="666ad-119">因此，應用程式可以在已安裝含相同 CLSID 值之相同 COM 類型的目標電腦上執行。</span><span class="sxs-lookup"><span data-stu-id="666ad-119">As a result, your application can run on a target computer that has installed the same COM types with the same CLSID values.</span></span> <span data-ttu-id="666ad-120">自動化 Microsoft Office 的應用程式即為一個很好的例子。</span><span class="sxs-lookup"><span data-stu-id="666ad-120">Applications that automate Microsoft Office are a good example.</span></span> <span data-ttu-id="666ad-121">由於 Office 等應用程式通常會在不同版本間保持相同的 CLSID 值，因此只要目標電腦上已安裝 .NET Framework 4 或更新版本，且應用程式使用包含在所參考 COM 類型中的方法、屬性或事件，應用程式就可以使用這些參考的 COM 類型。</span><span class="sxs-lookup"><span data-stu-id="666ad-121">Because applications like Office usually keep the same CLSID value across different versions, your application can use the referenced COM types as long as .NET Framework 4 or later is installed on the target computer and your application uses methods, properties, or events that are included in the referenced COM types.</span></span>

 <span data-ttu-id="666ad-122">`-link` 選項只能內嵌介面、結構和委派。</span><span class="sxs-lookup"><span data-stu-id="666ad-122">The `-link` option embeds only interfaces, structures, and delegates.</span></span> <span data-ttu-id="666ad-123">不支援內嵌 COM 類別。</span><span class="sxs-lookup"><span data-stu-id="666ad-123">Embedding COM classes is not supported.</span></span>

> [!NOTE]
> <span data-ttu-id="666ad-124">當您在程式碼中建立內嵌 COM 類型的執行個體時，必須使用適當的介面來建立執行個體。</span><span class="sxs-lookup"><span data-stu-id="666ad-124">When you create an instance of an embedded COM type in your code, you must create the instance by using the appropriate interface.</span></span> <span data-ttu-id="666ad-125">嘗試使用 CoClass 建立內嵌 COM 類型的執行個體將會導致錯誤。</span><span class="sxs-lookup"><span data-stu-id="666ad-125">Attempting to create an instance of an embedded COM type by using the CoClass causes an error.</span></span>

 <span data-ttu-id="666ad-126">若要在 Visual Studio 中設定 `-link` 選項，請新增組件參考，並將 `Embed Interop Types` 屬性設定為 **true**。</span><span class="sxs-lookup"><span data-stu-id="666ad-126">To set the `-link` option in Visual Studio, add an assembly reference and set the `Embed Interop Types` property to **true**.</span></span> <span data-ttu-id="666ad-127">`Embed Interop Types` 屬性的預設值為 **false**。</span><span class="sxs-lookup"><span data-stu-id="666ad-127">The default for the `Embed Interop Types` property is **false**.</span></span>

 <span data-ttu-id="666ad-128">如果您所連結的 COM 組件 (A) 本身參考另一個 COM 組件 (組件 B)，您也必須在發生下列任一情況時連結到 B 組件：</span><span class="sxs-lookup"><span data-stu-id="666ad-128">If you link to a COM assembly (Assembly A) which itself references another COM assembly (Assembly B), you also have to link to Assembly B if either of the following is true:</span></span>

- <span data-ttu-id="666ad-129">組件 A 的類型繼承自組件 B 的類型，或是實作組件 B 的介面。</span><span class="sxs-lookup"><span data-stu-id="666ad-129">A type from Assembly A inherits from a type or implements an interface from Assembly B.</span></span>

- <span data-ttu-id="666ad-130">所叫用的欄位、屬性、事件或方法具有組件 B 的傳回型別或參數類型。</span><span class="sxs-lookup"><span data-stu-id="666ad-130">A field, property, event, or method that has a return type or parameter type from Assembly B is invoked.</span></span>

 <span data-ttu-id="666ad-131">如同 [-reference](./reference-compiler-option.md) 編譯器選項，`-link` 編譯器選項會使用 Csc.rsp 回應檔，參考常用的 .NET Framework 組件。</span><span class="sxs-lookup"><span data-stu-id="666ad-131">Like the [-reference](./reference-compiler-option.md) compiler option, the `-link` compiler option uses the Csc.rsp response file, which references frequently used .NET Framework assemblies.</span></span> <span data-ttu-id="666ad-132">如果您不想要讓編譯器使用 Csc.rsp 檔，請使用 [-noconfig](./noconfig-compiler-option.md) 編譯器選項。</span><span class="sxs-lookup"><span data-stu-id="666ad-132">Use the [-noconfig](./noconfig-compiler-option.md) compiler option if you do not want the compiler to use the Csc.rsp file.</span></span>

 <span data-ttu-id="666ad-133">`-link` 的簡短形式為 `-l`。</span><span class="sxs-lookup"><span data-stu-id="666ad-133">The short form of `-link` is `-l`.</span></span>

## <a name="generics-and-embedded-types"></a><span data-ttu-id="666ad-134">泛型和內嵌類型</span><span class="sxs-lookup"><span data-stu-id="666ad-134">Generics and Embedded Types</span></span>
 <span data-ttu-id="666ad-135">下列各節說明在內嵌 Interop 類型的應用程式中使用泛型型別時的限制。</span><span class="sxs-lookup"><span data-stu-id="666ad-135">The following sections describe the limitations on using generic types in applications that embed interop types.</span></span>

### <a name="generic-interfaces"></a><span data-ttu-id="666ad-136">泛型介面</span><span class="sxs-lookup"><span data-stu-id="666ad-136">Generic Interfaces</span></span>
 <span data-ttu-id="666ad-137">無法使用從 Interop 組件內嵌的泛型介面。</span><span class="sxs-lookup"><span data-stu-id="666ad-137">Generic interfaces that are embedded from an interop assembly cannot be used.</span></span> <span data-ttu-id="666ad-138">下列範例會顯示這一點。</span><span class="sxs-lookup"><span data-stu-id="666ad-138">This is shown in the following example.</span></span>

 [!code-csharp[VbLinkCompilerCS#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/vblinkcompilercs/cs/program.cs#1)]

### <a name="types-that-have-generic-parameters"></a><span data-ttu-id="666ad-139">具有泛型參數的類型</span><span class="sxs-lookup"><span data-stu-id="666ad-139">Types That Have Generic Parameters</span></span>
 <span data-ttu-id="666ad-140">如果具有泛型參數的類型來自外部組件，且其參數的類型是從 Interop 組件內嵌的，則無法使用該類型。</span><span class="sxs-lookup"><span data-stu-id="666ad-140">Types that have a generic parameter whose type is embedded from an interop assembly cannot be used if that type is from an external assembly.</span></span> <span data-ttu-id="666ad-141">這項限制不適用於介面。</span><span class="sxs-lookup"><span data-stu-id="666ad-141">This restriction does not apply to interfaces.</span></span> <span data-ttu-id="666ad-142">例如，請考慮使用 <xref:Microsoft.Office.Interop.Excel> 組件中所定義的 <xref:Microsoft.Office.Interop.Excel.Range> 介面。</span><span class="sxs-lookup"><span data-stu-id="666ad-142">For example, consider the <xref:Microsoft.Office.Interop.Excel.Range> interface that is defined in the <xref:Microsoft.Office.Interop.Excel> assembly.</span></span> <span data-ttu-id="666ad-143">如果程式庫內嵌來自 <xref:Microsoft.Office.Interop.Excel> 組件的 Interop 類型，並公開傳回泛型型別的方法，但是此泛型型別具有類型為 <xref:Microsoft.Office.Interop.Excel.Range> 介面的參數，則該方法就必須傳回泛型介面，如下列程式碼範例所示。</span><span class="sxs-lookup"><span data-stu-id="666ad-143">If a library embeds interop types from the <xref:Microsoft.Office.Interop.Excel> assembly and exposes a method that returns a generic type that has a parameter whose type is the <xref:Microsoft.Office.Interop.Excel.Range> interface, that method must return a generic interface, as shown in the following code example.</span></span>

[!code-csharp[VbLinkCompilerCS#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/vblinkcompilercs/cs/utility.cs)]

 <span data-ttu-id="666ad-144">在下列範例中，用戶端程式碼可以呼叫傳回 <xref:System.Collections.IList> 泛型介面的方法，且不會發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="666ad-144">In the following example, client code can call the method that returns the <xref:System.Collections.IList> generic interface without error.</span></span>

 [!code-csharp[VbLinkCompilerCS#5](~/samples/snippets/csharp/VS_Snippets_VBCSharp/vblinkcompilercs/cs/program.cs#5)]

## <a name="example"></a><span data-ttu-id="666ad-145">範例</span><span class="sxs-lookup"><span data-stu-id="666ad-145">Example</span></span>
 <span data-ttu-id="666ad-146">下列程式碼會編譯原始程式檔 `OfficeApp.cs`，並參考 `COMData1.dll` 和 `COMData2.dll` 中的組件來產生`OfficeApp.exe`。</span><span class="sxs-lookup"><span data-stu-id="666ad-146">The following code compiles source file `OfficeApp.cs` and reference assemblies from `COMData1.dll` and `COMData2.dll` to produce `OfficeApp.exe`.</span></span>

```csharp
csc -link:COMData1.dll,COMData2.dll -out:OfficeApp.exe OfficeApp.cs
```

## <a name="see-also"></a><span data-ttu-id="666ad-147">另請參閱</span><span class="sxs-lookup"><span data-stu-id="666ad-147">See also</span></span>

- [<span data-ttu-id="666ad-148">C # 編譯器選項</span><span class="sxs-lookup"><span data-stu-id="666ad-148">C# Compiler Options</span></span>](./index.md)
- [<span data-ttu-id="666ad-149">Walkthrough: Embedding Types from Managed Assemblies (逐步解說：從 Managed 組件內嵌類型)</span><span class="sxs-lookup"><span data-stu-id="666ad-149">Walkthrough: Embedding Types from Managed Assemblies</span></span>](../../../standard/assembly/embed-types-visual-studio.md)
- [<span data-ttu-id="666ad-150">- (c # 編譯器選項的參考) </span><span class="sxs-lookup"><span data-stu-id="666ad-150">-reference (C# Compiler Options)</span></span>](./reference-compiler-option.md)
- [<span data-ttu-id="666ad-151">-noconfig (c # 編譯器選項) </span><span class="sxs-lookup"><span data-stu-id="666ad-151">-noconfig (C# Compiler Options)</span></span>](./noconfig-compiler-option.md)
- [<span data-ttu-id="666ad-152">使用 csc.exe 建置命令列</span><span class="sxs-lookup"><span data-stu-id="666ad-152">Command-line Building With csc.exe</span></span>](./command-line-building-with-csc-exe.md)
- [<span data-ttu-id="666ad-153">互通性概觀</span><span class="sxs-lookup"><span data-stu-id="666ad-153">Interoperability Overview</span></span>](../../programming-guide/interop/interoperability-overview.md)
