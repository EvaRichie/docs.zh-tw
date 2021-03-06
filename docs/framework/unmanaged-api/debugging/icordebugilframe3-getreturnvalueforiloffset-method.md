---
title: ICorDebugILFrame3::GetReturnValueForILOffset 方法
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
api_name:
- ICorDebugILFrame3.GetReturnValueForILOffset
api_location:
- mscordbi.dll
api_type:
- COM
ms.assetid: 06522727-5f64-4391-9331-11386883c352
topic_type:
- apiref
ms.openlocfilehash: 11207298b071527151535144330790df767c2101
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95724997"
---
# <a name="icordebugilframe3getreturnvalueforiloffset-method"></a>ICorDebugILFrame3::GetReturnValueForILOffset 方法

取得 "ICorDebugValue" 物件，此物件會封裝函式的傳回值。  
  
## <a name="syntax"></a>語法  
  
```cpp
HRESULT GetReturnValueForILOffset(  
    ULONG32 ILoffset,
    [out] ICorDebugValue **ppReturnValue  
);  
```  
  
## <a name="parameters"></a>參數  

 `ILOffset`  
 IL 位移。 請參閱＜備註＞一節。  
  
 `ppReturnValue`  
 "ICorDebugValue" 介面物件位址的指標，提供函式呼叫傳回值的相關資訊。  
  
## <a name="remarks"></a>備註  

 這個方法會搭配 [ICorDebugCode3：： GetReturnValueLiveOffset](icordebugcode3-getreturnvalueliveoffset-method.md) 方法使用，以取得方法的傳回值。 在會忽略傳回值的方法中，這種方法特別有用，如下列兩個程式碼範例所示。 第一個範例會呼叫 <xref:System.Int32.TryParse%2A?displayProperty=nameWithType> 方法，但會忽略方法的傳回值。  
  
 [!code-csharp[Unmanaged.Debugging.MRV#1](../../../../samples/snippets/csharp/VS_Snippets_CLR/unmanaged.debugging.mrv/cs/mrv1.cs#1)]
 [!code-vb[Unmanaged.Debugging.MRV#1](../../../../samples/snippets/visualbasic/VS_Snippets_CLR/unmanaged.debugging.mrv/vb/mrv1.vb#1)]  
  
 第二個範例說明更常見的調試問題。 由於方法會當做方法呼叫中的引數使用，因此只有在偵錯工具逐步執行呼叫的方法時，才能存取其傳回值。 在許多情況下，尤其是在外部程式庫中定義了被呼叫的方法時，就無法這麼做。  
  
 [!code-csharp[Unmanaged.Debugging.MRV#2](../../../../samples/snippets/csharp/VS_Snippets_CLR/unmanaged.debugging.mrv/cs/mrv2.cs#2)]
 [!code-vb[Unmanaged.Debugging.MRV#2](../../../../samples/snippets/visualbasic/VS_Snippets_CLR/unmanaged.debugging.mrv/vb/mrv2.vb#2)]  
  
 如果您傳遞 [ICorDebugCode3：： GetReturnValueLiveOffset](icordebugcode3-getreturnvalueliveoffset-method.md) 方法至函式呼叫位置的 IL 位移，則會傳回一或多個原生位移。 然後，偵錯工具可以在函式中的這些原生位移上設定中斷點。 當偵錯工具到達其中一個中斷點時，您便可以傳遞您傳遞給這個方法的相同 IL 位移，以取得傳回值。 偵錯工具接著應清除其設定的所有中斷點。  
  
> [!WARNING]
> [ICorDebugCode3：： GetReturnValueLiveOffset 方法](icordebugcode3-getreturnvalueliveoffset-method.md)和 `ICorDebugILFrame3::GetReturnValueForILOffset` 方法可讓您只取得參考型別的傳回值資訊。 從實值型別中取出傳回值資訊 (也就是說，不支援衍生自) 的所有類型 <xref:System.ValueType> 。  
  
 參數所指定的 IL 位移 `ILOffset` 應該位於函式呼叫位置，而偵錯工具應該在針對相同 IL 位移的 [ICorDebugCode3：： GetReturnValueLiveOffset](icordebugcode3-getreturnvalueliveoffset-method.md) 方法所傳回的原生位移上設定的中斷點停止。 如果偵錯工具未在指定之 IL 位移的正確位置停止，API 將會失敗。  
  
 如果函式呼叫不會傳回值，API 將會失敗。  
  
 `ICorDebugILFrame3::GetReturnValueForILOffset`只有 x86 型和 AMD64 系統才能使用此方法。  
  
## <a name="requirements"></a>需求  

 **平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** CorDebug.idl、CorDebug.h  
  
 **程式庫：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v451plus](../../../../includes/net-current-v451plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [GetReturnValueLiveOffset 方法](icordebugcode3-getreturnvalueliveoffset-method.md)
- [ICorDebugILFrame3 介面](icordebugilframe3-interface.md)
