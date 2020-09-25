---
title: 安全性概觀
ms.date: 03/30/2017
ms.assetid: 33e09965-61d5-48cc-9e8c-3b047cc4f194
ms.openlocfilehash: ede9b24828da74c043bed103595073c4607c51f2
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91188989"
---
# <a name="security-overview"></a><span data-ttu-id="840e1-102">安全性概觀</span><span class="sxs-lookup"><span data-stu-id="840e1-102">Security overview</span></span>

<span data-ttu-id="840e1-103">保護應用程式是持續進行的工作。</span><span class="sxs-lookup"><span data-stu-id="840e1-103">Securing an application is an ongoing process.</span></span> <span data-ttu-id="840e1-104">開發人員無法絕對保證應用程式可避開所有攻擊，因為您無法預測未來的新科技會帶來哪些類型的攻擊。</span><span class="sxs-lookup"><span data-stu-id="840e1-104">There will never be a point where a developer can guarantee that an application is safe from all attacks, because it is impossible to predict what kinds of future attacks new technologies will bring about.</span></span> <span data-ttu-id="840e1-105">反之，也不能因為至目前為止，沒有人察覺 (或公佈) 系統上的安全性漏洞，就表示安全性漏洞確實存在或確實不存在。</span><span class="sxs-lookup"><span data-stu-id="840e1-105">Conversely, just because nobody has yet discovered (or published) security flaws in a system does not mean that none exist or could exist.</span></span> <span data-ttu-id="840e1-106">您需要在專案的設計階段就進行安全性的規劃，也必須規劃該如何在應用程式的存留期維護安全性。</span><span class="sxs-lookup"><span data-stu-id="840e1-106">You need to plan for security during the design phase of the project, as well as plan how security will be maintained over the lifetime of the application.</span></span>

## <a name="design-for-security"></a><span data-ttu-id="840e1-107">安全性設計</span><span class="sxs-lookup"><span data-stu-id="840e1-107">Design for Security</span></span>

 <span data-ttu-id="840e1-108">開發安全的應用程式時，必須面臨的其中一個最大的問題，就是安全性通常是後續補充動作，也就是在完成專案程式碼後才會實際列入考量。</span><span class="sxs-lookup"><span data-stu-id="840e1-108">One of the biggest problems in developing secure applications is that security is often an afterthought, something to implement after a project is code-complete.</span></span> <span data-ttu-id="840e1-109">未在一開始就將安全性納入應用程式會導致應用程式變得不安全，因為對應用程式安全性所做的考量太少。</span><span class="sxs-lookup"><span data-stu-id="840e1-109">Not building security into an application at the outset leads to insecure applications because little thought has been given to what makes an application secure.</span></span>

 <span data-ttu-id="840e1-110">最後一分鐘的安全性實行會導致更多錯誤，因為軟體會在新的限制下中斷，或必須重寫以容納無法預期的功能。</span><span class="sxs-lookup"><span data-stu-id="840e1-110">Last-minute security implementation leads to more bugs, as software breaks under the new restrictions or has to be rewritten to accommodate unanticipated functionality.</span></span> <span data-ttu-id="840e1-111">每行修改的程式碼都可能會引進新的錯誤。</span><span class="sxs-lookup"><span data-stu-id="840e1-111">Every line of revised code contains the possibility of introducing a new bug.</span></span> <span data-ttu-id="840e1-112">因此，您應該在開發過程中儘早考慮安全性，以便在開發新功能時一併處理。</span><span class="sxs-lookup"><span data-stu-id="840e1-112">For this reason, you should consider security early in the development process so that it can proceed in tandem with the development of new features.</span></span>

