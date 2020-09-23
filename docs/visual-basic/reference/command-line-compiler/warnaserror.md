---
title: -warnaserror
ms.date: 03/13/2018
helpviewer_keywords:
- warnaserror compiler option [Visual Basic]
- /warnaserror compiler option [Visual Basic]
- -warnaserror compiler option [Visual Basic]
ms.assetid: 49819f1d-a1bd-4201-affe-5afe6d9712e1
ms.openlocfilehash: 2c243b05b7e819691165ef20996691c0bd38ae4a
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/23/2020
ms.locfileid: "91098861"
---
# <a name="-warnaserror-visual-basic"></a><span data-ttu-id="262c3-102">-warnaserror (Visual Basic) </span><span class="sxs-lookup"><span data-stu-id="262c3-102">-warnaserror (Visual Basic)</span></span>

<span data-ttu-id="262c3-103">導致編譯器將第一次出現的警告視為錯誤。</span><span class="sxs-lookup"><span data-stu-id="262c3-103">Causes the compiler to treat the first occurrence of a warning as an error.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="262c3-104">語法</span><span class="sxs-lookup"><span data-stu-id="262c3-104">Syntax</span></span>  
  
```console  
-warnaserror[+ | -][:numberList]  
```  
  
## <a name="arguments"></a><span data-ttu-id="262c3-105">引數</span><span class="sxs-lookup"><span data-stu-id="262c3-105">Arguments</span></span>  
  
|<span data-ttu-id="262c3-106">詞彙</span><span class="sxs-lookup"><span data-stu-id="262c3-106">Term</span></span>|<span data-ttu-id="262c3-107">定義</span><span class="sxs-lookup"><span data-stu-id="262c3-107">Definition</span></span>|  
|---|---|  
|<span data-ttu-id="262c3-108">+ &#124;-</span><span class="sxs-lookup"><span data-stu-id="262c3-108">+ &#124; -</span></span>|<span data-ttu-id="262c3-109">選擇性。</span><span class="sxs-lookup"><span data-stu-id="262c3-109">Optional.</span></span> <span data-ttu-id="262c3-110">依預設， `-warnaserror-` 會生效; 警告不會防止編譯器產生輸出檔。</span><span class="sxs-lookup"><span data-stu-id="262c3-110">By default, `-warnaserror-` is in effect; warnings do not prevent the compiler from producing an output file.</span></span> <span data-ttu-id="262c3-111">`-warnaserror`選項（與相同 `-warnaserror+` ）會導致將警告視為錯誤。</span><span class="sxs-lookup"><span data-stu-id="262c3-111">The `-warnaserror` option, which is the same as `-warnaserror+`, causes warnings to be treated as errors.</span></span>|  
|`numberList`|<span data-ttu-id="262c3-112">選擇性。</span><span class="sxs-lookup"><span data-stu-id="262c3-112">Optional.</span></span> <span data-ttu-id="262c3-113">選項套用之警告識別碼編號的逗號分隔清單 `-warnaserror` 。</span><span class="sxs-lookup"><span data-stu-id="262c3-113">Comma-delimited list of the warning ID numbers to which the `-warnaserror` option applies.</span></span> <span data-ttu-id="262c3-114">如果未指定警告識別碼，選項會 `-warnaserror` 套用至所有警告。</span><span class="sxs-lookup"><span data-stu-id="262c3-114">If no warning ID is specified, the `-warnaserror` option applies to all warnings.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="262c3-115">備註</span><span class="sxs-lookup"><span data-stu-id="262c3-115">Remarks</span></span>  

 <span data-ttu-id="262c3-116">選項會將 `-warnaserror` 所有警告視為錯誤。</span><span class="sxs-lookup"><span data-stu-id="262c3-116">The `-warnaserror` option treats all warnings as errors.</span></span> <span data-ttu-id="262c3-117">通常會回報為警告的任何訊息都會回報為錯誤。</span><span class="sxs-lookup"><span data-stu-id="262c3-117">Any messages that would ordinarily be reported as warnings are instead reported as errors.</span></span> <span data-ttu-id="262c3-118">編譯器會將後續出現的警告報告為警告。</span><span class="sxs-lookup"><span data-stu-id="262c3-118">The compiler reports subsequent occurrences of the same warning as warnings.</span></span>  
  
 <span data-ttu-id="262c3-119">依預設， `-warnaserror-` 會生效，而導致警告僅供參考。</span><span class="sxs-lookup"><span data-stu-id="262c3-119">By default, `-warnaserror-` is in effect, which causes the warnings to be informational only.</span></span> <span data-ttu-id="262c3-120">`-warnaserror`選項（與相同 `-warnaserror+` ）會導致將警告視為錯誤。</span><span class="sxs-lookup"><span data-stu-id="262c3-120">The `-warnaserror` option, which is the same as `-warnaserror+`, causes warnings to be treated as errors.</span></span>  
  
 <span data-ttu-id="262c3-121">如果您只想要將一些特定警告視為錯誤，您可以指定以逗號分隔的警告編號清單來視為錯誤。</span><span class="sxs-lookup"><span data-stu-id="262c3-121">If you want only a few specific warnings to be treated as errors, you may specify a comma-separated list of warning numbers to treat as errors.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="262c3-122">`-warnaserror`選項不會控制警告的顯示方式。</span><span class="sxs-lookup"><span data-stu-id="262c3-122">The `-warnaserror` option does not control how warnings are displayed.</span></span> <span data-ttu-id="262c3-123">使用 [-nowarn](nowarn.md) 選項來停用警告。</span><span class="sxs-lookup"><span data-stu-id="262c3-123">Use the [-nowarn](nowarn.md) option to disable warnings.</span></span>  
  
