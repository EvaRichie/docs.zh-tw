---
title: 建立並存執行元件的方針
description: 檢查建立並存執行元件的指導方針。 例如，將類型識別系結至特定的檔案版本，或使用版本感知的儲存體。
ms.date: 03/30/2017
helpviewer_keywords:
- side-by-side execution, multiple application versions
- side-by-side execution, multiple component versions
ms.assetid: 5c540161-6e40-42e9-be92-6175aee2c46a
ms.openlocfilehash: 3ac7c514a69ae05b00e7a486aadcbf41e5d1cbd6
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96262511"
---
# <a name="guidelines-for-creating-components-for-side-by-side-execution"></a><span data-ttu-id="16882-104">建立並存執行元件的方針</span><span class="sxs-lookup"><span data-stu-id="16882-104">Guidelines for Creating Components for Side-by-Side Execution</span></span>

<span data-ttu-id="16882-105">請遵循這些一般方針建立為並存執行而設計的 Managed 應用程式或元件：</span><span class="sxs-lookup"><span data-stu-id="16882-105">Follow these general guidelines to create managed applications or components designed for side-by-side execution:</span></span>  
  
- <span data-ttu-id="16882-106">將類型識別繫結至特定版本的檔案。</span><span class="sxs-lookup"><span data-stu-id="16882-106">Bind type identity to a particular version of a file.</span></span>  
  
     <span data-ttu-id="16882-107">Common Language Runtime 會使用強式名稱的組件，將類型識別繫結到特定的檔案版本。</span><span class="sxs-lookup"><span data-stu-id="16882-107">The common language runtime binds type identity to a particular file version by using strong-named assemblies.</span></span> <span data-ttu-id="16882-108">若要建立用於並存執行的應用程式或元件，您必須為所有組件指定強式名稱。</span><span class="sxs-lookup"><span data-stu-id="16882-108">To create an application or component for side-by-side execution, you must give all assemblies a strong name.</span></span> <span data-ttu-id="16882-109">這會建立精確的類型識別，並確保將任何的類型解析導向到正確的檔案。</span><span class="sxs-lookup"><span data-stu-id="16882-109">This creates precise type identity and ensures that any type resolution is directed to the correct file.</span></span> <span data-ttu-id="16882-110">強式名稱的組件包含版本、文化特性和發行者資訊，可供執行階段找出符合繫結要求的正確檔案。</span><span class="sxs-lookup"><span data-stu-id="16882-110">A strong-named assembly contains version, culture, and publisher information that the runtime uses to locate the correct file to fulfill a binding request.</span></span>  
  
- <span data-ttu-id="16882-111">使用版本感知儲存區。</span><span class="sxs-lookup"><span data-stu-id="16882-111">Use version-aware storage.</span></span>  
  
     <span data-ttu-id="16882-112">此執行階段使用全域組件快取提供版本感知儲存區。</span><span class="sxs-lookup"><span data-stu-id="16882-112">The runtime uses the global assembly cache to provide version-aware storage.</span></span> <span data-ttu-id="16882-113">全域組件快取是一種版本感知目錄結構，安裝在使用 .NET Framework 的每一台電腦上。</span><span class="sxs-lookup"><span data-stu-id="16882-113">The global assembly cache is a version-aware directory structure installed on every computer that uses the .NET Framework.</span></span> <span data-ttu-id="16882-114">安裝在全域組件快取的組件不會在安裝該組件新版本時被覆寫。</span><span class="sxs-lookup"><span data-stu-id="16882-114">Assemblies installed in the global assembly cache are not overwritten when a new version of that assembly is installed.</span></span>  
  
- <span data-ttu-id="16882-115">建立在隔離狀態執行的應用程式或元件。</span><span class="sxs-lookup"><span data-stu-id="16882-115">Create an application or component that runs in isolation.</span></span>  
  
     <span data-ttu-id="16882-116">在隔離狀態執行的應用程式或元件必須管理資源，以避免該應用程式或元件的兩個執行個體同時執行時產生衝突。</span><span class="sxs-lookup"><span data-stu-id="16882-116">An application or component that runs in isolation must manage resources to avoid conflicts when two instances of the application or component are running simultaneously.</span></span> <span data-ttu-id="16882-117">應用程式或元件也必須使用版本特定的檔案結構。</span><span class="sxs-lookup"><span data-stu-id="16882-117">The application or component must also use a version-specific file structure.</span></span>  
  
