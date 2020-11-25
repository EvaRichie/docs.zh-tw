---
title: CorSymAddrKind 列舉
ms.date: 03/30/2017
api_name:
- CorSymAddrKind
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorSymAddrKind
helpviewer_keywords:
- CorSymAddrKind enumeration [.NET Framework debugging]
ms.assetid: 3ef841c2-cade-42ee-ba34-2ef91d6d0879
topic_type:
- apiref
ms.openlocfilehash: f71d8956e8706cdc71b94b6e6e2e8210e5b9161e
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95725231"
---
# <a name="corsymaddrkind-enumeration"></a><span data-ttu-id="f1158-102">CorSymAddrKind 列舉</span><span class="sxs-lookup"><span data-stu-id="f1158-102">CorSymAddrKind Enumeration</span></span>

<span data-ttu-id="f1158-103">指出記憶體位址的類型。</span><span class="sxs-lookup"><span data-stu-id="f1158-103">Indicates the type of memory address.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="f1158-104">語法</span><span class="sxs-lookup"><span data-stu-id="f1158-104">Syntax</span></span>  
  
```cpp  
typedef enum CorSymAddrKind  
{  
    ADDR_IL_OFFSET          = 1,  
    ADDR_NATIVE_RVA         = 2,  
    ADDR_NATIVE_REGISTER    = 3,  
    ADDR_NATIVE_REGREL      = 4,  
    ADDR_NATIVE_OFFSET      = 5,  
    ADDR_NATIVE_REGREG      = 6,  
    ADDR_NATIVE_REGSTK      = 7,  
    ADDR_NATIVE_STKREG      = 8,  
    ADDR_BITFIELD           = 9,  
    ADDR_NATIVE_ISECTOFFSET = 10  
} CorSymAddrKind;  
```  
  
## <a name="members"></a><span data-ttu-id="f1158-105">成員</span><span class="sxs-lookup"><span data-stu-id="f1158-105">Members</span></span>  
  
|<span data-ttu-id="f1158-106">member</span><span class="sxs-lookup"><span data-stu-id="f1158-106">Member</span></span>|<span data-ttu-id="f1158-107">描述</span><span class="sxs-lookup"><span data-stu-id="f1158-107">Description</span></span>|  
|------------|-----------------|  
|`ADDR_IL_OFFSET`|<span data-ttu-id="f1158-108">指出 Microsoft 中繼語言 (MSIL) 本機變數或參數索引。</span><span class="sxs-lookup"><span data-stu-id="f1158-108">Indicates a Microsoft intermediate language (MSIL) local variable or parameter index.</span></span>|  
|`ADDR_NATIVE_RVA`|<span data-ttu-id="f1158-109">指出模組中的相對虛擬位址。</span><span class="sxs-lookup"><span data-stu-id="f1158-109">Indicates a relative virtual address into a module.</span></span>|  
|`ADDR_NATIVE_REGISTER`|<span data-ttu-id="f1158-110">指出 CPU 暫存器。</span><span class="sxs-lookup"><span data-stu-id="f1158-110">Indicates a CPU register.</span></span>|  
|`ADDR_NATIVE_REGREL`|<span data-ttu-id="f1158-111">指出第一個位址是暫存器，而第二個位址是位移。</span><span class="sxs-lookup"><span data-stu-id="f1158-111">Indicates that the first address is a register and the second address is an offset.</span></span>|  
|`ADDR_NATIVE_OFFSET`|<span data-ttu-id="f1158-112">表示來自基底位址的位移。</span><span class="sxs-lookup"><span data-stu-id="f1158-112">Indicates an offset from a base address.</span></span>|  
|`ADDR_NATIVE_REGREG`|<span data-ttu-id="f1158-113">指出第一個位址是暫存器的低部分，而第二個位址是最高的部分。</span><span class="sxs-lookup"><span data-stu-id="f1158-113">Indicates that the first address is the low portion of a register, and the second address is the high portion.</span></span>|  
|`ADDR_NATIVE_REGSTK`|<span data-ttu-id="f1158-114">指出第一個位址是暫存器的下半部，第二個則是高部分，而第三個是位移。</span><span class="sxs-lookup"><span data-stu-id="f1158-114">Indicates that the first address is the low portion of a register, the second is the high portion, and the third is an offset.</span></span>|  
|`ADDR_NATIVE_STKREG`|<span data-ttu-id="f1158-115">指出第一個位址是暫存器，第二個是位移，而第三個位址是暫存器的最高部分。</span><span class="sxs-lookup"><span data-stu-id="f1158-115">Indicates that the first address is a register, the second is an offset, and the third is the high portion of the register.</span></span>|  
|`ADDR_BITFIELD`|<span data-ttu-id="f1158-116">指出第一個位址是欄位的開頭，而第二個位址是欄位長度。</span><span class="sxs-lookup"><span data-stu-id="f1158-116">Indicates that the first address is the start of a field and the second address is the field length.</span></span>|  
|`ADDR_NATIVE_ISECTOFFSET`|<span data-ttu-id="f1158-117">指出第一個位址是區段，而第二個位址是位移。</span><span class="sxs-lookup"><span data-stu-id="f1158-117">Indicates that the first address is the section and the second address is an offset.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="f1158-118">需求</span><span class="sxs-lookup"><span data-stu-id="f1158-118">Requirements</span></span>  

 <span data-ttu-id="f1158-119">**標頭：** CorSym .idl、CorSym。h</span><span class="sxs-lookup"><span data-stu-id="f1158-119">**Header:** CorSym.idl, CorSym.h</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="f1158-120">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f1158-120">See also</span></span>

- [<span data-ttu-id="f1158-121">診斷符號存放區列舉</span><span class="sxs-lookup"><span data-stu-id="f1158-121">Diagnostics Symbol Store Enumerations</span></span>](diagnostics-symbol-store-enumerations.md)
