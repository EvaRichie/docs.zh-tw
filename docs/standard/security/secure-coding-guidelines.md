---
title: .NET 的安全程式碼撰寫方針
description: 設計要使用的程式碼。NET 強制許可權和其他強制性，以協助防止惡意程式碼存取資料或執行其他動作。
ms.date: 07/15/2020
helpviewer_keywords:
- managed wrapper to native code implementation
- secure coding
- reusable components
- library code that exposes protected resources
- code, security
- code security
- secure coding, options
- components [.NET], security
- code security, options
- security-neutral code
- security [.NET], coding guidelines
ms.assetid: 4f882d94-262b-4494-b0a6-ba9ba1f5f177
ms.openlocfilehash: a05e0cec2814be88ac835d05601d5cf5f66383c3
ms.sourcegitcommit: b7a8b09828bab4e90f66af8d495ecd7024c45042
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87555952"
---
# <a name="secure-coding-guidelines"></a><span data-ttu-id="29716-103">安全程式碼撰寫方針</span><span class="sxs-lookup"><span data-stu-id="29716-103">Secure coding guidelines</span></span>

<span data-ttu-id="29716-104">大部分的應用程式程式碼都可以直接使用 .NET 所實行的基礎結構。</span><span class="sxs-lookup"><span data-stu-id="29716-104">Most application code can simply use the infrastructure implemented by .NET.</span></span> <span data-ttu-id="29716-105">某些情況還需要其他的應用程式特定安全性 (藉由擴充安全性系統或是使用新的臨機操作方法來建置)。</span><span class="sxs-lookup"><span data-stu-id="29716-105">In some cases, additional application-specific security is required, built either by extending the security system or by using new ad hoc methods.</span></span>

<span data-ttu-id="29716-106">在您的程式碼中使用 .NET 強制執行的許可權和其他強制性時，您應該為防止惡意程式碼存取您不想要它擁有或執行其他不必要動作的資訊進行阻礙。</span><span class="sxs-lookup"><span data-stu-id="29716-106">Using .NET enforced permissions and other enforcement in your code, you should erect barriers to prevent malicious code from accessing information that you don't want it to have or performing other undesirable actions.</span></span> <span data-ttu-id="29716-107">此外，在所有使用受信任程式碼的可預期案例中，您必須在安全性與可用性之間達成平衡。</span><span class="sxs-lookup"><span data-stu-id="29716-107">Additionally, you must strike a balance between security and usability in all the expected scenarios using trusted code.</span></span>

<span data-ttu-id="29716-108">本概觀說明設計程式碼以搭配使用安全性系統時，可以採用的不同方式。</span><span class="sxs-lookup"><span data-stu-id="29716-108">This overview describes the different ways code can be designed to work with the security system.</span></span>

## <a name="securing-resource-access"></a><span data-ttu-id="29716-109">保護資源存取</span><span class="sxs-lookup"><span data-stu-id="29716-109">Securing resource access</span></span>

<span data-ttu-id="29716-110">當設計和撰寫程式碼時，您需要保護並限制程式碼對資源的存取，特別是當使用或叫用未知來源的程式碼時。</span><span class="sxs-lookup"><span data-stu-id="29716-110">When designing and writing your code, you need to protect and limit the access that code has to resources, especially when using or invoking code of unknown origin.</span></span> <span data-ttu-id="29716-111">因此，請牢記下列技術，以確保程式碼是安全的︰</span><span class="sxs-lookup"><span data-stu-id="29716-111">So, keep in mind the following techniques to ensure your code is secure:</span></span>

- <span data-ttu-id="29716-112">請勿使用程式碼存取安全性 (CAS)。</span><span class="sxs-lookup"><span data-stu-id="29716-112">Do not use Code Access Security (CAS).</span></span>

- <span data-ttu-id="29716-113">請勿使用部分信任程式碼。</span><span class="sxs-lookup"><span data-stu-id="29716-113">Do not use partial trusted code.</span></span>

