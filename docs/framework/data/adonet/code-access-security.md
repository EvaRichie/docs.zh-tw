---
title: 程式碼存取安全性
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 93e099eb-daa1-4f1e-b031-c1e10a996f88
ms.openlocfilehash: c4c18e8026dc230db896103d29d40426dbd11f16
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91203835"
---
# <a name="code-access-security-and-adonet"></a><span data-ttu-id="218fd-102">程式碼存取安全性和 ADO.NET</span><span class="sxs-lookup"><span data-stu-id="218fd-102">Code Access Security and ADO.NET</span></span>

<span data-ttu-id="218fd-103">.NET Framework 會提供以角色為基礎的安全性和程式碼存取安全性 (CAS)，而這兩種安全性都是使用 Common Language Runtime (CLR) 所提供的通用基礎結構所實作的。</span><span class="sxs-lookup"><span data-stu-id="218fd-103">The .NET Framework offers role-based security as well as code access security (CAS), both of which are implemented using a common infrastructure supplied by the common language runtime (CLR).</span></span> <span data-ttu-id="218fd-104">在 Unmanaged 程式碼的作用範圍內，大多數應用程式都是以使用者或主體的權限執行。</span><span class="sxs-lookup"><span data-stu-id="218fd-104">In the world of unmanaged code, most applications execute with the permissions of the user or principal.</span></span> <span data-ttu-id="218fd-105">因此，當擁有更高權限的使用者執行惡意或充滿錯誤的軟體時，就可能損害電腦系統和竊取私人資料。</span><span class="sxs-lookup"><span data-stu-id="218fd-105">As a result, computer systems can be damaged and private data compromised when malicious or error-filled software is run by a user with elevated privileges.</span></span>  
  
 <span data-ttu-id="218fd-106">相較之下，在 .NET Framework 中執行的 Managed 程式碼具有單獨套用至程式碼的程式碼存取安全性。</span><span class="sxs-lookup"><span data-stu-id="218fd-106">By contrast, managed code executing in the .NET Framework includes code access security, which applies to code alone.</span></span> <span data-ttu-id="218fd-107">系統是否允許執行程式碼會取決於程式碼的來源或程式碼識別的其他層面，而非單獨取決於主體的識別。</span><span class="sxs-lookup"><span data-stu-id="218fd-107">Whether the code is allowed to run or not depends on the code's origin or other aspects of the code's identity, not solely the identity of the principal.</span></span> <span data-ttu-id="218fd-108">這能降低 Managed 程式碼被誤用的可能性。</span><span class="sxs-lookup"><span data-stu-id="218fd-108">This reduces the likelihood that managed code can be misused.</span></span>  
  
## <a name="code-access-permissions"></a><span data-ttu-id="218fd-109">程式碼存取權限</span><span class="sxs-lookup"><span data-stu-id="218fd-109">Code Access Permissions</span></span>  

 <span data-ttu-id="218fd-110">執行程式碼時，它會顯示 CLR 安全性系統所評估的辨識項。</span><span class="sxs-lookup"><span data-stu-id="218fd-110">When code is executed, it presents evidence that is evaluated by the CLR security system.</span></span> <span data-ttu-id="218fd-111">一般來說，這個辨識項會洩露程式碼的來源，包含 URL、大小和區域，以及用來確保組件識別的數位簽章。</span><span class="sxs-lookup"><span data-stu-id="218fd-111">Typically, this evidence comprises the origin of the code including URL, site, and zone, and digital signatures that ensure the identity of the assembly.</span></span>  
  
 <span data-ttu-id="218fd-112">CLR 僅允許程式碼執行該程式碼有權執行的這些作業。</span><span class="sxs-lookup"><span data-stu-id="218fd-112">The CLR allows code to perform only those operations that the code has permission to perform.</span></span> <span data-ttu-id="218fd-113">程式碼可以要求權限，而且系統會根據系統管理員所設定的安全性原則來接受這些要求。</span><span class="sxs-lookup"><span data-stu-id="218fd-113">Code can request permissions, and those requests are honored based on the security policy set by an administrator.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="218fd-114">CLR 中執行的程式碼不能授與其本身的使用權限。</span><span class="sxs-lookup"><span data-stu-id="218fd-114">Code executing in the CLR cannot grant permissions to itself.</span></span> <span data-ttu-id="218fd-115">例如，程式碼可以要求而且被授與少於安全性原則允許的權限，但是它絕不會被授與更多權限。</span><span class="sxs-lookup"><span data-stu-id="218fd-115">For example, code can request and be granted fewer permissions than a security policy allows, but it will never be granted more permissions.</span></span> <span data-ttu-id="218fd-116">授與權限時，系統是以完全沒有權限開始，然後加入執行特定工作的最少權限。</span><span class="sxs-lookup"><span data-stu-id="218fd-116">When granting permissions, start with no permissions at all and then add the narrowest permissions for the particular task being performed.</span></span> <span data-ttu-id="218fd-117">如果一開始便使用所有權限，然後再拒絕個別的權限，則會造成應用程式不安全，因為可能會授與超出必要的權限而導致意外安全性漏洞。</span><span class="sxs-lookup"><span data-stu-id="218fd-117">Starting with all permissions and then denying individual ones leads to insecure applications that may contain unintentional security holes from granting more permissions than required.</span></span> <span data-ttu-id="218fd-118">如需詳細資訊，請參閱設定 [安全性原則](/previous-versions/dotnet/netframework-4.0/7c9c2y1w(v=vs.100)) 和 [安全性原則管理](/previous-versions/dotnet/netframework-4.0/c1k0eed6(v=vs.100))。</span><span class="sxs-lookup"><span data-stu-id="218fd-118">For more information, see [Configuring Security Policy](/previous-versions/dotnet/netframework-4.0/7c9c2y1w(v=vs.100)) and [Security Policy Management](/previous-versions/dotnet/netframework-4.0/c1k0eed6(v=vs.100)).</span></span>  
  
 <span data-ttu-id="218fd-119">程式碼存取權限有三種類型：</span><span class="sxs-lookup"><span data-stu-id="218fd-119">There are three types of code access permissions:</span></span>  
  
