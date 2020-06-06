---
title: 在查詢中使用附註
ms.date: 03/30/2017
ms.topic: reference
ms.assetid: 50855b30-d5fe-49a9-89d3-3f1bfd670958
ms.openlocfilehash: 728408e744bc1eca62158fab1a7a17e985fe3b6c
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "69947290"
---
# <a name="using-annotation-in-queries"></a><span data-ttu-id="2453e-102">在查詢中使用附註</span><span class="sxs-lookup"><span data-stu-id="2453e-102">Using Annotation in Queries</span></span>
<span data-ttu-id="2453e-103">附註可讓您使用值任意標記追蹤記錄，該值可在建置階段後設定。</span><span class="sxs-lookup"><span data-stu-id="2453e-103">Annotations allow you to arbitrarily tag tracking records with a value that can be configured after build time.</span></span> <span data-ttu-id="2453e-104">例如，您可能會想要將數個工作流程中的多個追蹤記錄標記為 "Mail Server" = = "Mail Server1"。</span><span class="sxs-lookup"><span data-stu-id="2453e-104">For example, you might want several tracking records across several workflows to be tagged with "Mail Server" == "Mail Server1".</span></span> <span data-ttu-id="2453e-105">當您稍後查詢追蹤記錄時，就可以更輕鬆地找到所有具有這個標記的記錄。</span><span class="sxs-lookup"><span data-stu-id="2453e-105">This makes it easy to find all records with this tag when querying tracking records later.</span></span>  
  
## <a name="adding-annotations"></a><span data-ttu-id="2453e-106">加入註解</span><span class="sxs-lookup"><span data-stu-id="2453e-106">Adding Annotations</span></span>  
 <span data-ttu-id="2453e-107">註解可加入至追蹤查詢，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="2453e-107">An annotation can be added to a tracking query as shown in the following example.</span></span>  
  
```xml  
<activityStateQuery activityName="SendEmailActivity">  
  <states>  
    <state name="Closed"/>  
  </states>  
  <annotations>  
    <annotation name="MailServer" value="Mail Server1"/>  
  </annotations>  
</activityStateQuery>  
```  
  
> [!NOTE]
> <span data-ttu-id="2453e-108">這些追蹤查詢項目可用來建立追蹤設定檔。</span><span class="sxs-lookup"><span data-stu-id="2453e-108">These tracking query elements can be used to create a tracking profile.</span></span> <span data-ttu-id="2453e-109">追蹤設定檔可在組態中建立，或是使用程式碼建立。</span><span class="sxs-lookup"><span data-stu-id="2453e-109">A tracking profile can be created either in configuration or using code.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="2453e-110">另請參閱</span><span class="sxs-lookup"><span data-stu-id="2453e-110">See also</span></span>

- <xref:System.ServiceModel.Activities.Tracking.Configuration.ProfileWorkflowElement>
- <xref:System.Activities.Tracking.TrackingProfile>
- [\<participants>](participants.md)
- [<span data-ttu-id="2453e-111">工作流程追蹤及追蹤</span><span class="sxs-lookup"><span data-stu-id="2453e-111">Workflow Tracking and Tracing</span></span>](../../../windows-workflow-foundation/workflow-tracking-and-tracing.md)
- [<span data-ttu-id="2453e-112">追蹤設定檔</span><span class="sxs-lookup"><span data-stu-id="2453e-112">Tracking Profiles</span></span>](../../../windows-workflow-foundation/tracking-profiles.md)
