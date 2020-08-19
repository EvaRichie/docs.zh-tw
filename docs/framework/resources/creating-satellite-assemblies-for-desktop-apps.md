---
title: 建立桌面應用程式的附屬組件
description: 開始建立桌面應用程式的附屬元件。 您可以輕鬆地更新或取代附屬元件，以提供當地語系化的資源。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- deploying applications [.NET Framework], resources
- resource files, deploying
- hub-and-spoke resource deployment model
- resource files, packaging
- application resources, packaging
- public keys, obtaining
- satellite assemblies
- assemblies [.NET Framework], signing
- application resources, deploying
- Al.exe
- GAC (global assembly cache), satellite assemblies
- Assembly Linker
- directory locations for satellite assemblies
- global assembly cache, satellite assemblies
- packaging application resources
- compiling satellite assemblies
- re-signing assemblies
ms.assetid: 8d5c6044-2919-41d2-8321-274706b295ac
ms.openlocfilehash: 3e515028919518cb93cdbec3417eef061a512832
ms.sourcegitcommit: 8bfeb5930ca48b2ee6053f16082dcaf24d46d221
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2020
ms.locfileid: "88558409"
---
# <a name="creating-satellite-assemblies-for-desktop-apps"></a><span data-ttu-id="5058c-104">建立桌面應用程式的附屬組件</span><span class="sxs-lookup"><span data-stu-id="5058c-104">Creating Satellite Assemblies for Desktop Apps</span></span>

<span data-ttu-id="5058c-105">資源檔在當地語系化的應用程式中扮演重要角色。</span><span class="sxs-lookup"><span data-stu-id="5058c-105">Resource files play a central role in localized applications.</span></span> <span data-ttu-id="5058c-106">它們可讓應用程式以使用者自己的語言和文化特性顯示字串、影像和其他資料，以及在使用者自己的語言或文化特性的資源無法使用時提供替代資料。</span><span class="sxs-lookup"><span data-stu-id="5058c-106">They enable an application to display strings, images, and other data in the user's own language and culture, and to provide alternate data if resources for the user's own language or culture are unavailable.</span></span> <span data-ttu-id="5058c-107">.NET Framework 會使用中樞和支點模型來尋找並擷取當地語系化的資源。</span><span class="sxs-lookup"><span data-stu-id="5058c-107">The .NET Framework uses a hub-and-spoke model to locate and retrieve localized resources.</span></span> <span data-ttu-id="5058c-108">中樞是主要組件，其中包含未當地語系化的可執行程式碼以及稱為中性或預設文化特性之單一文化特性的資源。</span><span class="sxs-lookup"><span data-stu-id="5058c-108">The hub is the main assembly that contains the non-localizable executable code and the resources for a single culture, which is called the neutral or default culture.</span></span> <span data-ttu-id="5058c-109">預設文化特性是應用程式的後援文化特性；當地語系化的資源無法使用時會使用它。</span><span class="sxs-lookup"><span data-stu-id="5058c-109">The default culture is the fallback culture for the application; it is used when no localized resources are available.</span></span> <span data-ttu-id="5058c-110">您使用 <xref:System.Resources.NeutralResourcesLanguageAttribute> 屬性來指定應用程式之預設文化特性的文化特性。</span><span class="sxs-lookup"><span data-stu-id="5058c-110">You use the <xref:System.Resources.NeutralResourcesLanguageAttribute> attribute to designate the culture of the application's default culture.</span></span> <span data-ttu-id="5058c-111">每個支點都會連線至附屬組件，其中包含單一當地語系化文化特性但未包含任何程式碼的資源。</span><span class="sxs-lookup"><span data-stu-id="5058c-111">Each spoke connects to a satellite assembly that contains the resources for a single localized culture but does not contain any code.</span></span> <span data-ttu-id="5058c-112">因為附屬組件不是主要組件的一部分，所以您可以輕鬆地更新或取代對應至特定文化特性的資源，而不需要取代應用程式的主要組件。</span><span class="sxs-lookup"><span data-stu-id="5058c-112">Because the satellite assemblies are not part of the main assembly, you can easily update or replace resources that correspond to a specific culture without replacing the main assembly for the application.</span></span>

> [!NOTE]
> <span data-ttu-id="5058c-113">應用程式之預設文化特性的資源也可以儲存在附屬組件中。</span><span class="sxs-lookup"><span data-stu-id="5058c-113">The resources of an application's default culture can also be stored in a satellite assembly.</span></span> <span data-ttu-id="5058c-114">若要這樣做，請將 <xref:System.Resources.UltimateResourceFallbackLocation.Satellite?displayProperty=nameWithType> 的值指派給 <xref:System.Resources.NeutralResourcesLanguageAttribute> 屬性。</span><span class="sxs-lookup"><span data-stu-id="5058c-114">To do this, you assign the <xref:System.Resources.NeutralResourcesLanguageAttribute> attribute a value of <xref:System.Resources.UltimateResourceFallbackLocation.Satellite?displayProperty=nameWithType>.</span></span>

## <a name="satellite-assembly-name-and-location"></a><span data-ttu-id="5058c-115">附屬組件名稱和位置</span><span class="sxs-lookup"><span data-stu-id="5058c-115">Satellite Assembly Name and Location</span></span>

<span data-ttu-id="5058c-116">中樞和支點模型需要您將資源放入特定位置，以輕鬆地找到和使用它們。</span><span class="sxs-lookup"><span data-stu-id="5058c-116">The hub-and-spoke model requires that you place resources in specific locations so that they can be easily located and used.</span></span> <span data-ttu-id="5058c-117">如果您未如預期編譯和命名資源，或未將它們放在正確位置，則 Common Language Runtime 會找不到它們，並改為使用預設文化特性的資源。</span><span class="sxs-lookup"><span data-stu-id="5058c-117">If you do not compile and name resources as expected, or if you do not place them in the correct locations, the common language runtime will not be able to locate them and will use the resources of the default culture instead.</span></span> <span data-ttu-id="5058c-118">以 <xref:System.Resources.ResourceManager> 物件代表的 .NET Framework Resource Manager 是用來自動存取當地語系化資源。</span><span class="sxs-lookup"><span data-stu-id="5058c-118">The .NET Framework Resource Manager, represented by a <xref:System.Resources.ResourceManager> object, is used to automatically access localized resources.</span></span> <span data-ttu-id="5058c-119">Resource Manager 需要下列各項：</span><span class="sxs-lookup"><span data-stu-id="5058c-119">The Resource Manager requires the following:</span></span>

- <span data-ttu-id="5058c-120">單一附屬組件必須包括特定文化特性的所有資源。</span><span class="sxs-lookup"><span data-stu-id="5058c-120">A single satellite assembly must include all the resources for a particular culture.</span></span> <span data-ttu-id="5058c-121">換句話說，您應該將多個 *.txt* 或 *.resx* 檔案編譯成單一的二進位 *.resources* 檔。</span><span class="sxs-lookup"><span data-stu-id="5058c-121">In other words, you should compile multiple *.txt* or *.resx* files into a single binary *.resources* file.</span></span>

