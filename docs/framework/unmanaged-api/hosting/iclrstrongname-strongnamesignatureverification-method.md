---
title: ICLRStrongName::StrongNameSignatureVerification 方法
ms.date: 03/30/2017
api_name:
- ICLRStrongName.StrongNameSignatureVerification
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRStrongName::StrongNameSignatureVerification
helpviewer_keywords:
- ICLRStrongName::StrongNameSignatureVerification method [.NET Framework hosting]
- StrongNameSignatureVerification method, ICLRStrongName interface [.NET Framework hosting]
ms.assetid: 734dc4d1-0a76-4736-b5ac-cb4253b3dd49
topic_type:
- apiref
ms.openlocfilehash: d31c9c0db306aad3a7c3472ef6329f25aa6c5902
ms.sourcegitcommit: c76c8b2c39ed2f0eee422b61a2ab4c05ca7771fa
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/21/2020
ms.locfileid: "83762652"
---
# <a name="iclrstrongnamestrongnamesignatureverification-method"></a>ICLRStrongName::StrongNameSignatureVerification 方法
取得值，指出所提供路徑的組件資訊清單是否包含強式名稱簽章，這會根據指定的旗標進行驗證。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT StrongNameSignatureVerification (  
    [in]  LPCWSTR   wszFilePath,  
    [in]  DWORD     dwInFlags,  
    [out] DWORD     *pdwOutFlags  
);  
```  
  
## <a name="parameters"></a>參數  
 `wszFilePath`  
 在要驗證之元件的可攜式可執行檔（.dll 或 .exe）的路徑。  
  
 `dwInFlags`  
 在用來修改驗證行為的旗標。 支援下列值：  
  
- `SN_INFLAG_FORCE_VER`（0x00000001）-強制進行驗證，即使需要覆寫登錄設定也一樣。  
  
- `SN_INFLAG_INSTALL`（0x00000002）-指定這是第一次驗證資訊清單。  
  
- `SN_INFLAG_ADMIN_ACCESS`（0x00000004）-指定快取只允許具有系統管理許可權的使用者進行存取。  
  
- `SN_INFLAG_USER_ACCESS`（0x00000008）-指定只有目前的使用者可以存取此元件。  
  
- `SN_INFLAG_ALL_ACCESS`（0x00000010）-指定快取不會提供存取限制的保證。  
  
- `SN_INFLAG_RUNTIME`（0x80000000）-保留供內部偵錯工具之用。  
  
 `pdwOutFlags`  
 脫銷旗標，指出是否已驗證強式名稱簽章。 支援下列值：  
  
- `SN_OUTFLAG_WAS_VERIFIED`（0x00000001）-此值設定為 `false` ，以指定驗證因為登錄設定而成功。  
  
## <a name="return-value"></a>傳回值  
 `S_OK`如果方法已成功完成，則為，否則，就是表示失敗的 HRESULT 值（請參閱清單的[一般 HRESULT 值](/windows/win32/seccrypto/common-hresult-values)）。  
  
## <a name="requirements"></a>規格需求  
 **平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** MetaHost。h  
  
 連結**庫：** 包含為 Mscoree.dll 中的資源  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [StrongNameSignatureVerificationEx 方法](iclrstrongname-strongnamesignatureverificationex-method.md)
- [ICLRStrongName 介面](iclrstrongname-interface.md)
