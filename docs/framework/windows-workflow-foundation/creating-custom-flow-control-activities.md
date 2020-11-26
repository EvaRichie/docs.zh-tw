---
title: 建立自訂流程控制活動
ms.date: 03/30/2017
ms.assetid: 27f409f6-2d1d-4cfb-9765-93eb2ad667d5
ms.openlocfilehash: 92d98d33b10e431248c4c482fcd26f3036c4c330
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96242067"
---
# <a name="creating-custom-flow-control-activities"></a><span data-ttu-id="7fd1d-102">建立自訂流程控制活動</span><span class="sxs-lookup"><span data-stu-id="7fd1d-102">Creating custom flow control activities</span></span>

<span data-ttu-id="7fd1d-103">.NET Framework 包含各種不同的流程式控制制活動，其運作方式類似于抽象程式設計結構 (例如 <xref:System.Activities.Statements.Flowchart>) 或標準程式設計語句 (例如 <xref:System.Activities.Statements.If>) 。</span><span class="sxs-lookup"><span data-stu-id="7fd1d-103">The .NET Framework contains a variety of flow-control activities that function similarly to abstract programming structures (such as <xref:System.Activities.Statements.Flowchart>)   or to standard programming statements (such as <xref:System.Activities.Statements.If>).</span></span> <span data-ttu-id="7fd1d-104">本主題討論其中一個範例專案（ [非一般 ForEach](./samples/non-generic-foreach.md)）的架構。</span><span class="sxs-lookup"><span data-stu-id="7fd1d-104">This topic discusses the architecture of one of the sample projects, [Non-Generic ForEach](./samples/non-generic-foreach.md).</span></span>  
  
## <a name="creating-the-custom-class"></a><span data-ttu-id="7fd1d-105">建立自訂類別</span><span class="sxs-lookup"><span data-stu-id="7fd1d-105">Creating the custom class</span></span>  

 <span data-ttu-id="7fd1d-106">因為非泛型 ForEach 類別必須排程子活動，而且衍生自 <xref:System.Activities.NativeActivity> 的活動沒有這項功能，所以它必須衍生自 <xref:System.Workflow.Activities.CodeActivity>。</span><span class="sxs-lookup"><span data-stu-id="7fd1d-106">Since the Non-Generic ForEach class will need to schedule child activities, it will need to derive from <xref:System.Activities.NativeActivity>, since activities that derive from <xref:System.Workflow.Activities.CodeActivity> do not have this functionality.</span></span>  
  
```csharp  
public sealed class ForEach : NativeActivity  
{
}
```  
  
 <span data-ttu-id="7fd1d-107">此自訂類別需要使用許多成員來儲存活動所使用的資料，以及提供執行活動之子活動的功能。</span><span class="sxs-lookup"><span data-stu-id="7fd1d-107">The custom class requires several members to store data being used by the activity, and to provide functionality to execute the activity’s child activities.</span></span> <span data-ttu-id="7fd1d-108">這些成員包括：</span><span class="sxs-lookup"><span data-stu-id="7fd1d-108">These members include:</span></span>  
  
- <span data-ttu-id="7fd1d-109">`valueEnumerator`：屬於用來反覆查看項目集合之 <xref:System.Activities.Variable%601> 型別的非公用 <xref:System.Collections.IEnumerator>。</span><span class="sxs-lookup"><span data-stu-id="7fd1d-109">`valueEnumerator`: The non-public <xref:System.Activities.Variable%601> of type <xref:System.Collections.IEnumerator> used to iterate over the collection of items.</span></span> <span data-ttu-id="7fd1d-110">這個成員屬於 <xref:System.Activities.Variable%601> 型別，因為它是在活動內部使用，而非引數或公用屬性。如果此物件的來源位於活動外部，就會使用引數或公用屬性。</span><span class="sxs-lookup"><span data-stu-id="7fd1d-110">This member is of type <xref:System.Activities.Variable%601> because it is used internally in the activity, rather than an argument or public property, which would be used if this object were to have an origin outside the activity.</span></span>  
  
