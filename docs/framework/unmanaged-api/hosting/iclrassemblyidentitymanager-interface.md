---
title: ICLRAssemblyIdentityManager 介面
ms.date: 03/30/2017
api_name:
- ICLRAssemblyIdentityManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRAssemblyIdentityManager
helpviewer_keywords:
- ICLRAssemblyIdentityManager interface [.NET Framework hosting]
ms.assetid: 6a81c6fe-cc22-4062-ae27-d6eeee03a7b9
topic_type:
- apiref
ms.openlocfilehash: 3611de471001d31c40984e71d49ce376bb3e4607
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84504286"
---
# <a name="iclrassemblyidentitymanager-interface"></a>ICLRAssemblyIdentityManager 介面
提供的方法可支援主機和元件的 common language runtime （CLR）之間的通訊。  
  
## <a name="methods"></a>方法  
  
|方法|描述|  
|------------|-----------------|  
|[GetBindingIdentityFromFile 方法](iclrassemblyidentitymanager-getbindingidentityfromfile-method.md)|取得位於指定檔案路徑之元件的元件識別系結資料。|  
|[GetBindingIdentityFromStream 方法](iclrassemblyidentitymanager-getbindingidentityfromstream-method.md)|取得指定資料流程中元件的標準元件識別資料。|  
|[GetCLRAssemblyReferenceList 方法](iclrassemblyidentitymanager-getclrassemblyreferencelist-method.md)|從提供的部分元件識別清單中取得[ICLRAssemblyReferenceList](iclrassemblyreferencelist-interface.md)實例。|  
|[GetProbingAssembliesFromReference 方法](iclrassemblyidentitymanager-getprobingassembliesfromreference-method.md)|取得具有指定身分識別之元件所參考之元件識別碼的[ICLRProbingAssemblyEnum](iclrprobingassemblyenum-interface.md)列舉值。|  
|[GetReferencedAssembliesFromFile 方法](iclrassemblyidentitymanager-getreferencedassembliesfromfile-method.md)|取得[ICLRReferenceAssemblyEnum](iclrreferenceassemblyenum-interface.md)實例，其中包含元件在指定檔案路徑中參考的元件清單。|  
|[GetReferencedAssembliesFromStream 方法](iclrassemblyidentitymanager-getreferencedassembliesfromstream-method.md)|取得 `ICLRReferenceAssemblyEnum` 物件的指標，其中包含指定之資料流程中元件所參考元件的元件識別資料。|  
|[IsStronglyNamed 方法](iclrassemblyidentitymanager-isstronglynamed-method.md)|取得值，指出指定的元件是否為強式名稱。|  
  
## <a name="remarks"></a>備註  
 使用 `ICLRAssemblyIdentityManager` 來取得和的實例， `ICLRAssemblyReferenceList` 以列舉元件身分識別。  
  
## <a name="requirements"></a>規格需求  
 **平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** Mscoree.dll. h  
  
 連結**庫：** 包含為 Mscoree.dll 中的資源  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [ICLRAssemblyReferenceList 介面](iclrassemblyreferencelist-interface.md)
- [ICLRProbingAssemblyEnum 介面](iclrprobingassemblyenum-interface.md)
- [裝載介面](hosting-interfaces.md)
