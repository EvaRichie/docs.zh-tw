---
ms.openlocfilehash: 4416a7c09f2d163961fe2fe3d6dfaa8bd5e66f93
ms.sourcegitcommit: cbacb5d2cebbf044547f6af6e74a9de866800985
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/05/2020
ms.locfileid: "89497002"
---
### <a name="change-in-behavior-in-data-definition-language-ddl-apis"></a><span data-ttu-id="935ea-101">資料定義語言 (DDL) API 的行為變更</span><span class="sxs-lookup"><span data-stu-id="935ea-101">Change in behavior in Data Definition Language (DDL) APIs</span></span>

#### <a name="details"></a><span data-ttu-id="935ea-102">詳細資料</span><span class="sxs-lookup"><span data-stu-id="935ea-102">Details</span></span>

<span data-ttu-id="935ea-103">指定 AttachDBFilename 時，DDL API 的行為已變更如下：</span><span class="sxs-lookup"><span data-stu-id="935ea-103">The behavior of DDL APIs when AttachDBFilename is specified has changed as follows:</span></span><ul><li><span data-ttu-id="935ea-104">連接字串不需要指定 Initial Catalog 值。</span><span class="sxs-lookup"><span data-stu-id="935ea-104">Connection strings need not specify an Initial Catalog value.</span></span> <span data-ttu-id="935ea-105">以往 AttachDBFilename 和 Initial Catalog 都是必要項。</span><span class="sxs-lookup"><span data-stu-id="935ea-105">Previously, both AttachDBFilename and Initial Catalog were required.</span></span></li><li><span data-ttu-id="935ea-106">如果同時指定 AttachDBFilename 和 Initial Catalog，且指定的 MDF 檔案存在，則 <xref:System.Data.Objects.ObjectContext.DatabaseExists%2A> 方法會傳回 <code>true</code>。</span><span class="sxs-lookup"><span data-stu-id="935ea-106">If both AttachDBFilename and Initial Catalog are specified and the given MDF file exists, the <xref:System.Data.Objects.ObjectContext.DatabaseExists%2A> method returns <code>true</code>.</span></span> <span data-ttu-id="935ea-107">以往它會傳回 <code>false</code>。</span><span class="sxs-lookup"><span data-stu-id="935ea-107">Previously, it returned <code>false</code>.</span></span></li><li><span data-ttu-id="935ea-108">如果同時指定 AttachDBFilename 和 Initial Catalog，且指定的 MDF 檔案存在，則呼叫 <xref:System.Data.Objects.ObjectContext.DeleteDatabase%2A> 方法會刪除檔案。</span><span class="sxs-lookup"><span data-stu-id="935ea-108">If both AttachDBFilename and Initial Catalog are specified and the given MDF file exists, calling the <xref:System.Data.Objects.ObjectContext.DeleteDatabase%2A> method deletes the files.</span></span></li><li><span data-ttu-id="935ea-109">如果在連接字串指定 AttachDBFilename，而其中 MDF 不存在且初始目錄也不存在時呼叫 <xref:System.Data.Objects.ObjectContext.DeleteDatabase%2A>，則方法會擲回 <xref:System.InvalidOperationException> 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="935ea-109">If <xref:System.Data.Objects.ObjectContext.DeleteDatabase%2A> is called when the connection string specifies an AttachDBFilename value with an MDF that doesn't exist and an Initial Catalog that doesn't exist, the method throws an <xref:System.InvalidOperationException> exception.</span></span> <span data-ttu-id="935ea-110">以往它會擲回 <xref:System.Data.SqlClient.SqlException> 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="935ea-110">Previously, it threw a <xref:System.Data.SqlClient.SqlException> exception.</span></span></li></ul>

#### <a name="suggestion"></a><span data-ttu-id="935ea-111">建議</span><span class="sxs-lookup"><span data-stu-id="935ea-111">Suggestion</span></span>

<span data-ttu-id="935ea-112">這些變更可讓您更容易建置使用 DDL 應用程式開發介面的工具和應用程式。</span><span class="sxs-lookup"><span data-stu-id="935ea-112">These changes make it easier to build tools and applications that use the DDL APIs.</span></span> <span data-ttu-id="935ea-113">在下列情節中，這些變更可能會影響應用程式相容性：</span><span class="sxs-lookup"><span data-stu-id="935ea-113">These changes can affect application compatibility in the following scenarios:</span></span><ul><li><span data-ttu-id="935ea-114">如果 <code>DROP DATABASE</code> 傳回 <xref:System.Data.Objects.ObjectContext.DeleteDatabase%2A>，使用者撰寫的程式碼會直接執行 <xref:System.Data.Objects.ObjectContext.DatabaseExists%2A> 命令，而不是呼叫 <code>true</code>。</span><span class="sxs-lookup"><span data-stu-id="935ea-114">The user writes code that executes a <code>DROP DATABASE</code> command directly instead of calling <xref:System.Data.Objects.ObjectContext.DeleteDatabase%2A> if <xref:System.Data.Objects.ObjectContext.DatabaseExists%2A> returns <code>true</code>.</span></span> <span data-ttu-id="935ea-115">如果未附加資料庫，但 MDF 檔案存在，則會使現有的程式碼中斷。</span><span class="sxs-lookup"><span data-stu-id="935ea-115">This breaks existing code If the database is not attached but the MDF file exists.</span></span></li><li><span data-ttu-id="935ea-116">當初始目錄和 MDF 檔案不存在時，使用者撰寫的程式碼預期 <xref:System.Data.Objects.ObjectContext.DeleteDatabase%2A> 方法會擲回 <xref:System.Data.SqlClient.SqlException>，而不是 <xref:System.InvalidOperationException>。</span><span class="sxs-lookup"><span data-stu-id="935ea-116">The user writes code that expects the <xref:System.Data.Objects.ObjectContext.DeleteDatabase%2A> method to throw a <xref:System.Data.SqlClient.SqlException> rather than an <xref:System.InvalidOperationException> when the Initial Catalog and MDF file don't exist.</span></span></li></ul>

| <span data-ttu-id="935ea-117">名稱</span><span class="sxs-lookup"><span data-stu-id="935ea-117">Name</span></span>    | <span data-ttu-id="935ea-118">值</span><span class="sxs-lookup"><span data-stu-id="935ea-118">Value</span></span>       |
|:--------|:------------|
| <span data-ttu-id="935ea-119">範圍</span><span class="sxs-lookup"><span data-stu-id="935ea-119">Scope</span></span>   |<span data-ttu-id="935ea-120">Minor</span><span class="sxs-lookup"><span data-stu-id="935ea-120">Minor</span></span>|
|<span data-ttu-id="935ea-121">版本</span><span class="sxs-lookup"><span data-stu-id="935ea-121">Version</span></span>|<span data-ttu-id="935ea-122">4.5</span><span class="sxs-lookup"><span data-stu-id="935ea-122">4.5</span></span>|
|<span data-ttu-id="935ea-123">類型</span><span class="sxs-lookup"><span data-stu-id="935ea-123">Type</span></span>|<span data-ttu-id="935ea-124">執行階段</span><span class="sxs-lookup"><span data-stu-id="935ea-124">Runtime</span></span>|

#### <a name="affected-apis"></a><span data-ttu-id="935ea-125">受影響的 API</span><span class="sxs-lookup"><span data-stu-id="935ea-125">Affected APIs</span></span>

<span data-ttu-id="935ea-126">無法透過 API 分析偵測。</span><span class="sxs-lookup"><span data-stu-id="935ea-126">Not detectable via API analysis.</span></span>

<!--

#### Affected APIs

Not detectable via API analysis.

-->
