---
title: ICorPublishProcessEnum::Next 方法
ms.date: 03/30/2017
api_name:
- ICorPublishProcessEnum.Next
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorPublishProcessEnum::Next
helpviewer_keywords:
- ICorPublishProcessEnum::Next method [.NET Framework debugging]
- Next method, ICorPublishProcessEnum interface [.NET Framework debugging]
ms.assetid: 6c399f37-1e38-4ca1-b70d-8ae41f7228b7
topic_type:
- apiref
ms.openlocfilehash: b3bb1857075f857f62ec92ac6a2876a49655c70e
ms.sourcegitcommit: 9a4488a3625866335e83a20da5e9c5286b1f034c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/15/2020
ms.locfileid: "83421055"
---
# <a name="icorpublishprocessenumnext-method"></a>ICorPublishProcessEnum::Next 方法
從目前的資料指標位置開始，取得集合中指定的進程數目。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT Next (  
    [in] ULONG celt,  
    [out, size_is(celt), length_is(*pceltFetched)]  
        ICorPublishProcess **objects,  
    [out] ULONG *pceltFetched  
);  
```  
  
## <a name="parameters"></a>參數  
 `celt`  
 在要抓取的進程數目。  
  
 `objects`  
 脫銷已抓取[ICorPublishProcess](icorpublishprocess-interface.md)物件之陣列的指標，每個物件都代表一個進程。  
  
 `pceltFetched`  
 脫銷實際傳回之進程數目的指標。 如果是一個，這個值可能會是 null `celt` 。  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** CorPub .idl，CorPub。h  
  
 **程式庫：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [ICorPublishProcessEnum 介面](icorpublishprocessenum-interface.md)