- <span data-ttu-id="218fd-120">`Code access permissions`衍生自 <xref:System.Security.CodeAccessPermission> 類別。</span><span class="sxs-lookup"><span data-stu-id="218fd-120">`Code access permissions` derive from the <xref:System.Security.CodeAccessPermission> class.</span></span> <span data-ttu-id="218fd-121">為了存取受保護資源 (例如檔案和環境變數) 以及執行受保護作業 (例如存取 Unmanaged 程式碼)，因此需要權限。</span><span class="sxs-lookup"><span data-stu-id="218fd-121">Permissions are required in order to access protected resources, such as files and environment variables, and to perform protected operations, such as accessing unmanaged code.</span></span>  
  
- <span data-ttu-id="218fd-122">`Identity permissions` 代表可識別組件的特性。</span><span class="sxs-lookup"><span data-stu-id="218fd-122">`Identity permissions` represent characteristics that identify an assembly.</span></span> <span data-ttu-id="218fd-123">系統會根據辨識項 (可能包含數位簽章或程式碼來源等項目)，將權限授與組件。</span><span class="sxs-lookup"><span data-stu-id="218fd-123">Permissions are granted to an assembly based on evidence, which can include items such as a digital signature or where the code originated.</span></span> <span data-ttu-id="218fd-124">識別權限也衍生自 <xref:System.Security.CodeAccessPermission> 基底類別 (Base Class)。</span><span class="sxs-lookup"><span data-stu-id="218fd-124">Identity permissions also derive from the <xref:System.Security.CodeAccessPermission> base class.</span></span>  
  
- <span data-ttu-id="218fd-125">`Role-based security permissions`是以主體是否具有指定的識別或屬於指定角色成員為基礎。</span><span class="sxs-lookup"><span data-stu-id="218fd-125">`Role-based security permissions` are based on whether a principal has a specified identity or is a member of a specified role.</span></span> <span data-ttu-id="218fd-126"><xref:System.Security.Permissions.PrincipalPermission> 類別允許針對使用中主體進行宣告式和必要的權限檢查。</span><span class="sxs-lookup"><span data-stu-id="218fd-126">The <xref:System.Security.Permissions.PrincipalPermission> class allows both declarative and imperative permission checks against the active principal.</span></span>  
  
 <span data-ttu-id="218fd-127">為了判斷程式碼是否經授權可存取資源或執行某項作業，執行階段的安全性系統會周遊呼叫堆疊，並比較每個呼叫端被授與的權限與要求的權限。</span><span class="sxs-lookup"><span data-stu-id="218fd-127">To determine whether code is authorized to access a resource or perform an operation, the runtime's security system traverses the call stack, comparing the granted permissions of each caller to the permission being demanded.</span></span> <span data-ttu-id="218fd-128">如果呼叫堆疊中的任何呼叫端沒有要求的權限，系統就會擲回 <xref:System.Security.SecurityException> 並拒絕存取。</span><span class="sxs-lookup"><span data-stu-id="218fd-128">If any caller in the call stack does not have the demanded permission, a <xref:System.Security.SecurityException> is thrown and access is refused.</span></span>  
  
### <a name="requesting-permissions"></a><span data-ttu-id="218fd-129">要求權限</span><span class="sxs-lookup"><span data-stu-id="218fd-129">Requesting Permissions</span></span>  

 <span data-ttu-id="218fd-130">要求權限的目的是向執行階段通知您的應用程式需要哪些權限才能執行，以及確保它只會收到實際需要的權限。</span><span class="sxs-lookup"><span data-stu-id="218fd-130">The purpose of requesting permissions is to inform the runtime which permissions your application requires in order to run, and to ensure that it receives only the permissions that it actually needs.</span></span> <span data-ttu-id="218fd-131">例如，如果您的應用程式必須將資料寫入本機磁碟，它就需要 <xref:System.Security.Permissions.FileIOPermission>。</span><span class="sxs-lookup"><span data-stu-id="218fd-131">For example, if your application needs to write data to the local disk, it requires <xref:System.Security.Permissions.FileIOPermission>.</span></span> <span data-ttu-id="218fd-132">如果系統沒有授與該權限，當此應用程式嘗試寫入磁碟時，它就會失敗。</span><span class="sxs-lookup"><span data-stu-id="218fd-132">If that permission hasn't been granted, the application will fail when it attempts to write to the disk.</span></span> <span data-ttu-id="218fd-133">不過，如果應用程式要求 `FileIOPermission`，但系統沒有授與該權限，則此應用程式一開始將產生例外狀況而且不會載入。</span><span class="sxs-lookup"><span data-stu-id="218fd-133">However, if the application requests `FileIOPermission` and that permission has not been granted, the application will generate the exception at the outset and will not load.</span></span>  
  
 <span data-ttu-id="218fd-134">在應用程式僅需要從磁碟中讀取資料的情況下，您可以要求絕不授與任何寫入權限給應用程式。</span><span class="sxs-lookup"><span data-stu-id="218fd-134">In a scenario where the application only needs to read data from the disk, you can request that it never be granted any write permissions.</span></span> <span data-ttu-id="218fd-135">在錯誤或惡意攻擊的事件中，您的程式碼無法破壞它所運作的資料。</span><span class="sxs-lookup"><span data-stu-id="218fd-135">In the event of a bug or a malicious attack, your code cannot damage the data on which it operates.</span></span> <span data-ttu-id="218fd-136">如需詳細資訊，請參閱 [要求許可權](/previous-versions/dotnet/netframework-4.0/yd267cce(v=vs.100))。</span><span class="sxs-lookup"><span data-stu-id="218fd-136">For more information, see [Requesting Permissions](/previous-versions/dotnet/netframework-4.0/yd267cce(v=vs.100)).</span></span>  
  