- <span data-ttu-id="29716-114">請勿使用[AllowPartiallyTrustedCaller](xref:System.Security.AllowPartiallyTrustedCallersAttribute)屬性 (APTCA) 。</span><span class="sxs-lookup"><span data-stu-id="29716-114">Do not use the [AllowPartiallyTrustedCaller](xref:System.Security.AllowPartiallyTrustedCallersAttribute) attribute (APTCA).</span></span>

- <span data-ttu-id="29716-115">請勿使用 .NET 遠端處理。</span><span class="sxs-lookup"><span data-stu-id="29716-115">Do not use .NET Remoting.</span></span>

- <span data-ttu-id="29716-116">請勿使用分散式元件物件模型 (DCOM)。</span><span class="sxs-lookup"><span data-stu-id="29716-116">Do not use Distributed Component Object Model (DCOM).</span></span>

- <span data-ttu-id="29716-117">請勿使用二進位格式器。</span><span class="sxs-lookup"><span data-stu-id="29716-117">Do not use binary formatters.</span></span>

<span data-ttu-id="29716-118">代碼啟用安全性和安全性透明的程式碼不支援做為部分信任程式碼的安全性界限。</span><span class="sxs-lookup"><span data-stu-id="29716-118">Code Access Security and Security-Transparent Code are not supported as a security boundary with partially trusted code.</span></span> <span data-ttu-id="29716-119">建議不要載入及執行未知來源的程式碼，如此便不需要使用替代的安全措施。</span><span class="sxs-lookup"><span data-stu-id="29716-119">We advise against loading and executing code of unknown origins without putting alternative security measures in place.</span></span> <span data-ttu-id="29716-120">替代的安全性措施包括︰</span><span class="sxs-lookup"><span data-stu-id="29716-120">The alternative security measures are:</span></span>

- <span data-ttu-id="29716-121">虛擬化</span><span class="sxs-lookup"><span data-stu-id="29716-121">Virtualization</span></span>

- <span data-ttu-id="29716-122">AppContainers</span><span class="sxs-lookup"><span data-stu-id="29716-122">AppContainers</span></span>

- <span data-ttu-id="29716-123">作業系統 (OS) 使用者和權限</span><span class="sxs-lookup"><span data-stu-id="29716-123">Operating system (OS) users and permissions</span></span>

- <span data-ttu-id="29716-124">Hyper-V 容器</span><span class="sxs-lookup"><span data-stu-id="29716-124">Hyper-V containers</span></span>

## <a name="security-neutral-code"></a><span data-ttu-id="29716-125">安全性中性的程式碼</span><span class="sxs-lookup"><span data-stu-id="29716-125">Security-neutral code</span></span>

<span data-ttu-id="29716-126">安全性中性的程式碼與安全性系統並無明顯關聯。</span><span class="sxs-lookup"><span data-stu-id="29716-126">Security-neutral code does nothing explicit with the security system.</span></span> <span data-ttu-id="29716-127">它會使用接收到的任何使用權限來執行。</span><span class="sxs-lookup"><span data-stu-id="29716-127">It runs with whatever permissions it receives.</span></span> <span data-ttu-id="29716-128">雖然無法攔截與受保護作業相關聯之安全性例外狀況的應用程式 (例如使用檔案、網路功能等等) 可能會導致未處理的例外狀況，但安全性中性的程式碼仍然會利用 .NET 中的安全性技術。</span><span class="sxs-lookup"><span data-stu-id="29716-128">Although applications that fail to catch security exceptions associated with protected operations (such as using files, networking, and so on) can result in an unhandled exception, security-neutral code still takes advantage of the security technologies in .NET.</span></span>

