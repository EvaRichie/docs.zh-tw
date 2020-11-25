---
title: CorDeclSecurity 列舉
ms.date: 03/30/2017
api_name:
- CorDeclSecurity
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorDeclSecurity
helpviewer_keywords:
- CorDeclSecurity enumeration [.NET Framework metadata]
ms.assetid: 864f1267-d267-4696-8df7-1f83f8444d6f
topic_type:
- apiref
ms.openlocfilehash: dd599ce8c63fa94e1a18b4e2d18fa334238728bd
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95718874"
---
# <a name="cordeclsecurity-enumeration"></a><span data-ttu-id="112dd-102">CorDeclSecurity 列舉</span><span class="sxs-lookup"><span data-stu-id="112dd-102">CorDeclSecurity Enumeration</span></span>

<span data-ttu-id="112dd-103">指定可以使用宣告式安全性執行的安全性動作。</span><span class="sxs-lookup"><span data-stu-id="112dd-103">Specifies the security actions that can be performed using declarative security.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="112dd-104">語法</span><span class="sxs-lookup"><span data-stu-id="112dd-104">Syntax</span></span>  
  
```cpp  
typedef enum CorDeclSecurity {  
  
    dclActionMask               =   0x001f,  
    dclActionNil                =   0x0000,  
    dclRequest                  =   0x0001,  
    dclDemand                   =   0x0002,  
    dclAssert                   =   0x0003,  
    dclDeny                     =   0x0004,  
    dclPermitOnly               =   0x0005,  
    dclLinktimeCheck            =   0x0006,  
    dclInheritanceCheck         =   0x0007,  
    dclRequestMinimum           =   0x0008,  
    dclRequestOptional          =   0x0009,  
    dclRequestRefuse            =   0x000a,  
    dclPrejitGrant              =   0x000b,  
    dclPrejitDenied             =   0x000c,  
    dclNonCasDemand             =   0x000d,  
    dclNonCasLinkDemand         =   0x000e,  
    dclNonCasInheritance        =   0x000f,  
    dclLinkDemandChoice         =   0x0010,  
    dclInheritanceDemandChoice  =   0x0011,  
    dclDemandChoice             =   0x0012,  
    dclMaximumValue             =   0x0012  
  
} CorDeclSecurity;  
```  
  
## <a name="members"></a><span data-ttu-id="112dd-105">成員</span><span class="sxs-lookup"><span data-stu-id="112dd-105">Members</span></span>  
  