|<span data-ttu-id="262c3-124">設定-warnaserror 會將所有警告視為 Visual Studio IDE 中的錯誤</span><span class="sxs-lookup"><span data-stu-id="262c3-124">To set -warnaserror to treat all warnings as errors in the Visual Studio IDE</span></span>|  
|---|  
|<span data-ttu-id="262c3-125">1. 在 **方案總管**中選取專案。</span><span class="sxs-lookup"><span data-stu-id="262c3-125">1.  Have a project selected in **Solution Explorer**.</span></span> <span data-ttu-id="262c3-126">按一下 [專案] 功能表上的 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="262c3-126">On the **Project** menu, click **Properties**.</span></span> <br /><span data-ttu-id="262c3-127">2. 按一下 [ **編譯** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="262c3-127">2.  Click the **Compile** tab.</span></span><br /><span data-ttu-id="262c3-128">3. 請確定未核取 [ **停用所有警告** ] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="262c3-128">3.  Make sure the **Disable all warnings** check box is unchecked.</span></span><br /><span data-ttu-id="262c3-129">4. 勾選 [將 **所有警告視為錯誤** ] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="262c3-129">4.  Check the **Treat all warnings as errors** check box.</span></span>|  
  
|<span data-ttu-id="262c3-130">Warnaserror 可將特定警告視為 Visual Studio IDE 中的錯誤</span><span class="sxs-lookup"><span data-stu-id="262c3-130">To set -warnaserror to treat specific warnings as errors in the Visual Studio IDE</span></span>|  
|---|  
|<span data-ttu-id="262c3-131">1. 在 **方案總管**中選取專案。</span><span class="sxs-lookup"><span data-stu-id="262c3-131">1.  Have a project selected in **Solution Explorer**.</span></span> <span data-ttu-id="262c3-132">按一下 [專案] 功能表上的 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="262c3-132">On the **Project** menu, click **Properties**.</span></span><br /><span data-ttu-id="262c3-133">2. 按一下 [ **編譯** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="262c3-133">2.  Click the **Compile** tab.</span></span><br /><span data-ttu-id="262c3-134">3. 請確定未核取 [ **停用所有警告** ] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="262c3-134">3.  Make sure the **Disable all warnings** check box is unchecked.</span></span><br /><span data-ttu-id="262c3-135">4. 請確定未核取 [將 **所有警告視為錯誤** ] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="262c3-135">4.  Make sure the **Treat all warnings as errors** check box is unchecked.</span></span><br /><span data-ttu-id="262c3-136">5. 從應視為錯誤的警告旁的**通知**資料行中選取 [**錯誤**]。</span><span class="sxs-lookup"><span data-stu-id="262c3-136">5.  Select **Error** from the **Notification** column adjacent to the warning that should be treated as an error.</span></span>|  
  
## <a name="example"></a><span data-ttu-id="262c3-137">範例</span><span class="sxs-lookup"><span data-stu-id="262c3-137">Example</span></span>  

 <span data-ttu-id="262c3-138">下列程式碼 `In.vb` 會編譯並指示編譯器在第一次出現所找到的每個警告時顯示錯誤。</span><span class="sxs-lookup"><span data-stu-id="262c3-138">The following code compiles `In.vb` and directs the compiler to display an error for the first occurrence of every warning it finds.</span></span>  
  
```console
vbc -warnaserror in.vb  
```  
  
## <a name="example"></a><span data-ttu-id="262c3-139">範例</span><span class="sxs-lookup"><span data-stu-id="262c3-139">Example</span></span>  

 <span data-ttu-id="262c3-140">下列 `T2.vb` 程式碼只會針對未使用的區域變數（ (42024) 視為錯誤）編譯和處理警告。</span><span class="sxs-lookup"><span data-stu-id="262c3-140">The following code compiles `T2.vb` and treats only the warning for unused local variables (42024) as an error.</span></span>  
  
```console
vbc -warnaserror:42024 t2.vb  
```  
  
## <a name="see-also"></a><span data-ttu-id="262c3-141">另請參閱</span><span class="sxs-lookup"><span data-stu-id="262c3-141">See also</span></span>

- [<span data-ttu-id="262c3-142">Visual Basic 命令列編譯器</span><span class="sxs-lookup"><span data-stu-id="262c3-142">Visual Basic Command-Line Compiler</span></span>](index.md)
- [<span data-ttu-id="262c3-143">編譯命令列的範例</span><span class="sxs-lookup"><span data-stu-id="262c3-143">Sample Compilation Command Lines</span></span>](sample-compilation-command-lines.md)
- [<span data-ttu-id="262c3-144">Configuring Warnings in Visual Basic</span><span class="sxs-lookup"><span data-stu-id="262c3-144">Configuring Warnings in Visual Basic</span></span>](/visualstudio/ide/configuring-warnings-in-visual-basic)
