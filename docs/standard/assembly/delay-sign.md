---
title: 延遲簽署組件
description: 本文說明延遲或部分簽署，其會在 PE 檔中保留強式名稱簽章的空間，但會延遲實際的簽章。
ms.date: 08/19/2019
helpviewer_keywords:
- deferring assembly signing
- signing assemblies
- assemblies [.NET Framework], signing
- strong-named assemblies, delaying assembly signing
- partial assembly signing
ms.assetid: 9d300e17-5bf1-4360-97da-2aa55efd9070
dev_langs:
- csharp
- vb
- cpp
ms.openlocfilehash: 7b5c8c8463fdc573782fa457bf5671c72a7e25f7
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/13/2020
ms.locfileid: "83378496"
---
# <a name="delay-sign-an-assembly"></a><span data-ttu-id="1d004-103">延遲簽署組件</span><span class="sxs-lookup"><span data-stu-id="1d004-103">Delay-sign an assembly</span></span>

<span data-ttu-id="1d004-104">組織可能會有一組嚴密受防護的金鑰組，開發人員每日無法存取。</span><span class="sxs-lookup"><span data-stu-id="1d004-104">An organization can have a closely guarded key pair that developers can't access on a daily basis.</span></span> <span data-ttu-id="1d004-105">公開金鑰經常都可以使用，但只有少數人才能存取私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="1d004-105">The public key is often available, but access to the private key is restricted to only a few individuals.</span></span> <span data-ttu-id="1d004-106">在以強式名稱開發組件時，每個參考強式名稱目標組件的組件都包含用來指定目標組件的強式名稱的公開金鑰語彙基元。</span><span class="sxs-lookup"><span data-stu-id="1d004-106">When developing assemblies with strong names, each assembly that references the strong-named target assembly contains the token of the public key used to give the target assembly a strong name.</span></span> <span data-ttu-id="1d004-107">這需要可在開發程序期間使用公開金鑰。</span><span class="sxs-lookup"><span data-stu-id="1d004-107">This requires that the public key be available during the development process.</span></span>

<span data-ttu-id="1d004-108">您可以在組建階段使用延遲或部分簽署，以在可移植執行檔（PE）中保留強式名稱簽章的空間，但在稍後的階段（通常是在出貨元件之前）延遲實際的簽署。</span><span class="sxs-lookup"><span data-stu-id="1d004-108">You can use delayed or partial signing at build time to reserve space in the portable executable (PE) file for the strong name signature, but defer the actual signing until some later stage, usually just before shipping the assembly.</span></span>

<span data-ttu-id="1d004-109">若要延遲簽署元件：</span><span class="sxs-lookup"><span data-stu-id="1d004-109">To delay-sign an assembly:</span></span>

1. <span data-ttu-id="1d004-110">從將執行最終簽署的組織取得金鑰組的公開金鑰部分。</span><span class="sxs-lookup"><span data-stu-id="1d004-110">Get the public key portion of the key pair from the organization that will do the eventual signing.</span></span> <span data-ttu-id="1d004-111">通常此金鑰的格式為 .snk 檔案，可以使用 Windows SDK 所提供的[強式名稱工具（sn.exe）](../../framework/tools/sn-exe-strong-name-tool.md)來建立 *。*</span><span class="sxs-lookup"><span data-stu-id="1d004-111">Typically this key is in the form of an *.snk* file, which can be created using the [Strong Name tool (Sn.exe)](../../framework/tools/sn-exe-strong-name-tool.md) provided by the Windows SDK.</span></span>

