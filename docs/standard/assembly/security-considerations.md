---
title: 組件安全性考量
description: 當您建立 .NET 元件時，您可以指定元件執行所需的許可權。 本文討論強式名稱的元件和簽署工具。
ms.date: 08/20/2019
helpviewer_keywords:
- assemblies [.NET Framework], security
- signcodes
- names [.NET Framework], assemblies
- strong-named assemblies, security considerations
- signing assemblies
- assemblies [.NET Framework], signing
- granting permissions, assemblies
- assemblies [.NET Framework], strong-named
- names [.NET Framework], strong names
- permissions [.NET Framework], assemblies
- security [.NET Framework], assemblies
- integrity with assemblies
ms.assetid: 1b5439c1-f3d5-4529-bd69-01814703d067
ms.openlocfilehash: 7f897241b121cf1bd52d02ee5f487aeafafc3cb0
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/13/2020
ms.locfileid: "83378664"
---
# <a name="assembly-security-considerations"></a><span data-ttu-id="a936f-104">組件安全性考量</span><span class="sxs-lookup"><span data-stu-id="a936f-104">Assembly security considerations</span></span>
<span data-ttu-id="a936f-105">當您建置組件時，您可以指定一組該組件需要用來執行的使用權限。</span><span class="sxs-lookup"><span data-stu-id="a936f-105">When you build an assembly, you can specify a set of permissions that the assembly requires to run.</span></span> <span data-ttu-id="a936f-106">是否將某些使用權限授予組件則以辨識項 (Evidence) 為基礎。</span><span class="sxs-lookup"><span data-stu-id="a936f-106">Whether certain permissions are granted or not granted to an assembly is based on evidence.</span></span>  
  
 <span data-ttu-id="a936f-107">使用辨識項有兩種不同的方法：</span><span class="sxs-lookup"><span data-stu-id="a936f-107">There are two distinct ways evidence is used:</span></span>  
  
- <span data-ttu-id="a936f-108">輸入辨識項會和載入器所集合的辨識項合併，以建立用於原則解析的最終辨識項組。</span><span class="sxs-lookup"><span data-stu-id="a936f-108">The input evidence is merged with the evidence gathered by the loader to create a final set of evidence used for policy resolution.</span></span> <span data-ttu-id="a936f-109">使用這個語意的方法包括 **Assembly.Load**、**Assembly.LoadFrom** 和 **Activator.CreateInstance**。</span><span class="sxs-lookup"><span data-stu-id="a936f-109">The methods that use this semantic include **Assembly.Load**, **Assembly.LoadFrom**, and **Activator.CreateInstance**.</span></span>  
  
- <span data-ttu-id="a936f-110">輸入辨識項使用時不會更改，就和用於原則解析的最終辨識項組一樣。</span><span class="sxs-lookup"><span data-stu-id="a936f-110">The input evidence is used unaltered as the final set of evidence used for policy resolution.</span></span> <span data-ttu-id="a936f-111">使用這個語意的方法包括 **Assembly.Load(byte[])** 和 **AppDomain.DefineDynamicAssembly()**。</span><span class="sxs-lookup"><span data-stu-id="a936f-111">The methods that use this semantic include **Assembly.Load(byte[])** and **AppDomain.DefineDynamicAssembly()**.</span></span>  
  
  <span data-ttu-id="a936f-112">選擇性的使用權限可以藉由該組件要在其上執行之電腦上所設定的[安全性原則](../../framework/misc/code-access-security-basics.md)來授與。</span><span class="sxs-lookup"><span data-stu-id="a936f-112">Optional permissions can be granted by the [security policy](../../framework/misc/code-access-security-basics.md) set on the computer where the assembly will run.</span></span> <span data-ttu-id="a936f-113">如果您希望程式碼處理所有可能的安全性例外狀況，您可以執行下列某一項動作：</span><span class="sxs-lookup"><span data-stu-id="a936f-113">If you want your code to handle all potential security exceptions, you can do one of the following:</span></span>  
  
