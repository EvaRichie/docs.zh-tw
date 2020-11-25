---
title: COR_IL_MAP 結構
ms.date: 03/30/2017
api_name:
- COR_IL_MAP
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- COR_IL_MAP
helpviewer_keywords:
- COR_IL_MAP structure [.NET Framework debugging]
ms.assetid: 534ebc17-963d-4b26-8375-8cd940281db3
topic_type:
- apiref
ms.openlocfilehash: fb6b5d43e60b52c867535c42d59a098ef3c959bc
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95726379"
---
# <a name="cor_il_map-structure"></a>COR_IL_MAP 結構

指定函式相關位移中的變更。  
  
## <a name="syntax"></a>語法  
  
```cpp  
typedef struct _COR_IL_MAP {  
    ULONG32 oldOffset;
    ULONG32 newOffset;
    BOOL    fAccurate;  
} COR_IL_MAP;  
```  
  
## <a name="members"></a>成員  
  
|member|描述|  
|------------|-----------------|  
|`oldOffset`|舊版 Microsoft 中繼語言 (MSIL) 相對於函數開頭的位移。|  
|`newOffset`|相對於函數開頭的新 MSIL 位移。|  
|`fAccurate`|`true` 如果已知對應是正確的，否則為 `false` 。|  
  
## <a name="remarks"></a>備註  

 對應的格式如下所示：偵錯工具會假設 `oldOffset` 參考原始、未修改之 msil 程式碼內的 MSIL 位移。 `newOffset`參數會參考新檢測程式碼內的對應 MSIL 位移。  
  
 若要讓逐步執行正常運作，應符合下列需求：  
  
- 地圖應該以遞增順序排序。  
  
- 已檢測的 MSIL 程式碼不應重新排序。  
  
- 不應移除原始 MSIL 程式碼。  
  
- 對應應包含專案，以對應程式資料庫 (PDB) 檔中的所有序列點。  
  
 地圖不會插補遺漏的專案。 下列範例顯示對應和其結果。  
  
 地圖：  
  
- 0舊位移，0新位移  
  
- 5個舊的位移，10個新的位移  
  
- 9個舊的位移，20個新的位移  
  
 結果：  
  
- 舊的位移0、1、2、3或4將會對應至新的位移0。  
  
- 舊的位移5、6、7或8將會對應至新的位移10。  
  
- 舊位移9或更高版本將會對應至新的位移20。  
  
- 新的位移0、1、2、3、4、5、6、7、8或9將會對應到舊的位移0。  
  
- 新的位移10、11、12、13、14、15、16、17、18或19將會對應到舊的位移5。  
  
- 新的位移20或更高的位移會對應到舊的位移9。  
  
## <a name="requirements"></a>需求  

 **平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** Cordebug.h .idl，Corprof.h .idl  
  
 **程式庫：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [偵錯結構](debugging-structures.md)
- [偵錯](index.md)
