---
ms.openlocfilehash: 22b5abbe769733e8d5ca3e78dd9e6e13b2363737
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620018"
---
### <a name="opt-in-break-to-revert-from-different-45-sql-generation-to-simpler-40-sql-generation"></a><span data-ttu-id="7a4fb-101">選擇中斷以從不同的 4.5 SQL 產生還原為更簡單的 4.0 SQL 產生</span><span class="sxs-lookup"><span data-stu-id="7a4fb-101">Opt-in break to revert from different 4.5 SQL generation to simpler 4.0 SQL generation</span></span>

#### <a name="details"></a><span data-ttu-id="7a4fb-102">詳細資料</span><span class="sxs-lookup"><span data-stu-id="7a4fb-102">Details</span></span>

<span data-ttu-id="7a4fb-103">產生 JOIN 陳述式並包含限制作業呼叫 (不先使用 OrderBy) 的查詢，現在能產生更簡單的 SQL。</span><span class="sxs-lookup"><span data-stu-id="7a4fb-103">Queries that produce JOIN statements and contain a call to a limiting operation without first using OrderBy now produce simpler SQL.</span></span> <span data-ttu-id="7a4fb-104">升級至 .NET Framework 4.5 之後，這些查詢會產生比舊版更複雜的 SQL。</span><span class="sxs-lookup"><span data-stu-id="7a4fb-104">After upgrading to .NET Framework 4.5, these queries produced more complicated SQL than previous versions.</span></span>

#### <a name="suggestion"></a><span data-ttu-id="7a4fb-105">建議</span><span class="sxs-lookup"><span data-stu-id="7a4fb-105">Suggestion</span></span>

<span data-ttu-id="7a4fb-106">此功能預設為停用。</span><span class="sxs-lookup"><span data-stu-id="7a4fb-106">This feature is disabled by default.</span></span> <span data-ttu-id="7a4fb-107">如果 Entity Framework 產生額外的 JOIN 陳述式而造成效能降低，您可以啟用這項功能，方法是在應用程式組態檔 (app.config) 的 <code>&lt;appSettings&gt;</code> 區段中新增下列項目：</span><span class="sxs-lookup"><span data-stu-id="7a4fb-107">If Entity Framework generates extra JOIN statements that cause performance degradation, you can enable this feature by adding the following entry to the <code>&lt;appSettings&gt;</code> section of the application configuration (app.config) file:</span></span><pre><code class="lang-xml">&lt;add key=&quot;EntityFramework_SimplifyLimitOperations&quot; value=&quot;true&quot; /&gt;&#13;&#10;</code></pre>

| <span data-ttu-id="7a4fb-108">名稱</span><span class="sxs-lookup"><span data-stu-id="7a4fb-108">Name</span></span>    | <span data-ttu-id="7a4fb-109">值</span><span class="sxs-lookup"><span data-stu-id="7a4fb-109">Value</span></span>       |
|:--------|:------------|
| <span data-ttu-id="7a4fb-110">影響範圍</span><span class="sxs-lookup"><span data-stu-id="7a4fb-110">Scope</span></span>   |<span data-ttu-id="7a4fb-111">透明</span><span class="sxs-lookup"><span data-stu-id="7a4fb-111">Transparent</span></span>|
|<span data-ttu-id="7a4fb-112">版本</span><span class="sxs-lookup"><span data-stu-id="7a4fb-112">Version</span></span>|<span data-ttu-id="7a4fb-113">4.5.2</span><span class="sxs-lookup"><span data-stu-id="7a4fb-113">4.5.2</span></span>|
|<span data-ttu-id="7a4fb-114">類型</span><span class="sxs-lookup"><span data-stu-id="7a4fb-114">Type</span></span>|<span data-ttu-id="7a4fb-115">執行階段</span><span class="sxs-lookup"><span data-stu-id="7a4fb-115">Runtime</span></span>|