## <a name="role-based-security-and-cas"></a><span data-ttu-id="218fd-137">以角色為基礎的安全性和 CAS</span><span class="sxs-lookup"><span data-stu-id="218fd-137">Role-Based Security and CAS</span></span>  

 <span data-ttu-id="218fd-138">同時實作以角色為基礎的安全性和程式碼存取安全性 (CAS) 可強化應用程式的整體安全性。</span><span class="sxs-lookup"><span data-stu-id="218fd-138">Implementing both role-based security and code-accessed security (CAS) enhances overall security for your application.</span></span> <span data-ttu-id="218fd-139">以角色為基礎的安全性可以根據 Windows 帳戶或自訂識別，將安全性主體的相關資訊提供給目前的執行緒。</span><span class="sxs-lookup"><span data-stu-id="218fd-139">Role-based security can be based on a Windows account or a custom identity, making information about the security principal available to the current thread.</span></span> <span data-ttu-id="218fd-140">此外，應用程式通常會根據使用者所提供的認證，提供對資料或資源的存取。</span><span class="sxs-lookup"><span data-stu-id="218fd-140">In addition, applications are often required to provide access to data or resources based on credentials supplied by the user.</span></span> <span data-ttu-id="218fd-141">基本上，這類應用程式會檢查使用者的角色並根據這些角色提供資源存取。</span><span class="sxs-lookup"><span data-stu-id="218fd-141">Typically, such applications check the role of a user and provide access to resources based on those roles.</span></span>  
  
 <span data-ttu-id="218fd-142">以角色為基礎的安全性可讓某個元件在執行階段識別目前的使用者及其相關聯的角色。</span><span class="sxs-lookup"><span data-stu-id="218fd-142">Role-based security enables a component to identify current users and their associated roles at run time.</span></span> <span data-ttu-id="218fd-143">然後，系統會使用 CAS 原則來對應這項資訊，以便判斷在執行階段授與的權限集合。</span><span class="sxs-lookup"><span data-stu-id="218fd-143">This information is then mapped using a CAS policy to determine the set of permissions granted at run time.</span></span> <span data-ttu-id="218fd-144">若為指定的應用程式定義域，主應用程式 (Host) 就可以變更預設的以角色為基礎安全性原則，並且設定預設的安全性主體，以便代表某位使用者以及與該使用相關聯的角色。</span><span class="sxs-lookup"><span data-stu-id="218fd-144">For a specified application domain, the host can change the default role-based security policy and set a default security principal that represents a user and the roles associated with that user.</span></span>  
  
 <span data-ttu-id="218fd-145">CLR 會使用某些權限來實作在 Managed 程式碼上強制執行限制的機制。</span><span class="sxs-lookup"><span data-stu-id="218fd-145">The CLR uses permissions to implement its mechanism for enforcing restrictions on managed code.</span></span> <span data-ttu-id="218fd-146">以角色為基礎的安全性權限會提供一項機制，讓您探索某位使用者 (或代表使用者運作的代理程式) 是否具有特定識別或屬於指定角色的成員。</span><span class="sxs-lookup"><span data-stu-id="218fd-146">Role-based security permissions provide a mechanism for discovering whether a user (or the agent acting on the user's behalf) has a particular identity or is a member of a specified role.</span></span> <span data-ttu-id="218fd-147">如需詳細資訊，請參閱 [安全性許可權](/previous-versions/dotnet/netframework-4.0/5ba4k1c5(v=vs.100))。</span><span class="sxs-lookup"><span data-stu-id="218fd-147">For more information, see [Security Permissions](/previous-versions/dotnet/netframework-4.0/5ba4k1c5(v=vs.100)).</span></span>  
  
 <span data-ttu-id="218fd-148">根據您所建立的應用程式類型，您也應該考慮在資料庫中實作以角色為基礎的權限。</span><span class="sxs-lookup"><span data-stu-id="218fd-148">Depending on the type of application you are building, you should also consider implementing role-based permissions in the database.</span></span> <span data-ttu-id="218fd-149">如需 SQL Server 中以角色為基礎之安全性的詳細資訊，請參閱 [SQL Server 安全性](./sql/sql-server-security.md)。</span><span class="sxs-lookup"><span data-stu-id="218fd-149">For more information on role-based security in SQL Server, see [SQL Server Security](./sql/sql-server-security.md).</span></span>  
  
## <a name="assemblies"></a><span data-ttu-id="218fd-150">組件</span><span class="sxs-lookup"><span data-stu-id="218fd-150">Assemblies</span></span>  

 <span data-ttu-id="218fd-151">組件會構成 .NET Framework 應用程式之部署、版本控制、重複使用、啟動範圍和安全性權限的基本單位。</span><span class="sxs-lookup"><span data-stu-id="218fd-151">Assemblies form the fundamental unit of deployment, version control, reuse, activation scoping, and security permissions for a .NET Framework application.</span></span> <span data-ttu-id="218fd-152">組件會提供針對一起運作而建立而且構成邏輯功能單位之類型和資源的組合。</span><span class="sxs-lookup"><span data-stu-id="218fd-152">An assembly provides a collection of types and resources that are built to work together and form a logical unit of functionality.</span></span> <span data-ttu-id="218fd-153">對 CLR 而言，類型不會存在組件內容外部。</span><span class="sxs-lookup"><span data-stu-id="218fd-153">To the CLR, a type does not exist outside the context of an assembly.</span></span> <span data-ttu-id="218fd-154">如需建立和部署元件的詳細資訊，請參閱 [使用元件進行程式設計](../../../standard/assembly/index.md)。</span><span class="sxs-lookup"><span data-stu-id="218fd-154">For more information on creating and deploying assemblies, see [Programming with Assemblies](../../../standard/assembly/index.md).</span></span>  
  
### <a name="strong-naming-assemblies"></a><span data-ttu-id="218fd-155">強式命名組件</span><span class="sxs-lookup"><span data-stu-id="218fd-155">Strong-naming Assemblies</span></span>  

 <span data-ttu-id="218fd-156">強式名稱 (Strong Name) 或數位簽章包含組件的識別，其中包括簡單文字名稱、版本號碼和文化特性資訊 (如果有提供的話)，以及公開金鑰 (Public Key) 和數位簽章。</span><span class="sxs-lookup"><span data-stu-id="218fd-156">A strong name, or digital signature, consists of the assembly's identity, which includes its simple text name, version number, and culture information (if provided), plus a public key and a digital signature.</span></span> <span data-ttu-id="218fd-157">數位簽章是從使用對應之私密金鑰的組件檔中產生的。</span><span class="sxs-lookup"><span data-stu-id="218fd-157">The digital signature is generated from an assembly file using the corresponding private key.</span></span> <span data-ttu-id="218fd-158">組件檔包含組件資訊清單 (Assembly Manifest)，其中包含組成組件之所有檔案的名稱和雜湊。</span><span class="sxs-lookup"><span data-stu-id="218fd-158">The assembly file contains the assembly manifest, which contains the names and hashes of all the files that make up the assembly.</span></span>  
  
 <span data-ttu-id="218fd-159">強式命名組件可提供應用程式或元件唯一的識別，讓其他軟體用來明確參考該應用程式或元件。</span><span class="sxs-lookup"><span data-stu-id="218fd-159">Strong naming an assembly gives an application or component a unique identity that other software can use to refer explicitly to it.</span></span> <span data-ttu-id="218fd-160">強式命名可保護組件，讓內含惡意程式碼的組件無法假冒該組件。</span><span class="sxs-lookup"><span data-stu-id="218fd-160">Strong naming guards assemblies against being spoofed by an assembly that contains hostile code.</span></span> <span data-ttu-id="218fd-161">此外，強式命名還能確保不同元件版本之間的版本一致性。</span><span class="sxs-lookup"><span data-stu-id="218fd-161">Strong-naming also ensures versioning consistency among different versions of a component.</span></span> <span data-ttu-id="218fd-162">您必須強式命名將部署到全域組件快取 (GAC) 的組件。</span><span class="sxs-lookup"><span data-stu-id="218fd-162">You must strong name assemblies that will be deployed to the Global Assembly Cache (GAC).</span></span> <span data-ttu-id="218fd-163">如需詳細資訊，請參閱[建立和使用強式名稱的組件](../../../standard/assembly/create-use-strong-named.md)。</span><span class="sxs-lookup"><span data-stu-id="218fd-163">For more information, see [Creating and Using Strong-Named Assemblies](../../../standard/assembly/create-use-strong-named.md).</span></span>  
  
## <a name="partial-trust-in-adonet-20"></a><span data-ttu-id="218fd-164">ADO.NET 2.0 中的部分信任</span><span class="sxs-lookup"><span data-stu-id="218fd-164">Partial Trust in ADO.NET 2.0</span></span>  

 <span data-ttu-id="218fd-165">在 ADO.NET 2.0 中，.NET Framework Data Provider for SQL Server、.NET Framework Data Provider for OLE DB、.NET Framework Data Provider for ODBC 和 .NET Framework Data Provider for Oracle 現在都可以在部分信任的環境中執行。</span><span class="sxs-lookup"><span data-stu-id="218fd-165">In ADO.NET 2.0, the .NET Framework Data Provider for SQL Server, the .NET Framework Data Provider for OLE DB, the .NET Framework Data Provider for ODBC, and the .NET Framework Data Provider for Oracle can now all run in partially trusted environments.</span></span> <span data-ttu-id="218fd-166">在舊版的 .NET Framework 中，只有 <xref:System.Data.SqlClient> 才能在低於完全信任的應用程式中使用。</span><span class="sxs-lookup"><span data-stu-id="218fd-166">In previous releases of the .NET Framework, only <xref:System.Data.SqlClient> was supported in less than full-trust applications.</span></span>  
  
 <span data-ttu-id="218fd-167">使用 SQL Server 提供者的部分信任應用程式至少必須具有執行和 <xref:System.Data.SqlClient.SqlClientPermission> 使用權限。</span><span class="sxs-lookup"><span data-stu-id="218fd-167">At minimum, a partially trusted application using the SQL Server provider must have execution and <xref:System.Data.SqlClient.SqlClientPermission> permissions.</span></span>  
  
### <a name="permission-attribute-properties-for-partial-trust"></a><span data-ttu-id="218fd-168">部分信任的使用權限屬性</span><span class="sxs-lookup"><span data-stu-id="218fd-168">Permission Attribute Properties for Partial Trust</span></span>  

 <span data-ttu-id="218fd-169">在部分信任案例中，可使用 <xref:System.Data.SqlClient.SqlClientPermissionAttribute> 成員進一步限制 SQL Server 的 .NET Framework 資料提供者之可用功能。</span><span class="sxs-lookup"><span data-stu-id="218fd-169">For partial trust scenarios, you can use <xref:System.Data.SqlClient.SqlClientPermissionAttribute> members to further restrict the capabilities available for the .NET Framework Data Provider for SQL Server.</span></span>  
  
 <span data-ttu-id="218fd-170">下列表格列出可用的 <xref:System.Data.SqlClient.SqlClientPermissionAttribute> 屬性及其說明：</span><span class="sxs-lookup"><span data-stu-id="218fd-170">The following table lists the available <xref:System.Data.SqlClient.SqlClientPermissionAttribute> properties and their descriptions:</span></span>  
  
|<span data-ttu-id="218fd-171">使用權限屬性</span><span class="sxs-lookup"><span data-stu-id="218fd-171">Permission attribute property</span></span>|<span data-ttu-id="218fd-172">描述</span><span class="sxs-lookup"><span data-stu-id="218fd-172">Description</span></span>|  
|-----------------------------------|-----------------|  
|`Action`|<span data-ttu-id="218fd-173">取得或設定安全性動作。</span><span class="sxs-lookup"><span data-stu-id="218fd-173">Gets or sets a security action.</span></span> <span data-ttu-id="218fd-174">繼承自 <xref:System.Security.Permissions.SecurityAttribute>。</span><span class="sxs-lookup"><span data-stu-id="218fd-174">Inherited from <xref:System.Security.Permissions.SecurityAttribute>.</span></span>|  
|`AllowBlankPassword`|<span data-ttu-id="218fd-175">啟用或停用在連接字串中使用空白密碼。</span><span class="sxs-lookup"><span data-stu-id="218fd-175">Enables or disables the use of a blank password in a connection string.</span></span> <span data-ttu-id="218fd-176">有效值為 `true` (表示啟用空白密碼) 和 `false` (表示停用空白密碼)。</span><span class="sxs-lookup"><span data-stu-id="218fd-176">Valid values are `true` (to enable the use of blank passwords) and `false` (to disable the use of blank passwords).</span></span> <span data-ttu-id="218fd-177">繼承自 <xref:System.Data.Common.DBDataPermissionAttribute>。</span><span class="sxs-lookup"><span data-stu-id="218fd-177">Inherited from <xref:System.Data.Common.DBDataPermissionAttribute>.</span></span>|  
|`ConnectionString`|<span data-ttu-id="218fd-178">識別允許的連接字串。</span><span class="sxs-lookup"><span data-stu-id="218fd-178">Identifies a permitted connection string.</span></span> <span data-ttu-id="218fd-179">可識別多個連接字串。</span><span class="sxs-lookup"><span data-stu-id="218fd-179">Multiple connection strings can be identified.</span></span> <span data-ttu-id="218fd-180">**注意：**  請勿在您的連接字串中包含使用者識別碼或密碼。</span><span class="sxs-lookup"><span data-stu-id="218fd-180">**Note:**  Do not include a user ID or password in your connection string.</span></span> <span data-ttu-id="218fd-181">在這個發行版本中，您無法使用 .NET Framework 組態工具變更連接字串限制。</span><span class="sxs-lookup"><span data-stu-id="218fd-181">In this release, you cannot change connection string restrictions using the .NET Framework Configuration Tool.</span></span> <br /><br /> <span data-ttu-id="218fd-182">繼承自 <xref:System.Data.Common.DBDataPermissionAttribute>。</span><span class="sxs-lookup"><span data-stu-id="218fd-182">Inherited from <xref:System.Data.Common.DBDataPermissionAttribute>.</span></span>|  
|`KeyRestrictions`|<span data-ttu-id="218fd-183">識別是否為允許的連接字串參數。</span><span class="sxs-lookup"><span data-stu-id="218fd-183">Identifies connection string parameters that are allowed or disallowed.</span></span> <span data-ttu-id="218fd-184">連接字串參數是在表單中識別 *\<parameter name>=* 。</span><span class="sxs-lookup"><span data-stu-id="218fd-184">Connection string parameters are identified in the form *\<parameter name>=*.</span></span> <span data-ttu-id="218fd-185">也可以指定多個參數，只要以分號 (;) 將其分隔即可。</span><span class="sxs-lookup"><span data-stu-id="218fd-185">Multiple parameters can be specified, delimited using a semicolon (;).</span></span> <span data-ttu-id="218fd-186">**注意：**  如果您未指定 `KeyRestrictions` ，但是將屬性設 `KeyRestrictionBehavior` 為 `AllowOnly` 或，則 `PreventUsage` 不允許任何其他連接字串參數。</span><span class="sxs-lookup"><span data-stu-id="218fd-186">**Note:**  If you do not specify `KeyRestrictions`, but you set `KeyRestrictionBehavior` property to `AllowOnly` or `PreventUsage`, no additional connection string parameters are allowed.</span></span> <span data-ttu-id="218fd-187">繼承自 <xref:System.Data.Common.DBDataPermissionAttribute>。</span><span class="sxs-lookup"><span data-stu-id="218fd-187">Inherited from <xref:System.Data.Common.DBDataPermissionAttribute>.</span></span>|  
|`KeyRestrictionBehavior`|<span data-ttu-id="218fd-188">將連接字串參數識別為唯一允許的其他參數 (`AllowOnly`)，或識別不允許的其他參數 (`PreventUsage`)。</span><span class="sxs-lookup"><span data-stu-id="218fd-188">Identifies the connection string parameters as the only additional parameters allowed (`AllowOnly`), or identifies the additional parameters that are not allowed (`PreventUsage`).</span></span> <span data-ttu-id="218fd-189">`AllowOnly` 是預設值。</span><span class="sxs-lookup"><span data-stu-id="218fd-189">`AllowOnly` is the default.</span></span> <span data-ttu-id="218fd-190">繼承自 <xref:System.Data.Common.DBDataPermissionAttribute>。</span><span class="sxs-lookup"><span data-stu-id="218fd-190">Inherited from <xref:System.Data.Common.DBDataPermissionAttribute>.</span></span>|  
|`TypeID`|<span data-ttu-id="218fd-191">在衍生類別中實作時，取得唯一識別項。</span><span class="sxs-lookup"><span data-stu-id="218fd-191">Gets a unique identifier for this attribute when implemented in a derived class.</span></span> <span data-ttu-id="218fd-192">繼承自 <xref:System.Attribute>。</span><span class="sxs-lookup"><span data-stu-id="218fd-192">Inherited from <xref:System.Attribute>.</span></span>|  
|`Unrestricted`|<span data-ttu-id="218fd-193">指示是否針對資源，宣告不受限的使用權限。</span><span class="sxs-lookup"><span data-stu-id="218fd-193">Indicates whether unrestricted permission to the resource is declared.</span></span> <span data-ttu-id="218fd-194">繼承自 <xref:System.Security.Permissions.SecurityAttribute>。</span><span class="sxs-lookup"><span data-stu-id="218fd-194">Inherited from <xref:System.Security.Permissions.SecurityAttribute>.</span></span>|  
  
#### <a name="connectionstring-syntax"></a><span data-ttu-id="218fd-195">ConnectionString 語法</span><span class="sxs-lookup"><span data-stu-id="218fd-195">ConnectionString Syntax</span></span>  

 <span data-ttu-id="218fd-196">下列範例將示範如何使用組態檔的 `connectionStrings` 項目，只允許使用特定的連接字串。</span><span class="sxs-lookup"><span data-stu-id="218fd-196">The following example demonstrates how to use the `connectionStrings` element of a configuration file to allow only a specific connection string to be used.</span></span> <span data-ttu-id="218fd-197">如需有關從設定檔儲存和取得連接字串的詳細資訊，請參閱 [連接字串](connection-strings.md) 。</span><span class="sxs-lookup"><span data-stu-id="218fd-197">See [Connection Strings](connection-strings.md) for more information on storing and retrieving connection strings from configuration files.</span></span>  
  
```xml  
<connectionStrings>  
  <add name="DatabaseConnection"
    connectionString="Data Source=(local);Initial
    Catalog=Northwind;Integrated Security=true;" />  
</connectionStrings>  
```  
  
#### <a name="keyrestrictions-syntax"></a><span data-ttu-id="218fd-198">KeyRestrictions 語法</span><span class="sxs-lookup"><span data-stu-id="218fd-198">KeyRestrictions Syntax</span></span>  

 <span data-ttu-id="218fd-199">下列範例會啟用相同的連接字串，以啟用 `Encrypt` 和 `Packet Size` 連接字串選項，但限制使用任何其他連接字串選項。</span><span class="sxs-lookup"><span data-stu-id="218fd-199">The following example enables the same connection string, enables the use of the `Encrypt` and `Packet Size` connection string options, but restricts the use of any other connection string options.</span></span>  
  
```xml  
<connectionStrings>  
  <add name="DatabaseConnection"
    connectionString="Data Source=(local);Initial
    Catalog=Northwind;Integrated Security=true;"  
    KeyRestrictions="Encrypt=;Packet Size=;"  
    KeyRestrictionBehavior="AllowOnly" />  
</connectionStrings>  
```  
  
#### <a name="keyrestrictionbehavior-with-preventusage-syntax"></a><span data-ttu-id="218fd-200">含 PreventUsage 的 KeyRestrictionBehavior 語法</span><span class="sxs-lookup"><span data-stu-id="218fd-200">KeyRestrictionBehavior with PreventUsage Syntax</span></span>  

 <span data-ttu-id="218fd-201">下列範例將啟用相同的連接字串，並允許 `User Id`、`Password` 和 `Persist Security Info` 以外的其他所有連接參數。</span><span class="sxs-lookup"><span data-stu-id="218fd-201">The following example enables the same connection string and allows all other connection parameters except for `User Id`, `Password` and `Persist Security Info`.</span></span>  
  
```xml  
<connectionStrings>  
  <add name="DatabaseConnection"
    connectionString="Data Source=(local);Initial
    Catalog=Northwind;Integrated Security=true;"  
    KeyRestrictions="User Id=;Password=;Persist Security Info=;"  
    KeyRestrictionBehavior="PreventUsage" />  
</connectionStrings>  
```  
  
#### <a name="keyrestrictionbehavior-with-allowonly-syntax"></a><span data-ttu-id="218fd-202">含 AllowOnly 的 KeyRestrictionBehavior 語法</span><span class="sxs-lookup"><span data-stu-id="218fd-202">KeyRestrictionBehavior with AllowOnly Syntax</span></span>  

 <span data-ttu-id="218fd-203">下列範例啟用兩個連接字串，這兩個連接字串同時包含 `Initial Catalog`、`Connection Timeout`、`Encrypt` 和 `Packet Size` 參數。</span><span class="sxs-lookup"><span data-stu-id="218fd-203">The following example enables two connection strings that also contain `Initial Catalog`, `Connection Timeout`, `Encrypt`, and `Packet Size` parameters.</span></span> <span data-ttu-id="218fd-204">所有其他的連接字串參數則都限制使用。</span><span class="sxs-lookup"><span data-stu-id="218fd-204">All other connection string parameters are restricted.</span></span>  
  
```xml  
<connectionStrings>  
  <add name="DatabaseConnection"
    connectionString="Data Source=(local);Initial
    Catalog=Northwind;Integrated Security=true;"  
    KeyRestrictions="Initial Catalog;Connection Timeout=;  
       Encrypt=;Packet Size=;"
    KeyRestrictionBehavior="AllowOnly" />  
  
  <add name="DatabaseConnection2"
    connectionString="Data Source=SqlServer2;Initial
    Catalog=Northwind2;Integrated Security=true;"  
    KeyRestrictions="Initial Catalog;Connection Timeout=;  
       Encrypt=;Packet Size=;"
    KeyRestrictionBehavior="AllowOnly" />  
</connectionStrings>  
```  
  
### <a name="enabling-partial-trust-with-a-custom-permission-set"></a><span data-ttu-id="218fd-205">以自訂的使用權限集啟用部份信任</span><span class="sxs-lookup"><span data-stu-id="218fd-205">Enabling Partial Trust with a Custom Permission Set</span></span>  

 <span data-ttu-id="218fd-206">若要啟用特定區域的 <xref:System.Data.SqlClient> 使用權限，系統管理員必須建立自訂的使用權限集合，並將其設定為特定區域的使用權限集合。</span><span class="sxs-lookup"><span data-stu-id="218fd-206">To enable the use of <xref:System.Data.SqlClient> permissions for a particular zone, a system administrator must create a custom permission set and set it as the permission set for a particular zone.</span></span> <span data-ttu-id="218fd-207">不可修改預設的使用權限集合 (例如 `LocalIntranet`)。</span><span class="sxs-lookup"><span data-stu-id="218fd-207">Default permission sets, such as `LocalIntranet`, cannot be modified.</span></span> <span data-ttu-id="218fd-208">例如，若要包含 <xref:System.Data.SqlClient> 具有之的程式碼許可權 <xref:System.Security.Policy.Zone> `LocalIntranet` ，系統管理員可以複製的許可權集合 `LocalIntranet` 、將它重新命名為 "CustomLocalIntranet"、新增 <xref:System.Data.SqlClient> 許可權、使用 [Caspol.exe (代碼啟用安全性原則工具) ](../../tools/caspol-exe-code-access-security-policy-tool.md)匯入 CustomLocalIntranet 許可權集合，以及將的許可權集合設定 `LocalIntranet_Zone` 為 CustomLocalIntranet。</span><span class="sxs-lookup"><span data-stu-id="218fd-208">For example, to include <xref:System.Data.SqlClient> permissions for code that has a <xref:System.Security.Policy.Zone> of `LocalIntranet`, a system administrator could copy the permission set for `LocalIntranet`, rename it to "CustomLocalIntranet", add the <xref:System.Data.SqlClient> permissions, import the CustomLocalIntranet permission set using the [Caspol.exe (Code Access Security Policy Tool)](../../tools/caspol-exe-code-access-security-policy-tool.md), and set the permission set of `LocalIntranet_Zone` to CustomLocalIntranet.</span></span>  
  
### <a name="sample-permission-set"></a><span data-ttu-id="218fd-209">使用權限集合範例</span><span class="sxs-lookup"><span data-stu-id="218fd-209">Sample Permission Set</span></span>  

 <span data-ttu-id="218fd-210">下列是部分受信任案例中的「SQL Server 的 .NET Framework 資料提供者」使用權限集合範例。</span><span class="sxs-lookup"><span data-stu-id="218fd-210">The following is a sample permission set for the .NET Framework Data Provider for SQL Server in a partially trusted scenario.</span></span> <span data-ttu-id="218fd-211">如需建立自訂許可權集合的詳細資訊，請參閱 [使用 Caspol.exe設定許可權集合 ](/previous-versions/dotnet/netframework-4.0/4ybs46y6(v=vs.100))。</span><span class="sxs-lookup"><span data-stu-id="218fd-211">For information on creating custom permission sets, see [Configuring Permission Sets Using Caspol.exe](/previous-versions/dotnet/netframework-4.0/4ybs46y6(v=vs.100)).</span></span>  
  
```xml  
<PermissionSet class="System.Security.NamedPermissionSet"  
  version="1"  
  Name="CustomLocalIntranet"  
  Description="Custom permission set given to applications on  
    the local intranet">  
  
<IPermission class="System.Data.SqlClient.SqlClientPermission, System.Data, Version=2.0.0000.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"  
version="1"  
AllowBlankPassword="False">  
<add ConnectionString="Data Source=(local);Integrated Security=true;"  
 KeyRestrictions="Initial Catalog=;Connection Timeout=;  
   Encrypt=;Packet Size=;"
 KeyRestrictionBehavior="AllowOnly" />  
 </IPermission>  
</PermissionSet>  
```  
  
## <a name="verifying-adonet-code-access-using-security-permissions"></a><span data-ttu-id="218fd-212">使用安全性使用權限驗證 ADO.NET 程式碼存取</span><span class="sxs-lookup"><span data-stu-id="218fd-212">Verifying ADO.NET Code Access Using Security Permissions</span></span>  

 <span data-ttu-id="218fd-213">若為部分信任案例，則可指定 <xref:System.Data.SqlClient.SqlClientPermissionAttribute>，藉以取得程式碼中之特定方法的 CAS 權限。</span><span class="sxs-lookup"><span data-stu-id="218fd-213">For partial-trust scenarios, you can require CAS privileges for particular methods in your code by specifying a <xref:System.Data.SqlClient.SqlClientPermissionAttribute>.</span></span> <span data-ttu-id="218fd-214">如果生效的限制安全性原則不允許該權限，則在執行程式碼前會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="218fd-214">If that privilege is not allowed by the restricted security policy in effect, an exception is thrown before your code is run.</span></span> <span data-ttu-id="218fd-215">如需安全性原則的詳細資訊，請參閱 [安全性原則管理](/previous-versions/dotnet/netframework-4.0/c1k0eed6(v=vs.100)) 和 [安全性原則的最佳作法](/previous-versions/dotnet/netframework-4.0/sa4se9bc(v=vs.100))。</span><span class="sxs-lookup"><span data-stu-id="218fd-215">For more information on security policy, see [Security Policy Management](/previous-versions/dotnet/netframework-4.0/c1k0eed6(v=vs.100)) and [Security Policy Best Practices](/previous-versions/dotnet/netframework-4.0/sa4se9bc(v=vs.100)).</span></span>  
  
### <a name="example"></a><span data-ttu-id="218fd-216">範例</span><span class="sxs-lookup"><span data-stu-id="218fd-216">Example</span></span>  

 <span data-ttu-id="218fd-217">下列範例示範如何撰寫需要特定連接字串的程式碼。</span><span class="sxs-lookup"><span data-stu-id="218fd-217">The following example demonstrates how to write code that requires a particular connection string.</span></span> <span data-ttu-id="218fd-218">它模擬如何拒絕 <xref:System.Data.SqlClient> 的不受限權限，而系統管理員在實務上會使用 CAS 原則來實作這些權限。</span><span class="sxs-lookup"><span data-stu-id="218fd-218">It simulates denying unrestricted permissions to <xref:System.Data.SqlClient>, which a system administrator would implement using a CAS policy in the real world.</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="218fd-219">設計 ADO.NET 的 CAS 權限時，最正確的模式是以最大的限制 (完全沒有權限) 開始，然後加入程式碼必須執行之特殊工作所需的特定權限。</span><span class="sxs-lookup"><span data-stu-id="218fd-219">When designing CAS permissions for ADO.NET, the correct pattern is to start with the most restrictive case (no permissions at all) and then add the specific permissions that are needed for the particular task that the code needs to perform.</span></span> <span data-ttu-id="218fd-220">相反的模式 (以所有權限開始，然後再拒絕特定權限) 並不安全，因為有許多方法可表示相同的連接字串。</span><span class="sxs-lookup"><span data-stu-id="218fd-220">The opposite pattern, starting with all permissions and then denying a specific permission, is not secure because there are many ways of expressing the same connection string.</span></span> <span data-ttu-id="218fd-221">例如，如果您以所有權限開始，然後嘗試拒絕連接字串 "server=someserver" 的用法，您仍可使用 "server=someserver.mycompany.com" 字串。</span><span class="sxs-lookup"><span data-stu-id="218fd-221">For example, if you start with all permissions and then attempt to deny the use of the connection string "server=someserver", the string "server=someserver.mycompany.com" would still be allowed.</span></span> <span data-ttu-id="218fd-222">只要以不授與任何權限開始，您就能減少權限集合具有漏洞的機會。</span><span class="sxs-lookup"><span data-stu-id="218fd-222">By always starting by granting no permissions at all, you reduce the chances that there are holes in the permission set.</span></span>  
  
 <span data-ttu-id="218fd-223">下列程式碼將示範 `SqlClient` 如何執行安全性需求，也就是在沒有適當的 CAS 權限時，擲回 <xref:System.Security.SecurityException>。</span><span class="sxs-lookup"><span data-stu-id="218fd-223">The following code demonstrates how `SqlClient` performs the security demand, which throws a <xref:System.Security.SecurityException> if the appropriate CAS permissions are not in place.</span></span> <span data-ttu-id="218fd-224">主控台視窗會顯示 <xref:System.Security.SecurityException> 輸出。</span><span class="sxs-lookup"><span data-stu-id="218fd-224">The <xref:System.Security.SecurityException> output is displayed in the console window.</span></span>  
  
 [!code-csharp[DataWorks SqlClient.CAS#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.CAS/CS/source.cs#1)]
 [!code-vb[DataWorks SqlClient.CAS#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.CAS/VB/source.vb#1)]  
  
 <span data-ttu-id="218fd-225">您應該在 [主控台] 視窗中看到以下輸出：</span><span class="sxs-lookup"><span data-stu-id="218fd-225">You should see this output in the Console window:</span></span>  
  
```output  
Failed, as expected: <IPermission class="System.Data.SqlClient.  
SqlClientPermission, System.Data, Version=2.0.0.0,
  Culture=neutral, PublicKeyToken=b77a5c561934e089" version="1"  
  AllowBlankPassword="False">  
<add ConnectionString="Data Source=(local);Initial Catalog=  
  Northwind;Integrated Security=SSPI" KeyRestrictions=""  
KeyRestrictionBehavior="AllowOnly"/>  
</IPermission>  
  
Connection opened, as expected.  
Failed, as expected: Request failed.  
```  
  
## <a name="interoperability-with-unmanaged-code"></a><span data-ttu-id="218fd-226">與 Unmanaged 程式碼的互通性</span><span class="sxs-lookup"><span data-stu-id="218fd-226">Interoperability with Unmanaged Code</span></span>  

 <span data-ttu-id="218fd-227">在 CLR 外部執行的程式碼稱為 Unmanaged 程式碼。</span><span class="sxs-lookup"><span data-stu-id="218fd-227">Code that runs outside the CLR is called unmanaged code.</span></span> <span data-ttu-id="218fd-228">因此，CAS 等安全性機制無法套用至 Unmanaged 程式碼。</span><span class="sxs-lookup"><span data-stu-id="218fd-228">Therefore, security mechanisms such as CAS cannot be applied to unmanaged code.</span></span> <span data-ttu-id="218fd-229">COM 元件、ActiveX 介面及 Windows API 函式都是 Unmanaged 程式碼的範例。</span><span class="sxs-lookup"><span data-stu-id="218fd-229">COM components, ActiveX interfaces, and Windows API functions are examples of unmanaged code.</span></span> <span data-ttu-id="218fd-230">執行 Unmanaged 程式碼時，您應該套用特殊安全性考量，以免危及整體應用程式安全性。</span><span class="sxs-lookup"><span data-stu-id="218fd-230">Special security considerations apply when executing unmanaged code so that you do not jeopardize overall application security.</span></span> <span data-ttu-id="218fd-231">如需詳細資訊，請參閱[與 Unmanaged 程式碼互通](../../interop/index.md)。</span><span class="sxs-lookup"><span data-stu-id="218fd-231">For more information, see [Interoperating with Unmanaged Code](../../interop/index.md).</span></span>  
  
 <span data-ttu-id="218fd-232">.NET Framework 也透過 COM Interop 提供存取，藉以支援現有 COM 元件的回溯相容性 (Backward Compatibility)。</span><span class="sxs-lookup"><span data-stu-id="218fd-232">The .NET Framework also supports backward compatibility to existing COM components by providing access through COM interop.</span></span> <span data-ttu-id="218fd-233">您可以使用 COM Interop 工具來匯入相關的 COM 型別，以便將 COM 元件併入 .NET Framework 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="218fd-233">You can incorporate COM components into a .NET Framework application by using COM interop tools to import the relevant COM types.</span></span> <span data-ttu-id="218fd-234">一旦匯入之後，COM 型別便可供使用。</span><span class="sxs-lookup"><span data-stu-id="218fd-234">Once imported, the COM types are ready to use.</span></span> <span data-ttu-id="218fd-235">COM Interop 也會將組件中繼資料匯出至型別程式庫並將 Managed 元件註冊為 COM 元件，藉以讓 COM 用戶端存取 Managed 程式碼。</span><span class="sxs-lookup"><span data-stu-id="218fd-235">COM interop also enables COM clients to access managed code by exporting assembly metadata to a type library and registering the managed component as a COM component.</span></span> <span data-ttu-id="218fd-236">如需詳細資訊，請參閱 [ADVANCED COM 互通性](/previous-versions/dotnet/netframework-4.0/bd9cdfyx(v=vs.100))。</span><span class="sxs-lookup"><span data-stu-id="218fd-236">For more information, see [Advanced COM Interoperability](/previous-versions/dotnet/netframework-4.0/bd9cdfyx(v=vs.100)).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="218fd-237">另請參閱</span><span class="sxs-lookup"><span data-stu-id="218fd-237">See also</span></span>

- [<span data-ttu-id="218fd-238">設定 ADO.NET 應用程式的安全性</span><span class="sxs-lookup"><span data-stu-id="218fd-238">Securing ADO.NET Applications</span></span>](securing-ado-net-applications.md)
- <span data-ttu-id="218fd-239">[機器碼和 .NET Framework 程式碼中的安全性](/previous-versions/visualstudio/visual-studio-2010/1787tk12(v=vs.100))</span><span class="sxs-lookup"><span data-stu-id="218fd-239">[Security in Native and .NET Framework Code](/previous-versions/visualstudio/visual-studio-2010/1787tk12(v=vs.100))</span></span>
- [<span data-ttu-id="218fd-240">以角色為基礎的安全性</span><span class="sxs-lookup"><span data-stu-id="218fd-240">Role-Based Security</span></span>](../../../standard/security/role-based-security.md)
- <span data-ttu-id="218fd-241">[ADO.NET 概觀](ado-net-overview.md) \(部分機器翻譯\)</span><span class="sxs-lookup"><span data-stu-id="218fd-241">[ADO.NET Overview](ado-net-overview.md)</span></span>
