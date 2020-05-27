---
title: CorFileFlags 列舉
ms.date: 03/30/2017
api_name:
- CorFileFlags
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorFileFlags
helpviewer_keywords:
- CorFileFlags enumeration [.NET Framework metadata]
ms.assetid: d16703fd-518f-412e-92cb-74433d11032e
topic_type:
- apiref
ms.openlocfilehash: c8c2757e99b80204ad52e69a596d62c55c369965
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/27/2020
ms.locfileid: "84007412"
---
# <a name="corfileflags-enumeration"></a><span data-ttu-id="c20a5-102">CorFileFlags 列舉</span><span class="sxs-lookup"><span data-stu-id="c20a5-102">CorFileFlags Enumeration</span></span>
<span data-ttu-id="c20a5-103">包含值，描述在[IMetaDataAssemblyEmit：:D efinefile](imetadataassemblyemit-definefile-method.md)的呼叫中所定義的檔案類型。</span><span class="sxs-lookup"><span data-stu-id="c20a5-103">Contains values that describe the type of file defined in a call to [IMetaDataAssemblyEmit::DefineFile](imetadataassemblyemit-definefile-method.md).</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="c20a5-104">語法</span><span class="sxs-lookup"><span data-stu-id="c20a5-104">Syntax</span></span>  
  
```cpp  
typedef enum CorFileFlags {  
  
    ffContainsMetaData      =   0x0000,  
    ffContainsNoMetaData    =   0x0001  
  
} CorFileFlags;  
```  
  
## <a name="members"></a><span data-ttu-id="c20a5-105">成員</span><span class="sxs-lookup"><span data-stu-id="c20a5-105">Members</span></span>  
  
|<span data-ttu-id="c20a5-106">成員</span><span class="sxs-lookup"><span data-stu-id="c20a5-106">Member</span></span>|<span data-ttu-id="c20a5-107">描述</span><span class="sxs-lookup"><span data-stu-id="c20a5-107">Description</span></span>|  
|------------|-----------------|  
|`ffContainsMetaData`|<span data-ttu-id="c20a5-108">表示檔案不是資源檔。</span><span class="sxs-lookup"><span data-stu-id="c20a5-108">Indicates that the file is not a resource file.</span></span>|  
|`ffContainsNoMetaData`|<span data-ttu-id="c20a5-109">指出檔案（可能是資源檔）不包含中繼資料。</span><span class="sxs-lookup"><span data-stu-id="c20a5-109">Indicates that the file, possibly a resource file, does not contain metadata.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="c20a5-110">需求</span><span class="sxs-lookup"><span data-stu-id="c20a5-110">Requirements</span></span>  
 <span data-ttu-id="c20a5-111">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="c20a5-111">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="c20a5-112">**標頭：** Corhdr.h。h</span><span class="sxs-lookup"><span data-stu-id="c20a5-112">**Header:** CorHdr.h</span></span>  
  
 <span data-ttu-id="c20a5-113">**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="c20a5-113">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="c20a5-114">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c20a5-114">See also</span></span>

- [<span data-ttu-id="c20a5-115">中繼資料列舉</span><span class="sxs-lookup"><span data-stu-id="c20a5-115">Metadata Enumerations</span></span>](metadata-enumerations.md)