- <span data-ttu-id="a936f-114">插入您程式碼必須擁有之所有使用權限的使用權限要求，並且處理萬一使用權限未獲授予時，發生在最前面位置的載入期間失敗。</span><span class="sxs-lookup"><span data-stu-id="a936f-114">Insert a permission request for all the permissions your code must have, and handle up front the load-time failure that occurs if the permissions are not granted.</span></span>  
  
- <span data-ttu-id="a936f-115">不要利用使用權限要求來取得程式碼可能需要的使用權限，但是要準備處理萬一使用權限未獲授予時的安全性例外狀況。</span><span class="sxs-lookup"><span data-stu-id="a936f-115">Do not use a permission request to obtain permissions your code might need, but be prepared to handle security exceptions if permissions are not granted.</span></span>  
  
  > [!NOTE]
  > <span data-ttu-id="a936f-116">安全性是個複雜的領域，有許多的選項可以供您選擇。</span><span class="sxs-lookup"><span data-stu-id="a936f-116">Security is a complex area, and you have many options to choose from.</span></span> <span data-ttu-id="a936f-117">如需詳細資訊，請參閱[重要的安全性概念](../../standard/security/key-security-concepts.md)。</span><span class="sxs-lookup"><span data-stu-id="a936f-117">For more information, see [Key Security Concepts](../../standard/security/key-security-concepts.md).</span></span>  
  
 <span data-ttu-id="a936f-118">在載入期間，組件的辨識項 (Evidence) 是用來做為安全性原則的輸入。</span><span class="sxs-lookup"><span data-stu-id="a936f-118">At load time, the assembly's evidence is used as input to security policy.</span></span> <span data-ttu-id="a936f-119">安全性原則是由企業和電腦的系統管理員以及使用者原則設定所建立的，它決定在執行時授予所有 Managed 程式碼的使用權限集。</span><span class="sxs-lookup"><span data-stu-id="a936f-119">Security policy is established by the enterprise and the computer's administrator as well as by user policy settings, and determines the set of permissions that is granted to all managed code when executed.</span></span> <span data-ttu-id="a936f-120">安全性原則可以針對組件 (如果具有簽署工具產生的簽章) 的發行者、針對要從其中下載組件的 Web 網站和區域 (Internet Explorer 的用詞)，或針對組件的強式名稱 (Strong Name) 建立。</span><span class="sxs-lookup"><span data-stu-id="a936f-120">Security policy can be established for the publisher of the assembly (if it has a signing tool generated signature), for the Web site and zone (in Internet Explorer terms) the assembly was downloaded from, or for the assembly's strong name.</span></span> <span data-ttu-id="a936f-121">例如，電腦的系統管理員可以建立安全性原則，允許從某一 Web 網站下載並且由特定軟體公司簽名的所有程式碼存取電腦上的某個資料庫，但是不授予寫入該電腦磁碟的存取權。</span><span class="sxs-lookup"><span data-stu-id="a936f-121">For example, a computer's administrator can establish security policy that allows all code downloaded from a Web site and signed by a given software company to access a database on a computer, but does not grant access to write to the computer's disk.</span></span>  
  
