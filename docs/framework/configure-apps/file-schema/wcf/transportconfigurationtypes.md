---
title: <transportConfigurationTypes>
ms.date: 03/30/2017
ms.assetid: 929c8b0a-5460-4f66-a098-2cb8d4e10b69
ms.openlocfilehash: 4be08f780c1095b0016bd130b5719a2a7307d019
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "70854935"
---
# \<transportConfigurationTypes>
<span data-ttu-id="fe5b7-101">代表組態項目的集合，這些項目會識別特定傳輸的類型。</span><span class="sxs-lookup"><span data-stu-id="fe5b7-101">Represents a collection of configuration elements that identify the type of a particular transport.</span></span> <span data-ttu-id="fe5b7-102">這可以用來加入自訂 WAS 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="fe5b7-102">This can be used to add custom WAS protocols.</span></span>  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<serviceHostingEnvironment>**](servicehostingenvironment.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<transportConfigurationTypes>**  
  
## <a name="syntax"></a><span data-ttu-id="fe5b7-103">語法</span><span class="sxs-lookup"><span data-stu-id="fe5b7-103">Syntax</span></span>  
  
```xml  
<serviceHostingEnvironment>
  <transportConfigurationTypes>
    <add name="String"
         transportConfigurationType="String" />
  </transportConfigurationTypes>
</serviceHostingEnvironment>
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="fe5b7-104">屬性和項目</span><span class="sxs-lookup"><span data-stu-id="fe5b7-104">Attributes and Elements</span></span>  
 <span data-ttu-id="fe5b7-105">下列章節說明屬性、子元素和父元素。</span><span class="sxs-lookup"><span data-stu-id="fe5b7-105">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="fe5b7-106">屬性</span><span class="sxs-lookup"><span data-stu-id="fe5b7-106">Attributes</span></span>  
  
|<span data-ttu-id="fe5b7-107">屬性</span><span class="sxs-lookup"><span data-stu-id="fe5b7-107">Attribute</span></span>|<span data-ttu-id="fe5b7-108">描述</span><span class="sxs-lookup"><span data-stu-id="fe5b7-108">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="fe5b7-109">NAME</span><span class="sxs-lookup"><span data-stu-id="fe5b7-109">name</span></span>|<span data-ttu-id="fe5b7-110">傳輸的名稱</span><span class="sxs-lookup"><span data-stu-id="fe5b7-110">The name of the transport</span></span>|  
|<span data-ttu-id="fe5b7-111">transportConfigurationType</span><span class="sxs-lookup"><span data-stu-id="fe5b7-111">transportConfigurationType</span></span>|<span data-ttu-id="fe5b7-112">實作傳輸的型別</span><span class="sxs-lookup"><span data-stu-id="fe5b7-112">The type that implements the transport</span></span>|  
  
### <a name="child-elements"></a><span data-ttu-id="fe5b7-113">子元素</span><span class="sxs-lookup"><span data-stu-id="fe5b7-113">Child Elements</span></span>  
  
|<span data-ttu-id="fe5b7-114">元素</span><span class="sxs-lookup"><span data-stu-id="fe5b7-114">Element</span></span>|<span data-ttu-id="fe5b7-115">描述</span><span class="sxs-lookup"><span data-stu-id="fe5b7-115">Description</span></span>|  
|-------------|-----------------|  
|[\<add>](add-of-transportconfigurationtype.md)|<span data-ttu-id="fe5b7-116">新增組態項目，此項目會識別特定傳輸的類型。</span><span class="sxs-lookup"><span data-stu-id="fe5b7-116">Adds a configuration element that identifies the type of a particular transport.</span></span>|  
  
### <a name="parent-elements"></a><span data-ttu-id="fe5b7-117">父項目</span><span class="sxs-lookup"><span data-stu-id="fe5b7-117">Parent Elements</span></span>  
  
|<span data-ttu-id="fe5b7-118">元素</span><span class="sxs-lookup"><span data-stu-id="fe5b7-118">Element</span></span>|<span data-ttu-id="fe5b7-119">描述</span><span class="sxs-lookup"><span data-stu-id="fe5b7-119">Description</span></span>|  
|-------------|-----------------|  
|[\<serviceHostingEnvironment>](servicehostingenvironment.md)|<span data-ttu-id="fe5b7-120">定義服務裝載環境為特定傳輸產生的類型。</span><span class="sxs-lookup"><span data-stu-id="fe5b7-120">Defines the type the service hosting environment instantiates for a particular transport.</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="fe5b7-121">另請參閱</span><span class="sxs-lookup"><span data-stu-id="fe5b7-121">See also</span></span>

- <xref:System.ServiceModel.Configuration.ServiceHostingEnvironmentSection>
- <xref:System.ServiceModel.ServiceHostingEnvironment>
- <xref:System.ServiceModel.Configuration.TransportConfigurationTypeElementCollection>
- [<span data-ttu-id="fe5b7-122">Hosting</span><span class="sxs-lookup"><span data-stu-id="fe5b7-122">Hosting</span></span>](../../../wcf/feature-details/hosting.md)
