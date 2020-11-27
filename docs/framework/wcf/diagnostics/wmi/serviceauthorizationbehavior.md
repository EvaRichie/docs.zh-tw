---
title: ServiceAuthorizationBehavior
ms.date: 03/30/2017
ms.assetid: 77dad8e8-fea4-4d1c-b366-2f01a2a87f78
ms.openlocfilehash: d3625865484568746888ef0638d9a8501e610bef
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96273200"
---
# <a name="serviceauthorizationbehavior"></a><span data-ttu-id="796a8-102">ServiceAuthorizationBehavior</span><span class="sxs-lookup"><span data-stu-id="796a8-102">ServiceAuthorizationBehavior</span></span>

<span data-ttu-id="796a8-103">ServiceAuthorizationBehavior</span><span class="sxs-lookup"><span data-stu-id="796a8-103">ServiceAuthorizationBehavior</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="796a8-104">Syntax</span><span class="sxs-lookup"><span data-stu-id="796a8-104">Syntax</span></span>  
  
```csharp
class ServiceAuthorizationBehavior : Behavior  
{  
  boolean ImpersonateCallerForAllOperations;  
  string PrincipalPermissionMode;  
  string RoleProvider;  
  string ServiceAuthorizationManager;  
};  
```  
  
## <a name="methods"></a><span data-ttu-id="796a8-105">方法</span><span class="sxs-lookup"><span data-stu-id="796a8-105">Methods</span></span>  

 <span data-ttu-id="796a8-106">ServiceAuthorizationBehavior 類別不會定義任何方法。</span><span class="sxs-lookup"><span data-stu-id="796a8-106">The ServiceAuthorizationBehavior class does not define any methods.</span></span>  
  
## <a name="properties"></a><span data-ttu-id="796a8-107">屬性</span><span class="sxs-lookup"><span data-stu-id="796a8-107">Properties</span></span>  

 <span data-ttu-id="796a8-108">ServiceAuthorizationBehavior 類別具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="796a8-108">The ServiceAuthorizationBehavior class has the following properties:</span></span>  
  
### <a name="impersonatecallerforalloperations"></a><span data-ttu-id="796a8-109">ImpersonateCallerForAllOperations</span><span class="sxs-lookup"><span data-stu-id="796a8-109">ImpersonateCallerForAllOperations</span></span>  

 <span data-ttu-id="796a8-110">資料型別：布林值</span><span class="sxs-lookup"><span data-stu-id="796a8-110">Data type: boolean</span></span>  
  
 <span data-ttu-id="796a8-111">存取類型：唯讀</span><span class="sxs-lookup"><span data-stu-id="796a8-111">Access type: Read-only</span></span>  
  
 <span data-ttu-id="796a8-112">值，控制服務是否使用傳入訊息所提供的認證來嘗試模擬。</span><span class="sxs-lookup"><span data-stu-id="796a8-112">A value that controls whether the service attempts to impersonate using the credentials provided by the incoming message.</span></span>  
  
### <a name="principalpermissionmode"></a><span data-ttu-id="796a8-113">PrincipalPermissionMode</span><span class="sxs-lookup"><span data-stu-id="796a8-113">PrincipalPermissionMode</span></span>  

 <span data-ttu-id="796a8-114">資料類型：字串</span><span class="sxs-lookup"><span data-stu-id="796a8-114">Data type: string</span></span>  
  
 <span data-ttu-id="796a8-115">存取類型：唯讀</span><span class="sxs-lookup"><span data-stu-id="796a8-115">Access type: Read-only</span></span>  
  
 <span data-ttu-id="796a8-116">用於在伺服器上執行作業的原則。</span><span class="sxs-lookup"><span data-stu-id="796a8-116">The principal used to carry out operations on the server.</span></span>  
  
### <a name="roleprovider"></a><span data-ttu-id="796a8-117">RoleProvider</span><span class="sxs-lookup"><span data-stu-id="796a8-117">RoleProvider</span></span>  

 <span data-ttu-id="796a8-118">資料類型：字串</span><span class="sxs-lookup"><span data-stu-id="796a8-118">Data type: string</span></span>  
  
 <span data-ttu-id="796a8-119">存取類型：唯讀</span><span class="sxs-lookup"><span data-stu-id="796a8-119">Access type: Read-only</span></span>  
  
 <span data-ttu-id="796a8-120">ASP.NET 角色提供者的名稱。</span><span class="sxs-lookup"><span data-stu-id="796a8-120">The name of the ASP.NET role provider.</span></span>  
  
### <a name="serviceauthorizationmanager"></a><span data-ttu-id="796a8-121">ServiceAuthorizationManager</span><span class="sxs-lookup"><span data-stu-id="796a8-121">ServiceAuthorizationManager</span></span>  

 <span data-ttu-id="796a8-122">資料類型：字串</span><span class="sxs-lookup"><span data-stu-id="796a8-122">Data type: string</span></span>  
  
 <span data-ttu-id="796a8-123">存取類型：唯讀</span><span class="sxs-lookup"><span data-stu-id="796a8-123">Access type: Read-only</span></span>  
  
 <span data-ttu-id="796a8-124">用於自訂授權的授權管理員。</span><span class="sxs-lookup"><span data-stu-id="796a8-124">The authorization manager used for custom authorization.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="796a8-125">規格需求</span><span class="sxs-lookup"><span data-stu-id="796a8-125">Requirements</span></span>  
  
|<span data-ttu-id="796a8-126">MOF</span><span class="sxs-lookup"><span data-stu-id="796a8-126">MOF</span></span>|<span data-ttu-id="796a8-127">於 Servicemodel.mof 中宣告。</span><span class="sxs-lookup"><span data-stu-id="796a8-127">Declared in Servicemodel.mof.</span></span>|  
|---------|-----------------------------------|  
|<span data-ttu-id="796a8-128">命名空間</span><span class="sxs-lookup"><span data-stu-id="796a8-128">Namespace</span></span>|<span data-ttu-id="796a8-129">於 root\ServiceModel 中定義</span><span class="sxs-lookup"><span data-stu-id="796a8-129">Defined in root\ServiceModel</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="796a8-130">另請參閱</span><span class="sxs-lookup"><span data-stu-id="796a8-130">See also</span></span>

- <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior>
