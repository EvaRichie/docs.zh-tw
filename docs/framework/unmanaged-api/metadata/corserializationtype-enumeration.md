---
title: CorSerializationType 列舉
ms.date: 03/30/2017
api_name:
- CorSerializationType
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorSerializationType
helpviewer_keywords:
- CorSerializationType enumeration [.NET Framework metadata]
ms.assetid: 6b1fcd11-c7fb-4be2-8910-abc862d4caf4
topic_type:
- apiref
ms.openlocfilehash: e9c9674bfe0e5a8006a4881e103b633ee8f2af1d
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95706044"
---
# <a name="corserializationtype-enumeration"></a><span data-ttu-id="edf30-102">CorSerializationType 列舉</span><span class="sxs-lookup"><span data-stu-id="edf30-102">CorSerializationType Enumeration</span></span>

<span data-ttu-id="edf30-103">指定由 common language runtime 序列化物件的方式。</span><span class="sxs-lookup"><span data-stu-id="edf30-103">Specifies how an object is serialized by the common language runtime.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="edf30-104">語法</span><span class="sxs-lookup"><span data-stu-id="edf30-104">Syntax</span></span>  
  
```cpp  
typedef enum CorSerializationType {  
  
    SERIALIZATION_TYPE_UNDEFINED     = 0,  
    SERIALIZATION_TYPE_BOOLEAN       = ELEMENT_TYPE_BOOLEAN,  
    SERIALIZATION_TYPE_CHAR          = ELEMENT_TYPE_CHAR,  
    SERIALIZATION_TYPE_I1            = ELEMENT_TYPE_I1,  
    SERIALIZATION_TYPE_U1            = ELEMENT_TYPE_U1,  
    SERIALIZATION_TYPE_I2            = ELEMENT_TYPE_I2,  
    SERIALIZATION_TYPE_U2            = ELEMENT_TYPE_U2,  
    SERIALIZATION_TYPE_I4            = ELEMENT_TYPE_I4,  
    SERIALIZATION_TYPE_U4            = ELEMENT_TYPE_U4,  
    SERIALIZATION_TYPE_I8            = ELEMENT_TYPE_I8,  
    SERIALIZATION_TYPE_U8            = ELEMENT_TYPE_U8,  
    SERIALIZATION_TYPE_R4            = ELEMENT_TYPE_R4,  
    SERIALIZATION_TYPE_R8            = ELEMENT_TYPE_R8,  
    SERIALIZATION_TYPE_STRING        = ELEMENT_TYPE_STRING,  
    SERIALIZATION_TYPE_SZARRAY       = ELEMENT_TYPE_SZARRAY,  
    SERIALIZATION_TYPE_TYPE          = 0x50,  
    SERIALIZATION_TYPE_TAGGED_OBJECT = 0x51,  
    SERIALIZATION_TYPE_FIELD         = 0x53,  
    SERIALIZATION_TYPE_PROPERTY      = 0x54,  
    SERIALIZATION_TYPE_ENUM          = 0x55  
  
} CorSerializationType;  
```  
  
## <a name="members"></a><span data-ttu-id="edf30-105">成員</span><span class="sxs-lookup"><span data-stu-id="edf30-105">Members</span></span>  
  
