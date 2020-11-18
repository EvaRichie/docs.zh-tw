---
title: 安全性和產生作業中的程式碼
description: 以較高的信任層級執行的較低信任程式碼產生程式碼，是一項安全性考慮，特別是當呼叫端可能會影響程式碼產生時。
ms.date: 07/15/2020
helpviewer_keywords:
- code security, on-the-fly code generation
- on-the-fly code generation
- security [.NET], on-the-fly code generation
- secure coding, on-the-fly code generation
ms.assetid: 6d221724-bb21-4d76-90c3-0ee2a2e69be2
ms.openlocfilehash: c94da31f464a5272dd3f3c9f767a40ba7ad88a47
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94824144"
---
# <a name="security-and-on-the-fly-code-generation"></a><span data-ttu-id="a811d-103">安全性和產生作業中的程式碼</span><span class="sxs-lookup"><span data-stu-id="a811d-103">Security and On-the-Fly Code Generation</span></span>

<span data-ttu-id="a811d-104">某些程式庫的運作方式為產生程式碼，然後執行這個程式碼以進行呼叫端的特定作業。</span><span class="sxs-lookup"><span data-stu-id="a811d-104">Some libraries operate by generating code and running it to perform some operation for the caller.</span></span> <span data-ttu-id="a811d-105">這種方法的基本問題在於程式庫可能會代表較不受信任的程式碼來產生程式碼，然後以較高的信任層級來執行這個程式碼。</span><span class="sxs-lookup"><span data-stu-id="a811d-105">The basic problem is generating code on behalf of lesser-trust code and running it at a higher trust.</span></span> <span data-ttu-id="a811d-106">當呼叫端可能影響程式碼產生時，這個問題會更嚴重，因此您必須確保產生的程式碼只會是您認為安全的程式碼。</span><span class="sxs-lookup"><span data-stu-id="a811d-106">The problem worsens when the caller can influence code generation, so you must ensure that only code you consider safe is generated.</span></span>  
  
<span data-ttu-id="a811d-107">您必須隨時掌握所產生的實際程式碼內容。</span><span class="sxs-lookup"><span data-stu-id="a811d-107">You need to know exactly what code you are generating at all times.</span></span> <span data-ttu-id="a811d-108">這表示您必須嚴格控制從使用者取得的任何值，這些值可以是以引號括住的字串 (必須逸出以避免包含未預期的程式碼項目)、識別項 (必須檢查以驗證是否為有效的識別項)，或其他任何值。</span><span class="sxs-lookup"><span data-stu-id="a811d-108">This means that you must have strict controls on any values that you get from a user, be they quote-enclosed strings (which should be escaped so they cannot include unexpected code elements), identifiers (which should be checked to verify that they are valid identifiers), or anything else.</span></span> <span data-ttu-id="a811d-109">識別項可能具有危險性，因為編譯過的組件可能會被修改，讓它的識別項包含一些可能會破壞組件的特殊字元 (雖然這通常不是安全性弱點)。</span><span class="sxs-lookup"><span data-stu-id="a811d-109">Identifiers can be dangerous because a compiled assembly can be modified so that its identifiers contain strange characters, which will probably break it (although this is rarely a security vulnerability).</span></span>  
  
<span data-ttu-id="a811d-110">建議您使用反映發出來產生程式碼，這通常可協助您避免許多問題。</span><span class="sxs-lookup"><span data-stu-id="a811d-110">It is recommended that you generate code with reflection emit, which often helps you avoid many of these problems.</span></span>  
  
<span data-ttu-id="a811d-111">當您編譯程式碼時，請考慮惡意程式是否有可能修改程式碼。</span><span class="sxs-lookup"><span data-stu-id="a811d-111">When you compile the code, consider whether there is some way a malicious program could modify it.</span></span> <span data-ttu-id="a811d-112">在編譯器讀取原始程式碼之前，或在您的程式碼載入 .dll 檔案之前，是不是有空檔時間可以讓惡意程式碼變更磁碟上的原始程式碼？</span><span class="sxs-lookup"><span data-stu-id="a811d-112">Is there a small window of time during which malicious code can change source code on disk before the compiler reads it or before your code loads the .dll file?</span></span> <span data-ttu-id="a811d-113">如果是，您必須視需要使用檔案系統中的存取控制清單，來保護含有這些檔案的目錄。</span><span class="sxs-lookup"><span data-stu-id="a811d-113">If so, you must protect the directory containing these files, using an Access Control List in the file system, as appropriate.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="a811d-114">請參閱</span><span class="sxs-lookup"><span data-stu-id="a811d-114">See also</span></span>

- [<span data-ttu-id="a811d-115">安全程式碼撰寫方針</span><span class="sxs-lookup"><span data-stu-id="a811d-115">Secure Coding Guidelines</span></span>](secure-coding-guidelines.md)
- [<span data-ttu-id="a811d-116">ASP.NET Core 安全性</span><span class="sxs-lookup"><span data-stu-id="a811d-116">ASP.NET Core Security</span></span>](/aspnet/core/security/)
