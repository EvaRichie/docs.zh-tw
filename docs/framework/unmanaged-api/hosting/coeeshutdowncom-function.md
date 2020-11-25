---
title: CoEEShutDownCOM 函式
ms.date: 03/30/2017
api_name:
- CoEEShutDownCOM
api_location:
- mscoree.dll
- clr.dll
- mscorwks.dll
- mscoreei.dll
- mscorsvr.dll
api_type:
- DLLExport
f1_keywords:
- CoEEShutDownCOM
helpviewer_keywords:
- CoEEShutDownCOM function [.NET Framework hosting]
ms.assetid: b634cae2-632f-4737-9be4-92d0652844d7
topic_type:
- apiref
ms.openlocfilehash: 774704698f92d546d6bafa61c65d18d083c65f89
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95716755"
---
# <a name="coeeshutdowncom-function"></a>CoEEShutDownCOM 函式

強制 common language runtime (CLR) 釋放它在執行時間可呼叫包裝函式中的所有介面指標 (RCW) 。 這有釋放所有 RCW 快取的效果。 此全域函式已在 .NET Framework 4 中淘汰。 相反地，請使用特定執行時間的進入點。  
  
## <a name="syntax"></a>語法  
  
```cpp  
void CoEEShutDownCOM ();  
```  
  
## <a name="remarks"></a>備註  

 此函式會 `CoEEShutDownCOM` 先釋出所有內容和所有快取中的所有 rcw，然後移除安裝程式中現有的任何終止通知。 不會卸載任何 DLL。  
  
> [!CAUTION]
> 此函式會影響載入至進程的所有執行時間。  
  
 從 .NET Framework 4 開始，請在您想要影響的特定執行時間上，呼叫此函式的進入點。 若要取得進入點，請呼叫 [ICLRRuntimeInfo：： GetProcAddress](iclrruntimeinfo-getprocaddress-method.md) 方法，並指定 "CoEEShutDownCOM"。  
  
## <a name="requirements"></a>需求  

 **平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** Cor。h  
  
 連結 **庫：** 以資源的形式包含在 MsCorEE.dll 中  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [中繼資料全域靜態函式](../metadata/metadata-global-static-functions.md)