## <a name="application-and-component-isolation"></a><span data-ttu-id="16882-118">應用程式和元件隔離</span><span class="sxs-lookup"><span data-stu-id="16882-118">Application and Component Isolation</span></span>  

 <span data-ttu-id="16882-119">隔離是成功設計用於並存執行之應用程式或元件的其中一個關鍵。</span><span class="sxs-lookup"><span data-stu-id="16882-119">One key to successfully designing an application or component for side-by-side execution is isolation.</span></span> <span data-ttu-id="16882-120">應用程式或元件必須以隔離的方式管理所有資源，尤其是檔案 I/O。</span><span class="sxs-lookup"><span data-stu-id="16882-120">The application or component must manage all resources, particularly file I/O, in an isolated manner.</span></span> <span data-ttu-id="16882-121">請遵循這些方針，確定您的應用程式或元件在隔離狀態執行：</span><span class="sxs-lookup"><span data-stu-id="16882-121">Follow these guidelines to make sure your application or component runs in isolation:</span></span>  
  
- <span data-ttu-id="16882-122">以版本特定的方式寫入登錄。</span><span class="sxs-lookup"><span data-stu-id="16882-122">Write to the registry in a version-specific way.</span></span> <span data-ttu-id="16882-123">將值儲存在指出此版本的登錄區或機碼中，且不要在各種版本的元件之間共用資訊或狀態。</span><span class="sxs-lookup"><span data-stu-id="16882-123">Store values in hives or keys that indicate the version, and do not share information or state across versions of a component.</span></span> <span data-ttu-id="16882-124">這可防止同時執行的兩個應用程式或元件覆寫資訊。</span><span class="sxs-lookup"><span data-stu-id="16882-124">This prevents two applications or components running at the same time from overwriting information.</span></span>  
  
- <span data-ttu-id="16882-125">使具名的核心物件變成版本特定的物件，讓競爭情形不要發生。</span><span class="sxs-lookup"><span data-stu-id="16882-125">Make named kernel objects version-specific so that a race condition does not occur.</span></span> <span data-ttu-id="16882-126">例如，當相同應用程式之兩個版本的兩個信號互相等候時就會發生競爭情形。</span><span class="sxs-lookup"><span data-stu-id="16882-126">For example, a race condition occurs when two semaphores from two versions of the same application wait on each other.</span></span>  
  
- <span data-ttu-id="16882-127">將檔案和目錄名稱變成版本感知的名稱。</span><span class="sxs-lookup"><span data-stu-id="16882-127">Make file and directory names version-aware.</span></span> <span data-ttu-id="16882-128">這表示檔案結構應該要依賴版本資訊。</span><span class="sxs-lookup"><span data-stu-id="16882-128">This means that file structures should rely on version information.</span></span>  
  
- <span data-ttu-id="16882-129">使用版本特定的方式建立帳戶和群組。</span><span class="sxs-lookup"><span data-stu-id="16882-129">Create user accounts and groups in a version-specific manner.</span></span> <span data-ttu-id="16882-130">應用程式所建立的使用者帳戶和群組應該以版本識別。</span><span class="sxs-lookup"><span data-stu-id="16882-130">User accounts and groups created by an application should be identified by version.</span></span> <span data-ttu-id="16882-131">請勿在應用程式版本之間共用使用者帳戶和群組。</span><span class="sxs-lookup"><span data-stu-id="16882-131">Do not share user accounts and groups between versions of an application.</span></span>  
  
## <a name="installing-and-uninstalling-versions"></a><span data-ttu-id="16882-132">安裝和解除安裝版本</span><span class="sxs-lookup"><span data-stu-id="16882-132">Installing and Uninstalling Versions</span></span>  

 <span data-ttu-id="16882-133">設定用於並存執行的應用程式時，請遵循這些有關安裝及解除安裝版本的方針：</span><span class="sxs-lookup"><span data-stu-id="16882-133">When designing an application for side-by-side execution, follow these guidelines concerning installing and uninstalling versions:</span></span>  
  
- <span data-ttu-id="16882-134">請勿從登錄中刪除資訊；其他應用程式在不同版本的 .NET Framework 下執行時可能需要用到這些資訊。</span><span class="sxs-lookup"><span data-stu-id="16882-134">Do not delete information from the registry that may be needed by other applications running under a different version of the .NET Framework.</span></span>  
  
