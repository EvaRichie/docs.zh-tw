---
title: 設定組件屬性
description: 您可以設定 .NET 元件的元件屬性，包括元件身分識別、參考、組件資訊清單和強式名稱屬性。
ms.date: 08/20/2019
helpviewer_keywords:
- assemblies [.NET], attributes
- assembly binding, attributes
- assembly manifest, attributes
ms.assetid: 36a98a81-b5b5-4c19-912a-11f91eff7f4e
dev_langs:
- csharp
- vb
- cpp
ms.openlocfilehash: 32318d647dee8f3f397e3497e7c2da640bd492d0
ms.sourcegitcommit: 279fb6e8d515df51676528a7424a1df2f0917116
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/27/2020
ms.locfileid: "92687683"
---
# <a name="set-assembly-attributes"></a><span data-ttu-id="0e396-103">設定組件屬性</span><span class="sxs-lookup"><span data-stu-id="0e396-103">Set assembly attributes</span></span>

<span data-ttu-id="0e396-104">組件屬性是提供組件相關資訊的值。</span><span class="sxs-lookup"><span data-stu-id="0e396-104">Assembly attributes are values that provide information about an assembly.</span></span> <span data-ttu-id="0e396-105">屬性可分成下列幾組資訊：</span><span class="sxs-lookup"><span data-stu-id="0e396-105">The attributes are divided into the following sets of information:</span></span>

- <span data-ttu-id="0e396-106">組件識別屬性</span><span class="sxs-lookup"><span data-stu-id="0e396-106">Assembly identity attributes</span></span>

- <span data-ttu-id="0e396-107">資訊屬性</span><span class="sxs-lookup"><span data-stu-id="0e396-107">Informational attributes</span></span>

- <span data-ttu-id="0e396-108">組件資訊清單屬性</span><span class="sxs-lookup"><span data-stu-id="0e396-108">Assembly manifest attributes</span></span>

- <span data-ttu-id="0e396-109">強式名稱屬性</span><span class="sxs-lookup"><span data-stu-id="0e396-109">Strong name attributes</span></span>

## <a name="assembly-identity-attributes"></a><span data-ttu-id="0e396-110">組件識別屬性</span><span class="sxs-lookup"><span data-stu-id="0e396-110">Assembly identity attributes</span></span>

<span data-ttu-id="0e396-111">三個屬性連同強式名稱 (如果適用) 會判斷組件的識別：名稱、版本與文化特性。</span><span class="sxs-lookup"><span data-stu-id="0e396-111">Three attributes, together with a strong name (if applicable), determine the identity of an assembly: name, version, and culture.</span></span> <span data-ttu-id="0e396-112">這些屬性會形成組件的完整名稱，且在參考程式碼中的組件時會需要用到。</span><span class="sxs-lookup"><span data-stu-id="0e396-112">These attributes form the full name of the assembly and are required when referencing the assembly in code.</span></span> <span data-ttu-id="0e396-113">您可以使用屬性來設定組件的版本和文化特性。</span><span class="sxs-lookup"><span data-stu-id="0e396-113">You can use attributes to set an assembly's version and culture.</span></span> <span data-ttu-id="0e396-114">編譯器或 [組件連結器 (Al.exe)](../../framework/tools/al-exe-assembly-linker.md) 會在建立組件時，以包含組件資訊清單的檔案為基礎來設定名稱值。</span><span class="sxs-lookup"><span data-stu-id="0e396-114">The compiler or the [Assembly Linker (Al.exe)](../../framework/tools/al-exe-assembly-linker.md) sets the name value when the assembly is created, based on the file containing the assembly manifest.</span></span>

<span data-ttu-id="0e396-115">下表說明版本與文化特性屬性。</span><span class="sxs-lookup"><span data-stu-id="0e396-115">The following table describes the version and culture attributes.</span></span>