|<span data-ttu-id="edf30-106">member</span><span class="sxs-lookup"><span data-stu-id="edf30-106">Member</span></span>|<span data-ttu-id="edf30-107">描述</span><span class="sxs-lookup"><span data-stu-id="edf30-107">Description</span></span>|  
|------------|-----------------|  
|`SERIALIZATION_TYPE_UNDEFINED`|<span data-ttu-id="edf30-108">未定義物件的序列化。</span><span class="sxs-lookup"><span data-stu-id="edf30-108">Serialization of the object is undefined.</span></span>|  
|`SERIALIZATION_TYPE_BOOLEAN`|<span data-ttu-id="edf30-109">物件序列化為布林類型</span><span class="sxs-lookup"><span data-stu-id="edf30-109">Object is serialized as a Boolean type</span></span>|  
|`SERIALIZATION_TYPE_CHAR`|<span data-ttu-id="edf30-110">物件會序列化為字元類型。</span><span class="sxs-lookup"><span data-stu-id="edf30-110">Object is serialized as a character type.</span></span>|  
|`SERIALIZATION_TYPE_I1`|<span data-ttu-id="edf30-111">物件會序列化為帶正負號的1位元組整數。</span><span class="sxs-lookup"><span data-stu-id="edf30-111">Object is serialized as a signed 1-byte integer.</span></span>|  
|`SERIALIZATION_TYPE_U1`|<span data-ttu-id="edf30-112">物件會序列化為不帶正負號的1位元組整數。</span><span class="sxs-lookup"><span data-stu-id="edf30-112">Object is serialized as an unsigned 1-byte integer.</span></span>|  
|`SERIALIZATION_TYPE_I2`|<span data-ttu-id="edf30-113">物件會序列化為帶正負號的2位元組整數。</span><span class="sxs-lookup"><span data-stu-id="edf30-113">Object is serialized as a signed 2-byte integer.</span></span>|  
|`SERIALIZATION_TYPE_U2`|<span data-ttu-id="edf30-114">物件會序列化為不帶正負號的2位元組整數。</span><span class="sxs-lookup"><span data-stu-id="edf30-114">Object is serialized as an unsigned 2-byte integer.</span></span>|  
|`SERIALIZATION_TYPE_I4`|<span data-ttu-id="edf30-115">物件會序列化為帶正負號的4位元組整數。</span><span class="sxs-lookup"><span data-stu-id="edf30-115">Object is serialized as a signed 4-byte integer.</span></span>|  
|`SERIALIZATION_TYPE_U4`|<span data-ttu-id="edf30-116">物件會序列化為不帶正負號的4位元組整數。</span><span class="sxs-lookup"><span data-stu-id="edf30-116">Object is serialized as an unsigned 4-byte integer.</span></span>|  
|`SERIALIZATION_TYPE_I8`|<span data-ttu-id="edf30-117">物件會序列化為帶正負號的8位元組整數。</span><span class="sxs-lookup"><span data-stu-id="edf30-117">Object is serialized as a signed 8-byte integer.</span></span>|  
|`SERIALIZATION_TYPE_U8`|<span data-ttu-id="edf30-118">物件會序列化為不帶正負號的8位元組整數。</span><span class="sxs-lookup"><span data-stu-id="edf30-118">Object is serialized as an unsigned 8-byte integer.</span></span>|  
|`SERIALIZATION_TYPE_R4`|<span data-ttu-id="edf30-119">物件會序列化為4位元組浮點數。</span><span class="sxs-lookup"><span data-stu-id="edf30-119">Object is serialized as a 4-byte floating point.</span></span>|  
|`SERIALIZATION_TYPE_R8`|<span data-ttu-id="edf30-120">物件會序列化為8位元組浮點數。</span><span class="sxs-lookup"><span data-stu-id="edf30-120">Object is serialized as an 8-byte floating point.</span></span>|  
|`SERIALIZATION_TYPE_STRING`|<span data-ttu-id="edf30-121">物件會序列化為 System.string 類型。</span><span class="sxs-lookup"><span data-stu-id="edf30-121">Object is serialized as a System.String type.</span></span>|  
|`SERIALIZATION_TYPE_SZARRAY`|<span data-ttu-id="edf30-122">物件會序列化為一維、零下限的陣列。</span><span class="sxs-lookup"><span data-stu-id="edf30-122">Object is serialized as a single-dimensional, zero lower-bound array.</span></span>|  
|`SERIALIZATION_TYPE_TYPE`|<span data-ttu-id="edf30-123">物件會序列化為泛型型別。</span><span class="sxs-lookup"><span data-stu-id="edf30-123">Object is serialized as a generic type.</span></span>|  
|`SERIALIZATION_TYPE_TAGGED_OBJECT`|<span data-ttu-id="edf30-124">物件會序列化為加上標籤的物件。</span><span class="sxs-lookup"><span data-stu-id="edf30-124">Object is serialized as a tagged object.</span></span>|  
|`SERIALIZATION_TYPE_FIELD`|<span data-ttu-id="edf30-125">物件會序列化為欄位。</span><span class="sxs-lookup"><span data-stu-id="edf30-125">Object is serialized as a field.</span></span>|  
|`SERIALIZATION_TYPE_PROPERTY`|<span data-ttu-id="edf30-126">物件會序列化為屬性。</span><span class="sxs-lookup"><span data-stu-id="edf30-126">Object is serialized as a property.</span></span>|  
|`SERIALIZATION_TYPE_ENUM`|<span data-ttu-id="edf30-127">物件會序列化為列舉。</span><span class="sxs-lookup"><span data-stu-id="edf30-127">Object is serialized as an enumeration.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="edf30-128">需求</span><span class="sxs-lookup"><span data-stu-id="edf30-128">Requirements</span></span>  

 <span data-ttu-id="edf30-129">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="edf30-129">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="edf30-130">**標頭：** Corhdr.h。h</span><span class="sxs-lookup"><span data-stu-id="edf30-130">**Header:** CorHdr.h</span></span>  
  
 <span data-ttu-id="edf30-131">**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="edf30-131">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="edf30-132">另請參閱</span><span class="sxs-lookup"><span data-stu-id="edf30-132">See also</span></span>

- [<span data-ttu-id="edf30-133">中繼資料列舉</span><span class="sxs-lookup"><span data-stu-id="edf30-133">Metadata Enumerations</span></span>](metadata-enumerations.md)
