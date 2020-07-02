---
ms.openlocfilehash: ddc98448101c65003001ad05e67f29d75d99ad44
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85616034"
---
### <a name="workflowdesignerload-doesnt-remove-symbol-property"></a><span data-ttu-id="6fa93-101">WorkflowDesigner.Load 不會移除符號屬性</span><span class="sxs-lookup"><span data-stu-id="6fa93-101">WorkflowDesigner.Load doesn't remove symbol property</span></span>

#### <a name="details"></a><span data-ttu-id="6fa93-102">詳細資料</span><span class="sxs-lookup"><span data-stu-id="6fa93-102">Details</span></span>

<span data-ttu-id="6fa93-103">如果工作流程設計工具是以 .NET Framework 4.5 為目標，並使用 <xref:System.Activities.Presentation.WorkflowDesigner.Load> 方法載入重新裝載的 3.5 工作流程，則會在儲存工作流程時擲回 <xref:System.Xaml.XamlDuplicateMemberException?displayProperty=fullName>。</span><span class="sxs-lookup"><span data-stu-id="6fa93-103">When targeting the .NET Framework 4.5 in the workflow designer, and loading a re-hosted 3.5 workflow with the <xref:System.Activities.Presentation.WorkflowDesigner.Load> method, a <xref:System.Xaml.XamlDuplicateMemberException?displayProperty=fullName> is thrown while saving the workflow.</span></span>

#### <a name="suggestion"></a><span data-ttu-id="6fa93-104">建議</span><span class="sxs-lookup"><span data-stu-id="6fa93-104">Suggestion</span></span>

<span data-ttu-id="6fa93-105">只有在工作流程設計工具是以 .NET Framework 4.5 為目標時才會出現此 Bug，因此可藉由將 `WorkflowDesigner.Context.Services.GetService&lt;DesignerConfigurationService&gt;().TargetFrameworkName` 設定為 .NET Framework 4.0 來解決。或者，可以使用 <xref:System.Activities.Presentation.WorkflowDesigner.Load(System.String)> 方法載入工作流桯來避免問題，而不要使用 <xref:System.Activities.Presentation.WorkflowDesigner.Load>。</span><span class="sxs-lookup"><span data-stu-id="6fa93-105">This bug only manifests when targeting .NET Framework 4.5 in the workflow designer, so it can be worked around by setting the `WorkflowDesigner.Context.Services.GetService&lt;DesignerConfigurationService&gt;().TargetFrameworkName` to the 4.0 .NET Framework.Alternatively, the issue may be avoided by using the <xref:System.Activities.Presentation.WorkflowDesigner.Load(System.String)> method to load the workflow, instead of <xref:System.Activities.Presentation.WorkflowDesigner.Load>.</span></span>

| <span data-ttu-id="6fa93-106">名稱</span><span class="sxs-lookup"><span data-stu-id="6fa93-106">Name</span></span>    | <span data-ttu-id="6fa93-107">值</span><span class="sxs-lookup"><span data-stu-id="6fa93-107">Value</span></span>       |
|:--------|:------------|
| <span data-ttu-id="6fa93-108">影響範圍</span><span class="sxs-lookup"><span data-stu-id="6fa93-108">Scope</span></span>   | <span data-ttu-id="6fa93-109">主要</span><span class="sxs-lookup"><span data-stu-id="6fa93-109">Major</span></span>       |
| <span data-ttu-id="6fa93-110">版本</span><span class="sxs-lookup"><span data-stu-id="6fa93-110">Version</span></span> | <span data-ttu-id="6fa93-111">4.5</span><span class="sxs-lookup"><span data-stu-id="6fa93-111">4.5</span></span>         |
| <span data-ttu-id="6fa93-112">類型</span><span class="sxs-lookup"><span data-stu-id="6fa93-112">Type</span></span>    | <span data-ttu-id="6fa93-113">正在重定目標</span><span class="sxs-lookup"><span data-stu-id="6fa93-113">Retargeting</span></span> |

#### <a name="affected-apis"></a><span data-ttu-id="6fa93-114">受影響的 API</span><span class="sxs-lookup"><span data-stu-id="6fa93-114">Affected APIs</span></span>

- <xref:System.Activities.Presentation.WorkflowDesigner.Load?displayProperty=nameWithType>