<span data-ttu-id="29716-129">安全性中性程式庫具有您須了解的特殊特性。</span><span class="sxs-lookup"><span data-stu-id="29716-129">A security-neutral library has special characteristics that you should understand.</span></span> <span data-ttu-id="29716-130">假設您的程式庫提供使用檔案或呼叫非受控碼的 API 元素。</span><span class="sxs-lookup"><span data-stu-id="29716-130">Suppose your library provides API elements that use files or call unmanaged code.</span></span> <span data-ttu-id="29716-131">如果您的程式碼沒有對應的許可權，則不會如所述執行。</span><span class="sxs-lookup"><span data-stu-id="29716-131">If your code doesn't have the corresponding permission, it won't run as described.</span></span> <span data-ttu-id="29716-132">然而，即使程式碼擁有使用權限，呼叫它的任何應用程式程式碼也必須要有相同的使用權限才能運作。</span><span class="sxs-lookup"><span data-stu-id="29716-132">However, even if the code has the permission, any application code that calls it must have the same permission in order to work.</span></span> <span data-ttu-id="29716-133">如果呼叫程式碼沒有正確的許可權，則 <xref:System.Security.SecurityException> 會顯示為代碼啟用安全性堆疊逐步解說的結果。</span><span class="sxs-lookup"><span data-stu-id="29716-133">If the calling code doesn't have the right permission, a <xref:System.Security.SecurityException> appears as a result of the code access security stack walk.</span></span>

## <a name="application-code-that-isnt-a-reusable-component"></a><span data-ttu-id="29716-134">不是可重複使用元件的應用程式代碼</span><span class="sxs-lookup"><span data-stu-id="29716-134">Application code that isn't a reusable component</span></span>

<span data-ttu-id="29716-135">如果您的程式碼是不會被其他程式碼呼叫之應用程式的一部分，安全性就很簡單，而且可能不需要特殊的編碼。</span><span class="sxs-lookup"><span data-stu-id="29716-135">If your code is part of an application that won't be called by other code, security is simple and special coding might not be required.</span></span> <span data-ttu-id="29716-136">不過請記住，惡意程式碼可以呼叫您的程式碼。</span><span class="sxs-lookup"><span data-stu-id="29716-136">However, remember that malicious code can call your code.</span></span> <span data-ttu-id="29716-137">雖然程式碼存取安全性可以制止惡意程式碼存取資源，這類的程式碼還是可以讀取可能含有敏感資訊的欄位或屬性的值。</span><span class="sxs-lookup"><span data-stu-id="29716-137">While code access security might stop malicious code from accessing resources, such code could still read values of your fields or properties that might contain sensitive information.</span></span>

<span data-ttu-id="29716-138">此外，如果您的程式碼接受網際網路或其他不可靠來源的使用者輸入，您也必須小心惡意輸入。</span><span class="sxs-lookup"><span data-stu-id="29716-138">Additionally, if your code accepts user input from the Internet or other unreliable sources, you must be careful about malicious input.</span></span>

## <a name="managed-wrapper-to-native-code-implementation"></a><span data-ttu-id="29716-139">原生程式碼執行的 Managed 包裝函式</span><span class="sxs-lookup"><span data-stu-id="29716-139">Managed wrapper to native code implementation</span></span>

<span data-ttu-id="29716-140">在這個案例中，通常某些有用的功能是在您想提供給 Managed 程式碼的機器碼中所實作。</span><span class="sxs-lookup"><span data-stu-id="29716-140">Typically in this scenario, some useful functionality is implemented in native code that you want to make available to managed code.</span></span> <span data-ttu-id="29716-141">使用平台叫用或 COM Interop 就可輕鬆撰寫 Managed 包裝函式。</span><span class="sxs-lookup"><span data-stu-id="29716-141">Managed wrappers are easy to write using either platform invoke or COM interop.</span></span> <span data-ttu-id="29716-142">但是，如果您這麼做，包裝函式的呼叫端就必須具有 Unmanaged 程式碼的權限才會成功。</span><span class="sxs-lookup"><span data-stu-id="29716-142">However, if you do this, callers of your wrappers must have unmanaged code rights in order to succeed.</span></span> <span data-ttu-id="29716-143">在 [預設原則] 底下，這表示從內部網路或網際網路下載的程式碼不會與包裝函式一起使用。</span><span class="sxs-lookup"><span data-stu-id="29716-143">Under default policy, this means that code downloaded from an intranet or the Internet won't work with the wrappers.</span></span>

