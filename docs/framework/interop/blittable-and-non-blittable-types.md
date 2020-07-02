---
title: Blittable 和非 Blittable 類型
description: 深入瞭解全像一層和非直接的類型。 可直接上建的資料類型通常會在受控和非受控記憶體中表示，不需要特殊處理。
ms.date: 03/30/2017
helpviewer_keywords:
- interop marshaling, blittable types
- blittable types, interop marshaling
ms.assetid: d03b050e-2916-49a0-99ba-f19316e5c1b3
ms.openlocfilehash: 68f4197a2710b6825c83bbc51daaf8f6b5a2c81f
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85621531"
---
# <a name="blittable-and-non-blittable-types"></a>Blittable 和非 Blittable 類型
大部分的資料類型是 Managed 和 Unmanaged 記憶體中的常見呈現，而且 Interop 封送處理器不需要特殊處理。 這些類型稱為「Blittable 類型」**，因為它們在 Managed 與 Unmanaged 程式碼之間傳遞時不需要進行轉換。  
  
 從平台叫用呼叫傳回的結構必須是 Blittable 類型。 平台叫用不支援非 Blittable 結構作為傳回類型。  
  
 <xref:System> 命名空間中的下列類型是 Blittable 類型：  
  
- <xref:System.Byte?displayProperty=nameWithType>  
  
- <xref:System.SByte?displayProperty=nameWithType>  
  
- <xref:System.Int16?displayProperty=nameWithType>  
  
- <xref:System.UInt16?displayProperty=nameWithType>  
  
- <xref:System.Int32?displayProperty=nameWithType>  
  
- <xref:System.UInt32?displayProperty=nameWithType>  
  
- <xref:System.Int64?displayProperty=nameWithType>  
  
- <xref:System.UInt64?displayProperty=nameWithType>  
  
- <xref:System.IntPtr?displayProperty=nameWithType>  
  
- <xref:System.UIntPtr?displayProperty=nameWithType>  
  
- <xref:System.Single?displayProperty=nameWithType>  
  
- <xref:System.Double?displayProperty=nameWithType>  
  
 下列複雜類型也是 Blittable 類型：  
  
- Blittable 類型的一維陣列 (例如整數陣列)。 不過，包含 Blittable 類型之可變陣列的類型本身不是 Blittable。  
  
- 只包含 Blittable 類型 (將它們封送處理為格式化類型時也包含類別) 的格式化實值型別。 如需格式化實值型別的詳細資訊，請參閱[實值型別的預設封送處理](default-marshaling-behavior.md#default-marshaling-for-value-types)。  
  
 物件參考不是 Blittable。 這包含自行 Blittable 之物件參考的陣列。 例如，您可以定義 Blittable 結構，但無法定義包含這些結構參考之陣列的 Blittable 類型。  
  
 進行最佳化時，在封送處理期間，會[釘選](copying-and-pinning.md) Blittable 類型以及只包含 Blittable 成員之類別的陣列，而不是複製。 呼叫者和被呼叫者位於相同的 Apartment 時，可以將這些類型封送處理為 In/Out 參數。 不過，會將這些類型實際封送處理為 In 參數；而且，如果您想要將引數封送處理為 In/Out 參數，則您必須套用 <xref:System.Runtime.InteropServices.InAttribute> 和 <xref:System.Runtime.InteropServices.OutAttribute> 屬性。  
  
 部分 Managed 資料類型需要 Unmanaged 環境中有不同的呈現。 這些非 Blittable 資料類型必須轉換成可封送處理的形式。 例如，Managed 字串是非 Blittable 類型，因為它們必須先轉換成字串物件，才能進行封送處理。  
  
 下表列出 <xref:System> 命名空間中的非 Blittable 類型。 [委派](default-marshaling-behavior.md#default-marshaling-for-delegates) (這是參照靜態方法或類別執行個體的資料結構) 也是非 Blittable。  
  
|非 Blittable 類型|描述|  
|-------------------------|-----------------|  
|[System.Array](default-marshaling-for-arrays.md)|轉換成 C 樣式陣列或 `SAFEARRAY`。|  
|[System.Boolean](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/t2t3725f(v=vs.100))|轉換成 `true` 為 1 或 -1 的 1、2 或 4 位元組值。|  
|[System.object](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/6tyybbf2(v=vs.100))|轉換成 Unicode 或 ANSI 字元。|  
|[System.Class](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/s0968xy8(v=vs.100))|轉換成類別介面。|  
|[System.object](default-marshaling-for-objects.md)|轉換成變異值或介面。|  
|[System.Mdarray](default-marshaling-for-arrays.md)|轉換成 C 樣式陣列或 `SAFEARRAY`。|  
|[System.string](default-marshaling-for-strings.md)|轉換成 Null 參考中的字串終止，或轉換成 BSTR。|  
|[System.Valuetype](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/0t2cwe11(v=vs.100))|轉換成具有固定記憶體配置的結構。|  
|[System.Szarray](default-marshaling-for-arrays.md)|轉換成 C 樣式陣列或 `SAFEARRAY`。|  
  
 COM Interop 只能支援類別和物件類型。 如需 Visual Basic、C# 和 C++ 中的對應類型，請參閱[類別庫概觀](../../standard/class-library-overview.md)。  
  
## <a name="see-also"></a>另請參閱

- [預設的封送處理行為](default-marshaling-behavior.md)
