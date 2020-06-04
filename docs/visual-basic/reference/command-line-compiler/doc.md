---
title: -doc
ms.date: 03/10/2018
helpviewer_keywords:
- doc compiler option [Visual Basic]
- -doc compiler option [Visual Basic]
- /doc compiler option [Visual Basic]
ms.assetid: 5fc32ec9-a149-4648-994c-a8d0cccd0a65
ms.openlocfilehash: 57a81983278c26090c62995f4da55c5cbfd66047
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84408669"
---
# <a name="-doc"></a><span data-ttu-id="8d631-102">-doc</span><span class="sxs-lookup"><span data-stu-id="8d631-102">-doc</span></span>
<span data-ttu-id="8d631-103">將文件註解處理成 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="8d631-103">Processes documentation comments to an XML file.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="8d631-104">語法</span><span class="sxs-lookup"><span data-stu-id="8d631-104">Syntax</span></span>  
  
```console  
-doc[+ | -]  
```

<span data-ttu-id="8d631-105">或</span><span class="sxs-lookup"><span data-stu-id="8d631-105">or</span></span>  

```console
-doc:file  
```  
  
## <a name="arguments"></a><span data-ttu-id="8d631-106">引數</span><span class="sxs-lookup"><span data-stu-id="8d631-106">Arguments</span></span>  
  
|<span data-ttu-id="8d631-107">詞彙</span><span class="sxs-lookup"><span data-stu-id="8d631-107">Term</span></span>|<span data-ttu-id="8d631-108">定義</span><span class="sxs-lookup"><span data-stu-id="8d631-108">Definition</span></span>|  
|---|---|  
|<span data-ttu-id="8d631-109">`+` &#124; `-`</span><span class="sxs-lookup"><span data-stu-id="8d631-109">`+` &#124; `-`</span></span>|<span data-ttu-id="8d631-110">選擇性。</span><span class="sxs-lookup"><span data-stu-id="8d631-110">Optional.</span></span> <span data-ttu-id="8d631-111">指定 + 或只是 `-doc` ，會使編譯器產生檔資訊，並將它放在 XML 檔案中。</span><span class="sxs-lookup"><span data-stu-id="8d631-111">Specifying +, or just `-doc`, causes the compiler to generate documentation information and place it in an XML file.</span></span> <span data-ttu-id="8d631-112">指定 `-` 等同于不指定，因此不 `-doc` 會建立任何檔資訊。</span><span class="sxs-lookup"><span data-stu-id="8d631-112">Specifying `-` is the equivalent of not specifying `-doc`, causing no documentation information to be created.</span></span>|  
|`file`|<span data-ttu-id="8d631-113">如果使用 `-doc:`，則為必要項。</span><span class="sxs-lookup"><span data-stu-id="8d631-113">Required if `-doc:` is used.</span></span> <span data-ttu-id="8d631-114">指定輸出 XML 檔案，其中會填入編譯的原始程式碼檔案中的批註。</span><span class="sxs-lookup"><span data-stu-id="8d631-114">Specifies the output XML file, which is populated with the comments from the source-code files of the compilation.</span></span> <span data-ttu-id="8d631-115">如果檔案名包含空格，請使用引號（""）來括住名稱。</span><span class="sxs-lookup"><span data-stu-id="8d631-115">If the file name contains a space, surround the name with quotation marks (" ").</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="8d631-116">備註</span><span class="sxs-lookup"><span data-stu-id="8d631-116">Remarks</span></span>  
 <span data-ttu-id="8d631-117">`-doc`選項控制編譯器是否產生包含檔批註的 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="8d631-117">The `-doc` option controls whether the compiler generates an XML file containing the documentation comments.</span></span> <span data-ttu-id="8d631-118">如果您使用 `-doc:file` 語法，參數會 `file` 指定 XML 檔的名稱。</span><span class="sxs-lookup"><span data-stu-id="8d631-118">If you use the `-doc:file` syntax, the `file` parameter specifies the name of the XML file.</span></span> <span data-ttu-id="8d631-119">如果您使用 `-doc` 或 `-doc+` ，編譯器會從編譯器所建立的可執行檔或程式庫取得 XML 檔案名。</span><span class="sxs-lookup"><span data-stu-id="8d631-119">If you use `-doc` or `-doc+`, the compiler takes the XML file name from the executable file or library that the compiler is creating.</span></span> <span data-ttu-id="8d631-120">如果您使用 `-doc-` 或未指定 `-doc` 選項，編譯器不會建立 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="8d631-120">If you use `-doc-` or do not specify the `-doc` option, the compiler does not create an XML file.</span></span>  
  
 <span data-ttu-id="8d631-121">在原始程式碼檔中，檔批註可以在下列定義之前：</span><span class="sxs-lookup"><span data-stu-id="8d631-121">In source-code files, documentation comments can precede the following definitions:</span></span>  
  
- <span data-ttu-id="8d631-122">使用者定義類型，例如[類別](../../language-reference/statements/class-statement.md)或[介面](../../language-reference/statements/interface-statement.md)</span><span class="sxs-lookup"><span data-stu-id="8d631-122">User-defined types, such as a [class](../../language-reference/statements/class-statement.md) or [interface](../../language-reference/statements/interface-statement.md)</span></span>  
  
