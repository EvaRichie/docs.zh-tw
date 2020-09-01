---
description: -deterministic (C# 編譯器選項)
title: -deterministic (C# 編譯器選項)
ms.date: 04/12/2018
f1_keywords:
- /deterministic
helpviewer_keywords:
- -deterministic compiler option [C#]
- deterministic compiler option [C#]
- /deterministic compiler option [C#]
ms.openlocfilehash: 9d0bcc2957e5a666c21cdc2ce61e74fc90fe3530
ms.sourcegitcommit: d579fb5e4b46745fd0f1f8874c94c6469ce58604
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2020
ms.locfileid: "89125822"
---
# <a name="-deterministic"></a><span data-ttu-id="a8b21-103">-deterministic</span><span class="sxs-lookup"><span data-stu-id="a8b21-103">-deterministic</span></span>

<span data-ttu-id="a8b21-104">可讓編譯器產生相同輸入之編譯間的逐一位元組輸出相同的組件。</span><span class="sxs-lookup"><span data-stu-id="a8b21-104">Causes the compiler to produce an assembly whose byte-for-byte output is identical across compilations for identical inputs.</span></span>

## <a name="syntax"></a><span data-ttu-id="a8b21-105">語法</span><span class="sxs-lookup"><span data-stu-id="a8b21-105">Syntax</span></span>

```console
-deterministic
```

## <a name="remarks"></a><span data-ttu-id="a8b21-106">備註</span><span class="sxs-lookup"><span data-stu-id="a8b21-106">Remarks</span></span>

<span data-ttu-id="a8b21-107">根據預設，一組指定輸入的編譯器輸出是唯一的，因為編譯器會新增時間戳記以及透過亂數所產生的 GUID。</span><span class="sxs-lookup"><span data-stu-id="a8b21-107">By default, compiler output from a given set of inputs is unique, since the compiler adds a timestamp and a GUID that is generated from random numbers.</span></span> <span data-ttu-id="a8b21-108">您可以使用 `-deterministic` 選項來產生「確定性組件」\*\*，這是只要輸入維持不變，其二進位內容在編譯之間就相同的組件。</span><span class="sxs-lookup"><span data-stu-id="a8b21-108">You use the `-deterministic` option to produce a *deterministic assembly*, one whose binary content is identical across compilations as long as the input remains the same.</span></span>

<span data-ttu-id="a8b21-109">編譯器會基於確定性而考慮下列輸入：</span><span class="sxs-lookup"><span data-stu-id="a8b21-109">The compiler considers the following inputs for the purpose of determinism:</span></span>

- <span data-ttu-id="a8b21-110">命令列參數序列。</span><span class="sxs-lookup"><span data-stu-id="a8b21-110">The sequence of command-line parameters.</span></span>
- <span data-ttu-id="a8b21-111">編譯器之 .rsp 回應檔的內容。</span><span class="sxs-lookup"><span data-stu-id="a8b21-111">The contents of the compiler's .rsp response file.</span></span>
- <span data-ttu-id="a8b21-112">使用的編譯器精確版本和其參考的組件。</span><span class="sxs-lookup"><span data-stu-id="a8b21-112">The precise version of the compiler used, and its referenced assemblies.</span></span>
- <span data-ttu-id="a8b21-113">目前的目錄路徑。</span><span class="sxs-lookup"><span data-stu-id="a8b21-113">The current directory path.</span></span>
- <span data-ttu-id="a8b21-114">以直接或間接方式明確地傳遞給編譯器之所有檔案的二進位內容，包含：</span><span class="sxs-lookup"><span data-stu-id="a8b21-114">The binary contents of all files explicitly passed to the compiler either directly or indirectly, including:</span></span>
  - <span data-ttu-id="a8b21-115">原始程式檔</span><span class="sxs-lookup"><span data-stu-id="a8b21-115">Source files</span></span>
  - <span data-ttu-id="a8b21-116">參考的組件</span><span class="sxs-lookup"><span data-stu-id="a8b21-116">Referenced assemblies</span></span>
  - <span data-ttu-id="a8b21-117">參考的模組</span><span class="sxs-lookup"><span data-stu-id="a8b21-117">Referenced modules</span></span>
  - <span data-ttu-id="a8b21-118">資源</span><span class="sxs-lookup"><span data-stu-id="a8b21-118">Resources</span></span>
  - <span data-ttu-id="a8b21-119">強式名稱金鑰檔</span><span class="sxs-lookup"><span data-stu-id="a8b21-119">The strong name key file</span></span>
  - <span data-ttu-id="a8b21-120">@ 回應檔</span><span class="sxs-lookup"><span data-stu-id="a8b21-120">@ response files</span></span>
  - <span data-ttu-id="a8b21-121">分析器</span><span class="sxs-lookup"><span data-stu-id="a8b21-121">Analyzers</span></span>
  - <span data-ttu-id="a8b21-122">規則集</span><span class="sxs-lookup"><span data-stu-id="a8b21-122">Rulesets</span></span>
  - <span data-ttu-id="a8b21-123">分析器可能使用的其他檔案</span><span class="sxs-lookup"><span data-stu-id="a8b21-123">Additional files that may be used by analyzers</span></span>
- <span data-ttu-id="a8b21-124">目前文化特性 (Culture) (適用於用來產生診斷和例外狀況訊息的語言)。</span><span class="sxs-lookup"><span data-stu-id="a8b21-124">The current culture (for the language in which diagnostics and exception messages are produced).</span></span>
- <span data-ttu-id="a8b21-125">如果未指定編碼，則為預設編碼 (或目前字碼頁)。</span><span class="sxs-lookup"><span data-stu-id="a8b21-125">The default encoding (or the current code page) if the encoding is not specified.</span></span>
- <span data-ttu-id="a8b21-126">存在、不存在，以及編譯器搜尋路徑 (例如，透過 `-lib` 或 `-recurse` 指定) 上檔案的內容。</span><span class="sxs-lookup"><span data-stu-id="a8b21-126">The existence, non-existence, and contents of files on the compiler's search paths (specified, for example, by `-lib` or `-recurse`).</span></span>
- <span data-ttu-id="a8b21-127">在其上執行編譯器的 CLR 平台。</span><span class="sxs-lookup"><span data-stu-id="a8b21-127">The CLR platform on which the compiler is run.</span></span>
- <span data-ttu-id="a8b21-128">`%LIBPATH%` 的值，可能會影響分析器相依性載入。</span><span class="sxs-lookup"><span data-stu-id="a8b21-128">The value of `%LIBPATH%`, which can affect analyzer dependency loading.</span></span>

<span data-ttu-id="a8b21-129">來源公開可用時，確定性編譯可以用於建立是否從信任的來源編譯二進位檔。</span><span class="sxs-lookup"><span data-stu-id="a8b21-129">When sources are publicly available, deterministic compilation can be used for establishing whether a binary is compiled from a trusted source.</span></span> <span data-ttu-id="a8b21-130">它也可以用於持續建置系統，確定是否需要執行與二進位檔變更相依的建置步驟。</span><span class="sxs-lookup"><span data-stu-id="a8b21-130">It can also be useful in a continuous build system for determining whether build steps that are dependent on changes to a binary need to be executed.</span></span>

## <a name="see-also"></a><span data-ttu-id="a8b21-131">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a8b21-131">See also</span></span>

- [<span data-ttu-id="a8b21-132">C # 編譯器選項</span><span class="sxs-lookup"><span data-stu-id="a8b21-132">C# Compiler Options</span></span>](./index.md)
- [<span data-ttu-id="a8b21-133">管理專案和方案屬性</span><span class="sxs-lookup"><span data-stu-id="a8b21-133">Managing Project and Solution Properties</span></span>](/visualstudio/ide/managing-project-and-solution-properties)