<span data-ttu-id="29716-144">除了將非受控程式碼許可權提供給使用這些包裝函式的所有應用程式，最好只將這些許可權授與包裝函式程式碼。</span><span class="sxs-lookup"><span data-stu-id="29716-144">Instead of giving unmanaged code rights to all applications that use these wrappers, it's better to give these rights only to the wrapper code.</span></span> <span data-ttu-id="29716-145">如果基礎功能未公開任何資源而且實作也一樣安全，包裝函式就只需要判斷它的權限，讓任何程式碼都可以透過它來呼叫。</span><span class="sxs-lookup"><span data-stu-id="29716-145">If the underlying functionality exposes no resources and the implementation is likewise safe, the wrapper only needs to assert its rights, which enables any code to call through it.</span></span> <span data-ttu-id="29716-146">當牽涉到資源時，安全性程式碼撰寫應該與下一章節說明的程式庫程式碼的狀況相同。</span><span class="sxs-lookup"><span data-stu-id="29716-146">When resources are involved, security coding should be the same as the library code case described in the next section.</span></span> <span data-ttu-id="29716-147">由於包裝函式對這些資源而言是可能公開的呼叫端，因此小心驗證機器碼安全性的程序是必要的，而且這個程序必須由包裝函式負責執行。</span><span class="sxs-lookup"><span data-stu-id="29716-147">Because the wrapper is potentially exposing callers to these resources, careful verification of the safety of the native code is necessary and is the wrapper's responsibility.</span></span>

## <a name="library-code-that-exposes-protected-resources"></a><span data-ttu-id="29716-148">公開受保護資源的程式庫程式碼</span><span class="sxs-lookup"><span data-stu-id="29716-148">Library code that exposes protected resources</span></span>

<span data-ttu-id="29716-149">下列方法最強大，因此可能會有危險 (如果不正確地進行安全性編碼) ：您的程式庫可作為介面，讓其他程式碼存取某些無法使用的特定資源，就像 .NET 類別會強制執行所用資源的許可權一樣。</span><span class="sxs-lookup"><span data-stu-id="29716-149">The following approach is the most powerful and hence potentially dangerous (if done incorrectly) for security coding: your library serves as an interface for other code to access certain resources that aren't otherwise available, just as the .NET classes enforce permissions for the resources they use.</span></span> <span data-ttu-id="29716-150">不論您在何處公開資源，您的程式都必須先要求適用於資源的使用權限 (亦即它必須執行安全性檢查)，然後再判斷它的權限，以執行實際的作業。</span><span class="sxs-lookup"><span data-stu-id="29716-150">Wherever you expose a resource, your code must first demand the permission appropriate to the resource (that is, it must perform a security check) and then typically assert its rights to perform the actual operation.</span></span>

## <a name="see-also"></a><span data-ttu-id="29716-151">另請參閱</span><span class="sxs-lookup"><span data-stu-id="29716-151">See also</span></span>

- [<span data-ttu-id="29716-152">設定狀態資料的安全性</span><span class="sxs-lookup"><span data-stu-id="29716-152">Securing State Data</span></span>](securing-state-data.md)
- [<span data-ttu-id="29716-153">安全性和使用者輸入</span><span class="sxs-lookup"><span data-stu-id="29716-153">Security and User Input</span></span>](security-and-user-input.md)
- [<span data-ttu-id="29716-154">安全性和競爭情形</span><span class="sxs-lookup"><span data-stu-id="29716-154">Security and Race Conditions</span></span>](security-and-race-conditions.md)
- [<span data-ttu-id="29716-155">安全性和產生作業中的程式碼</span><span class="sxs-lookup"><span data-stu-id="29716-155">Security and On-the-Fly Code Generation</span></span>](security-and-on-the-fly-code-generation.md)
- [<span data-ttu-id="29716-156">以角色為基礎的安全性</span><span class="sxs-lookup"><span data-stu-id="29716-156">Role-Based Security</span></span>](role-based-security.md)
- [<span data-ttu-id="29716-157">ASP.NET Core 安全性</span><span class="sxs-lookup"><span data-stu-id="29716-157">ASP.NET Core Security</span></span>](/aspnet/core/security/)