2. <span data-ttu-id="1d004-112">使用來自 <xref:System.Reflection> 的兩個自訂屬性為組件的原始碼加上註解：</span><span class="sxs-lookup"><span data-stu-id="1d004-112">Annotate the source code for the assembly with two custom attributes from <xref:System.Reflection>:</span></span>

   - <span data-ttu-id="1d004-113"><xref:System.Reflection.AssemblyKeyFileAttribute>，它會將傳遞包含公開金鑰的檔案名稱，作為其建構函式的參數。</span><span class="sxs-lookup"><span data-stu-id="1d004-113"><xref:System.Reflection.AssemblyKeyFileAttribute>, which passes the name of the file containing the public key as a parameter to its constructor.</span></span>

   - <span data-ttu-id="1d004-114"><xref:System.Reflection.AssemblyDelaySignAttribute>，表示藉由將**true**當做參數傳遞至其函式，來使用延遲簽署。</span><span class="sxs-lookup"><span data-stu-id="1d004-114"><xref:System.Reflection.AssemblyDelaySignAttribute>, which indicates that delay signing is being used by passing **true** as a parameter to its constructor.</span></span>

   <span data-ttu-id="1d004-115">例如：</span><span class="sxs-lookup"><span data-stu-id="1d004-115">For example:</span></span>

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

3. <span data-ttu-id="1d004-116">編譯器會將公開金鑰插入到組件資訊清單，並在 PE 檔中保留完整強式名稱簽章的空間。</span><span class="sxs-lookup"><span data-stu-id="1d004-116">The compiler inserts the public key into the assembly manifest and reserves space in the PE file for the full strong name signature.</span></span> <span data-ttu-id="1d004-117">在建置組件時必須儲存真正的公開金鑰，以便參考這個組件的其他組件可以取得金鑰，儲存在它們自己的組件參考。</span><span class="sxs-lookup"><span data-stu-id="1d004-117">The real public key must be stored while the assembly is built so that other assemblies that reference this assembly can obtain the key to store in their own assembly reference.</span></span>

4. <span data-ttu-id="1d004-118">因為組件沒有有效的強式名稱簽章，所以該簽章的驗證作業必須關閉。</span><span class="sxs-lookup"><span data-stu-id="1d004-118">Because the assembly does not have a valid strong name signature, the verification of that signature must be turned off.</span></span> <span data-ttu-id="1d004-119">您可以使用 **-Vr** 選項搭配強式名稱工具完成此作業。</span><span class="sxs-lookup"><span data-stu-id="1d004-119">You can do this by using the **–Vr** option with the Strong Name tool.</span></span>

     <span data-ttu-id="1d004-120">下列範例會關閉名為*myAssembly*之元件的驗證。</span><span class="sxs-lookup"><span data-stu-id="1d004-120">The following example turns off verification for an assembly called *myAssembly.dll*.</span></span>

   ```console
   sn –Vr myAssembly.dll
   ```

   <span data-ttu-id="1d004-121">若要在您無法在執行強式名稱工具的平台上關閉驗證，例如 Advanced RISC Machine (ARM) 微處理器，請使用 **– Vk** 選項來建立登錄檔。</span><span class="sxs-lookup"><span data-stu-id="1d004-121">To turn off verification on platforms where you can’t run the Strong Name tool, such as Advanced RISC Machine (ARM) microprocessors, use the **–Vk** option to create a registry file.</span></span> <span data-ttu-id="1d004-122">將登錄檔匯入到您要關閉驗證的電腦上的登錄。</span><span class="sxs-lookup"><span data-stu-id="1d004-122">Import the registry file into the registry on the computer where you want to turn off verification.</span></span> <span data-ttu-id="1d004-123">下列範例將建立 `myAssembly.dll` 的登錄檔。</span><span class="sxs-lookup"><span data-stu-id="1d004-123">The following example creates a registry file for `myAssembly.dll`.</span></span>

   ```console
   sn –Vk myRegFile.reg myAssembly.dll
   ```

   <span data-ttu-id="1d004-124">使用 **-Vr**或 **– Vk**選項時，您可以選擇性地包含用於測試金鑰簽署的 *.snk*檔案。</span><span class="sxs-lookup"><span data-stu-id="1d004-124">With either the **–Vr** or **–Vk** option, you can optionally include an *.snk* file for test key signing.</span></span>

   > [!WARNING]
   > <span data-ttu-id="1d004-125">請勿依賴強式名稱提供安全性。</span><span class="sxs-lookup"><span data-stu-id="1d004-125">Do not rely on strong names for security.</span></span> <span data-ttu-id="1d004-126">強式名稱僅提供唯一識別。</span><span class="sxs-lookup"><span data-stu-id="1d004-126">They provide a unique identity only.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1d004-127">如果您在 64 位元電腦上，使用 Visual Studio 進行開發期間使用延遲簽署，並且編譯**任何 CPU** 的組件，您可能要套用 **-Vr** 選項兩次。</span><span class="sxs-lookup"><span data-stu-id="1d004-127">If you use delay signing during development with Visual Studio on a 64-bit computer, and you compile an assembly for **Any CPU**, you might have to apply the **-Vr** option twice.</span></span> <span data-ttu-id="1d004-128">（在 Visual Studio 中，**任何 CPU**都是 [**平臺目標**組建] 屬性的值。當您從命令列進行編譯時，它是預設值）。若要從命令列或從 [檔案管理器] 執行應用程式，請使用64位版本的[sn.exe （強式名稱工具）](../../framework/tools/sn-exe-strong-name-tool.md) ，將 **-Vr**選項套用至元件。</span><span class="sxs-lookup"><span data-stu-id="1d004-128">(In Visual Studio, **Any CPU** is a value of the **Platform Target** build property; when you compile from the command line, it is the default.) To run your application from the command line or from File Explorer, use the 64-bit version of the [Sn.exe (Strong Name tool)](../../framework/tools/sn-exe-strong-name-tool.md) to apply the **-Vr** option to the assembly.</span></span> <span data-ttu-id="1d004-129">若要在設計階段將組件載入到 Visual Studio (例如，如果組件包含您應用程式中其他組件使用的元件)，請使用 32 位元版本的強式名稱工具。</span><span class="sxs-lookup"><span data-stu-id="1d004-129">To load the assembly into Visual Studio at design time (for example, if the assembly contains components that are used by other assemblies in your application), use the 32-bit version of the strong-name tool.</span></span> <span data-ttu-id="1d004-130">這是因為當組件是從命令列執行時，just-in-time (JIT) 編譯器會將組件編譯為 64 位元原生程式碼，而當載入到設計階段環境時，編譯為 32 位元原生程式碼。</span><span class="sxs-lookup"><span data-stu-id="1d004-130">This is because the just-in-time (JIT) compiler compiles the assembly to 64-bit native code when the assembly is run from the command line, and to 32-bit native code when the assembly is loaded into the design-time environment.</span></span>