|<span data-ttu-id="0e396-116">組件識別屬性</span><span class="sxs-lookup"><span data-stu-id="0e396-116">Assembly identity attribute</span></span>|<span data-ttu-id="0e396-117">描述</span><span class="sxs-lookup"><span data-stu-id="0e396-117">Description</span></span>|
|---------------------------------|-----------------|
|<xref:System.Reflection.AssemblyCultureAttribute>|<span data-ttu-id="0e396-118">列舉的欄位，會指出組件所支援的文化特性。</span><span class="sxs-lookup"><span data-stu-id="0e396-118">Enumerated field indicating the culture that the assembly supports.</span></span> <span data-ttu-id="0e396-119">組件也可以指定文化特性獨立性，表示其包含預設文化特性的資源。</span><span class="sxs-lookup"><span data-stu-id="0e396-119">An assembly can also specify culture independence, indicating that it contains the resources for the default culture.</span></span> <span data-ttu-id="0e396-120">**注意：** 執行階段會將任何未將文化特性屬性設為 null 的組件作為附屬組件。</span><span class="sxs-lookup"><span data-stu-id="0e396-120">**Note:**  The runtime treats any assembly that does not have the culture attribute set to null as a satellite assembly.</span></span> <span data-ttu-id="0e396-121">這類組件會受限於附屬組件繫結規則。</span><span class="sxs-lookup"><span data-stu-id="0e396-121">Such assemblies are subject to satellite assembly binding rules.</span></span> <span data-ttu-id="0e396-122">如需詳細資訊，請參閱 [執行時間如何找出元件](../../framework/deployment/how-the-runtime-locates-assemblies.md)。</span><span class="sxs-lookup"><span data-stu-id="0e396-122">For more information, see [How the runtime locates assemblies](../../framework/deployment/how-the-runtime-locates-assemblies.md).</span></span>|
|<xref:System.Reflection.AssemblyFlagsAttribute>|<span data-ttu-id="0e396-123">此值用以設定組件屬性，例如組件是否可並存執行。</span><span class="sxs-lookup"><span data-stu-id="0e396-123">Value that sets assembly attributes, such as whether the assembly can be run side by side.</span></span>|
|<xref:System.Reflection.AssemblyVersionAttribute>|<span data-ttu-id="0e396-124">格式為 *major* . *minor* . *build* . *revision* 的數值 (例如 2.4.0.0)。</span><span class="sxs-lookup"><span data-stu-id="0e396-124">Numeric value in the format *major* . *minor* . *build* . *revision* (for example, 2.4.0.0).</span></span> <span data-ttu-id="0e396-125">通用語言執行平台會使用此值來執行強式名稱組件中的繫結作業。</span><span class="sxs-lookup"><span data-stu-id="0e396-125">The common language runtime uses this value to perform binding operations in strong-named assemblies.</span></span> <span data-ttu-id="0e396-126">**注意：**  如果屬性未套用 <xref:System.Reflection.AssemblyInformationalVersionAttribute> 至元件，則 <xref:System.Reflection.AssemblyVersionAttribute> 會使用 <xref:System.Windows.Forms.Application.ProductVersion%2A?displayProperty=nameWithType> 、 <xref:System.Windows.Forms.Application.UserAppDataPath%2A?displayProperty=nameWithType> 和屬性所指定的版本號碼 <xref:System.Windows.Forms.Application.UserAppDataRegistry%2A?displayProperty=nameWithType> 。</span><span class="sxs-lookup"><span data-stu-id="0e396-126">**Note:**  If the <xref:System.Reflection.AssemblyInformationalVersionAttribute> attribute is not applied to an assembly, the version number specified by the <xref:System.Reflection.AssemblyVersionAttribute> attribute is used by the <xref:System.Windows.Forms.Application.ProductVersion%2A?displayProperty=nameWithType>, <xref:System.Windows.Forms.Application.UserAppDataPath%2A?displayProperty=nameWithType>, and <xref:System.Windows.Forms.Application.UserAppDataRegistry%2A?displayProperty=nameWithType> properties.</span></span>|

<span data-ttu-id="0e396-127">下列程式碼範例顯示如何將版本與文化特性屬性套用至組件。</span><span class="sxs-lookup"><span data-stu-id="0e396-127">The following code example shows how to apply the version and culture attributes to an assembly.</span></span>

