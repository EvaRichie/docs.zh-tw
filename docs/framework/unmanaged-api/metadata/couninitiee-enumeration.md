---
title: COUNINITIEE 列舉
ms.date: 03/30/2017
api_name:
- COUNINITIEE
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- COUNINITIEE
helpviewer_keywords:
- COUNINITIEE enumeration [.NET Framework metadata]
ms.assetid: c42baa79-f469-4330-95a2-baf7f021c2fc
topic_type:
- apiref
ms.openlocfilehash: b0f8c7e6d2acf4d4c080cc147bf6d42bf13cb51b
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95723827"
---
# <a name="couninitiee-enumeration"></a><span data-ttu-id="37323-102">COUNINITIEE 列舉</span><span class="sxs-lookup"><span data-stu-id="37323-102">COUNINITIEE Enumeration</span></span>

<span data-ttu-id="37323-103">指定初始化 common language runtime 時， [CoUninitializeEE](../hosting/couninitializeee-function.md) 所使用的常數。</span><span class="sxs-lookup"><span data-stu-id="37323-103">Specifies constants used by [CoUninitializeEE](../hosting/couninitializeee-function.md) when initializing the common language runtime.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="37323-104">語法</span><span class="sxs-lookup"><span data-stu-id="37323-104">Syntax</span></span>  
  
```cpp  
typedef enum tagCOUNINITEE  
{  
    COUNINITEE_DEFAULT  = 0x0,
    COUNINITEE_DLL      = 0x1  
} COUNINITIEE;  
```  
  
## <a name="members"></a><span data-ttu-id="37323-105">成員</span><span class="sxs-lookup"><span data-stu-id="37323-105">Members</span></span>  
  
|<span data-ttu-id="37323-106">member</span><span class="sxs-lookup"><span data-stu-id="37323-106">Member</span></span>|<span data-ttu-id="37323-107">描述</span><span class="sxs-lookup"><span data-stu-id="37323-107">Description</span></span>|  
|------------|-----------------|  
|`COUNINITEE_DEFAULT`|<span data-ttu-id="37323-108">表示預設的解除初始化模式。</span><span class="sxs-lookup"><span data-stu-id="37323-108">Indicates default uninitialization mode.</span></span>|  
|`COUNINITEE_DLL`|<span data-ttu-id="37323-109">表示卸載元件的解除初始化模式。</span><span class="sxs-lookup"><span data-stu-id="37323-109">Indicates uninitialization mode for unloading an assembly.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="37323-110">需求</span><span class="sxs-lookup"><span data-stu-id="37323-110">Requirements</span></span>  

 <span data-ttu-id="37323-111">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="37323-111">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="37323-112">**標頭：** Cor。h</span><span class="sxs-lookup"><span data-stu-id="37323-112">**Header:** Cor.h</span></span>  
  
 <span data-ttu-id="37323-113">連結 **庫：** 以資源的形式包含在 MsCorEE.dll 中</span><span class="sxs-lookup"><span data-stu-id="37323-113">**Library:** Included as a resource in MsCorEE.dll</span></span>  
  
 <span data-ttu-id="37323-114">**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="37323-114">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="37323-115">另請參閱</span><span class="sxs-lookup"><span data-stu-id="37323-115">See also</span></span>

- [<span data-ttu-id="37323-116">中繼資料列舉</span><span class="sxs-lookup"><span data-stu-id="37323-116">Metadata Enumerations</span></span>](metadata-enumerations.md)