## <a name="strong-named-assemblies-and-signing-tools"></a><span data-ttu-id="a936f-122">強式名稱的元件和簽署工具</span><span class="sxs-lookup"><span data-stu-id="a936f-122">Strong-named assemblies and signing tools</span></span>  

 > [!WARNING]
 > <span data-ttu-id="a936f-123">請勿依賴強式名稱提供安全性。</span><span class="sxs-lookup"><span data-stu-id="a936f-123">Do not rely on strong names for security.</span></span> <span data-ttu-id="a936f-124">強式名稱僅提供唯一識別。</span><span class="sxs-lookup"><span data-stu-id="a936f-124">They provide a unique identity only.</span></span>

 <span data-ttu-id="a936f-125">您可以用兩種不同但互補的方式來簽署組件：運用強式名稱，或是使用 [SignTool.exe (簽署工具)](../../framework/tools/signtool-exe.md)。</span><span class="sxs-lookup"><span data-stu-id="a936f-125">You can sign an assembly in two different but complementary ways: with a strong name or by using  [SignTool.exe (Sign Tool)](../../framework/tools/signtool-exe.md).</span></span> <span data-ttu-id="a936f-126">使用強式名稱簽署組件，就會將公開金鑰加密新增至含有組件資訊清單的檔案。</span><span class="sxs-lookup"><span data-stu-id="a936f-126">Signing an assembly with a strong name adds public key encryption to the file containing the assembly manifest.</span></span> <span data-ttu-id="a936f-127">強式名稱簽署可協助驗證唯一名稱，防止冒用名稱，並且在解析參考時為呼叫端提供某種識別 (Identity)。</span><span class="sxs-lookup"><span data-stu-id="a936f-127">Strong name signing helps to verify name uniqueness, prevent name spoofing, and provide callers with some identity when a reference is resolved.</span></span>  
  
 <span data-ttu-id="a936f-128">並沒有任何信任層級與強式名稱建立關聯，這也使得 [SignTool.exe (簽署工具)](../../framework/tools/signtool-exe.md) 更為重要。</span><span class="sxs-lookup"><span data-stu-id="a936f-128">No level of trust is associated with a strong name, which makes [SignTool.exe (Sign Tool)](../../framework/tools/signtool-exe.md) important.</span></span> <span data-ttu-id="a936f-129">這兩種簽署工具需要發行者向協力廠商授權單位證明其識別並取得憑證。</span><span class="sxs-lookup"><span data-stu-id="a936f-129">The two signing tools require a publisher to prove its identity to a third-party authority and obtain a certificate.</span></span> <span data-ttu-id="a936f-130">然後將這項憑證嵌入您的檔案，就可以讓系統管理員用來決定是否要信任程式碼的真實性。</span><span class="sxs-lookup"><span data-stu-id="a936f-130">This certificate is then embedded in your file and can be used by an administrator to decide whether to trust the code's authenticity.</span></span>  
  
 <span data-ttu-id="a936f-131">您可以同時對組件賦予強式名稱和使用 [SignTool.exe (簽署工具)](../../framework/tools/signtool-exe.md) 建立的數位簽章，或是只使用其中一種。</span><span class="sxs-lookup"><span data-stu-id="a936f-131">You can give both a strong name and a digital signature created using [SignTool.exe (Sign Tool)](../../framework/tools/signtool-exe.md) to an assembly, or you can use either alone.</span></span> <span data-ttu-id="a936f-132">這兩種簽署工具只能同時簽署一個檔案。對於多檔案組件，您必須簽署含有組件資訊清單的檔案。</span><span class="sxs-lookup"><span data-stu-id="a936f-132">The two signing tools can sign only one file at a time; for a multifile assembly, you sign the file that contains the assembly manifest.</span></span> <span data-ttu-id="a936f-133">強式名稱儲存在包含組件資訊清單的檔案中，但是使用 [SignTool.exe (簽署工具)](../../framework/tools/signtool-exe.md) 建立的簽章，則是儲存在包含組件資訊清單的可攜式執行檔 (PE) 中的保留位置。</span><span class="sxs-lookup"><span data-stu-id="a936f-133">A strong name is stored in the file containing the assembly manifest, but a signature created using [SignTool.exe (Sign Tool)](../../framework/tools/signtool-exe.md) is stored in a reserved slot in the portable executable (PE) file containing the assembly manifest.</span></span> <span data-ttu-id="a936f-134">當您已經擁有依靠 [SignTool.exe (簽署工具)](../../framework/tools/signtool-exe.md) 所產生簽章的信任階層，或您的原則只使用金鑰部分而不檢查信任鏈結，即可使用 [SignTool.exe (簽署工具)](../../framework/tools/signtool-exe.md) 來簽署組件 (不論是否使用強式名稱)。</span><span class="sxs-lookup"><span data-stu-id="a936f-134">Signing of an assembly using [SignTool.exe (Sign Tool)](../../framework/tools/signtool-exe.md) can be used (with or without a strong name) when you already have a trust hierarchy that relies on [SignTool.exe (Sign Tool)](../../framework/tools/signtool-exe.md) generated signatures, or when your policy uses only the key portion and does not check a chain of trust.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="a936f-135">在組件上同時使用強式名稱和簽署工具簽章時，必須先指定強式名稱。</span><span class="sxs-lookup"><span data-stu-id="a936f-135">When using both a strong name and a signing tool signature on an assembly, the strong name must be assigned first.</span></span>  
  
 <span data-ttu-id="a936f-136">Common Language Runtime 也會執行雜湊驗證；組件資訊清單包含構成組件的所有檔案清單，包括建置資訊清單時所在的每一個檔案的雜湊。</span><span class="sxs-lookup"><span data-stu-id="a936f-136">The common language runtime also performs a hash verification; the assembly manifest contains a list of all files that make up the assembly, including a hash of each file as it existed when the manifest was built.</span></span> <span data-ttu-id="a936f-137">載入每一個檔案時，它的內容會被雜湊並且與資訊清單中儲存的雜湊值進行比對。</span><span class="sxs-lookup"><span data-stu-id="a936f-137">As each file is loaded, its contents are hashed and compared with the hash value stored in the manifest.</span></span> <span data-ttu-id="a936f-138">如果兩個雜湊不相符，就無法載入組件。</span><span class="sxs-lookup"><span data-stu-id="a936f-138">If the two hashes do not match, the assembly fails to load.</span></span>  
  
 <span data-ttu-id="a936f-139">由於強式命名和使用 [SignTool.exe (簽署工具)](../../framework/tools/signtool-exe.md) 的簽署可保證完整性，所以您可以讓程式碼存取安全性原則以這兩種形式的組件辨識項作為基礎。</span><span class="sxs-lookup"><span data-stu-id="a936f-139">Because strong naming and signing using [SignTool.exe (Sign Tool)](../../framework/tools/signtool-exe.md) guarantee integrity, you can base code access security policy on these two forms of assembly evidence.</span></span> <span data-ttu-id="a936f-140">強式命名和使用 [SignTool.exe (簽署工具)](../../framework/tools/signtool-exe.md) 的簽署，可以透過數位簽章和憑證來保證完整性。</span><span class="sxs-lookup"><span data-stu-id="a936f-140">Strong naming and signing using [SignTool.exe (Sign Tool)](../../framework/tools/signtool-exe.md) guarantee integrity through digital signatures and certificates.</span></span> <span data-ttu-id="a936f-141">所有前述技術 (雜湊驗證、強式命名和使用 [SignTool.exe (簽署工具)](../../framework/tools/signtool-exe.md) 的簽署)，合在一起即可確保組件沒有以任何方式改變。</span><span class="sxs-lookup"><span data-stu-id="a936f-141">All the technologies mentioned—hash verification, strong naming, and signing using [SignTool.exe (Sign Tool)](../../framework/tools/signtool-exe.md)—work together to ensure that the assembly has not been altered in any way.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="a936f-142">請參閱</span><span class="sxs-lookup"><span data-stu-id="a936f-142">See also</span></span>

- [<span data-ttu-id="a936f-143">強式名稱組件</span><span class="sxs-lookup"><span data-stu-id="a936f-143">Strong-named assemblies</span></span>](strong-named.md)
- [<span data-ttu-id="a936f-144">.NET 中的組件</span><span class="sxs-lookup"><span data-stu-id="a936f-144">Assemblies in .NET</span></span>](index.md)
- [<span data-ttu-id="a936f-145">SignTool .exe （簽署工具）</span><span class="sxs-lookup"><span data-stu-id="a936f-145">SignTool.exe (Sign Tool)</span></span>](../../framework/tools/signtool-exe.md)
