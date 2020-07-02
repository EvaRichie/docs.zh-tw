---
ms.openlocfilehash: 2d0798917b639bc90bf3f78f6fb9f19d0eaf2c71
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614381"
---
### <a name="incorrect-implementation-of-memberdescriptorequals"></a><span data-ttu-id="ebfc5-101">MemberDescriptor.Equals 的實作不正確</span><span class="sxs-lookup"><span data-stu-id="ebfc5-101">Incorrect implementation of MemberDescriptor.Equals</span></span>

#### <a name="details"></a><span data-ttu-id="ebfc5-102">詳細資料</span><span class="sxs-lookup"><span data-stu-id="ebfc5-102">Details</span></span>

<span data-ttu-id="ebfc5-103"><xref:System.ComponentModel.MemberDescriptor.Equals%2A?displayProperty=nameWithType> 方法的原始實作會比較正在比較之物件的兩個不同字串屬性：分類名稱與描述字串。</span><span class="sxs-lookup"><span data-stu-id="ebfc5-103">The original implementation of the <xref:System.ComponentModel.MemberDescriptor.Equals%2A?displayProperty=nameWithType> method compares two different string properties from the objects being compared: the category name and the description string.</span></span> <span data-ttu-id="ebfc5-104">修正方法是比較第一個物件的 <xref:System.ComponentModel.MemberDescriptor.Category> 和第二個物件的 <xref:System.ComponentModel.MemberDescriptor.Category>，比較第一個物件的 <xref:System.ComponentModel.MemberDescriptor.Description> 和第二個物件的 <xref:System.ComponentModel.MemberDescriptor.Description>。</span><span class="sxs-lookup"><span data-stu-id="ebfc5-104">The fix is to compare the <xref:System.ComponentModel.MemberDescriptor.Category> of the first object to the <xref:System.ComponentModel.MemberDescriptor.Category> of the second one, and the <xref:System.ComponentModel.MemberDescriptor.Description> of the first to the <xref:System.ComponentModel.MemberDescriptor.Description> of the second.</span></span>

#### <a name="suggestion"></a><span data-ttu-id="ebfc5-105">建議</span><span class="sxs-lookup"><span data-stu-id="ebfc5-105">Suggestion</span></span>

<span data-ttu-id="ebfc5-106">如果您的應用程式相依於當描述項相等時有時會傳回 `false` 的 <xref:System.ComponentModel.MemberDescriptor.Equals%2A?displayProperty=nameWithType>，而且您的目標是 .NET Framework 4.6.2 版或更新版本，則有數個選項：</span><span class="sxs-lookup"><span data-stu-id="ebfc5-106">If your application depends on <xref:System.ComponentModel.MemberDescriptor.Equals%2A?displayProperty=nameWithType> sometimes returning `false` when descriptors are equivalent, and you are targeting the .NET Framework 4.6.2 or later, you have several options:</span></span>

- <span data-ttu-id="ebfc5-107">變更程式碼以在呼叫 <xref:System.ComponentModel.MemberDescriptor.Equals%2A?displayProperty=nameWithType> 方法之外，手動比較 <xref:System.ComponentModel.MemberDescriptor.Category> 和 <xref:System.ComponentModel.MemberDescriptor.Description> 欄位。</span><span class="sxs-lookup"><span data-stu-id="ebfc5-107">Make code changes to compare the <xref:System.ComponentModel.MemberDescriptor.Category> and <xref:System.ComponentModel.MemberDescriptor.Description> fields manually in addition to calling the <xref:System.ComponentModel.MemberDescriptor.Equals%2A?displayProperty=nameWithType> method.</span></span>
- <span data-ttu-id="ebfc5-108">在 app.config 檔案中新增下列值，選擇不進行這項變更：</span><span class="sxs-lookup"><span data-stu-id="ebfc5-108">Opt out of this change by adding the following value to the app.config file:</span></span>

```xml
<runtime>
  <AppContextSwitchOverrides value="Switch.System.MemberDescriptorEqualsReturnsFalseIfEquivalent=true" />
</runtime>
```

<span data-ttu-id="ebfc5-109">如果您的應用程式目標設為 .NET Framework 4.6.1 或較舊版本，但在 .NET Framework 4.6.2 或更新版本上執行，而您想要啟用這項變更，您可以在 app.config 檔案中新增下列值，將相容性參數設為 `false`：</span><span class="sxs-lookup"><span data-stu-id="ebfc5-109">If your application targets .NET Framework 4.6.1 or earlier and is running on the .NET Framework 4.6.2 or later and you want this change enabled, you can set the compatibility switch to `false` by adding the following value to the app.config file:</span></span>

```xml
<runtime>
  <AppContextSwitchOverrides value="Switch.System.MemberDescriptorEqualsReturnsFalseIfEquivalent=false" />
</runtime>
```

| <span data-ttu-id="ebfc5-110">名稱</span><span class="sxs-lookup"><span data-stu-id="ebfc5-110">Name</span></span>    | <span data-ttu-id="ebfc5-111">值</span><span class="sxs-lookup"><span data-stu-id="ebfc5-111">Value</span></span>       |
|:--------|:------------|
| <span data-ttu-id="ebfc5-112">影響範圍</span><span class="sxs-lookup"><span data-stu-id="ebfc5-112">Scope</span></span>   | <span data-ttu-id="ebfc5-113">Edge</span><span class="sxs-lookup"><span data-stu-id="ebfc5-113">Edge</span></span>        |
| <span data-ttu-id="ebfc5-114">版本</span><span class="sxs-lookup"><span data-stu-id="ebfc5-114">Version</span></span> | <span data-ttu-id="ebfc5-115">4.6.2</span><span class="sxs-lookup"><span data-stu-id="ebfc5-115">4.6.2</span></span>       |
| <span data-ttu-id="ebfc5-116">類型</span><span class="sxs-lookup"><span data-stu-id="ebfc5-116">Type</span></span>    | <span data-ttu-id="ebfc5-117">正在重定目標</span><span class="sxs-lookup"><span data-stu-id="ebfc5-117">Retargeting</span></span> |

#### <a name="affected-apis"></a><span data-ttu-id="ebfc5-118">受影響的 API</span><span class="sxs-lookup"><span data-stu-id="ebfc5-118">Affected APIs</span></span>

- <xref:System.ComponentModel.MemberDescriptor.Equals(System.Object)?displayProperty=nameWithType>
