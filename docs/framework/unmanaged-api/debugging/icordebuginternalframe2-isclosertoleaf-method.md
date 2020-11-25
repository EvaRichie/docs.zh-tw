---
title: ICorDebugInternalFrame2::IsCloserToLeaf 方法
ms.date: 03/30/2017
api_name:
- ICorDebugInternalFrame2.IsCloserToLeaf Method
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugInternalFrame2::IsCloserToLeaf
helpviewer_keywords:
- ICorDebugInternalFrame2::IsCloserToLeaf method [.NET Framework debugging]
- IsCloserToLeaf method [.NET Framework debugging]
ms.assetid: c1d3d1eb-8370-4f25-8297-3bd262b4740a
topic_type:
- apiref
ms.openlocfilehash: 83d3eda0f3c4619ec7a5df91d13ab9f3a58e5f01
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95721344"
---
# <a name="icordebuginternalframe2isclosertoleaf-method"></a>ICorDebugInternalFrame2::IsCloserToLeaf 方法

檢查 `this` 內部框架是否比指定的 ICorDebugFrame 物件更接近分葉。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT IsCloserToLeaf([in] ICorDebugFrame * pFrameToCompare,  
                       [out] BOOL * pIsCloser);  
```  
  
## <a name="parameters"></a>參數  

 `pFrameToCompare`  
 在比較物件的指標 `ICorDebugFrame` 。  
  
 `pIsCloser`  
 [out] `true` 如果 `this` 內部框架比指定的框架更接近分葉，則為 `pFrameToCompare` ，否則為 `false` 。  
  
## <a name="return-value"></a>傳回值  

 這個方法會傳回下列特定的 HRESULT，以及表示方法失敗的 HRESULT 錯誤。  
  
|HRESULT|描述|  
|-------------|-----------------|  
|S_OK|已成功執行比較。|  
|E_FAIL|無法執行比較。|  
|E_INVALIDARG|`pFrameToCompare` 或 `pIsCloser` 為 null。|  
  
## <a name="remarks"></a>備註  

 `IsCloserToLeaf` 可以用來針對與堆疊上其他框架交錯的內部框架執行原則。  
  
## <a name="requirements"></a>需求  

 **平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** CorDebug.idl、CorDebug.h  
  
 **程式庫：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [ICorDebugInternalFrame2 介面](icordebuginternalframe2-interface.md)
- [偵錯介面](debugging-interfaces.md)
- [偵錯](index.md)