```cpp
// Set version number for the assembly.
[assembly:AssemblyVersionAttribute("4.3.2.1")];
// Set culture as German.
[assembly:AssemblyCultureAttribute("de")];
```

```csharp
// Set version number for the assembly.
[assembly:AssemblyVersionAttribute("4.3.2.1")]
// Set culture as German.
[assembly:AssemblyCultureAttribute("de")]
```

```vb
' Set version number for the assembly.
<Assembly:AssemblyVersionAttribute("4.3.2.1")>
' Set culture as German.
<Assembly:AssemblyCultureAttribute("de")>
```

## <a name="informational-attributes"></a><span data-ttu-id="0e396-128">資訊屬性</span><span class="sxs-lookup"><span data-stu-id="0e396-128">Informational attributes</span></span>

<span data-ttu-id="0e396-129">您可以使用資訊屬性，以提供組件其他的公司或產品資訊。</span><span class="sxs-lookup"><span data-stu-id="0e396-129">You can use informational attributes to provide additional company or product information for an assembly.</span></span> <span data-ttu-id="0e396-130">下表說明可套用至組件的資訊屬性。</span><span class="sxs-lookup"><span data-stu-id="0e396-130">The following table describes the informational attributes you can apply to an assembly.</span></span>

|<span data-ttu-id="0e396-131">資訊屬性</span><span class="sxs-lookup"><span data-stu-id="0e396-131">Informational attribute</span></span>|<span data-ttu-id="0e396-132">描述</span><span class="sxs-lookup"><span data-stu-id="0e396-132">Description</span></span>|
|-----------------------------|-----------------|
|<xref:System.Reflection.AssemblyCompanyAttribute>|<span data-ttu-id="0e396-133">此字串值指定公司名稱。</span><span class="sxs-lookup"><span data-stu-id="0e396-133">String value specifying a company name.</span></span>|
|<xref:System.Reflection.AssemblyCopyrightAttribute>|<span data-ttu-id="0e396-134">此字串值指定著作權資訊。</span><span class="sxs-lookup"><span data-stu-id="0e396-134">String value specifying copyright information.</span></span>|
|<xref:System.Reflection.AssemblyFileVersionAttribute>|<span data-ttu-id="0e396-135">此字串值指定 Win32 檔案版本號碼。</span><span class="sxs-lookup"><span data-stu-id="0e396-135">String value specifying the Win32 file version number.</span></span> <span data-ttu-id="0e396-136">這通常會預設為組件版本。</span><span class="sxs-lookup"><span data-stu-id="0e396-136">This normally defaults to the assembly version.</span></span>|
|<xref:System.Reflection.AssemblyInformationalVersionAttribute>|<span data-ttu-id="0e396-137">此字串值指定的版本資訊不為通用語言執行平台所用，例如完整的產品版本號碼。</span><span class="sxs-lookup"><span data-stu-id="0e396-137">String value specifying version information that is not used by the common language runtime, such as a full product version number.</span></span> <span data-ttu-id="0e396-138">**注意：** 如果這個屬性會套用至組件，則其所指定的字串可以在執行階段透過使用 <xref:System.Windows.Forms.Application.ProductVersion%2A?displayProperty=nameWithType> 屬性加以取得。</span><span class="sxs-lookup"><span data-stu-id="0e396-138">**Note:**  If this attribute is applied to an assembly, the string it specifies can be obtained at run time by using the <xref:System.Windows.Forms.Application.ProductVersion%2A?displayProperty=nameWithType> property.</span></span> <span data-ttu-id="0e396-139">字串也會在 <xref:System.Windows.Forms.Application.UserAppDataPath%2A?displayProperty=nameWithType> 與 <xref:System.Windows.Forms.Application.UserAppDataRegistry%2A?displayProperty=nameWithType> 屬性所提供的路徑及登錄機碼中使用。</span><span class="sxs-lookup"><span data-stu-id="0e396-139">The string is also used in the path and registry key provided by the <xref:System.Windows.Forms.Application.UserAppDataPath%2A?displayProperty=nameWithType> and <xref:System.Windows.Forms.Application.UserAppDataRegistry%2A?displayProperty=nameWithType> properties.</span></span>|
|<xref:System.Reflection.AssemblyProductAttribute>|<span data-ttu-id="0e396-140">此字串值指定產品資訊。</span><span class="sxs-lookup"><span data-stu-id="0e396-140">String value specifying product information.</span></span>|
|<xref:System.Reflection.AssemblyTrademarkAttribute>|<span data-ttu-id="0e396-141">此字串值指定商標資訊。</span><span class="sxs-lookup"><span data-stu-id="0e396-141">String value specifying trademark information.</span></span>|