- <span data-ttu-id="5058c-122">在儲存該文化特性資源之每個當地語系化文化特性的應用程式目錄中，都必須有不同的子目錄。</span><span class="sxs-lookup"><span data-stu-id="5058c-122">There must be a separate subdirectory in the application directory for each localized culture that stores that culture's resources.</span></span> <span data-ttu-id="5058c-123">子目錄名稱必須與文化特性名稱相同。</span><span class="sxs-lookup"><span data-stu-id="5058c-123">The subdirectory name must be the same as the culture name.</span></span> <span data-ttu-id="5058c-124">或者，您可以在全域組件快取中儲存附屬組件。</span><span class="sxs-lookup"><span data-stu-id="5058c-124">Alternately, you can store your satellite assemblies in the global assembly cache.</span></span> <span data-ttu-id="5058c-125">在此情況下，組件強式名稱的文化特性資訊元件必須指出其文化特性。</span><span class="sxs-lookup"><span data-stu-id="5058c-125">In this case, the culture information component of the assembly's strong name must indicate its culture.</span></span> <span data-ttu-id="5058c-126">(請參閱本主題稍後的[在全域組件快取中安裝附屬組件](#SN)一節)。</span><span class="sxs-lookup"><span data-stu-id="5058c-126">(See the [Installing Satellite Assemblies in the Global Assembly Cache](#SN) section later in this topic.)</span></span>

  > [!NOTE]
  > <span data-ttu-id="5058c-127">如果您的應用程式包括子文化特性的資源，請將每個子文化特性放在應用程式目錄下的不同子目錄中。</span><span class="sxs-lookup"><span data-stu-id="5058c-127">If your application includes resources for subcultures, place each subculture in a separate subdirectory under the application directory.</span></span> <span data-ttu-id="5058c-128">請不要將子文化特性放在其主要文化特性目錄的子目錄中。</span><span class="sxs-lookup"><span data-stu-id="5058c-128">Do not place subcultures in subdirectories under their main culture's directory.</span></span>

- <span data-ttu-id="5058c-129">附屬組件的名稱必須與應用程式相同，而且必須使用副檔名 ".resources.dll"。</span><span class="sxs-lookup"><span data-stu-id="5058c-129">The satellite assembly must have the same name as the application, and must use the file name extension ".resources.dll".</span></span> <span data-ttu-id="5058c-130">例如，如果應用程式的名稱為 *Example.exe*，則應該 *Example.resources.dll*每個附屬元件的名稱。</span><span class="sxs-lookup"><span data-stu-id="5058c-130">For example, if an application is named *Example.exe*, the name of each satellite assembly should be *Example.resources.dll*.</span></span> <span data-ttu-id="5058c-131">請注意，附屬組件名稱不會指出其資源檔的文化特性。</span><span class="sxs-lookup"><span data-stu-id="5058c-131">Note that the satellite assembly name does not indicate the culture of its resource files.</span></span> <span data-ttu-id="5058c-132">不過，附屬組件會出現在確實指定文化特性的目錄中。</span><span class="sxs-lookup"><span data-stu-id="5058c-132">However, the satellite assembly appears in a directory that does specify the culture.</span></span>

- <span data-ttu-id="5058c-133">附屬組件文化特性的資訊必須包括在組件的中繼資料內。</span><span class="sxs-lookup"><span data-stu-id="5058c-133">Information about the culture of the satellite assembly must be included in the assembly's metadata.</span></span> <span data-ttu-id="5058c-134">若要將文化特性名稱儲存在附屬組件的中繼資料內，請在使用[組件連結器](../tools/al-exe-assembly-linker.md)將資源內嵌在附屬組件時指定 `/culture` 選項。</span><span class="sxs-lookup"><span data-stu-id="5058c-134">To store the culture name in the satellite assembly's metadata, you specify the `/culture` option when you use [Assembly Linker](../tools/al-exe-assembly-linker.md) to embed resources in the satellite assembly.</span></span>

<span data-ttu-id="5058c-135">下圖顯示未在[全域組件快取](../app-domains/gac.md)中安裝之應用程式的範例目錄結構和位置需求。</span><span class="sxs-lookup"><span data-stu-id="5058c-135">The following illustration shows a sample directory structure and location requirements for applications that you are not installing in the [global assembly cache](../app-domains/gac.md).</span></span> <span data-ttu-id="5058c-136">副檔名為 .txt 和 .resources 的項目將不會隨附最終應用程式。</span><span class="sxs-lookup"><span data-stu-id="5058c-136">The items with .txt and .resources extensions will not ship with the final application.</span></span> <span data-ttu-id="5058c-137">這些是用來建立最終附屬資源組件的中繼資源檔。</span><span class="sxs-lookup"><span data-stu-id="5058c-137">These are the intermediate resource files used to create the final satellite resource assemblies.</span></span> <span data-ttu-id="5058c-138">在此範例中，您可以將 .resx 檔案取代為 .txt 檔案。</span><span class="sxs-lookup"><span data-stu-id="5058c-138">In this example, you could substitute .resx files for the .txt files.</span></span> <span data-ttu-id="5058c-139">如需詳細資訊，請參閱[封裝和部署資源](packaging-and-deploying-resources-in-desktop-apps.md)。</span><span class="sxs-lookup"><span data-stu-id="5058c-139">For more information, see [Packaging and Deploying Resources](packaging-and-deploying-resources-in-desktop-apps.md).</span></span>

<span data-ttu-id="5058c-140">下圖顯示附屬組件目錄：</span><span class="sxs-lookup"><span data-stu-id="5058c-140">The following image shows the satellite assembly directory:</span></span>

![使用當地語系化文化特性 (Culture) 子目錄的附屬組件目錄。](./media/creating-satellite-assemblies-for-desktop-apps/satellite-assembly-directory.gif)

## <a name="compiling-satellite-assemblies"></a><span data-ttu-id="5058c-142">編譯附屬組件</span><span class="sxs-lookup"><span data-stu-id="5058c-142">Compiling Satellite Assemblies</span></span>

<span data-ttu-id="5058c-143">您可以使用 [資源檔產生器 ( # A0) ](../tools/resgen-exe-resource-file-generator.md) 將文字檔或 XML (*.resx*) 包含資源的檔案編譯成二進位 *.resources* 檔。</span><span class="sxs-lookup"><span data-stu-id="5058c-143">You use [Resource File Generator (Resgen.exe)](../tools/resgen-exe-resource-file-generator.md) to compile text files or XML (*.resx*) files that contain resources to binary *.resources* files.</span></span> <span data-ttu-id="5058c-144">然後，您可以使用 [元件連結器 ( # A0) ](../tools/al-exe-assembly-linker.md) 將 *.resources* 檔編譯成附屬元件。</span><span class="sxs-lookup"><span data-stu-id="5058c-144">You then use [Assembly Linker (Al.exe)](../tools/al-exe-assembly-linker.md) to compile *.resources* files into satellite assemblies.</span></span> <span data-ttu-id="5058c-145">*Al.exe* 會從您指定的 *.resources* 檔建立元件。</span><span class="sxs-lookup"><span data-stu-id="5058c-145">*Al.exe* creates an assembly from the *.resources* files that you specify.</span></span> <span data-ttu-id="5058c-146">附屬組件只能包含資源，而不能包含任何可執行程式碼。</span><span class="sxs-lookup"><span data-stu-id="5058c-146">Satellite assemblies can contain only resources; they cannot contain any executable code.</span></span>

<span data-ttu-id="5058c-147">下列*Al.exe*命令會 `Example` 從德文資源檔字串中，建立應用程式的附屬元件 *。*</span><span class="sxs-lookup"><span data-stu-id="5058c-147">The following *Al.exe* command creates a satellite assembly for the application `Example` from the German resources file *strings.de.resources*.</span></span>

```console
al -target:lib -embed:strings.de.resources -culture:de -out:Example.resources.dll
```

<span data-ttu-id="5058c-148">下列*Al.exe*命令也會 `Example` 從檔字串中建立應用程式的附屬元件 *。*</span><span class="sxs-lookup"><span data-stu-id="5058c-148">The following *Al.exe* command also creates a satellite assembly for the application `Example` from the file *strings.de.resources*.</span></span> <span data-ttu-id="5058c-149">**/Template**選項會使附屬元件繼承所有元件中繼資料，但父元件 (*Example.dll*) 的文化特性資訊除外。</span><span class="sxs-lookup"><span data-stu-id="5058c-149">The **/template** option causes the satellite assembly to inherit all assembly metadata except for its culture information from the parent assembly (*Example.dll*).</span></span>

```console
al -target:lib -embed:strings.de.resources -culture:de -out:Example.resources.dll -template:Example.dll
```  
  
<span data-ttu-id="5058c-150">下表詳細說明這些命令中使用的 *Al.exe* 選項：</span><span class="sxs-lookup"><span data-stu-id="5058c-150">The following table describes the *Al.exe* options used in these commands in more detail:</span></span>
  
|<span data-ttu-id="5058c-151">選項</span><span class="sxs-lookup"><span data-stu-id="5058c-151">Option</span></span>|<span data-ttu-id="5058c-152">描述</span><span class="sxs-lookup"><span data-stu-id="5058c-152">Description</span></span>|
|------------|-----------------|
|`-target:lib`|<span data-ttu-id="5058c-153">指定將附屬組件編譯成程式庫 (.dll) 檔案。</span><span class="sxs-lookup"><span data-stu-id="5058c-153">Specifies that your satellite assembly is compiled to a library (.dll) file.</span></span> <span data-ttu-id="5058c-154">因為附屬組件未包含可執行程式碼，而且不是應用程式的主要組件，所以您必須將附屬組件儲存為 DLL。</span><span class="sxs-lookup"><span data-stu-id="5058c-154">Because a satellite assembly does not contain executable code and is not an application's main assembly, you must save satellite assemblies as DLLs.</span></span>|
|`-embed:strings.de.resources`|<span data-ttu-id="5058c-155">當 *Al.exe* 編譯元件時，指定要內嵌的資源檔名稱。</span><span class="sxs-lookup"><span data-stu-id="5058c-155">Specifies the name of the resource file to embed when *Al.exe* compiles the assembly.</span></span> <span data-ttu-id="5058c-156">您可以在附屬組件中內嵌多個 .resources 檔案；但是，如果您遵循中樞和支點模型，則必須為每個文化特性編譯一個附屬組件。</span><span class="sxs-lookup"><span data-stu-id="5058c-156">You can embed multiple .resources files in a satellite assembly, but if you are following the hub-and-spoke model, you must compile one satellite assembly for each culture.</span></span> <span data-ttu-id="5058c-157">不過，您可以為字串和物件建立個別的 .resources 檔案。</span><span class="sxs-lookup"><span data-stu-id="5058c-157">However, you can create separate .resources files for strings and objects.</span></span>|
|`-culture:de`|<span data-ttu-id="5058c-158">指定要編譯之資源的文化特性。</span><span class="sxs-lookup"><span data-stu-id="5058c-158">Specifies the culture of the resource to compile.</span></span> <span data-ttu-id="5058c-159">Common Language Runtime 在搜尋所指定文化特性的資源時會使用這項資訊。</span><span class="sxs-lookup"><span data-stu-id="5058c-159">The common language runtime uses this information when it searches for the resources for a specified culture.</span></span> <span data-ttu-id="5058c-160">如果您省略此選項， *Al.exe* 仍會編譯資源，但是當使用者要求時，執行時間將找不到它。</span><span class="sxs-lookup"><span data-stu-id="5058c-160">If you omit this option, *Al.exe* will still compile the resource, but the runtime will not be able to find it when a user requests it.</span></span>|
|`-out:Example.resources.dll`|<span data-ttu-id="5058c-161">指定輸出檔案的名稱。</span><span class="sxs-lookup"><span data-stu-id="5058c-161">Specifies the name of the output file.</span></span> <span data-ttu-id="5058c-162">名稱必須遵循命名標準 <基底名稱>**.resources.<副檔名>**，其中 <基底名稱>\*\* 為主要組件的名稱，<副檔名>\*\* 則為有效的副檔名 (例如 .dll)。</span><span class="sxs-lookup"><span data-stu-id="5058c-162">The name must follow the naming standard *baseName*.resources.*extension*, where *baseName* is the name of the main assembly and *extension* is a valid file name extension (such as .dll).</span></span> <span data-ttu-id="5058c-163">請注意，執行階段無法根據輸出檔名稱來判斷附屬組件的文化特性；您必須使用 **/culture** 選項來指定它。</span><span class="sxs-lookup"><span data-stu-id="5058c-163">Note that the runtime is not able to determine the culture of a satellite assembly based on its output file name; you must use the **/culture** option to specify it.</span></span>|
|`-template:Example.dll`|<span data-ttu-id="5058c-164">指定附屬組件要從中繼承所有組件中繼資料的組件，但不包括文化特性欄位。</span><span class="sxs-lookup"><span data-stu-id="5058c-164">Specifies an assembly from which the satellite assembly will inherit all assembly metadata except the culture field.</span></span> <span data-ttu-id="5058c-165">只有在您指定的組件具有[強式名稱](../../standard/assembly/strong-named.md)時，此選項才會影響附屬組件。</span><span class="sxs-lookup"><span data-stu-id="5058c-165">This option affects satellite assemblies only if you specify an assembly that has a [strong name](../../standard/assembly/strong-named.md).</span></span>|
  
 <span data-ttu-id="5058c-166">如需 *Al.exe*可用選項的完整清單，請參閱 [元件連結器 ( # A1) ](../tools/al-exe-assembly-linker.md)。</span><span class="sxs-lookup"><span data-stu-id="5058c-166">For a complete list of options available with *Al.exe*, see [Assembly Linker (Al.exe)](../tools/al-exe-assembly-linker.md).</span></span>
  
## <a name="satellite-assemblies-an-example"></a><span data-ttu-id="5058c-167">附屬組件：範例</span><span class="sxs-lookup"><span data-stu-id="5058c-167">Satellite Assemblies: An Example</span></span>

<span data-ttu-id="5058c-168">下列簡單 "Hello world" 範例會顯示包含當地語系化問候語的訊息方塊。</span><span class="sxs-lookup"><span data-stu-id="5058c-168">The following is a simple "Hello world" example that displays a message box containing a localized greeting.</span></span> <span data-ttu-id="5058c-169">此範例包括英文 (美國)、法文 (法國) 和俄文 (俄國) 文化特性的資源，而其後援文化特性是英文。</span><span class="sxs-lookup"><span data-stu-id="5058c-169">The example includes resources for the English (United States), French (France), and Russian (Russia) cultures, and its fallback culture is English.</span></span> <span data-ttu-id="5058c-170">若要建立範例，請執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="5058c-170">To create the example, do the following:</span></span>
  
1. <span data-ttu-id="5058c-171">建立名為 *問候 .resx* 或 *Greeting.txt* 的資源檔，以包含預設文化特性的資源。</span><span class="sxs-lookup"><span data-stu-id="5058c-171">Create a resource file named *Greeting.resx* or *Greeting.txt* to contain the resource for the default culture.</span></span> <span data-ttu-id="5058c-172">將名為 `HelloString` 且其值為 "Hello world!" 的單一字串儲存</span><span class="sxs-lookup"><span data-stu-id="5058c-172">Store a single string named `HelloString` whose value is "Hello world!"</span></span> <span data-ttu-id="5058c-173">在此檔案中。</span><span class="sxs-lookup"><span data-stu-id="5058c-173">in this file.</span></span>

2. <span data-ttu-id="5058c-174">若要指出英文 (en) 是應用程式的預設文化特性，請將下列 <xref:System.Resources.NeutralResourcesLanguageAttribute?displayProperty=nameWithType> 屬性新增至應用程式的 AssemblyInfo 檔案或將編譯為應用程式主要組件的主要原始程式碼檔案。</span><span class="sxs-lookup"><span data-stu-id="5058c-174">To indicate that English (en) is the application's default culture, add the following <xref:System.Resources.NeutralResourcesLanguageAttribute?displayProperty=nameWithType> attribute to the application's AssemblyInfo file or to the main source code file that will be compiled into the application's main assembly.</span></span>

    ```csharp
    [assembly: NeutralResourcesLanguageAttribute("en")]
    ```

    ```vb
    <Assembly: NeutralResourcesLanguageAttribute("en")>
    ```
  
3. <span data-ttu-id="5058c-175">將其他文化特性 (en-US、fr-FR 和 ru-RU) 的支援新增至應用程式，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5058c-175">Add support for additional cultures (en-US, fr-FR, and ru-RU) to the application as follows:</span></span>  
  
    - <span data-ttu-id="5058c-176">若要支援 en-us 或英文 (美國) 文化特性，請建立一個名為 [en-us *Greeting.en-US.resx* ] 或 [ *Greeting.en-US.txt*] 的資源檔，然後將其 `HelloString` 值為 "Hi world！" 的單一字串儲存在其中。</span><span class="sxs-lookup"><span data-stu-id="5058c-176">To support the en-US or English (United States) culture, create a resource file named *Greeting.en-US.resx* or *Greeting.en-US.txt*, and store in it a single string named `HelloString` whose value is "Hi world!".</span></span>
  
    - <span data-ttu-id="5058c-177">若要支援 fr 或法文 (法國) 文化特性，請建立名為 *Greeting.fr* 的資源檔，或 *Greeting.fr-FR.txt*，然後將 `HelloString` 其值為 "Salut tout le monde！" 的單一字串儲存在其中。</span><span class="sxs-lookup"><span data-stu-id="5058c-177">To support the fr-FR or French (France) culture, create a resource file named *Greeting.fr-FR.resx* or *Greeting.fr-FR.txt*, and store in it a single string named `HelloString` whose value is "Salut tout le monde!".</span></span>
  
    - <span data-ttu-id="5058c-178">若要支援 ru-RU 或俄文 (俄羅斯) 文化特性，請建立名為 *Greeting.ru-ru* 或 *Greeting.ru-RU.txt*的資源檔，並將其 `HelloString` 值為 "Всемпривет！" 的單一字串儲存在其中。</span><span class="sxs-lookup"><span data-stu-id="5058c-178">To support the ru-RU or Russian (Russia) culture, create a resource file named *Greeting.ru-RU.resx* or *Greeting.ru-RU.txt*, and store in it a single string named `HelloString` whose value is "Всем привет!".</span></span>
  
4. <span data-ttu-id="5058c-179">使用 [Resgen.exe](../tools/resgen-exe-resource-file-generator.md) ，將每個文字或 XML 資源檔編譯成二進位 *.resources* 檔。</span><span class="sxs-lookup"><span data-stu-id="5058c-179">Use [Resgen.exe](../tools/resgen-exe-resource-file-generator.md) to compile each text or XML resource file to a binary *.resources* file.</span></span> <span data-ttu-id="5058c-180">輸出是一組檔案，與 *.resx* 或 *.txt* 檔案具有相同的根檔案名，但副檔名為 *.resources* 。</span><span class="sxs-lookup"><span data-stu-id="5058c-180">The output is a set of files that have the same root file name as the *.resx* or *.txt* files, but a *.resources* extension.</span></span> <span data-ttu-id="5058c-181">如果您使用 Visual Studio 建立範例，則會自動處理編譯程序。</span><span class="sxs-lookup"><span data-stu-id="5058c-181">If you create the example with Visual Studio, the compilation process is handled automatically.</span></span> <span data-ttu-id="5058c-182">如果您未使用 Visual Studio，請執行下列命令，將 *.resx* 檔案編譯為 *.resources* 檔案：</span><span class="sxs-lookup"><span data-stu-id="5058c-182">If you aren't using Visual Studio, run the following commands to compile the *.resx* files into *.resources* files:</span></span>  
  
    ```console
    resgen Greeting.resx
    resgen Greeting.en-us.resx
    resgen Greeting.fr-FR.resx
    resgen Greeting.ru-RU.resx
    ```

    <span data-ttu-id="5058c-183">如果您的資源是在文字檔中，而不是 XML 檔案，請將 *.resx* 副檔名取代為 *.txt*。</span><span class="sxs-lookup"><span data-stu-id="5058c-183">If your resources are in text files instead of XML files, replace the *.resx* extension with *.txt*.</span></span>

5. <span data-ttu-id="5058c-184">將下列原始程式碼與預設文化特性的資源編譯為應用程式的主要組件：</span><span class="sxs-lookup"><span data-stu-id="5058c-184">Compile the following source code along with the resources for the default culture into the application's main assembly:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="5058c-185">如果您使用命令列建立範例而非 Visual Studio，則應該將 <xref:System.Resources.ResourceManager> 類別建構函式的呼叫修改為下列：`ResourceManager rm = new ResourceManager("Greetings", typeof(Example).Assembly);`</span><span class="sxs-lookup"><span data-stu-id="5058c-185">If you are using the command line rather than Visual Studio to create the example, you should modify the call to the <xref:System.Resources.ResourceManager> class constructor to the following: `ResourceManager rm = new ResourceManager("Greetings", typeof(Example).Assembly);`</span></span>

    [!code-csharp[Conceptual.Resources.Locating#1](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.locating/cs/program.cs#1)]
    [!code-vb[Conceptual.Resources.Locating#1](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.resources.locating/vb/module1.vb#1)]

    <span data-ttu-id="5058c-186">如果應用程式名為 Example，而您要從命令列進行編譯，則 c # 編譯器的命令是：</span><span class="sxs-lookup"><span data-stu-id="5058c-186">If the application is named Example and you are compiling from the command-line, the command for the C# compiler is:</span></span>

    ```console
    csc Example.cs -res:Greeting.resources
    ```

    <span data-ttu-id="5058c-187">對應的 Visual Basic 編譯器命令為：</span><span class="sxs-lookup"><span data-stu-id="5058c-187">The corresponding Visual Basic compiler command is:</span></span>

    ```console
    vbc Example.vb -res:Greeting.resources
    ```

6. <span data-ttu-id="5058c-188">在應用程式所支援之每個當地語系化文化特性的主要應用程式目錄中，建立子目錄。</span><span class="sxs-lookup"><span data-stu-id="5058c-188">Create a subdirectory in the main application directory for each localized culture supported by the application.</span></span> <span data-ttu-id="5058c-189">您應建立 *en-us*、 *FR-FR*和 *ru ru 的* 子目錄。</span><span class="sxs-lookup"><span data-stu-id="5058c-189">You should create an *en-US*, an *fr-FR*, and an *ru-RU* subdirectory.</span></span> <span data-ttu-id="5058c-190">Visual Studio 會在編譯程序時自動建立這些子目錄。</span><span class="sxs-lookup"><span data-stu-id="5058c-190">Visual Studio creates these subdirectories automatically as part of the compilation process.</span></span>

7. <span data-ttu-id="5058c-191">將個別的文化特性特定 *.resources* 檔案內嵌到附屬元件，並將它們儲存到適當的目錄。</span><span class="sxs-lookup"><span data-stu-id="5058c-191">Embed the individual culture-specific *.resources* files into satellite assemblies and save them to the appropriate directory.</span></span> <span data-ttu-id="5058c-192">針對每個 *.resources* 檔案執行此動作的命令為：</span><span class="sxs-lookup"><span data-stu-id="5058c-192">The command to do this for each *.resources* file is:</span></span>

    ```console
    al -target:lib -embed:Greeting.culture.resources -culture:culture -out:culture\Example.resources.dll
    ```

     <span data-ttu-id="5058c-193">其中 *culture* 是附屬組件會包含其資源的文化特性名稱。</span><span class="sxs-lookup"><span data-stu-id="5058c-193">where *culture* is the name of the culture whose resources the satellite assembly contains.</span></span> <span data-ttu-id="5058c-194">Visual Studio 會自動處理這個程序。</span><span class="sxs-lookup"><span data-stu-id="5058c-194">Visual Studio handles this process automatically.</span></span>

<span data-ttu-id="5058c-195">您接著可以執行此範例。</span><span class="sxs-lookup"><span data-stu-id="5058c-195">You can then run the example.</span></span> <span data-ttu-id="5058c-196">它會隨機讓其中一個支援的文化特性成為目前文化特性，並顯示當地語系化的問候語。</span><span class="sxs-lookup"><span data-stu-id="5058c-196">It will randomly make one of the supported cultures the current culture and display a localized greeting.</span></span>

<a name="SN"></a>

## <a name="installing-satellite-assemblies-in-the-global-assembly-cache"></a><span data-ttu-id="5058c-197">在全域組件快取中安裝附屬組件</span><span class="sxs-lookup"><span data-stu-id="5058c-197">Installing Satellite Assemblies in the Global Assembly Cache</span></span>

<span data-ttu-id="5058c-198">您可以將組件安裝在全域組件快取中，而不是在本機應用程式子目錄中安裝組件。</span><span class="sxs-lookup"><span data-stu-id="5058c-198">Instead of installing assemblies in a local application subdirectory, you can install them in the global assembly cache.</span></span> <span data-ttu-id="5058c-199">如果您有供多個應用程式使用的類別庫和類別庫資源組件，則這特別有用。</span><span class="sxs-lookup"><span data-stu-id="5058c-199">This is particularly useful if you have class libraries and class library resource assemblies that are used by multiple applications.</span></span>
  
<span data-ttu-id="5058c-200">在全域組件快取中安裝組件時，需要組件具有強式名稱。</span><span class="sxs-lookup"><span data-stu-id="5058c-200">Installing assemblies in the global assembly cache requires that they have strong names.</span></span> <span data-ttu-id="5058c-201">強式名稱組件會使用有效的公開/私密金鑰組進行簽署。</span><span class="sxs-lookup"><span data-stu-id="5058c-201">Strong-named assemblies are signed with a valid public/private key pair.</span></span> <span data-ttu-id="5058c-202">它們包含執行階段用來判斷要用來滿足繫結要求之組件的版本資訊。</span><span class="sxs-lookup"><span data-stu-id="5058c-202">They contain version information that the runtime uses to determine which assembly to use to satisfy a binding request.</span></span> <span data-ttu-id="5058c-203">如需強式名稱和版本控制的詳細資訊，請參閱[組件版本控制](../../standard/assembly/versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="5058c-203">For more information about strong names and versioning, see [Assembly Versioning](../../standard/assembly/versioning.md).</span></span> <span data-ttu-id="5058c-204">如需強式名稱的詳細資訊，請參閱[強式名稱的組件](../../standard/assembly/strong-named.md)。</span><span class="sxs-lookup"><span data-stu-id="5058c-204">For more information about strong names, see [Strong-Named Assemblies](../../standard/assembly/strong-named.md).</span></span>

<span data-ttu-id="5058c-205">當您開發應用程式時，可能無法存取最終公開/私密金鑰組。</span><span class="sxs-lookup"><span data-stu-id="5058c-205">When you are developing an application, it is unlikely that you will have access to the final public/private key pair.</span></span> <span data-ttu-id="5058c-206">若要在全域組件快取中安裝附屬組件，並確認它的運作正常，您可以使用稱為延遲簽署的技術。</span><span class="sxs-lookup"><span data-stu-id="5058c-206">In order to install a satellite assembly in the global assembly cache and ensure that it works as expected, you can use a technique called delayed signing.</span></span> <span data-ttu-id="5058c-207">當您延遲簽署組件時，請在建置時間於檔案中保留強式名稱簽章的空間。</span><span class="sxs-lookup"><span data-stu-id="5058c-207">When you delay sign an assembly, at build time you reserve space in the file for the strong name signature.</span></span> <span data-ttu-id="5058c-208">有最終公開/私密金鑰組可用時，會將實際簽署延遲到稍後。</span><span class="sxs-lookup"><span data-stu-id="5058c-208">The actual signing is delayed until later, when the final public/private key pair is available.</span></span> <span data-ttu-id="5058c-209">如需延遲簽署的詳細資訊，請參閱[延遲簽署組件](../../standard/assembly/delay-sign.md)。</span><span class="sxs-lookup"><span data-stu-id="5058c-209">For more information about delayed signing, see [Delay Signing an Assembly](../../standard/assembly/delay-sign.md).</span></span>

### <a name="obtaining-the-public-key"></a><span data-ttu-id="5058c-210">取得公開金鑰</span><span class="sxs-lookup"><span data-stu-id="5058c-210">Obtaining the Public Key</span></span>

<span data-ttu-id="5058c-211">若要延遲簽署組件，您必須具有公開金鑰的存取權。</span><span class="sxs-lookup"><span data-stu-id="5058c-211">To delay sign an assembly, you must have access to the public key.</span></span> <span data-ttu-id="5058c-212">您可以從公司中進行最後簽署的組織中取得實際公開金鑰，或使用[強式名稱工具 (Sn.exe)](../tools/sn-exe-strong-name-tool.md) 建立公開金鑰。</span><span class="sxs-lookup"><span data-stu-id="5058c-212">You can either obtain the real public key from the organization in your company that will do the eventual signing, or create a public key by using the [Strong Name Tool (Sn.exe)](../tools/sn-exe-strong-name-tool.md).</span></span>

<span data-ttu-id="5058c-213">下列 *Sn.exe* 命令會建立測試公開/私密金鑰組。</span><span class="sxs-lookup"><span data-stu-id="5058c-213">The following *Sn.exe* command creates a test public/private key pair.</span></span> <span data-ttu-id="5058c-214">**– K**選項指定*Sn.exe*應該建立新的金鑰組，並將它儲存在名為*testkeypair.snk*的檔案中。</span><span class="sxs-lookup"><span data-stu-id="5058c-214">The **–k** option specifies that *Sn.exe* should create a new key pair and save it in a file named *TestKeyPair.snk*.</span></span>
  
```console
sn –k TestKeyPair.snk
```

<span data-ttu-id="5058c-215">您可以從包含測試金鑰組的檔案中擷取公開金鑰。</span><span class="sxs-lookup"><span data-stu-id="5058c-215">You can extract the public key from the file that contains the test key pair.</span></span> <span data-ttu-id="5058c-216">下列命令會從 *testkeypair.snk* 中解壓縮公開金鑰，並將它儲存在 *PublicKey*中：</span><span class="sxs-lookup"><span data-stu-id="5058c-216">The following command extracts the public key from *TestKeyPair.snk* and saves it in *PublicKey.snk*:</span></span>

```console
sn –p TestKeyPair.snk PublicKey.snk
```

### <a name="delay-signing-an-assembly"></a><span data-ttu-id="5058c-217">延遲簽署組件</span><span class="sxs-lookup"><span data-stu-id="5058c-217">Delay Signing an Assembly</span></span>

<span data-ttu-id="5058c-218">在您取得或建立公開金鑰之後，請使用[組件連結器 (Al.exe)](../tools/al-exe-assembly-linker.md) 編譯組件，並指定延遲簽署。</span><span class="sxs-lookup"><span data-stu-id="5058c-218">After you obtain or create the public key, you use the [Assembly Linker (Al.exe)](../tools/al-exe-assembly-linker.md) to compile the assembly and specify delayed signing.</span></span>

<span data-ttu-id="5058c-219">下列 *Al.exe* 命令會針對 StringLibrary 自 *字串 ja-jp* 檔案的應用程式，建立強式名稱的附屬元件：</span><span class="sxs-lookup"><span data-stu-id="5058c-219">The following *Al.exe* command creates a strong-named satellite assembly for the application StringLibrary from the *strings.ja.resources* file:</span></span>

```console
al -target:lib -embed:strings.ja.resources -culture:ja -out:StringLibrary.resources.dll -delay+ -keyfile:PublicKey.snk
```

<span data-ttu-id="5058c-220">\*\*\*\* 選項指定組件連結器應該延遲簽署組件。</span><span class="sxs-lookup"><span data-stu-id="5058c-220">The **-delay+** option specifies that the Assembly Linker should delay sign the assembly.</span></span> <span data-ttu-id="5058c-221">**-Keyfile**選項會指定金鑰檔的名稱，該檔案包含用來延遲簽署元件的公開金鑰。</span><span class="sxs-lookup"><span data-stu-id="5058c-221">The **-keyfile** option specifies the name of the key file that contains the public key to use to delay sign the assembly.</span></span>

### <a name="re-signing-an-assembly"></a><span data-ttu-id="5058c-222">重新簽署組件</span><span class="sxs-lookup"><span data-stu-id="5058c-222">Re-signing an Assembly</span></span>

<span data-ttu-id="5058c-223">部署您的應用程式之前，必須使用實際金鑰組來重新簽署延遲簽署的附屬組件。</span><span class="sxs-lookup"><span data-stu-id="5058c-223">Before you deploy your application, you must re-sign the delay signed satellite assembly with the real key pair.</span></span> <span data-ttu-id="5058c-224">您可以使用 *Sn.exe*來完成這項作業。</span><span class="sxs-lookup"><span data-stu-id="5058c-224">You can do this by using *Sn.exe*.</span></span>

<span data-ttu-id="5058c-225">下列*Sn.exe*命令會使用儲存在*RealKeyPair*檔案中的金鑰組來簽署*StringLibrary.resources.dll* 。</span><span class="sxs-lookup"><span data-stu-id="5058c-225">The following *Sn.exe* command signs *StringLibrary.resources.dll* with the key pair stored in the file *RealKeyPair.snk*.</span></span> <span data-ttu-id="5058c-226">**–R** 選項指定要重新簽署先前簽署的組件還是延遲簽署的組件。</span><span class="sxs-lookup"><span data-stu-id="5058c-226">The **–R** option specifies that a previously signed or delay signed assembly is to be re-signed.</span></span>

```console
sn –R StringLibrary.resources.dll RealKeyPair.snk
```

### <a name="installing-a-satellite-assembly-in-the-global-assembly-cache"></a><span data-ttu-id="5058c-227">在全域組件快取中安裝附屬組件</span><span class="sxs-lookup"><span data-stu-id="5058c-227">Installing a Satellite Assembly in the Global Assembly Cache</span></span>

<span data-ttu-id="5058c-228">執行階段在資源後援程序中搜尋資源時，會先尋找[全域組件快取](../app-domains/gac.md)</span><span class="sxs-lookup"><span data-stu-id="5058c-228">When the runtime searches for resources in the resource fallback process, it looks in the [global assembly cache](../app-domains/gac.md) first.</span></span> <span data-ttu-id="5058c-229"> (需詳細資訊，請參閱 [封裝和部署資源](packaging-and-deploying-resources-in-desktop-apps.md) 主題的「資源回溯程式」一節 ) 。當附屬元件以強式名稱簽署時，就可以在全域組件快取中安裝它，方法是使用 [全域組件快取工具 ( # A0) ](../tools/gacutil-exe-gac-tool.md)。</span><span class="sxs-lookup"><span data-stu-id="5058c-229">(For more information, see the "Resource Fallback Process" section of the [Packaging and Deploying Resources](packaging-and-deploying-resources-in-desktop-apps.md) topic.) As soon as a satellite assembly is signed with a strong name, it can be installed in the global assembly cache by using the [Global Assembly Cache Tool (Gacutil.exe)](../tools/gacutil-exe-gac-tool.md).</span></span>

<span data-ttu-id="5058c-230">下列 *Gacutil.exe* 命令會在全域組件快取中安裝 \*StringLibrary.resources.dll\*\*：</span><span class="sxs-lookup"><span data-stu-id="5058c-230">The following *Gacutil.exe* command installs *StringLibrary.resources.dll*\* in the global assembly cache:</span></span>

```console
gacutil -i:StringLibrary.resources.dll
```

<span data-ttu-id="5058c-231">**/I**選項指定*Gacutil.exe*應該將指定的元件安裝到全域組件快取中。</span><span class="sxs-lookup"><span data-stu-id="5058c-231">The **/i** option specifies that *Gacutil.exe* should install the specified assembly into the global assembly cache.</span></span> <span data-ttu-id="5058c-232">在快取中安裝附屬組件之後，其所含的資源可供設計成使用附屬組件的所有應用程式使用。</span><span class="sxs-lookup"><span data-stu-id="5058c-232">After the satellite assembly is installed in the cache, the resources it contains become available to all applications that are designed to use the satellite assembly.</span></span>

### <a name="resources-in-the-global-assembly-cache-an-example"></a><span data-ttu-id="5058c-233">全域組件快取中的資源：範例</span><span class="sxs-lookup"><span data-stu-id="5058c-233">Resources in the Global Assembly Cache: An Example</span></span>

<span data-ttu-id="5058c-234">下列範例會使用 .NET Framework 類別庫中的方法，從資源檔擷取並傳回當地語系化的問候。</span><span class="sxs-lookup"><span data-stu-id="5058c-234">The following example uses a method in a .NET Framework class library to extract and return a localized greeting from a resource file.</span></span> <span data-ttu-id="5058c-235">程式庫和其資源都會註冊在全域組件快取中。</span><span class="sxs-lookup"><span data-stu-id="5058c-235">The library and its resources are registered in the global assembly cache.</span></span> <span data-ttu-id="5058c-236">此範例包括英文 (美國)、法文 (法國)、俄文 (俄國) 和英文文化特性的資源。</span><span class="sxs-lookup"><span data-stu-id="5058c-236">The example includes resources for the English (United States), French (France), Russian (Russia), and English cultures.</span></span> <span data-ttu-id="5058c-237">英文是預設文化特性；其資源儲存在主要組件中。</span><span class="sxs-lookup"><span data-stu-id="5058c-237">English is the default culture; its resources are stored in the main assembly.</span></span> <span data-ttu-id="5058c-238">此範例一開始會使用公開金鑰來延遲簽署程式庫和其附屬組件，然後使用公開/私密金鑰組來重新簽署它們。</span><span class="sxs-lookup"><span data-stu-id="5058c-238">The example initially delay signs the library and its satellite assemblies with a public key, then re-signs them with a public/private key pair.</span></span> <span data-ttu-id="5058c-239">若要建立範例，請執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="5058c-239">To create the example, do the following:</span></span>

1. <span data-ttu-id="5058c-240">如果您不是使用 Visual Studio，請使用下列 [強式名稱工具 ( # A0) ](../tools/sn-exe-strong-name-tool.md) 命令來建立名為 *ResKey*的公開/私密金鑰組：</span><span class="sxs-lookup"><span data-stu-id="5058c-240">If you are not using Visual Studio, use the following [Strong Name Tool (Sn.exe)](../tools/sn-exe-strong-name-tool.md) command to create a public/private key pair named *ResKey.snk*:</span></span>

    ```console
    sn –k ResKey.snk
    ```

    <span data-ttu-id="5058c-241">如果您使用 Visual Studio，請使用專案 [屬性]\*\*\*\* 對話方塊的 [簽署]\*\*\*\* 索引標籤來產生金鑰檔。</span><span class="sxs-lookup"><span data-stu-id="5058c-241">If you are using Visual Studio, use the **Signing** tab of the project **Properties** dialog box to generate the key file.</span></span>

2. <span data-ttu-id="5058c-242">使用下列 [強式名稱工具 ( # A0) ](../tools/sn-exe-strong-name-tool.md) 命令來建立名為 *PublicKey*的公開金鑰檔案：</span><span class="sxs-lookup"><span data-stu-id="5058c-242">Use the following [Strong Name Tool (Sn.exe)](../tools/sn-exe-strong-name-tool.md) command to create a public key file named *PublicKey.snk*:</span></span>

    ```console
    sn –p ResKey.snk PublicKey.snk
    ```

3. <span data-ttu-id="5058c-243">建立名為 *Strings* 的資源檔，以包含預設文化特性的資源。</span><span class="sxs-lookup"><span data-stu-id="5058c-243">Create a resource file named *Strings.resx* to contain the resource for the default culture.</span></span> <span data-ttu-id="5058c-244">將名為 `Greeting` 且其值為 "How do you do?" 的單一字串儲存</span><span class="sxs-lookup"><span data-stu-id="5058c-244">Store a single string named `Greeting` whose value is "How do you do?"</span></span> <span data-ttu-id="5058c-245">在該檔案中。</span><span class="sxs-lookup"><span data-stu-id="5058c-245">in that file.</span></span>

4. <span data-ttu-id="5058c-246">若要指出 "en" 是應用程式的預設文化特性，請將下列 <xref:System.Resources.NeutralResourcesLanguageAttribute?displayProperty=nameWithType> 屬性新增至應用程式的 AssemblyInfo 檔案或將編譯為應用程式主要組件的主要原始程式碼檔案：</span><span class="sxs-lookup"><span data-stu-id="5058c-246">To indicate that "en" is the application's default culture, add the following <xref:System.Resources.NeutralResourcesLanguageAttribute?displayProperty=nameWithType> attribute to the application's AssemblyInfo file or to the main source code file that will be compiled into the application's main assembly:</span></span>

    [!code-csharp[Conceptual.Resources.Satellites#2](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.satellites/cs/stringlibrary.cs#2)]
    [!code-vb[Conceptual.Resources.Satellites#2](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.resources.satellites/vb/stringlibrary.vb#2)]

5. <span data-ttu-id="5058c-247">將其他文化特性 (en-US、fr-FR 和 ru-RU 文化特性) 的支援新增至應用程式，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5058c-247">Add support for additional cultures (the en-US, fr-FR, and ru-RU cultures) to the application as follows:</span></span>

    - <span data-ttu-id="5058c-248">若要支援美國) 文化特性的 "en-us" 或英文 (，請建立名為 *Strings* 或 *Strings.en-US.txt*的資源檔，並將其 `Greeting` 值為 "Hello！" 的單一字串儲存在其中。</span><span class="sxs-lookup"><span data-stu-id="5058c-248">To support the "en-US" or English (United States) culture, create a resource file named *Strings.en-US.resx* or *Strings.en-US.txt*, and store in it a single string named `Greeting` whose value is "Hello!".</span></span>

    - <span data-ttu-id="5058c-249">若要支援 "fr" 或法文 (法國) 文化特性，請建立名為 *Strings.fr* 的資源檔，或 *Strings.fr-FR.txt* 並儲存在其中的單一字串， `Greeting` 其值為 "Bon 日記！"。</span><span class="sxs-lookup"><span data-stu-id="5058c-249">To support the "fr-FR" or French (France) culture, create a resource file named *Strings.fr-FR.resx* or *Strings.fr-FR.txt* and store in it a single string named `Greeting` whose value is "Bon jour!".</span></span>

    - <span data-ttu-id="5058c-250">若要支援「ru RU」或俄文 (俄羅斯) 文化特性，請建立名為 *Strings.ru-ru* 或 *Strings.ru-RU.txt* 的資源檔，並將 `Greeting` 其值為 "Привет！" 的單一字串儲存在其中。</span><span class="sxs-lookup"><span data-stu-id="5058c-250">To support the "ru-RU" or Russian (Russia) culture, create a resource file named *Strings.ru-RU.resx* or *Strings.ru-RU.txt* and store in it a single string named `Greeting` whose value is "Привет!".</span></span>

6. <span data-ttu-id="5058c-251">使用 [Resgen.exe](../tools/resgen-exe-resource-file-generator.md)，將每一個文字或 XML 資源檔編譯成二進位 .resources 檔案。</span><span class="sxs-lookup"><span data-stu-id="5058c-251">Use [Resgen.exe](../tools/resgen-exe-resource-file-generator.md) to compile each text or XML resource file to a binary .resources file.</span></span> <span data-ttu-id="5058c-252">輸出是一組檔案，與 *.resx* 或 *.txt* 檔案具有相同的根檔案名，但副檔名為 *.resources* 。</span><span class="sxs-lookup"><span data-stu-id="5058c-252">The output is a set of files that have the same root file name as the *.resx* or *.txt* files, but a *.resources* extension.</span></span> <span data-ttu-id="5058c-253">如果您使用 Visual Studio 建立範例，則會自動處理編譯程序。</span><span class="sxs-lookup"><span data-stu-id="5058c-253">If you create the example with Visual Studio, the compilation process is handled automatically.</span></span> <span data-ttu-id="5058c-254">如果您未使用 Visual Studio，請執行下列命令，將 *.resx* 檔案編譯為 *.resources* 檔案：</span><span class="sxs-lookup"><span data-stu-id="5058c-254">If you aren't using Visual Studio, run the following command to compile the *.resx* files into *.resources* files:</span></span>

    ```console
    resgen filename
    ```

    <span data-ttu-id="5058c-255">其中*filename*是 .resx 或文字檔的選擇性路徑、檔案名和副檔名 *。*</span><span class="sxs-lookup"><span data-stu-id="5058c-255">Where *filename* is the optional path, file name, and extension of the *.resx* or text file.</span></span>

7. <span data-ttu-id="5058c-256">將下列適用于 *StringLibrary* 的原始程式碼或 *StringLibrary.cs* ，以及預設文化特性的資源，編譯為名為 *StringLibrary.dll*的延遲簽署程式庫元件：</span><span class="sxs-lookup"><span data-stu-id="5058c-256">Compile the following source code for *StringLibrary.vb* or *StringLibrary.cs* along with the resources for the default culture into a delay signed library assembly named *StringLibrary.dll*:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="5058c-257">如果您使用命令列而不是 Visual Studio 建立範例，則應該將對類別的呼叫函式的呼叫修改 <xref:System.Resources.ResourceManager> 為 `ResourceManager rm = new ResourceManager("Strings",` `typeof(Example).Assembly);` 。</span><span class="sxs-lookup"><span data-stu-id="5058c-257">If you are using the command line rather than Visual Studio to create the example, you should modify the call to the <xref:System.Resources.ResourceManager> class constructor to `ResourceManager rm = new ResourceManager("Strings",` `typeof(Example).Assembly);`.</span></span>

    [!code-csharp[Conceptual.Resources.Satellites#1](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.satellites/cs/stringlibrary.cs#1)]
    [!code-vb[Conceptual.Resources.Satellites#1](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.resources.satellites/vb/stringlibrary.vb#1)]

    <span data-ttu-id="5058c-258">C# 編譯器的命令是：</span><span class="sxs-lookup"><span data-stu-id="5058c-258">The command for the C# compiler is:</span></span>

    ```console
    csc -t:library -resource:Strings.resources -delaysign+ -keyfile:publickey.snk StringLibrary.cs
    ```

    <span data-ttu-id="5058c-259">對應的 Visual Basic 編譯器命令為：</span><span class="sxs-lookup"><span data-stu-id="5058c-259">The corresponding Visual Basic compiler command is:</span></span>

    ```console
    vbc -t:library -resource:Strings.resources -delaysign+ -keyfile:publickey.snk StringLibrary.vb
    ```

8. <span data-ttu-id="5058c-260">在應用程式所支援之每個當地語系化文化特性的主要應用程式目錄中，建立子目錄。</span><span class="sxs-lookup"><span data-stu-id="5058c-260">Create a subdirectory in the main application directory for each localized culture supported by the application.</span></span> <span data-ttu-id="5058c-261">您應建立 *en-us*、 *FR-FR*和 *ru ru 的* 子目錄。</span><span class="sxs-lookup"><span data-stu-id="5058c-261">You should create an *en-US*, an *fr-FR*, and an *ru-RU* subdirectory.</span></span> <span data-ttu-id="5058c-262">Visual Studio 會在編譯程序時自動建立這些子目錄。</span><span class="sxs-lookup"><span data-stu-id="5058c-262">Visual Studio creates these subdirectories automatically as part of the compilation process.</span></span> <span data-ttu-id="5058c-263">因為所有附屬組件都有相同的檔案名稱，所以使用子目錄來儲存個別文化特性特定附屬組件，直到使用公開/私密金鑰組簽署它們為止。</span><span class="sxs-lookup"><span data-stu-id="5058c-263">Because all satellite assemblies have the same file name, the subdirectories are used to store individual culture-specific satellite assemblies until they are signed with a public/private key pair.</span></span>

9. <span data-ttu-id="5058c-264">將個別的文化特性特定 *.resources* 檔案內嵌至延遲簽署的附屬元件，並將它們儲存到適當的目錄。</span><span class="sxs-lookup"><span data-stu-id="5058c-264">Embed the individual culture-specific *.resources* files into delay signed satellite assemblies and save them to the appropriate directory.</span></span> <span data-ttu-id="5058c-265">針對每個 *.resources* 檔案執行此動作的命令為：</span><span class="sxs-lookup"><span data-stu-id="5058c-265">The command to do this for each *.resources* file is:</span></span>

    ```console
    al -target:lib -embed:Strings.culture.resources -culture:culture -out:culture\StringLibrary.resources.dll -delay+ -keyfile:publickey.snk
    ```

    <span data-ttu-id="5058c-266">其中 *culture* 是文化特性的名稱。</span><span class="sxs-lookup"><span data-stu-id="5058c-266">where *culture* is the name of a culture.</span></span> <span data-ttu-id="5058c-267">在此範例中，文化特性名稱是 en-US、fr-FR 和 ru-RU。</span><span class="sxs-lookup"><span data-stu-id="5058c-267">In this example, the culture names are en-US, fr-FR, and ru-RU.</span></span>

10. <span data-ttu-id="5058c-268">使用[強式名稱工具 ( # A1) ](../tools/sn-exe-strong-name-tool.md)重新簽署*StringLibrary.dll* ，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5058c-268">Re-sign *StringLibrary.dll* by using the [Strong Name Tool (Sn.exe)](../tools/sn-exe-strong-name-tool.md) as follows:</span></span>

    ```console
    sn –R StringLibrary.dll RealKeyPair.snk
    ```

11. <span data-ttu-id="5058c-269">重新簽署個別附屬組件。</span><span class="sxs-lookup"><span data-stu-id="5058c-269">Re-sign the individual satellite assemblies.</span></span> <span data-ttu-id="5058c-270">若要這樣做，請使用每個附屬組件的[強式名稱工具 (Sn.exe)](../tools/sn-exe-strong-name-tool.md)，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5058c-270">To do this, use the [Strong Name Tool (Sn.exe)](../tools/sn-exe-strong-name-tool.md) as follows for each satellite assembly:</span></span>

    ```console
    sn –R StringLibrary.resources.dll RealKeyPair.snk
    ```

12. <span data-ttu-id="5058c-271">使用下列命令，在全域組件快取中註冊 *StringLibrary.dll* 和其每個附屬元件：</span><span class="sxs-lookup"><span data-stu-id="5058c-271">Register *StringLibrary.dll* and each of its satellite assemblies in the global assembly cache by using the following command:</span></span>

    ```console
    gacutil -i filename
    ```

    <span data-ttu-id="5058c-272">其中 <檔案名稱>\*\* 是要註冊之檔案的名稱。</span><span class="sxs-lookup"><span data-stu-id="5058c-272">where *filename* is the name of the file to register.</span></span>

13. <span data-ttu-id="5058c-273">如果您使用 Visual Studio，請建立名為的新 **主控台應用程式** 專案 `Example` ，並在其中加入 *StringLibrary.dll* 的參考和下列原始程式碼，然後編譯。</span><span class="sxs-lookup"><span data-stu-id="5058c-273">If you are using Visual Studio, create a new **Console Application** project named `Example`, add a reference to *StringLibrary.dll* and the following source code to it, and compile.</span></span>

    [!code-csharp[Conceptual.Resources.Satellites#3](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.satellites/cs/example.cs#3)]
    [!code-vb[Conceptual.Resources.Satellites#3](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.resources.satellites/vb/example.vb#3)]

    <span data-ttu-id="5058c-274">若要從命令列進行編譯，請針對 C# 編譯器使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="5058c-274">To compile from the command line, use the following command for the C# compiler:</span></span>

    ```console
    csc Example.cs -r:StringLibrary.dll
    ```

    <span data-ttu-id="5058c-275">Visual Basic 編譯器的命令列為：</span><span class="sxs-lookup"><span data-stu-id="5058c-275">The command line for the Visual Basic compiler is:</span></span>

    ```console
    vbc Example.vb -r:StringLibrary.dll
    ```

14. <span data-ttu-id="5058c-276">執行 *Example.exe*。</span><span class="sxs-lookup"><span data-stu-id="5058c-276">Run *Example.exe*.</span></span>

## <a name="see-also"></a><span data-ttu-id="5058c-277">請參閱</span><span class="sxs-lookup"><span data-stu-id="5058c-277">See also</span></span>

- [<span data-ttu-id="5058c-278">封裝和部署資源</span><span class="sxs-lookup"><span data-stu-id="5058c-278">Packaging and Deploying Resources</span></span>](packaging-and-deploying-resources-in-desktop-apps.md)
- [<span data-ttu-id="5058c-279">延遲簽署組件</span><span class="sxs-lookup"><span data-stu-id="5058c-279">Delay Signing an Assembly</span></span>](../../standard/assembly/delay-sign.md)
- [<span data-ttu-id="5058c-280">Al.exe (元件連結器) </span><span class="sxs-lookup"><span data-stu-id="5058c-280">Al.exe (Assembly Linker)</span></span>](../tools/al-exe-assembly-linker.md)
- [<span data-ttu-id="5058c-281">Sn.exe (強式名稱工具) </span><span class="sxs-lookup"><span data-stu-id="5058c-281">Sn.exe (Strong Name Tool)</span></span>](../tools/sn-exe-strong-name-tool.md)
- [<span data-ttu-id="5058c-282">Gacutil.exe (全域組件快取工具) </span><span class="sxs-lookup"><span data-stu-id="5058c-282">Gacutil.exe (Global Assembly Cache Tool)</span></span>](../tools/gacutil-exe-gac-tool.md)
- [<span data-ttu-id="5058c-283">桌面應用程式中的資源</span><span class="sxs-lookup"><span data-stu-id="5058c-283">Resources in Desktop Apps</span></span>](index.md)
