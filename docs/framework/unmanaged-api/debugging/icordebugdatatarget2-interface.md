---
title: ICorDebugDataTarget2 介面
ms.date: 03/30/2017
ms.assetid: 13f11388-2f91-48d8-98d6-6a4a63cb5746
ms.openlocfilehash: 1c598d23cac77e50cf302e6936b88b5eb6e558c2
ms.sourcegitcommit: fff146ba3fd1762c8c432d95c8b877825ae536fc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/08/2020
ms.locfileid: "82976430"
---
# <a name="icordebugdatatarget2-interface"></a>ICorDebugDataTarget2 介面
以邏輯方式擴充[ICorDebugDataTarget](icordebugdatatarget-interface.md)介面。  
  
## <a name="methods"></a>方法  
  
|方法|描述|  
|------------|-----------------|  
|[CreateVirtualUnwinder 方法](icordebugdatatarget2-createvirtualunwinder-method.md)|建立新的堆疊 unwinder，以從初始內容 (不一定是執行緒的分葉) 開始回溯。|  
|[EnumerateThreadIDs 方法](icordebugdatatarget2-enumeratethreadids-method.md)|傳回使用中執行緒 ID 的清單。|  
|[GetImageFromPointer 方法](icordebugdatatarget2-getimagefrompointer-method.md)|從模組中的位址傳回模組基底位址和大小。|  
|[GetImageLocation 方法](icordebugdatatarget2-getimagelocation-method.md)|從模組的基底位址傳回模組的路徑。|  
|[GetSymbolProviderForImage 方法](icordebugdatatarget2-getsymbolproviderforimage-method.md)|從模組的基底位址傳回模組的符號提供者。|  
  
## <a name="remarks"></a>備註  
  
> [!NOTE]
> 這個介面僅適用於 .NET 原生。 如果您在 .NET 原生之外針對 ICorDebug 案例實作這個介面，Common Language Runtime 會忽略這個介面。  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** CorDebug.idl、CorDebug.h  
  
 **程式庫：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [偵錯介面](debugging-interfaces.md)
- [偵錯](index.md)
