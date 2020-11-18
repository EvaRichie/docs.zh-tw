---
title: 安全性和使用者輸入
description: 您的程式碼可能會將使用者輸入的資料當作參數傳遞給其他程式碼，這可能會影響安全性。 您可以進行範圍檢查，以拒絕有問題的輸入。
ms.date: 07/15/2020
helpviewer_keywords:
- security [.NET], user input
- user input, security
- secure coding, user input
- code security, user input
ms.assetid: 9141076a-96c9-4b01-93de-366bb1d858bc
ms.openlocfilehash: e476db90dd1fd579f4ecfe3f2088cc76c955b9c0
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94824053"
---
# <a name="security-and-user-input"></a><span data-ttu-id="eed7b-104">安全性和使用者輸入</span><span class="sxs-lookup"><span data-stu-id="eed7b-104">Security and User Input</span></span>

<span data-ttu-id="eed7b-105">使用者資料，也就是任何種類的輸入 (來自 Web 要求或 URL 的資料、對 Microsoft Windows Forms 應用程式之控制項的輸入等等)，可以會對程式碼有不良影響，因為通常該資料會直接做為參數來呼叫其他程式碼。</span><span class="sxs-lookup"><span data-stu-id="eed7b-105">User data, which is any kind of input (data from a Web request or URL, input to controls of a Microsoft Windows Forms application, and so on), can adversely influence code because often that data is used directly as parameters to call other code.</span></span> <span data-ttu-id="eed7b-106">這種情況類似惡意程式碼使用奇怪的參數呼叫您的程式碼，應該採取相同的預防措施。</span><span class="sxs-lookup"><span data-stu-id="eed7b-106">This situation is analogous to malicious code calling your code with strange parameters, and the same precautions should be taken.</span></span> <span data-ttu-id="eed7b-107">使用者輸入實際上較難以保護其安全，因為沒有任何堆疊框架，可以追蹤可能不受信任的資料存在。</span><span class="sxs-lookup"><span data-stu-id="eed7b-107">User input is actually harder to make safe because there is no stack frame to trace the presence of the potentially untrusted data.</span></span>

<span data-ttu-id="eed7b-108">它們是在最細微且最難以尋找的安全性錯誤當中，因為，雖然它們可以存在於似乎是與安全性沒有相關的程式碼中，但是它們是將錯誤資料傳遞給其他程式碼的閘道。</span><span class="sxs-lookup"><span data-stu-id="eed7b-108">These are among the subtlest and hardest security bugs to find because, although they can exist in code that is seemingly unrelated to security, they are a gateway to pass bad data through to other code.</span></span> <span data-ttu-id="eed7b-109">若要找出這些錯誤，請依照下列任何一種輸入資料，想像一下可能值的範圍，並且考量查看此資料的程式碼是否可以處理所有這些情況。</span><span class="sxs-lookup"><span data-stu-id="eed7b-109">To look for these bugs, follow any kind of input data, imagine what the range of possible values might be, and consider whether the code seeing this data can handle all those cases.</span></span> <span data-ttu-id="eed7b-110">您可以透過檢查範圍以及拒絕程式碼無法處理的任何輸入，來修正這些錯誤。</span><span class="sxs-lookup"><span data-stu-id="eed7b-110">You can fix these bugs through range checking and rejecting any input the code cannot handle.</span></span>

<span data-ttu-id="eed7b-111">與使用者資料相關的一些重要考量包括下列項目︰</span><span class="sxs-lookup"><span data-stu-id="eed7b-111">Some important considerations involving user data include the following:</span></span>

- <span data-ttu-id="eed7b-112">伺服器回應的任何使用者資料會在用戶端的伺服器網站內容中執行。</span><span class="sxs-lookup"><span data-stu-id="eed7b-112">Any user data in a server response runs in the context of the server's site on the client.</span></span> <span data-ttu-id="eed7b-113">例如，如果您的 Web 服務器接受使用者資料並將它插入傳回的網頁中，它可能會包含一個 **\<script>** 標記，並在伺服器上以 as 的形式執行。</span><span class="sxs-lookup"><span data-stu-id="eed7b-113">If your Web server takes user data and inserts it into the returned Web page, it might, for example, include a **\<script>** tag and run as if from the server.</span></span>

- <span data-ttu-id="eed7b-114">請記住，用戶端可以要求任何 URL。</span><span class="sxs-lookup"><span data-stu-id="eed7b-114">Remember that the client can request any URL.</span></span>