<span data-ttu-id="0e396-142">這些屬性可以出現在組件的 Windows 內容頁面上，或可以使用 **/win32res** 編譯器選項加以覆寫，以指定您自己的 Win32 資源檔。</span><span class="sxs-lookup"><span data-stu-id="0e396-142">These attributes can appear on the Windows Properties page of the assembly, or they can be overridden using the **/win32res** compiler option to specify your own Win32 resource file.</span></span>

## <a name="assembly-manifest-attributes"></a><span data-ttu-id="0e396-143">組件資訊清單屬性</span><span class="sxs-lookup"><span data-stu-id="0e396-143">Assembly manifest attributes</span></span>

<span data-ttu-id="0e396-144">您可以使用組件資訊清單屬性，在組件資訊清單中提供資訊，包括標題、描述、預設別名以及設定。</span><span class="sxs-lookup"><span data-stu-id="0e396-144">You can use assembly manifest attributes to provide information in the assembly manifest, including title, description, the default alias, and configuration.</span></span> <span data-ttu-id="0e396-145">下表說明組件資訊清單屬性。</span><span class="sxs-lookup"><span data-stu-id="0e396-145">The following table describes the assembly manifest attributes.</span></span>

|<span data-ttu-id="0e396-146">組件資訊清單屬性</span><span class="sxs-lookup"><span data-stu-id="0e396-146">Assembly manifest attribute</span></span>|<span data-ttu-id="0e396-147">描述</span><span class="sxs-lookup"><span data-stu-id="0e396-147">Description</span></span>|
|---------------------------------|-----------------|
|<xref:System.Reflection.AssemblyConfigurationAttribute>|<span data-ttu-id="0e396-148">此字串值表示組件的設定，例如 Retail 或 Debug。</span><span class="sxs-lookup"><span data-stu-id="0e396-148">String value indicating the configuration of the assembly, such as Retail or Debug.</span></span> <span data-ttu-id="0e396-149">執行階段不使用此值。</span><span class="sxs-lookup"><span data-stu-id="0e396-149">The runtime does not use this value.</span></span>|
|<xref:System.Reflection.AssemblyDefaultAliasAttribute>|<span data-ttu-id="0e396-150">此字串值指定可供參考組件使用的預設別名。</span><span class="sxs-lookup"><span data-stu-id="0e396-150">String value specifying a default alias to be used by referencing assemblies.</span></span> <span data-ttu-id="0e396-151">此值會在組件本身的名稱不容易記時 (例如 GUID 值) 提供易記名稱。</span><span class="sxs-lookup"><span data-stu-id="0e396-151">This value provides a friendly name when the name of the assembly itself is not friendly (such as a GUID value).</span></span> <span data-ttu-id="0e396-152">也可以使用此值作為完整組件名稱的簡短形式。</span><span class="sxs-lookup"><span data-stu-id="0e396-152">This value can also be used as a short form of the full assembly name.</span></span>|
|<xref:System.Reflection.AssemblyDescriptionAttribute>|<span data-ttu-id="0e396-153">此字串值指定簡短描述，該描述彙總組件的本質與用途。</span><span class="sxs-lookup"><span data-stu-id="0e396-153">String value specifying a short description that summarizes the nature and purpose of the assembly.</span></span>|
|<xref:System.Reflection.AssemblyTitleAttribute>|<span data-ttu-id="0e396-154">此字串值指定組件的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="0e396-154">String value specifying a friendly name for the assembly.</span></span> <span data-ttu-id="0e396-155">例如，名為 *comdlg* 的元件可能會有 Microsoft 通用對話方塊控制項標題。</span><span class="sxs-lookup"><span data-stu-id="0e396-155">For example, an assembly named *comdlg* might have the title Microsoft Common Dialog Control.</span></span>|

