---
title: ICeeGen::GetSectionBlock 方法
ms.date: 03/30/2017
api_name:
- ICeeGen.GetSectionBlock
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICeeGen::GetSectionBlock
helpviewer_keywords:
- GetSectionBlock method [.NET Framework metadata]
- ICeeGen::GetSectionBlock method [.NET Framework metadata]
ms.assetid: 05c78aaf-5bbd-497e-9ae2-55f4fae0c5fb
topic_type:
- apiref
ms.openlocfilehash: ed534890fc90d3b8543a1166c85903f10163f0a8
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/27/2020
ms.locfileid: "84008314"
---
# <a name="iceegengetsectionblock-method"></a>ICeeGen::GetSectionBlock 方法
取得程式碼基底的區段區塊。  
  
 這個方法已過時，不應使用。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT GetSectionBlock (  
    [in]  HCEESECTION    section,
    [in]  ULONG          len,  
    [in]  ULONG          align     = 1,  
    [out] void           **ppBytes = 0  
);
```  
  
## <a name="parameters"></a>參數  
 `section`  
 在要從中取得程式碼基底區塊的區段。  
  
 `len`  
 在要抓取的區塊長度。  
  
 `align`  
 在相對於區段開頭的位元組，用來對齊區塊的第一個位元組。 這是區段內區塊的位置。  
  
 `ppBytes`  
 脫銷接收所抓取區塊位址之位置的指標。  
  
## <a name="remarks"></a>備註  
 `GetSectionBlock`只有當您有其他方法未處理的特殊區段需求時，才需要呼叫。  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** Cor。h  
  
 連結**庫：** 做為 Mscoree.dll 中的資源使用  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [ICeeGen 介面](iceegen-interface.md)
