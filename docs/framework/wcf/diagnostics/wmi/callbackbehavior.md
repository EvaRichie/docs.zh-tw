---
title: CallbackBehavior
ms.date: 03/30/2017
ms.assetid: 42acd302-2b62-4849-a2d1-a03084343ecd
ms.openlocfilehash: cec9005a099247671dbebaacc0b242ca8d7a0144
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96269644"
---
# <a name="callbackbehavior"></a>CallbackBehavior

CallbackBehavior  
  
## <a name="syntax"></a>Syntax  
  
```csharp
class CallbackBehavior : Behavior  
{  
  boolean AutomaticSessionShutdown;  
  string ConcurrencyMode;  
  boolean IgnoreExtensionDataObject;  
  boolean IncludeExceptionDetailInFaults;  
  boolean MaxItemsInObjectGraph;  
  boolean UseSynchronizationContext;  
  boolean ValidateMustUnderstand;  
};  
```  
  
## <a name="methods"></a>方法  

 CallbackBehavior 類別不會定義任何方法。  
  
## <a name="properties"></a>屬性  

 CallbackBehavior 類別具有下列屬性：  
  
### <a name="automaticsessionshutdown"></a>AutomaticSessionShutdown  

 資料型別：布林值  
  
 存取類型：唯讀  
  
 如果是 true，當服務關閉雙工工作階段時會自動關閉該工作階段。  
  
### <a name="concurrencymode"></a>ConcurrencyMode  

 資料類型：字串  
存取類型：唯讀  
  
 指定服務支援單一執行緒、多重執行緒或可重新進入 (Reentrant) 呼叫。  
  
### <a name="ignoreextensiondataobject"></a>IgnoreExtensionDataObject  

 資料型別：布林值  
  
 存取類型：唯讀  
  
 指定是否要將未知的序列化資料傳送到網路上的值。  
  
### <a name="includeexceptiondetailinfaults"></a>IncludeExceptionDetailInFaults  

 資料型別：布林值  
  
 存取類型：唯讀  
  
 啟用時，回呼上之例外狀況的詳細資料會附加到傳回到服務的錯誤中。  
  
### <a name="maxitemsinobjectgraph"></a>MaxItemsInObjectGraph  

 資料型別：布林值  
  
 存取類型：唯讀  
  
 已序列化物件中允許的項目數目上限。  
  
### <a name="usesynchronizationcontext"></a>UseSynchronizationContext  

 資料型別：布林值  
  
 存取類型：唯讀  
  
 指定是否使用目前的同步化內容來選擇執行的執行緒。  
  
### <a name="validatemustunderstand"></a>ValidateMustUnderstand  

 資料型別：布林值  
  
 存取類型：唯讀  
  
 指定系統或應用程式是否會強制執行 SOAP MustUnderstand 標頭處理。  
  
## <a name="requirements"></a>規格需求  
  
|MOF|於 Servicemodel.mof 中宣告。|  
|---------|-----------------------------------|  
|命名空間|於 root\ServiceModel 中定義|  
  
## <a name="see-also"></a>另請參閱

- <xref:System.ServiceModel.CallbackBehaviorAttribute>
