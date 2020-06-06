---
title: 如何判斷 .NET Standard 物件是否可序列化
description: 顯示如何判斷在執行時間是否可以序列化 .NET Standard 類型。
ms.date: 10/20/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- serializing objects
- objects, serializing steps
ms.openlocfilehash: b6791ae0666aeb0ac02d8a38ca419d7de2b263cf
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "84289599"
---
# <a name="how-to-determine-if-a-net-standard-object-is-serializable"></a>如何判斷 .NET Standard 物件是否可序列化

.NET Standard 是一項規格，定義必須存在於符合該標準版本之特定 .NET 部署上的類型和成員。 不過，.NET Standard 不會定義型別是否為可序列化。 .NET Standard 程式庫中定義的類型不會以屬性標記 <xref:System.SerializableAttribute> 。 相反地，特定的 .NET 部署（例如 .NET Framework 和 .NET Core）可自由判斷特定類型是否可序列化。

如果您已開發以 .NET Standard 為目標的程式庫，則任何支援 .NET Standard 的 .NET 部署都可以使用您的程式庫。 這表示您無法事先知道特定類型是否可序列化;您只能判斷它在執行時間是否可序列化。

您可以藉由抓取 <xref:System.Type.IsSerializable> 代表物件類型之物件的屬性值，判斷物件是否可在執行時間序列化 <xref:System.Type> 。 下列範例提供一個實作為。 它會定義 `IsSerializable(Object)` 擴充方法，以指出是否 <xref:System.Object> 可以序列化任何實例。

[!code-csharp[is-a-type-serializable](~/samples/snippets/standard/serialization/is-serializable/csharp/program.cs#2)]
[!code-vb[is-a-type-serializable](~/samples/snippets/standard/serialization/is-serializable/vb/library.vb#2)]

接著，您可以將任何物件傳遞至方法，以判斷它是否可以在目前的 .NET 執行中進行序列化和還原序列化，如下列範例所示：

[!code-csharp[test-is-a-type-serializable](~/samples/snippets/standard/serialization/is-serializable/csharp/program.cs#1)]
[!code-vb[test-is-a-type-serializable](~/samples/snippets/standard/serialization/is-serializable/vb/program.vb#1)]

## <a name="see-also"></a>另請參閱

- [二進位序列化](binary-serialization.md)
- <xref:System.SerializableAttribute?displayProperty=nameWithType>
- <xref:System.Type.IsSerializable?displayProperty=nameWithType>