### <a name="threat-modeling"></a><span data-ttu-id="840e1-113">威脅模型</span><span class="sxs-lookup"><span data-stu-id="840e1-113">Threat Modeling</span></span>

 <span data-ttu-id="840e1-114">除非您了解系統可能遭受的所有潛伏攻擊，否則就無法保護系統。</span><span class="sxs-lookup"><span data-stu-id="840e1-114">You cannot protect a system against attack unless you understand all the potential attacks that it is exposed to.</span></span> <span data-ttu-id="840e1-115">評估安全性威脅的程式（稱為 *威脅分析模型*），是判斷 ADO.NET 應用程式中安全性缺口的可能性和後果的必要程式。</span><span class="sxs-lookup"><span data-stu-id="840e1-115">The process of evaluating security threats, called *threat modeling*, is necessary to determine the likelihood and ramifications of security breaches in your ADO.NET application.</span></span>

 <span data-ttu-id="840e1-116">威脅模型是由三個高階步驟所組成：了解敵人的觀點、描繪系統安全性的特徵，以及判斷威脅來源。</span><span class="sxs-lookup"><span data-stu-id="840e1-116">Threat modeling is composed of three high-level steps: understanding the adversary’s view, characterizing the security of the system, and determining threats.</span></span>

 <span data-ttu-id="840e1-117">威脅模型是一種反覆性的方法，可評估應用程式中的漏洞，找出因為會公開最機密的資料而最具危險性的漏洞。</span><span class="sxs-lookup"><span data-stu-id="840e1-117">Threat modeling is an iterative approach to assessing vulnerabilities in your application to find those that are the most dangerous because they expose the most sensitive data.</span></span> <span data-ttu-id="840e1-118">一旦找出漏洞之後，就要依照嚴重性順序來加以分類，並建立具有優先順序的反制措施來對抗這些威脅。</span><span class="sxs-lookup"><span data-stu-id="840e1-118">Once you identify the vulnerabilities, you rank them in order of severity and create a prioritized set of countermeasures to counter the threats.</span></span>

<span data-ttu-id="840e1-119">如需詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="840e1-119">For more information, see the following resources:</span></span>

