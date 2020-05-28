---
title: CeeSectionRelocType 列舉
ms.date: 03/30/2017
api_name:
- CeeSectionRelocType
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CeeSectionRelocType
helpviewer_keywords:
- CeeSectionRelocType enumeration [.NET Framework metadata]
ms.assetid: 124656f6-0dad-4ceb-9043-d3869ab65cde
topic_type:
- apiref
ms.openlocfilehash: 78b30f624bd71234e8f1b56600b3a23d15fdf517
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/27/2020
ms.locfileid: "84006024"
---
# <a name="ceesectionreloctype-enumeration"></a>CeeSectionRelocType 列舉
提供值，以影響 `reloc` 呼叫[ICeeGen：： AddSectionReloc](iceegen-addsectionreloc-method.md)時所發出的指令類型。  
  
## <a name="syntax"></a>語法  
  
```cpp  
typedef enum  {  
    srRelocAbsolute,  
    srRelocHighLow          = 3,  
    srRelocHighAdj,
    srRelocMapToken,  
    srRelocRelative,  
    srRelocFilePos,  
    srRelocCodeRelative,  
    srRelocIA64Imm64,  
    srRelocDir64,  
    srRelocIA64PcRel25,  
    srRelocIA64PcRel64,    srRelocAbsoluteTagged,    srRelocSentinel,    srNoBaseReloc       = 0x4000,  
    srRelocPtr          = 0x8000,  
    srRelocAbsolutePtr      = srRelocPtr + srRelocAbsolute,  
    srRelocHighLowPtr       = srRelocPtr + srRelocHighLow,  
    srRelocRelativePtr      = srRelocPtr + srRelocRelative,  
    srRelocIA64Imm64Ptr     = srRelocPtr + srRelocIA64Imm64,  
    srRelocDir64Ptr         = srRelocPtr + srRelocDir64  
    } CeeSectionRelocType;  
```  
  
## <a name="members"></a>成員  
  
|成員|描述|  
|------------|-----------------|  
|`srRelocAbsolute`|只產生區段相對，不傳送 `reloc` 任何內容到 reloc 區段。|  
|`srRelocHighLow`|產生 `reloc` 指標大小位置的。 這會根據平臺轉換成 BASED_HIGHLOW 或 BASED_DIR64。|  
|`srRelocHighAdj`|`reloc`為32位數位的前16位產生，其中的下16位會包含在 reloc 資料表的下一個單字中。|  
|`srRelocMapToken`|會產生標記對應重新配置，而不傳送任何內容到 reloc 區段。|  
|`srRelocRelative`|表示此值是相對位址修復。|  
|`srRelocFilePos`|只產生區段相對，不傳送 `reloc` 任何內容到 reloc 區段。 這 `reloc` 是相對於區段的檔案位置，而不是區段的虛擬位址。|  
|`srRelocCodeRelative`|指定程式碼相對位址修復。|  
|`srRelocIA64Imm64`|`reloc`在 ia64 指示中產生64位位址的 `movl` 。|  
|`srRelocDir64`|產生 `reloc` 64 位位址的。|  
|`srRelocIA64PcRel25`|`reloc`在 ia64 指示中，為25位電腦的相對位址產生 `br.call` 。|  
|`srRelocIA64PcRel64`|`reloc`在 ia64 指示中，產生64位電腦相對位址的 `brl.call` 。|  
|`srRelocAbsoluteTagged`|產生與標記指標值相關的30位區段相對 `reloc` 。|  
|`srRelocSentinel`|Sentinel 值，可協助確保此列舉的任何新增專案都會反映到內部 `reloc` 名稱陣列。|  
|`srNoBaseReloc`|指定不發出基底 `reloc` 。|  
|`srRelocPtr`|值，表示記憶體的修復前內容是指標，而不是區段位移。|  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** Cor。h  
  
 連結**庫：** 包含為 Mscoree.dll 中的資源  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [中繼資料列舉](metadata-enumerations.md)
- [ICeeGen 介面](iceegen-interface.md)
- [AddSectionReloc 方法](iceegen-addsectionreloc-method.md)