## <a name="strong-name-attributes"></a><span data-ttu-id="0e396-156">強式名稱屬性</span><span class="sxs-lookup"><span data-stu-id="0e396-156">Strong name attributes</span></span>

<span data-ttu-id="0e396-157">您可以使用強式名稱屬性來設定組件的強式名稱。</span><span class="sxs-lookup"><span data-stu-id="0e396-157">You can use strong name attributes to set a strong name for an assembly.</span></span> <span data-ttu-id="0e396-158">下表說明強式名稱屬性。</span><span class="sxs-lookup"><span data-stu-id="0e396-158">The following table describes the strong name attributes.</span></span>

|<span data-ttu-id="0e396-159">強式名稱屬性</span><span class="sxs-lookup"><span data-stu-id="0e396-159">Strong name attribute</span></span>|<span data-ttu-id="0e396-160">描述</span><span class="sxs-lookup"><span data-stu-id="0e396-160">Description</span></span>|
|----------------------------|-----------------|
|<xref:System.Reflection.AssemblyDelaySignAttribute>|<span data-ttu-id="0e396-161">此布林值表示正在使用延遲簽章。</span><span class="sxs-lookup"><span data-stu-id="0e396-161">Boolean value indicating that delay signing is being used.</span></span>|
|<xref:System.Reflection.AssemblyKeyFileAttribute>|<span data-ttu-id="0e396-162">此字串值表示檔案名稱，該檔案包含公開金鑰 (如果使用延遲簽章) 或公開與私密金鑰，而金鑰以參數形式傳遞至該屬性的建構函式。</span><span class="sxs-lookup"><span data-stu-id="0e396-162">String value indicating the name of the file that contains either the public key (if using delay signing) or both the public and private keys passed as a parameter to the constructor of this attribute.</span></span> <span data-ttu-id="0e396-163">請注意，檔案名是相對於 *.exe* 或 *.dll* )  (輸出檔案路徑，而不是原始程式檔路徑。</span><span class="sxs-lookup"><span data-stu-id="0e396-163">Note that the file name is relative to the output file path (the *.exe* or *.dll* ), not the source file path.</span></span>|
|<xref:System.Reflection.AssemblyKeyNameAttribute>|<span data-ttu-id="0e396-164">表示內含金鑰組的金鑰容器，而該金鑰組以參數形式傳遞至該屬性的建構函式。</span><span class="sxs-lookup"><span data-stu-id="0e396-164">Indicates the key container that contains the key pair passed as a parameter to the constructor of this attribute.</span></span>|

<span data-ttu-id="0e396-165">下列程式碼範例顯示使用延遲簽署來建立強式名稱的元件，以及名為 *myKey* 的公開金鑰檔案時，所要套用的屬性。</span><span class="sxs-lookup"><span data-stu-id="0e396-165">The following code example shows the attributes to apply when using delay signing to create a strong-named assembly with a public key file called *myKey.snk* .</span></span>

```cpp
[assembly:AssemblyKeyFileAttribute("myKey.snk")];
[assembly:AssemblyDelaySignAttribute(true)];
```

```csharp
[assembly:AssemblyKeyFileAttribute("myKey.snk")]
[assembly:AssemblyDelaySignAttribute(true)]
```

```vb
<Assembly:AssemblyKeyFileAttribute("myKey.snk")>
<Assembly:AssemblyDelaySignAttribute(True)>
```

## <a name="see-also"></a><span data-ttu-id="0e396-166">請參閱</span><span class="sxs-lookup"><span data-stu-id="0e396-166">See also</span></span>

- [<span data-ttu-id="0e396-167">建立組件</span><span class="sxs-lookup"><span data-stu-id="0e396-167">Create assemblies</span></span>](create.md)
