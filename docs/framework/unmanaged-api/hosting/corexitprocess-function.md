---
title: CorExitProcess 函式
ms.date: 03/30/2017
api_name:
- CorExitProcess
api_location:
- mscoree.dll
- clr.dll
- mscorwks.dll
- mscoreei.dll
- mscorsvr.dll
api_type:
- DLLExport
f1_keywords:
- CorExitProcess
helpviewer_keywords:
- CorExitProcess function [.NET Framework hosting]
ms.assetid: a5cab4c6-990e-47f3-8798-cf422b791015
topic_type:
- apiref
ms.openlocfilehash: a60805e1fd78cb14835957a7afc14fe279cb20fb
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2020
ms.locfileid: "83616563"
---
# <a name="corexitprocess-function"></a>CorExitProcess 函式
關閉目前的非受控進程。  
  
 此函式在 .NET Framework 4 中已被取代。 請改用[ICLRMetaHost：： ExitProcess](iclrmetahost-exitprocess-method.md)方法。  
  
## <a name="syntax"></a>語法  
  
```cpp  
void STDMETHODCALLTYPE CorExitProcess (
  int  exitCode  
);  
```  
  
## <a name="parameters"></a>參數  
 `exitCode`  
 指定進程結束代碼的整數。  
  
## <a name="remarks"></a>備註  
  
> [!NOTE]
> 從 .NET Framework 4 開始， `CorExitProcess` 會在進程中結束每個已啟動的執行時間，而不只是舊版 api 已系結的執行時間。  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** Mscoree.dll. h  
  
 連結**庫：** Mscoree.dll .dll  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [已被取代的 CLR 裝載函式](deprecated-clr-hosting-functions.md)
