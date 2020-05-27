---
title: CorElementType 列舉
ms.date: 03/30/2017
api_name:
- CorElementType
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorElementType
helpviewer_keywords:
- CorElementType enumeration [.NET Framework metadata]
ms.assetid: c3809c8f-1737-4f0f-9442-0c01ee689871
topic_type:
- apiref
ms.openlocfilehash: 25fb3278e576ebe4a538379918e868b2e5f87911
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/27/2020
ms.locfileid: "84007867"
---
# <a name="corelementtype-enumeration"></a>CorElementType 列舉

指定通用語言執行時間 <xref:System.Type> 、類型修飾詞，或元資料類型簽章中類型的相關資訊。

## <a name="syntax"></a>語法

```cpp
typedef enum CorElementType {
    ELEMENT_TYPE_END            = 0x0,
    ELEMENT_TYPE_VOID           = 0x1,
    ELEMENT_TYPE_BOOLEAN        = 0x2,
    ELEMENT_TYPE_CHAR           = 0x3,
    ELEMENT_TYPE_I1             = 0x4,
    ELEMENT_TYPE_U1             = 0x5,
    ELEMENT_TYPE_I2             = 0x6,
    ELEMENT_TYPE_U2             = 0x7,
    ELEMENT_TYPE_I4             = 0x8,
    ELEMENT_TYPE_U4             = 0x9,
    ELEMENT_TYPE_I8             = 0xa,
    ELEMENT_TYPE_U8             = 0xb,
    ELEMENT_TYPE_R4             = 0xc,
    ELEMENT_TYPE_R8             = 0xd,
    ELEMENT_TYPE_STRING         = 0xe,

    ELEMENT_TYPE_PTR            = 0xf,
    ELEMENT_TYPE_BYREF          = 0x10,

    ELEMENT_TYPE_VALUETYPE      = 0x11,
    ELEMENT_TYPE_CLASS          = 0x12,
    ELEMENT_TYPE_VAR            = 0x13,
    ELEMENT_TYPE_ARRAY          = 0x14,
    ELEMENT_TYPE_GENERICINST    = 0x15,
    ELEMENT_TYPE_TYPEDBYREF     = 0x16,

    ELEMENT_TYPE_I              = 0x18,
    ELEMENT_TYPE_U              = 0x19,
    ELEMENT_TYPE_FNPTR          = 0x1B,
    ELEMENT_TYPE_OBJECT         = 0x1C,
    ELEMENT_TYPE_SZARRAY        = 0x1D,
    ELEMENT_TYPE_MVAR           = 0x1e,

    ELEMENT_TYPE_CMOD_REQD      = 0x1F,
    ELEMENT_TYPE_CMOD_OPT       = 0x20,

    ELEMENT_TYPE_INTERNAL       = 0x21,
    ELEMENT_TYPE_MAX            = 0x22,

    ELEMENT_TYPE_MODIFIER       = 0x40,
    ELEMENT_TYPE_SENTINEL       = 0x01 | ELEMENT_TYPE_MODIFIER,
    ELEMENT_TYPE_PINNED         = 0x05 | ELEMENT_TYPE_MODIFIER

} CorElementType;
```

## <a name="members"></a>成員

