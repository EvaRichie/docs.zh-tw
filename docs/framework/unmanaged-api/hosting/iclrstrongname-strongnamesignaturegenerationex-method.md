---
title: ICLRStrongName::StrongNameSignatureGenerationEx 方法
ms.date: 03/30/2017
api_name:
- ICLRStrongName.StrongNameSignatureGenerationEx
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRStrongName::StrongNameSignatureGenerationEx
helpviewer_keywords:
- ICLRStrongName::StrongNameSignatureGenerationEx method [.NET Framework hosting]
- StrongNameSignatureGenerationEx method, ICLRStrongName interface [.NET Framework hosting]
ms.assetid: c3f34584-c6e2-41fd-bb44-e44da8546309
topic_type:
- apiref
ms.openlocfilehash: 3529eceb179cc4b08d39f83d97d001a16e716918
ms.sourcegitcommit: c76c8b2c39ed2f0eee422b61a2ab4c05ca7771fa
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/21/2020
ms.locfileid: "83763055"
---
# <a name="iclrstrongnamestrongnamesignaturegenerationex-method"></a>ICLRStrongName::StrongNameSignatureGenerationEx 方法
根據指定的旗標，產生指定元件的強式名稱簽章。  
  
## <a name="syntax"></a>語法  
  
```cpp
HRESULT StrongNameSignatureGenerationEx (  
    [in]  LPCWSTR   wszFilePath,  
    [in]  LPCWSTR   wszKeyContainer,  
    [in]  BYTE      *pbKeyBlob,  
    [in]  ULONG     cbKeyBlob,  
    [out] BYTE      **ppbSignatureBlob,  
    [out] ULONG     *pcbSignatureBlob,  
    [in]  DWORD     dwFlags  
);  
```  
  
## <a name="parameters"></a>參數  
 `wszFilePath`  
 在檔案的路徑，該檔案包含將產生強式名稱簽章之元件的資訊清單。  
  
 `wszKeyContainer`  
 在包含公開/私密金鑰組的金鑰容器名稱。  
  
 如果 `pbKeyBlob` 為 null， `wszKeyContainer` 必須在密碼編譯服務提供者（CSP）內指定有效的容器。 在此情況下，會使用儲存在容器中的金鑰組來簽署檔案。  
  
 如果不 `pbKeyBlob` 是 null，則會假設金鑰組包含在金鑰二進位大型物件（BLOB）中。  
  
 `pbKeyBlob`  
 在公開/私密金鑰組的指標。 這組會使用 Win32 函式所建立的格式 `CryptExportKey` 。 如果 `pbKeyBlob` 為 null，則會假設指定的金鑰容器 `wszKeyContainer` 包含金鑰組。  
  
 `cbKeyBlob`  
 在的大小（以位元組為單位） `pbKeyBlob` 。  
  
 `ppbSignatureBlob`  
 脫銷通用語言執行時間傳回簽章之位置的指標。 如果 `ppbSignatureBlob` 為 null，則執行時間會將簽章儲存在所指定的檔案中 `wszFilePath` 。  
  
 如果不 `ppbSignatureBlob` 是 null，通用語言執行時間會配置用來傳回簽章的空間。 呼叫端必須使用[ICLRStrongName：： StrongNameFreeBuffer](iclrstrongname-strongnamefreebuffer-method.md)方法來釋放此空間。  
  
 `pcbSignatureBlob`  
 脫銷所傳回簽章的大小（以位元組為單位）。  
  
 `dwFlags`  
 在下列一個或多個值：  
  
- `SN_SIGN_ALL_FILES`（0x00000001）-重新計算連結模組的所有雜湊。  
  
- `SN_TEST_SIGN`（0x00000002）-測試-簽署元件。  
  
## <a name="return-value"></a>傳回值  
 `S_OK`如果方法已成功完成，則為，否則，就是表示失敗的 HRESULT 值（請參閱清單的[一般 HRESULT 值](/windows/win32/seccrypto/common-hresult-values)）。  
  
## <a name="remarks"></a>備註  
 針對指定 null `wszFilePath` 以計算簽章的大小，而不建立簽章。  
  
 簽章可以直接儲存在檔案中，或傳回給呼叫端。  
  
 如果 `SN_SIGN_ALL_FILES` 指定了，但不包含公開金鑰（ `pbKeyBlob` 和 `wszFilePath` 都是 null），則會重新計算連結模組的雜湊，但不會重新簽署元件。  
  
 如果 `SN_TEST_SIGN` 指定了，就不會修改 common language runtime 標頭，以指出元件是以強式名稱簽署。  
  
## <a name="requirements"></a>規格需求  
 **平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** MetaHost。h  
  
 連結**庫：** 包含為 Mscoree.dll 中的資源  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [StrongNameSignatureGeneration 方法](iclrstrongname-strongnamesignaturegeneration-method.md)
- [ICLRStrongName 介面](iclrstrongname-interface.md)