- <span data-ttu-id="8d631-123">成員，例如欄位、[事件](../../language-reference/statements/event-statement.md)、[屬性](../../language-reference/statements/property-statement.md)、[函數](../../language-reference/statements/function-statement.md)或[副程式](../../language-reference/statements/sub-statement.md)。</span><span class="sxs-lookup"><span data-stu-id="8d631-123">Members, such as a field, [event](../../language-reference/statements/event-statement.md), [property](../../language-reference/statements/property-statement.md), [function](../../language-reference/statements/function-statement.md), or [subroutine](../../language-reference/statements/sub-statement.md).</span></span>  
  
 <span data-ttu-id="8d631-124">若要使用產生的 XML 檔案搭配 Visual Studio [IntelliSense](/visualstudio/ide/using-intellisense)功能，請讓 xml 檔案的檔案名與您要支援的元件相同。</span><span class="sxs-lookup"><span data-stu-id="8d631-124">To use the generated XML file with the Visual Studio [IntelliSense](/visualstudio/ide/using-intellisense) feature, let the file name of the XML file be the same as the assembly you want to support.</span></span> <span data-ttu-id="8d631-125">請確定 XML 檔案與元件位於相同的目錄中，如此一來，當元件在 Visual Studio 專案中被參考時，也會找到 .xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="8d631-125">Make sure the XML file is in the same directory as the assembly so that when the assembly is referenced in the Visual Studio project, the .xml file is found as well.</span></span> <span data-ttu-id="8d631-126">IntelliSense 在專案內或專案所參考的專案內的程式碼都不需要使用 XML 檔檔案。</span><span class="sxs-lookup"><span data-stu-id="8d631-126">XML documentation files are not required for IntelliSense to work for code within a project or within projects referenced by a project.</span></span>  
  
 <span data-ttu-id="8d631-127">除非您使用進行編譯，否則 XML 檔案會 `-target:module` 包含標記 `<assembly></assembly>` 。</span><span class="sxs-lookup"><span data-stu-id="8d631-127">Unless you compile with `-target:module`, the XML file contains the tags `<assembly></assembly>`.</span></span> <span data-ttu-id="8d631-128">這些標記會指定包含編譯輸出檔的組件資訊清單的檔案名。</span><span class="sxs-lookup"><span data-stu-id="8d631-128">These tags specify the name of the file containing the assembly manifest for the output file of the compilation.</span></span>  
  
 <span data-ttu-id="8d631-129">如需從程式碼中的批註產生檔的方式，請參閱[XML 註解標記](../../language-reference/xmldoc/index.md)。</span><span class="sxs-lookup"><span data-stu-id="8d631-129">See [XML Comment Tags](../../language-reference/xmldoc/index.md) for ways to generate documentation from comments in your code.</span></span>  
  
|<span data-ttu-id="8d631-130">若要在 Visual Studio 的整合式開發環境中設定-doc</span><span class="sxs-lookup"><span data-stu-id="8d631-130">To set -doc in the Visual Studio integrated development environment</span></span>|  
|---|  
|<span data-ttu-id="8d631-131">1. 在**方案總管**中選取專案。</span><span class="sxs-lookup"><span data-stu-id="8d631-131">1.  Have a project selected in **Solution Explorer**.</span></span> <span data-ttu-id="8d631-132">按一下 [專案]\*\*\*\* 功能表上的 [屬性]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="8d631-132">On the **Project** menu, click **Properties**.</span></span> <br /><span data-ttu-id="8d631-133">2. 按一下 [**編譯**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="8d631-133">2.  Click the **Compile** tab.</span></span><br /><span data-ttu-id="8d631-134">3. 在 [**產生 XML 檔**檔] 方塊中設定值。</span><span class="sxs-lookup"><span data-stu-id="8d631-134">3.  Set the value in the **Generate XML documentation file** box.</span></span>|  
  
## <a name="example"></a><span data-ttu-id="8d631-135">範例</span><span class="sxs-lookup"><span data-stu-id="8d631-135">Example</span></span>  
 <span data-ttu-id="8d631-136">如需範例，請參閱[使用 XML 記載您的程式碼](../../programming-guide/program-structure/documenting-your-code-with-xml.md)。</span><span class="sxs-lookup"><span data-stu-id="8d631-136">See [Documenting Your Code with XML](../../programming-guide/program-structure/documenting-your-code-with-xml.md) for a sample.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="8d631-137">另請參閱</span><span class="sxs-lookup"><span data-stu-id="8d631-137">See also</span></span>

- [<span data-ttu-id="8d631-138">Visual Basic 命令列編譯器</span><span class="sxs-lookup"><span data-stu-id="8d631-138">Visual Basic Command-Line Compiler</span></span>](index.md)
- [<span data-ttu-id="8d631-139">使用 XML 加入程式碼註解</span><span class="sxs-lookup"><span data-stu-id="8d631-139">Documenting Your Code with XML</span></span>](../../programming-guide/program-structure/documenting-your-code-with-xml.md)