|<span data-ttu-id="840e1-120">資源</span><span class="sxs-lookup"><span data-stu-id="840e1-120">Resource</span></span>|<span data-ttu-id="840e1-121">描述</span><span class="sxs-lookup"><span data-stu-id="840e1-121">Description</span></span>|
|--------------|-----------------|
|<span data-ttu-id="840e1-122">安全性工程入口網站上的 [威脅模型](https://www.microsoft.com/securityengineering/sdl/threatmodeling) 化網站</span><span class="sxs-lookup"><span data-stu-id="840e1-122">The [Threat Modeling](https://www.microsoft.com/securityengineering/sdl/threatmodeling) site on the Security Engineering Portal</span></span>|<span data-ttu-id="840e1-123">此網頁上的資源可協助您了解威脅模型程序，並建立可用來確保應用程式安全性的威脅模型。</span><span class="sxs-lookup"><span data-stu-id="840e1-123">The resources on this page will help you understand the threat modeling process and build threat models that you can use to secure your own applications</span></span>|

## <a name="the-principle-of-least-privilege"></a><span data-ttu-id="840e1-124">最小權限的原則</span><span class="sxs-lookup"><span data-stu-id="840e1-124">The Principle of Least Privilege</span></span>

 <span data-ttu-id="840e1-125">在設計、建立及部署應用程式時，必須假設應用程式將遭受攻擊。</span><span class="sxs-lookup"><span data-stu-id="840e1-125">When you design, build, and deploy your application, you must assume that your application will be attacked.</span></span> <span data-ttu-id="840e1-126">這些攻擊往往來自惡意程式碼，而這些程式碼常藉由執行程式碼的使用者權限而執行。</span><span class="sxs-lookup"><span data-stu-id="840e1-126">Often these attacks come from malicious code that executes with the permissions of the user running the code.</span></span> <span data-ttu-id="840e1-127">其他攻擊則可能源自本意良好，但遭到攻擊者利用的程式碼。</span><span class="sxs-lookup"><span data-stu-id="840e1-127">Others can originate with well-intentioned code that has been exploited by an attacker.</span></span> <span data-ttu-id="840e1-128">在規劃安全性時，請務必假設會發生最糟的狀況。</span><span class="sxs-lookup"><span data-stu-id="840e1-128">When planning security, always assume the worst-case scenario will occur.</span></span>

 <span data-ttu-id="840e1-129">您可以運用的一種反制措施，是使用最小權限執行並嘗試在程式碼周圍盡可能豎立起防線。</span><span class="sxs-lookup"><span data-stu-id="840e1-129">One counter-measure you can employ is to try to erect as many walls around your code as possible by running with least privilege.</span></span> <span data-ttu-id="840e1-130">根據最小權限的原則，應該針對完成工作所需的最短期間，將任何指定權限授與最少量的必要程式碼。</span><span class="sxs-lookup"><span data-stu-id="840e1-130">The principle of least privilege says that any given privilege should be granted to the least amount of code necessary for the shortest duration of time that is required to get the job done.</span></span>

 <span data-ttu-id="840e1-131">建立安全應用程式的最佳做法，是以完全沒有權限開始，然後加入執行特定工作的最少權限。</span><span class="sxs-lookup"><span data-stu-id="840e1-131">The best practice for creating secure applications is to start with no permissions at all and then add the narrowest permissions for the particular task being performed.</span></span> <span data-ttu-id="840e1-132">相反地，如果開始時使用全部的權限，然後再拒絕個別的權限，則會造成難以測試及維護的不安全應用程式，因為可能會因為不小心授與超出必要的權限而導致安全性漏洞。</span><span class="sxs-lookup"><span data-stu-id="840e1-132">By contrast, starting with all permissions and then denying individual ones leads to insecure applications that are difficult to test and maintain because security holes may exist from unintentionally granting more permissions than required.</span></span>

<span data-ttu-id="840e1-133">如需保護應用程式的詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="840e1-133">For more information on securing your applications, see the following resources:</span></span>

|<span data-ttu-id="840e1-134">資源</span><span class="sxs-lookup"><span data-stu-id="840e1-134">Resource</span></span>|<span data-ttu-id="840e1-135">描述</span><span class="sxs-lookup"><span data-stu-id="840e1-135">Description</span></span>|
|--------------|-----------------|
|[<span data-ttu-id="840e1-136">保護應用程式</span><span class="sxs-lookup"><span data-stu-id="840e1-136">Securing Applications</span></span>](/visualstudio/ide/securing-applications)|<span data-ttu-id="840e1-137">包含一般安全性主題的連結，</span><span class="sxs-lookup"><span data-stu-id="840e1-137">Contains links to general security topics.</span></span> <span data-ttu-id="840e1-138">也包含保護分散式應用程式、Web 應用程式、行動應用程式和桌面應用程式等主題的連結。</span><span class="sxs-lookup"><span data-stu-id="840e1-138">Also contains links to topics for securing distributed applications, Web applications, mobile applications, and desktop applications.</span></span>|

## <a name="code-access-security-cas"></a><span data-ttu-id="840e1-139">程式碼存取安全性 (CAS)</span><span class="sxs-lookup"><span data-stu-id="840e1-139">Code Access Security (CAS)</span></span>

<span data-ttu-id="840e1-140">程式碼存取安全性 (CAS) 是一種機制，有助於限制程式碼對受保護資源及作業的存取。</span><span class="sxs-lookup"><span data-stu-id="840e1-140">Code access security (CAS) is a mechanism that helps limit the access that code has to protected resources and operations.</span></span> <span data-ttu-id="840e1-141">在 .NET Framework 中，CAS 可執行下列功能：</span><span class="sxs-lookup"><span data-stu-id="840e1-141">In the .NET Framework, CAS performs the following functions:</span></span>

- <span data-ttu-id="840e1-142">定義代表存取各種系統資源之權利的權限和權限集合。</span><span class="sxs-lookup"><span data-stu-id="840e1-142">Defines permissions and permission sets that represent the right to access various system resources.</span></span>

- <span data-ttu-id="840e1-143">使權限集合與程式碼群組產生關聯，讓系統管理員得以設定安全性原則。</span><span class="sxs-lookup"><span data-stu-id="840e1-143">Enables administrators to configure security policy by associating sets of permissions with groups of code (code groups).</span></span>

- <span data-ttu-id="840e1-144">讓程式碼能夠要求執行所需的權限及有用的權限，並可指定程式碼絕對不可擁有的權限。</span><span class="sxs-lookup"><span data-stu-id="840e1-144">Enables code to request the permissions it requires in order to run, as well as the permissions that would be useful to have, and specifies which permissions the code must never have.</span></span>

- <span data-ttu-id="840e1-145">根據程式碼要求的權限以及安全性原則允許的作業，對每個載入的組件 (Assembly) 授與權限。</span><span class="sxs-lookup"><span data-stu-id="840e1-145">Grants permissions to each assembly that is loaded, based on the permissions requested by the code and on the operations permitted by security policy.</span></span>

- <span data-ttu-id="840e1-146">讓程式碼得以要求其呼叫端必須具備特定的權限。</span><span class="sxs-lookup"><span data-stu-id="840e1-146">Enables code to demand that its callers have specific permissions.</span></span>

- <span data-ttu-id="840e1-147">使程式碼要求它的呼叫端處理數位簽章，而只允許特定組織或站台的呼叫端可以呼叫受保護的程式碼。</span><span class="sxs-lookup"><span data-stu-id="840e1-147">Enables code to demand that its callers possess a digital signature, thus allowing only callers from a particular organization or site to call the protected code.</span></span>

- <span data-ttu-id="840e1-148">藉由比較呼叫堆疊上授與每個呼叫端的權限與呼叫端必須具備的權限，在執行階段對程式碼強制執行限制。</span><span class="sxs-lookup"><span data-stu-id="840e1-148">Enforces restrictions on code at run time by comparing the granted permissions of every caller on the call stack to the permissions that callers must have.</span></span>

<span data-ttu-id="840e1-149">若要將攻擊成功時所可能發生的損害程度降至最低，請在選擇程式碼的安全性內容時，僅授與完成工作所需資源的存取權。</span><span class="sxs-lookup"><span data-stu-id="840e1-149">To minimize the amount of damage that can occur if an attack succeeds, choose a security context for your code that grants access only to the resources it needs to get its work done and no more.</span></span>

<span data-ttu-id="840e1-150">如需詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="840e1-150">For more information, see the following resources:</span></span>

|<span data-ttu-id="840e1-151">資源</span><span class="sxs-lookup"><span data-stu-id="840e1-151">Resource</span></span>|<span data-ttu-id="840e1-152">描述</span><span class="sxs-lookup"><span data-stu-id="840e1-152">Description</span></span>|
|--------------|-----------------|
|[<span data-ttu-id="840e1-153">程式碼存取安全性和 ADO.NET</span><span class="sxs-lookup"><span data-stu-id="840e1-153">Code Access Security and ADO.NET</span></span>](code-access-security.md)|<span data-ttu-id="840e1-154">從 ADO.NET 應用程式的角度，描述在程式碼存取安全性、以角色為基礎的安全性與部分信任環境之間的互動。</span><span class="sxs-lookup"><span data-stu-id="840e1-154">Describes the interactions between code access security, role-based security, and partially trusted environments from the perspective of an ADO.NET application.</span></span>|
|[<span data-ttu-id="840e1-155">程式碼存取安全性</span><span class="sxs-lookup"><span data-stu-id="840e1-155">Code Access Security</span></span>](../../misc/code-access-security.md)|<span data-ttu-id="840e1-156">包含說明 .NET Framework 中的 CAS 的其他主題連結。</span><span class="sxs-lookup"><span data-stu-id="840e1-156">Contains links to additional topics describing CAS in the .NET Framework.</span></span>|

## <a name="database-security"></a><span data-ttu-id="840e1-157">資料庫安全性</span><span class="sxs-lookup"><span data-stu-id="840e1-157">Database Security</span></span>

<span data-ttu-id="840e1-158">最小權限的原則也適用於資料來源。</span><span class="sxs-lookup"><span data-stu-id="840e1-158">The principle of least privilege also applies to your data source.</span></span> <span data-ttu-id="840e1-159">資料庫安全性的一些一般方針包括：</span><span class="sxs-lookup"><span data-stu-id="840e1-159">Some general guidelines for database security include:</span></span>

- <span data-ttu-id="840e1-160">建立具有最低可能權限的帳戶。</span><span class="sxs-lookup"><span data-stu-id="840e1-160">Create accounts with the lowest possible privileges.</span></span>

- <span data-ttu-id="840e1-161">不允許使用者只為了讓程式碼運作就存取管理帳戶。</span><span class="sxs-lookup"><span data-stu-id="840e1-161">Do not allow users access to administrative accounts just to get code working.</span></span>

- <span data-ttu-id="840e1-162">不將伺服器端的錯誤訊息傳回至用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="840e1-162">Do not return server-side error messages to client applications.</span></span>

- <span data-ttu-id="840e1-163">驗證所有在用戶端及伺服器端的輸入。</span><span class="sxs-lookup"><span data-stu-id="840e1-163">Validate all input at both the client and the server.</span></span>

- <span data-ttu-id="840e1-164">使用參數化命令並避免動態 SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="840e1-164">Use parameterized commands and avoid dynamic SQL statements.</span></span>

- <span data-ttu-id="840e1-165">為正在使用的資料庫啟用安全性稽核和記錄功能，使您可以接到任何安全性破壞的警示。</span><span class="sxs-lookup"><span data-stu-id="840e1-165">Enable security auditing and logging for the database you are using so that you are alerted to any security breaches.</span></span>

<span data-ttu-id="840e1-166">如需詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="840e1-166">For more information, see the following resources:</span></span>

|<span data-ttu-id="840e1-167">資源</span><span class="sxs-lookup"><span data-stu-id="840e1-167">Resource</span></span>|<span data-ttu-id="840e1-168">描述</span><span class="sxs-lookup"><span data-stu-id="840e1-168">Description</span></span>|
|--------------|-----------------|
|[<span data-ttu-id="840e1-169">SQL Server 安全性</span><span class="sxs-lookup"><span data-stu-id="840e1-169">SQL Server Security</span></span>](./sql/sql-server-security.md)|<span data-ttu-id="840e1-170">使用應用程式案例提供 SQL Server 安全性概觀，可針對建立以 SQL Server 為目標的安全 ADO.NET 應用程式提供指引。</span><span class="sxs-lookup"><span data-stu-id="840e1-170">Provides an overview of SQL Server security with application scenarios that provide guidance for creating secure ADO.NET applications that target SQL Server.</span></span>|
|<span data-ttu-id="840e1-171">[資料存取策略的建議](/previous-versions/visualstudio/visual-studio-2008/8fxztkff(v=vs.90))</span><span class="sxs-lookup"><span data-stu-id="840e1-171">[Recommendations for Data Access Strategies](/previous-versions/visualstudio/visual-studio-2008/8fxztkff(v=vs.90))</span></span>|<span data-ttu-id="840e1-172">提供存取資料及執行資料庫作業的建議。</span><span class="sxs-lookup"><span data-stu-id="840e1-172">Provides recommendations for accessing data and performing database operations.</span></span>|

## <a name="security-policy-and-administration"></a><span data-ttu-id="840e1-173">安全性原則和管理</span><span class="sxs-lookup"><span data-stu-id="840e1-173">Security Policy and Administration</span></span>

<span data-ttu-id="840e1-174">如果程式碼存取安全性 (CAS) 原則管理不當，可能會造成安全上的弱點。</span><span class="sxs-lookup"><span data-stu-id="840e1-174">Improperly administering code access security (CAS) policy can potentially create security weaknesses.</span></span> <span data-ttu-id="840e1-175">部署應用程式後，必須使用監視安全性的技術，並評估新威脅所帶來的風險。</span><span class="sxs-lookup"><span data-stu-id="840e1-175">Once an application is deployed, techniques for monitoring security should be used and risks evaluated as new threats emerge.</span></span>

<span data-ttu-id="840e1-176">如需詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="840e1-176">For more information, see the following resources:</span></span>

|<span data-ttu-id="840e1-177">資源</span><span class="sxs-lookup"><span data-stu-id="840e1-177">Resource</span></span>|<span data-ttu-id="840e1-178">描述</span><span class="sxs-lookup"><span data-stu-id="840e1-178">Description</span></span>|
|--------------|-----------------|
|<span data-ttu-id="840e1-179">[安全性原則管理](/previous-versions/dotnet/netframework-4.0/c1k0eed6(v=vs.100))</span><span class="sxs-lookup"><span data-stu-id="840e1-179">[Security Policy Management](/previous-versions/dotnet/netframework-4.0/c1k0eed6(v=vs.100))</span></span>|<span data-ttu-id="840e1-180">提供建立和管理安全性原則的資訊。</span><span class="sxs-lookup"><span data-stu-id="840e1-180">Provides information on creating and administering security policy.</span></span>|
|<span data-ttu-id="840e1-181">[安全性原則的最佳作法](/previous-versions/dotnet/netframework-4.0/sa4se9bc(v=vs.100))</span><span class="sxs-lookup"><span data-stu-id="840e1-181">[Security Policy Best Practices](/previous-versions/dotnet/netframework-4.0/sa4se9bc(v=vs.100))</span></span>|<span data-ttu-id="840e1-182">提供說明如何管理安全性原則的連結。</span><span class="sxs-lookup"><span data-stu-id="840e1-182">Provides links describing how to administer security policy.</span></span>|

## <a name="see-also"></a><span data-ttu-id="840e1-183">另請參閱</span><span class="sxs-lookup"><span data-stu-id="840e1-183">See also</span></span>

- [<span data-ttu-id="840e1-184">設定 ADO.NET 應用程式的安全性</span><span class="sxs-lookup"><span data-stu-id="840e1-184">Securing ADO.NET Applications</span></span>](securing-ado-net-applications.md)
- [<span data-ttu-id="840e1-185">.NET 的安全性</span><span class="sxs-lookup"><span data-stu-id="840e1-185">Security in .NET</span></span>](../../../standard/security/index.md)
- [<span data-ttu-id="840e1-186">SQL Server 安全性</span><span class="sxs-lookup"><span data-stu-id="840e1-186">SQL Server Security</span></span>](./sql/sql-server-security.md)
- <span data-ttu-id="840e1-187">[ADO.NET 概觀](ado-net-overview.md) \(部分機器翻譯\)</span><span class="sxs-lookup"><span data-stu-id="840e1-187">[ADO.NET Overview](ado-net-overview.md)</span></span>