- <span data-ttu-id="16882-135">請勿取代登錄中的資訊；其他應用程式在不同版本的 .NET Framework 下執行時可能需要用到這些資訊。</span><span class="sxs-lookup"><span data-stu-id="16882-135">Do not replace information in the registry that may be needed by other applications running under a different version of the .NET Framework.</span></span>  
  
- <span data-ttu-id="16882-136">請勿移除註冊 COM 元件；其他應用程式在不同版本的 .NET Framework 下執行時可能需要用到這些資訊。</span><span class="sxs-lookup"><span data-stu-id="16882-136">Do not unregister COM components that may be needed by other applications running under a different version of the .NET Framework.</span></span>  
  
- <span data-ttu-id="16882-137">請勿變更 **InprocServer32** 或已登錄的 COM 伺服器的其他登錄項目。</span><span class="sxs-lookup"><span data-stu-id="16882-137">Do not change **InprocServer32** or other registry entries for a COM server that was already registered.</span></span>  
  
- <span data-ttu-id="16882-138">請勿刪除使用者帳戶或群組；其他應用程式在不同版本的 .NET Framework 下執行時可能需要用到這些資訊。</span><span class="sxs-lookup"><span data-stu-id="16882-138">Do not delete user accounts or groups that may be needed by other applications running under a different version of the .NET Framework.</span></span>  
  
- <span data-ttu-id="16882-139">請勿將任何項目加入包含未建立版本之路徑的登錄。</span><span class="sxs-lookup"><span data-stu-id="16882-139">Do not add anything to the registry that contains an unversioned path.</span></span>  
  
## <a name="file-version-number-and-assembly-version-number"></a><span data-ttu-id="16882-140">檔案版本號碼和組件版本號碼</span><span class="sxs-lookup"><span data-stu-id="16882-140">File Version Number and Assembly Version Number</span></span>  

 <span data-ttu-id="16882-141">檔案版本是執行階段不使用的 Win32 版本資源。</span><span class="sxs-lookup"><span data-stu-id="16882-141">File version is a Win32 version resource that is not used by the runtime.</span></span> <span data-ttu-id="16882-142">一般來說，您甚至可以就地更新檔案版本。</span><span class="sxs-lookup"><span data-stu-id="16882-142">In general, you update the file version even for an in-place update.</span></span> <span data-ttu-id="16882-143">兩個相同的檔案可以有不同的檔案版本資訊，而兩個不同的檔案也可以有相同的檔案版本資訊。</span><span class="sxs-lookup"><span data-stu-id="16882-143">Two identical files can have different file version information, and two different files can have the same file version information.</span></span>  
  
 <span data-ttu-id="16882-144">組件版本可供執行階段用於組件繫結。</span><span class="sxs-lookup"><span data-stu-id="16882-144">The assembly version is used by the runtime for assembly binding.</span></span> <span data-ttu-id="16882-145">執行階段會將兩個具有不同版本號碼的相同組件視為兩個不同的組件。</span><span class="sxs-lookup"><span data-stu-id="16882-145">Two identical assemblies with different version numbers are treated as two different assemblies by the runtime.</span></span>  
  
 <span data-ttu-id="16882-146">當只有檔案版本號碼是新的時，[全域組件快取工具 (Gacutil.exe)](../tools/gacutil-exe-gac-tool.md) 可讓您替換組件。</span><span class="sxs-lookup"><span data-stu-id="16882-146">The [Global Assembly Cache tool (Gacutil.exe)](../tools/gacutil-exe-gac-tool.md) allows you to replace an assembly when only the file version number is newer.</span></span> <span data-ttu-id="16882-147">除非組件版本號碼比較高，否則安裝程式通常不會在組件上執行覆寫安裝。</span><span class="sxs-lookup"><span data-stu-id="16882-147">The installer generally does not install over an assembly unless the assembly version number is greater.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="16882-148">另請參閱</span><span class="sxs-lookup"><span data-stu-id="16882-148">See also</span></span>

- [<span data-ttu-id="16882-149">並存執行</span><span class="sxs-lookup"><span data-stu-id="16882-149">Side-by-Side Execution</span></span>](side-by-side-execution.md)
- [<span data-ttu-id="16882-150">作法：啟用和停用自動繫結重新導向</span><span class="sxs-lookup"><span data-stu-id="16882-150">How to: Enable and Disable Automatic Binding Redirection</span></span>](../configure-apps/how-to-enable-and-disable-automatic-binding-redirection.md)
