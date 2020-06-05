---
title: -errorreport
ms.date: 08/14/2018
helpviewer_keywords:
- -errorreport compiler option [Visual Basic]
- /errorreport compiler option [Visual Basic]
- errorreport compiler option [Visual Basic]
ms.assetid: a7fe83a2-a6d8-460c-8dad-79a8f433f501
ms.openlocfilehash: b6a1c8fce17e3e5a54366c2ff4dff4e6aa668f56
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84408656"
---
# <a name="-errorreport"></a><span data-ttu-id="0d3d1-102">-errorreport</span><span class="sxs-lookup"><span data-stu-id="0d3d1-102">-errorreport</span></span>

<span data-ttu-id="0d3d1-103">指定 Visual Basic 編譯器應該如何報告內部編譯器錯誤。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-103">Specifies how the Visual Basic compiler should report internal compiler errors.</span></span>

## <a name="syntax"></a><span data-ttu-id="0d3d1-104">語法</span><span class="sxs-lookup"><span data-stu-id="0d3d1-104">Syntax</span></span>

```console
-errorreport:{ prompt | queue | send | none }
```

## <a name="remarks"></a><span data-ttu-id="0d3d1-105">備註</span><span class="sxs-lookup"><span data-stu-id="0d3d1-105">Remarks</span></span>

<span data-ttu-id="0d3d1-106">此選項提供一個便利的方式，向 Microsoft 的 Visual Basic 團隊報告 Visual Basic 的內部編譯器錯誤（ICE）。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-106">This option provides a convenient way to report a Visual Basic internal compiler error (ICE) to the Visual Basic team at Microsoft.</span></span> <span data-ttu-id="0d3d1-107">根據預設，編譯器不會將任何資訊傳送至 Microsoft。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-107">By default, the compiler sends no information to Microsoft.</span></span> <span data-ttu-id="0d3d1-108">不過，如果您遇到內部編譯器錯誤，此選項可讓您向 Microsoft 報告錯誤。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-108">However, if you do encounter an internal compiler error, this option allows you to report the error to Microsoft.</span></span> <span data-ttu-id="0d3d1-109">這項資訊可協助 Microsoft 工程師找出原因，並可協助改善下一版的 Visual Basic。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-109">That information will help Microsoft engineers identify the cause and may help improve the next release of Visual Basic.</span></span>

<span data-ttu-id="0d3d1-110">使用者傳送報表的能力取決於電腦和使用者原則許可權。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-110">A user's ability to send reports depends on machine and user policy permissions.</span></span>

<span data-ttu-id="0d3d1-111">下表摘要說明選項的效果 `-errorreport` 。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-111">The following table summarizes the effect of the `-errorreport` option.</span></span>