5. <span data-ttu-id="1d004-131">稍後，通常就在傳送之前，您會將組件送出給貴組織的簽署授權單位，以便使用強式名稱工具的 **–R** 選項進行實際的強式名稱簽署。</span><span class="sxs-lookup"><span data-stu-id="1d004-131">Later, usually just before shipping, you submit the assembly to your organization's signing authority for the actual strong name signing using the **–R** option with the Strong Name tool.</span></span>

   <span data-ttu-id="1d004-132">下列範例會使用*sgKey*金鑰組，以強式名稱簽署名為*myAssembly*的元件。</span><span class="sxs-lookup"><span data-stu-id="1d004-132">The following example signs an assembly called *myAssembly.dll* with a strong name using the *sgKey.snk* key pair.</span></span>

   ```console
   sn -R myAssembly.dll sgKey.snk
   ```

## <a name="see-also"></a><span data-ttu-id="1d004-133">請參閱</span><span class="sxs-lookup"><span data-stu-id="1d004-133">See also</span></span>

- [<span data-ttu-id="1d004-134">建立組件</span><span class="sxs-lookup"><span data-stu-id="1d004-134">Create assemblies</span></span>](create.md)
- [<span data-ttu-id="1d004-135">如何：建立公開/私密金鑰組</span><span class="sxs-lookup"><span data-stu-id="1d004-135">How to: Create a public-private key pair</span></span>](create-public-private-key-pair.md)
- [<span data-ttu-id="1d004-136">Sn.exe （強式名稱工具）</span><span class="sxs-lookup"><span data-stu-id="1d004-136">Sn.exe (Strong Name tool)</span></span>](../../framework/tools/sn-exe-strong-name-tool.md)