|<span data-ttu-id="112dd-106">member</span><span class="sxs-lookup"><span data-stu-id="112dd-106">Member</span></span>|<span data-ttu-id="112dd-107">描述</span><span class="sxs-lookup"><span data-stu-id="112dd-107">Description</span></span>|  
|------------|-----------------|  
|`dclActionMask`|<span data-ttu-id="112dd-108">保留的。</span><span class="sxs-lookup"><span data-stu-id="112dd-108">Reserved.</span></span>|  
|`dclActionNil`|<span data-ttu-id="112dd-109">保留的。</span><span class="sxs-lookup"><span data-stu-id="112dd-109">Reserved.</span></span>|  
|`dclRequest`|<span data-ttu-id="112dd-110">保留的。</span><span class="sxs-lookup"><span data-stu-id="112dd-110">Reserved.</span></span>|  
|`dclDemand`|<span data-ttu-id="112dd-111">呼叫堆疊中較高層的所有呼叫端，必須已獲得目前權限物件所指定的權限。</span><span class="sxs-lookup"><span data-stu-id="112dd-111">All callers higher in the call stack are required to have been granted the permission specified by the current permission object.</span></span>|  
|`dclAssert`|<span data-ttu-id="112dd-112">呼叫程式碼可以存取目前權限物件所識別的資源，即使堆疊中較高層的呼叫端未獲得存取資源的許可權。</span><span class="sxs-lookup"><span data-stu-id="112dd-112">The calling code can access the resource identified by the current permission object, even if callers higher in the stack have not been granted permission to access the resource</span></span>|  
|`dclDeny`|<span data-ttu-id="112dd-113">呼叫端會拒絕存取目前權限物件所指定之資源的能力，即使它們已獲得存取權。</span><span class="sxs-lookup"><span data-stu-id="112dd-113">The ability to access the resource specified by the current permission object is denied to callers, even if they have been granted permission to access it.</span></span>|  
|`dclPermitOnly`|<span data-ttu-id="112dd-114">只可存取這個權限物件所指定的資源，即使程式碼已獲得其他資源存取權限亦然。</span><span class="sxs-lookup"><span data-stu-id="112dd-114">Only the resources specified by this permission object can be accessed, even if the code has been granted permission to access other resources.</span></span>|  
|`dclLinktimeCheck`|<span data-ttu-id="112dd-115">立即呼叫端必須在指定的時間內被授與指定的許可權。</span><span class="sxs-lookup"><span data-stu-id="112dd-115">The immediate caller is required to have been granted the specified permission for a given period of time.</span></span>|  
|`dclInheritanceCheck`|<span data-ttu-id="112dd-116">繼承另一個類別或覆寫方法的衍生類別必須被授與指定的許可權。</span><span class="sxs-lookup"><span data-stu-id="112dd-116">The derived class inheriting another class or overriding a method is required to have been granted the specified permission.</span></span>|  
|`dclRequestMinimum`|<span data-ttu-id="112dd-117">呼叫端可以要求執行程式碼所需的最低許可權。</span><span class="sxs-lookup"><span data-stu-id="112dd-117">The caller can request for the minimum permissions required for code to run.</span></span> <span data-ttu-id="112dd-118">這個動作只能在組件的範圍內使用。</span><span class="sxs-lookup"><span data-stu-id="112dd-118">This action can only be used within the scope of the assembly.</span></span>|  
|`dclRequestOptional`|<span data-ttu-id="112dd-119">呼叫端可以要求其他許可權，這些許可權是選擇性的 (不需要執行) 。</span><span class="sxs-lookup"><span data-stu-id="112dd-119">The caller can request for additional permissions that are optional (not required to run).</span></span> <span data-ttu-id="112dd-120">這項要求會隱含拒絕未特別要求的所有其他權限。</span><span class="sxs-lookup"><span data-stu-id="112dd-120">This request implicitly refuses all other permissions not specifically requested.</span></span> <span data-ttu-id="112dd-121">這個動作只能在組件的範圍內使用。</span><span class="sxs-lookup"><span data-stu-id="112dd-121">This action can only be used within the scope of the assembly.</span></span>|  
|`dclRequestRefuse`|<span data-ttu-id="112dd-122">系統將不會授與呼叫端可能被誤用之許可權的要求。</span><span class="sxs-lookup"><span data-stu-id="112dd-122">The caller's request for permissions that might be misused will not be granted.</span></span> <span data-ttu-id="112dd-123">這個動作只能在組件的範圍內使用。</span><span class="sxs-lookup"><span data-stu-id="112dd-123">This action can only be used within the scope of the assembly.</span></span>|  
|`dclPrejitGrant`|<span data-ttu-id="112dd-124">保留的。</span><span class="sxs-lookup"><span data-stu-id="112dd-124">Reserved.</span></span>|  
|`dclPrejitDenied`|<span data-ttu-id="112dd-125">保留的。</span><span class="sxs-lookup"><span data-stu-id="112dd-125">Reserved.</span></span>|  
|`dclNonCasDemand`|<span data-ttu-id="112dd-126">保留的。</span><span class="sxs-lookup"><span data-stu-id="112dd-126">Reserved.</span></span>|  
|`dclNonCasLinkDemand`|<span data-ttu-id="112dd-127">直接呼叫端必須已獲得指定權限。</span><span class="sxs-lookup"><span data-stu-id="112dd-127">The immediate caller is required to have been granted the specified permission.</span></span>|  
|`dclNonCasInheritance`|<span data-ttu-id="112dd-128">保留的。</span><span class="sxs-lookup"><span data-stu-id="112dd-128">Reserved.</span></span>|  
|`dclLinkDemandChoice`|<span data-ttu-id="112dd-129">保留的。</span><span class="sxs-lookup"><span data-stu-id="112dd-129">Reserved.</span></span>|  
|`dclInheritanceDemandChoice`|<span data-ttu-id="112dd-130">保留的。</span><span class="sxs-lookup"><span data-stu-id="112dd-130">Reserved.</span></span>|  
|`dclDemandChoice`|<span data-ttu-id="112dd-131">保留的。</span><span class="sxs-lookup"><span data-stu-id="112dd-131">Reserved.</span></span>|  
|`dclMaximumValue`|<span data-ttu-id="112dd-132">保留的。</span><span class="sxs-lookup"><span data-stu-id="112dd-132">Reserved.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="112dd-133">需求</span><span class="sxs-lookup"><span data-stu-id="112dd-133">Requirements</span></span>  

 <span data-ttu-id="112dd-134">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="112dd-134">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="112dd-135">**標頭：** Corhdr.h。h</span><span class="sxs-lookup"><span data-stu-id="112dd-135">**Header:** CorHdr.h</span></span>  
  
 <span data-ttu-id="112dd-136">**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="112dd-136">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="112dd-137">另請參閱</span><span class="sxs-lookup"><span data-stu-id="112dd-137">See also</span></span>

- [<span data-ttu-id="112dd-138">中繼資料列舉</span><span class="sxs-lookup"><span data-stu-id="112dd-138">Metadata Enumerations</span></span>](metadata-enumerations.md)