- <span data-ttu-id="eed7b-115">請考慮棘手或無效的路徑︰</span><span class="sxs-lookup"><span data-stu-id="eed7b-115">Consider tricky or invalid paths:</span></span>

  - <span data-ttu-id="eed7b-116">..\，非常長的路徑。</span><span class="sxs-lookup"><span data-stu-id="eed7b-116">..\ , extremely long paths.</span></span>

  - <span data-ttu-id="eed7b-117">使用萬用字元 (\*)。</span><span class="sxs-lookup"><span data-stu-id="eed7b-117">Use of wild card characters (\*).</span></span>

  - <span data-ttu-id="eed7b-118">語彙基元展開 (%token%)。</span><span class="sxs-lookup"><span data-stu-id="eed7b-118">Token expansion (%token%).</span></span>

  - <span data-ttu-id="eed7b-119">具有特殊意義的奇怪格式路徑。</span><span class="sxs-lookup"><span data-stu-id="eed7b-119">Strange forms of paths with special meaning.</span></span>

  - <span data-ttu-id="eed7b-120">替代的檔案系統資料流名稱，例如 `filename::$DATA`。</span><span class="sxs-lookup"><span data-stu-id="eed7b-120">Alternate file system stream names such as `filename::$DATA`.</span></span>

  - <span data-ttu-id="eed7b-121">簡短版本的檔案名稱，例如 `longfilename` 的 `longfi~1`。</span><span class="sxs-lookup"><span data-stu-id="eed7b-121">Short versions of file names such as `longfi~1` for `longfilename`.</span></span>

- <span data-ttu-id="eed7b-122">請記住，Eval(userdata) 可以執行任何動作。</span><span class="sxs-lookup"><span data-stu-id="eed7b-122">Remember that Eval(userdata) can do anything.</span></span>

- <span data-ttu-id="eed7b-123">請小心晚期繫結至包含一些使用者資料的名稱。</span><span class="sxs-lookup"><span data-stu-id="eed7b-123">Be wary of late binding to a name that includes some user data.</span></span>

- <span data-ttu-id="eed7b-124">如果您正在處理 Web 資料，請考慮允許的各種形式逸出，包括︰</span><span class="sxs-lookup"><span data-stu-id="eed7b-124">If you are dealing with Web data, consider the various forms of escapes that are permissible, including:</span></span>

  - <span data-ttu-id="eed7b-125">十六進位逸出 (%nn)。</span><span class="sxs-lookup"><span data-stu-id="eed7b-125">Hexadecimal escapes (%nn).</span></span>

  - <span data-ttu-id="eed7b-126">Unicode 逸出 (%nnn)。</span><span class="sxs-lookup"><span data-stu-id="eed7b-126">Unicode escapes (%nnn).</span></span>

  - <span data-ttu-id="eed7b-127">過長 UTF-8 逸出 (%nn%nn)。</span><span class="sxs-lookup"><span data-stu-id="eed7b-127">Overlong UTF-8 escapes (%nn%nn).</span></span>

  - <span data-ttu-id="eed7b-128">雙逸出 (%nn 變成 %mmnn，其中 %mm 是 '%' 的逸出)。</span><span class="sxs-lookup"><span data-stu-id="eed7b-128">Double escapes (%nn becomes %mmnn, where %mm is the escape for '%').</span></span>

- <span data-ttu-id="eed7b-129">請小心可能有一個以上標準格式的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="eed7b-129">Be wary of user names that might have more than one canonical format.</span></span> <span data-ttu-id="eed7b-130">例如，您通常可以使用 MYDOMAIN\\username 形式或 username@mydomain.example.com 形式。</span><span class="sxs-lookup"><span data-stu-id="eed7b-130">For example, you can often use either the MYDOMAIN\\*username* form or the *username*@mydomain.example.com form.</span></span>

## <a name="see-also"></a><span data-ttu-id="eed7b-131">請參閱</span><span class="sxs-lookup"><span data-stu-id="eed7b-131">See also</span></span>

- [<span data-ttu-id="eed7b-132">安全程式碼撰寫方針</span><span class="sxs-lookup"><span data-stu-id="eed7b-132">Secure Coding Guidelines</span></span>](secure-coding-guidelines.md)
- [<span data-ttu-id="eed7b-133">ASP.NET Core 安全性</span><span class="sxs-lookup"><span data-stu-id="eed7b-133">ASP.NET Core Security</span></span>](/aspnet/core/security/)