|成員|描述|
|------------|-----------------|
|`ELEMENT_TYPE_END`|內部使用。|
|`ELEMENT_TYPE_VOID`|Void 類型。|
|`ELEMENT_TYPE_BOOLEAN`|布林值類型|
|`ELEMENT_TYPE_CHAR`|字元類型。|
|`ELEMENT_TYPE_I1`|帶正負號的1位元組整數。|
|`ELEMENT_TYPE_U1`|不帶正負號的 1 位元整數。|
|`ELEMENT_TYPE_I2`|帶正負號的2位元組整數。|
|`ELEMENT_TYPE_U2`|不帶正負號的2位元組整數。|
|`ELEMENT_TYPE_I4`|帶正負號的4位元組整數。|
|`ELEMENT_TYPE_U4`|不帶正負號的4位元組整數。|
|`ELEMENT_TYPE_I8`|帶正負號的8位元組整數。|
|`ELEMENT_TYPE_U8`|不帶正負號的8位元組整數。|
|`ELEMENT_TYPE_R4`|4位元組浮點數。|
|`ELEMENT_TYPE_R8`|8位元組浮點數。|
|`ELEMENT_TYPE_STRING`|System.string 類型。|
|`ELEMENT_TYPE_PTR`|指標類型修飾詞。|
|`ELEMENT_TYPE_BYREF`|參考型別修飾詞。|
|`ELEMENT_TYPE_VALUETYPE`|實值型別修飾詞。|
|`ELEMENT_TYPE_CLASS`|類別類型修飾詞。|
|`ELEMENT_TYPE_VAR`|類別變數類型修飾詞。|
|`ELEMENT_TYPE_ARRAY`|多維度陣列型別修飾詞。|
|`ELEMENT_TYPE_GENERICINST`|泛型型別的類型修飾詞。|
|`ELEMENT_TYPE_TYPEDBYREF`|具型別參考。|
|`ELEMENT_TYPE_I`|原生整數的大小。|
|`ELEMENT_TYPE_U`|不帶正負號的原生整數大小。|
|`ELEMENT_TYPE_FNPTR`|函式的指標。|
|`ELEMENT_TYPE_OBJECT`|System.object 類型。|
|`ELEMENT_TYPE_SZARRAY`|一維、零下限陣列類型修飾詞。|
|`ELEMENT_TYPE_MVAR`|方法變數類型修飾詞。|
|`ELEMENT_TYPE_CMOD_REQD`|C 語言所需的修飾詞。|
|`ELEMENT_TYPE_CMOD_OPT`|C 語言選用修飾詞。|
|`ELEMENT_TYPE_INTERNAL`|內部使用。|
|`ELEMENT_TYPE_MAX`|類型無效。|
|`ELEMENT_TYPE_MODIFIER`|內部使用。|
|`ELEMENT_TYPE_SENTINEL`|類型修飾詞，這是可變數數目之參數清單的 sentinel。|
|`ELEMENT_TYPE_PINNED`|內部使用。|

## <a name="remarks"></a>備註

類型修飾詞會形成代表更複雜類型的基礎。 `CorElementType`型別修飾詞值會套用至緊接在型別簽章中的值後面。 在類型修飾詞值之後的值 `CorElementType` 可以是 `CorElementType` 簡單類型值、元資料標記或其他值，如下表中所指定。

> [!NOTE]
> 所有數位（*數位*、*引數計數*、*元資料標記*、順*位*、*計數*和系*結）都會*儲存為壓縮整數。 如需詳細資訊，請參閱 ECMA 網站上的[標準 ECMA-335-通用語言基礎結構（CLI）](http://www.ecma-international.org/publications/standards/Ecma-335.htm) 。

|類型修飾詞|格式|
|-------------------|------------|
|`ELEMENT_TYPE_PTR`|ELEMENT_TYPE_PTR\<a `CorElementType` value>|
|`ELEMENT_TYPE_BYREF`|ELEMENT_TYPE_BYREF\<a `CorElementType` value>|
|`ELEMENT_TYPE_VALUETYPE`|ELEMENT_TYPE_VALUETYPE\<an `mdTypeDef` metadata token>|
|`ELEMENT_TYPE_CLASS`|ELEMENT_TYPE_CLASS\<an `mdTypeDef` metadata token>|
|`ELEMENT_TYPE_VAR`|ELEMENT_TYPE_VAR\<number>|
|`ELEMENT_TYPE_ARRAY`|ELEMENT_TYPE_ARRAY \<a `CorElementType` value> \<rank> \<count1> \<bound1> ... \<countN>\<boundN>|
|`ELEMENT_TYPE_GENERICINST`|ELEMENT_TYPE_GENERICINST \<an `mdTypeDef` metadata token> \<argument Count> \<arg1> .。。\<argN>|
|`ELEMENT_TYPE_FNPTR`|ELEMENT_TYPE_FNPTR\<complete signature for the function, including calling convention>|
|`ELEMENT_TYPE_SZARRAY`|ELEMENT_TYPE_SZARRAY\<a `CorElementType` value>|
|`ELEMENT_TYPE_MVAR`|ELEMENT_TYPE_MVAR\<number>|
|`ELEMENT_TYPE_CMOD_REQD`|ELEMENT_TYPE_\<a `mdTypeRef` or `mdTypeDef` metadata token>|
|`ELEMENT_TYPE_CMOD_OPT`|E_T_CMOD_OPT\<a `mdTypeRef` or `mdTypeDef` metadata token>|

## <a name="requirements"></a>需求

**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。

**標頭：** Corhdr.h。h

**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]

## <a name="see-also"></a>另請參閱

- [中繼資料列舉](metadata-enumerations.md)
