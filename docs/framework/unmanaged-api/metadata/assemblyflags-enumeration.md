---
title: AssemblyFlags 列舉
ms.date: 03/30/2017
api_name:
- AssemblyFlags
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- AssemblyFlags
helpviewer_keywords:
- AssemblyFlags enumeration [.NET Framework metadata]
ms.assetid: 40f9bd9e-16ec-447e-81b0-168c875e9866
topic_type:
- apiref
ms.openlocfilehash: 1cb84b94b37a2e9e8dd4d20d09cbca82db290c0f
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/27/2020
ms.locfileid: "84009443"
---
# <a name="assemblyflags-enumeration"></a>AssemblyFlags 列舉
包含描述元件執行時間功能的值。  
  
## <a name="syntax"></a>語法  
  
```cpp  
typedef enum {  
    afImplicitExportedTypes = 0x0001,  
    afImplicitResources = 0x0002,  
    afNonSideBySideAppDomain = 0x0010,  
    afNonSideBySideProcess = 0x0020,  
    afNonSideBySideMachine = 0x0030  
} AssemblyFlags;  
```  
  
## <a name="members"></a>成員  
  
|成員|描述|  
|------------|-----------------|  
|`afImplicitExportedTypes`|指定匯出的類型定義在組成元件的檔案中是隱含的。 在 .NET Framework 版本1.0 和1.1 中，一律假設已設定此值。|  
|`afImplicitResources`|指定資源定義在組成元件的檔案中是隱含的。 在 .NET Framework 1.0 和1.1 中，一律假設已設定此值。|  
|`afNonSideBySideAppDomain`|指定如果元件在相同的應用程式域中執行，則無法與其他版本一起執行。|  
|`afNonSideBySideProcess`|指定如果元件在相同的進程中執行，則無法與其他版本一起執行。|  
|`afNonSideBySideMachine`|指定如果元件在同一部電腦上執行，則無法與其他版本一起執行。|  
  
## <a name="remarks"></a>備註  
 0x0010 和0x0070 之間的值（含）是用來描述所參考元件的並存相容性功能。 如果未設定這些值，則會假設元件與並存相容。  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** Mscoree.dll. h  
  
 連結**庫：** 包含為 Mscoree.dll 中的資源  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [中繼資料列舉](metadata-enumerations.md)
- [IMetaDataAssemblyEmit 介面](imetadataassemblyemit-interface.md)