|<span data-ttu-id="0d3d1-112">選項</span><span class="sxs-lookup"><span data-stu-id="0d3d1-112">Option</span></span>|<span data-ttu-id="0d3d1-113">行為</span><span class="sxs-lookup"><span data-stu-id="0d3d1-113">Behavior</span></span>|
|---|---|
|`prompt`|<span data-ttu-id="0d3d1-114">如果發生內部編譯器錯誤，則會出現對話方塊，讓您可以查看編譯器所收集的確切資料。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-114">If an internal compiler error occurs, a dialog box comes up so that you can view the exact data that the compiler collected.</span></span> <span data-ttu-id="0d3d1-115">您可以判斷錯誤報表中是否有任何機密資訊，並決定是否要將它傳送給 Microsoft。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-115">You can determine if there is any sensitive information in the error report and make a decision on whether to send it to Microsoft.</span></span> <span data-ttu-id="0d3d1-116">如果您決定傳送它，且電腦和使用者原則設定允許，則編譯器會將資料傳送給 Microsoft。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-116">If you decide to send it, and the machine and user policy settings allow it, the compiler sends the data to Microsoft.</span></span>|
|`queue`|<span data-ttu-id="0d3d1-117">佇列錯誤報告。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-117">Queues the error report.</span></span> <span data-ttu-id="0d3d1-118">當您使用系統管理員許可權登入時，可以報告自上次登入後的任何失敗時間（每隔三天不會提示您傳送失敗的報告一次以上）。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-118">When you log in with administrator privileges, you can report any failures since the last time you were logged in (you will not be prompted to send reports for failures more than once every three days).</span></span> <span data-ttu-id="0d3d1-119">這是未指定選項時的預設行為 `-errorreport` 。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-119">This is the default behavior when the `-errorreport` option is not specified.</span></span>|
|`send`|<span data-ttu-id="0d3d1-120">如果發生內部編譯器錯誤，而且電腦和使用者原則設定允許，則編譯器會將資料傳送給 Microsoft。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-120">If an internal compiler error occurs, and the machine and user policy settings allow it, the compiler sends the data to Microsoft.</span></span><br /><br /> <span data-ttu-id="0d3d1-121">`-errorreport:send`如果[Windows 錯誤報告](/windows/desktop/wer/windows-error-reporting)系統設定啟用 [報表]，則選項會嘗試自動傳送錯誤資訊給 Microsoft。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-121">The option `-errorreport:send` attempts to automatically send error information to Microsoft if reporting is enabled by the [Windows Error Reporting](/windows/desktop/wer/windows-error-reporting) system settings.</span></span> |
|`none`|<span data-ttu-id="0d3d1-122">如果發生內部編譯器錯誤，則不會將它收集或傳送給 Microsoft。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-122">If an internal compiler error occurs, it will not be collected or sent to Microsoft.</span></span>|

<span data-ttu-id="0d3d1-123">編譯器會在錯誤發生時傳送包含堆疊的資料，這通常會包含一些原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-123">The compiler sends data that includes the stack at the time of the error, which usually includes some source code.</span></span> <span data-ttu-id="0d3d1-124">如果搭配 `-errorreport` [-bugreport](bugreport.md)選項使用，則會傳送整個來源檔案。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-124">If `-errorreport` is used with the [-bugreport](bugreport.md) option, then the entire source file is sent.</span></span>

<span data-ttu-id="0d3d1-125">此選項最適合搭配[-bugreport](bugreport.md)選項使用，因為它可讓 Microsoft 工程師更輕鬆地重現錯誤。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-125">This option is best used with the [-bugreport](bugreport.md) option, because it allows Microsoft engineers to more easily reproduce the error.</span></span>

> [!NOTE]
> <span data-ttu-id="0d3d1-126">此 `-errorreport` 選項無法從 Visual Studio 開發環境中使用; 只有在從命令列進行編譯時，才能使用此選項。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-126">The `-errorreport` option is not available from within the Visual Studio development environment; it is available only when compiling from the command line.</span></span>

## <a name="example"></a><span data-ttu-id="0d3d1-127">範例</span><span class="sxs-lookup"><span data-stu-id="0d3d1-127">Example</span></span>

<span data-ttu-id="0d3d1-128">下列程式碼會嘗試進行編譯 `T2.vb` ，如果編譯器遇到編譯器內部錯誤，則會提示您將錯誤報表傳送給 Microsoft。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-128">The following code attempts to compile `T2.vb`, and if the compiler encounters an internal compiler error, it prompts you to send the error report to Microsoft.</span></span>

```console
vbc -errorreport:prompt t2.vb
```

## <a name="see-also"></a><span data-ttu-id="0d3d1-129">另請參閱</span><span class="sxs-lookup"><span data-stu-id="0d3d1-129">See also</span></span>

- [<span data-ttu-id="0d3d1-130">Visual Basic 命令列編譯器</span><span class="sxs-lookup"><span data-stu-id="0d3d1-130">Visual Basic Command-Line Compiler</span></span>](index.md)
- [<span data-ttu-id="0d3d1-131">編譯命令列的範例</span><span class="sxs-lookup"><span data-stu-id="0d3d1-131">Sample Compilation Command Lines</span></span>](sample-compilation-command-lines.md)
- [<span data-ttu-id="0d3d1-132">-bugreport</span><span class="sxs-lookup"><span data-stu-id="0d3d1-132">-bugreport</span></span>](bugreport.md)