- <span data-ttu-id="7fd1d-111">`OnChildComplete`：每個子系完成執行時所執行的公用 <xref:System.Activities.CompletionCallback> 屬性。</span><span class="sxs-lookup"><span data-stu-id="7fd1d-111">`OnChildComplete`: The public <xref:System.Activities.CompletionCallback> property that executes when each child completes execution.</span></span> <span data-ttu-id="7fd1d-112">這個成員會定義為 CLR 屬性，因為其值不會針對活動的不同執行個體變更。</span><span class="sxs-lookup"><span data-stu-id="7fd1d-112">This member is defined as a CLR property, since its value will not change for different instances of the activity.</span></span>  
  
- <span data-ttu-id="7fd1d-113">`Values`：用於子活動之反覆項目的輸入集合。</span><span class="sxs-lookup"><span data-stu-id="7fd1d-113">`Values`: The collection of inputs used for the iterations of the child activity.</span></span> <span data-ttu-id="7fd1d-114">這個成員屬於 <xref:System.Activities.InArgument%601> 型別，因為資料的來源位於活動外部，但是集合的內容不應該在活動執行期間變更。</span><span class="sxs-lookup"><span data-stu-id="7fd1d-114">This member is of type <xref:System.Activities.InArgument%601>, since the origin of the data is outside the activity, but the contents of the collection is not expected to change during the execution of the activity.</span></span> <span data-ttu-id="7fd1d-115">如果活動需要在活動執行時變更此集合內容的功能 (例如加入或移除活動)，這個成員就會定義為 <xref:System.Activities.ActivityAction>，然後每次存取該成員時就會進行評估，以便將變更提供給活動。</span><span class="sxs-lookup"><span data-stu-id="7fd1d-115">If the activity needed the functionality to change the contents of this collection while the activity was executing (to add or remove activities, for instance), this member would have been defined as an <xref:System.Activities.ActivityAction>, which then would have been evaluated every time it was accessed, so that changes would be available to the activity.</span></span>  
  
- <span data-ttu-id="7fd1d-116">`Body`：這個成員會定義要針對 `Values` 集合中每個項目執行的活動。</span><span class="sxs-lookup"><span data-stu-id="7fd1d-116">`Body`: This member defines the activity to be executed for each item in the `Values` collection.</span></span> <span data-ttu-id="7fd1d-117">這個成員會定義為 <xref:System.Activities.ActivityAction>，以便每次存取該成員時進行評估。</span><span class="sxs-lookup"><span data-stu-id="7fd1d-117">This member is defined as an <xref:System.Activities.ActivityAction> so that it is evaluated every time it is accessed.</span></span>  
  
- <span data-ttu-id="7fd1d-118">`Execute`：這個方法會使用 `InternalExecute`、`OnForEachComplete` 和 `GetStateAndExecute` 非共用成員來排程執行作業，並且指派 Body 成員中定義之子活動的完成處理常式。</span><span class="sxs-lookup"><span data-stu-id="7fd1d-118">`Execute`: This method uses the `InternalExecute`, `OnForEachComplete`, and `GetStateAndExecute` non-public members to schedule the execution and assign the completion handler of the child activity defined in the Body member.</span></span>  
  
- <span data-ttu-id="7fd1d-119">`CacheMetadata`：這個成員會為執行階段提供執行活動所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="7fd1d-119">`CacheMetadata`: This member provides the runtime with the information it needs to execute the activity.</span></span> <span data-ttu-id="7fd1d-120">根據預設，活動的 `CacheMetadata` 方法會將活動的所有公用成員告知執行階段，但是因為此活動會針對部分功能使用私用成員，所以它必須將這些成員的存在告知執行階段，才能讓執行階段注意它們。</span><span class="sxs-lookup"><span data-stu-id="7fd1d-120">By default, an activity’s `CacheMetadata` method will inform the runtime of all public members of the activity, but since this activity uses private members for some functionality, it needs to inform the runtime of their existence so that the runtime can be aware of them.</span></span> <span data-ttu-id="7fd1d-121">在此情況下，系統會覆寫 `CacheMetadata` 函式，以便存取私用 `valueEnumerator` 成員。</span><span class="sxs-lookup"><span data-stu-id="7fd1d-121">In this case, the `CacheMetadata` function is overridden so that the private `valueEnumerator` member can be accessed.</span></span> <span data-ttu-id="7fd1d-122">這個成員也會針對活動的值建立引數，以便在執行期間將它們傳入活動。</span><span class="sxs-lookup"><span data-stu-id="7fd1d-122">This member also creates an argument for the values for the activity so that they can be passed in to the activity during execution.</span></span>
