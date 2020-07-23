---
title: 屬性 (C#)
description: '瞭解如何使用屬性，將中繼資料或宣告式資訊與 c # 中的程式碼產生關聯。 您可以在執行時間使用反映來查詢屬性。'
ms.date: 04/26/2018
ms.openlocfilehash: 5c57838b649531d8e8fe89919771adf8830e7f54
ms.sourcegitcommit: 40de8df14289e1e05b40d6e5c1daabd3c286d70c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86924981"
---
# <a name="attributes-c"></a>屬性 (C#)

屬性提供一種功能強大的方法，可將中繼資料或宣告資訊關聯至程式碼 (組建、型別、方法、屬性等)。 將屬性關聯至程式實體之後，就能在執行階段使用稱為「反映」** 的技術來查詢該屬性。 如需詳細資訊，請參閱[反映 (C#)](../reflection.md)。

屬性 (Attribute) 包含下列屬性 (Property)：

- 屬性會將中繼資料新增至您的程式。 「中繼資料」** 是在程式中定義的型別相關資訊。 所有的 .NET 組件都包含一組指定的中繼資料，來描述組件中所定義的型別和型別成員。 您可以新增自訂屬性來指定所需的任何其他資訊。 如需詳細資訊，請參閱[建立自訂屬性 (C#)](creating-custom-attributes.md)。
- 您可以將一或多個屬性 (Attribute) 套用至整個組件、模組或較小的程式元素，例如類別和屬性 (Property)。
- 屬性 (Attribute) 可以利用與方法與屬性 (Property) 相同的方式來接受引數。
- 您的程式可以使用反映，來檢查自己的中繼資料或其他程式的中繼資料。 如需詳細資訊，請參閱[使用反映存取屬性 (C#)](accessing-attributes-by-using-reflection.md)。

## <a name="using-attributes"></a>使用屬性

屬性可以放置於大多數的任意宣告中，但特定的屬性可能會限制它適用的宣告型別。 在 C# 中，指定屬性的方式是以方括弧 ([]) 括住屬性的名稱，並放置在要套用的實體宣告上方。

在此範例中，會使用 <xref:System.SerializableAttribute> 屬性來將特定的特性套用至類別：

[!code-csharp[Using the serializable attribute](~/samples/snippets/csharp/attributes/AttributesOverview.cs#1)]

具有 <xref:System.Runtime.InteropServices.DllImportAttribute> 屬性的方法會如下範例宣告：

[!code-csharp[Declaring a method to import from an external library](../../../../../samples/snippets/csharp/attributes/AttributesOverview.cs#2)]

多個屬性可以放在宣告，如下列範例所示：

[!code-csharp[Including the interop namespace](~/samples/snippets/csharp/attributes/AttributesOverview.cs#3)]
[!code-csharp[Declaring two way marshaling for arguments](~/samples/snippets/csharp/attributes/AttributesOverview.cs#4)]

可以針對特定實體多次指定某些屬性。 <xref:System.Diagnostics.ConditionalAttribute> 就是這種多次使用屬性的一個例子：

[!code-csharp[Using the conditional attribute](~/samples/snippets/csharp/attributes/AttributesOverview.cs#5)]

> [!NOTE]
> 依照慣例，所有的屬性名稱都會以 "Attribute" 這個字結尾，以便與 .NET 程式庫中的其他項目有所區別。 不過，您在程式碼中使用屬性時，不需要指定屬性的後置詞。 例如， `[DllImport]` 相當於 `[DllImportAttribute]` ，但 `DllImportAttribute` 是屬性在 .net 類別庫中的實際名稱。

### <a name="attribute-parameters"></a>屬性參數

許多屬性的參數可以是位置、未命名或具名的參數。 任何位置的參數必須以特定順序指定，而且不能省略。 具名的參數是選擇性的，可以依照任何順序指定。 位置參數會先指定。 例如，這三個屬性是相等的：

```csharp
[DllImport("user32.dll")]
[DllImport("user32.dll", SetLastError=false, ExactSpelling=false)]
[DllImport("user32.dll", ExactSpelling=false, SetLastError=false)]
```

第一個參數 (DLL 名稱) 是位置參數，一律會先出現；其他的則為具名參數。 在此案例中，這兩個具名參數預設為 false，因此可以省略。 位置參數對應至屬性建構函式的參數。 對應屬性或欄位屬性的具名或選擇性參數。 請參閱個別屬性的文件，以取得預設參數值的詳細資訊。

### <a name="attribute-targets"></a>屬性目標

屬性的「目標」** 是要套用屬性的實體。 例如，屬性可套用至類別、特定的方法或整個組件。 根據預設，屬性會套用至其後的元素。 但是，舉例來說，您也可以明確地識別是否要將屬性套用到方法、它的參數或它的傳回值。

若要明確地識別屬性目標，請使用下列語法：

```csharp
[target : attribute-list]
```

下表顯示可能的 `target` 值清單。

|目標值|適用於|
|------------------|----------------|
|`assembly`|整個組件|
|`module`|目前的組件模組|
|`field`|類別或結構中的欄位|
|`event`|事件|
|`method`|方法或 `get` 和 `set` 屬性存取子|
|`param`|方法參數或 `set` 屬性存取子參數|
|`property`|屬性|
|`return`|方法的傳回值、屬性索引子或 `get` 屬性存取子|
|`type`|結構、類別、介面、列舉或委派|

您可以指定`field`屬性套用至支援欄位的目標值建立[自動實作屬性](../../../properties.md)。

下列範例示範如何將屬性套用到組件和模組。 如需詳細資訊，請參閱[常見屬性 (C#)](../../../language-reference/attributes/global.md)。

```csharp
using System;
using System.Reflection;
[assembly: AssemblyTitleAttribute("Production assembly 4")]
[module: CLSCompliant(true)]
```

下列範例示範如何在 C# 中將屬性套用至方法、方法參數和方法傳回值。

[!code-csharp[Applying attributes to different code elements](../../../../../samples/snippets/csharp/attributes/AttributesOverview.cs#6)]

> [!NOTE]
> 不論 `ValidatedContract` 定義為有效的目標為何，都必須指定 `return` 目標，即使 `ValidatedContract` 已定義為只套用至傳回值也一樣。 換句話說，編譯器不會使用 `AttributeUsage` 資訊來解析模稜兩可的屬性目標。 如需詳細資訊，請參閱 [AttributeUsage (C#)](../../../language-reference/attributes/general.md)。

## <a name="common-uses-for-attributes"></a>屬性的常見用法

下列清單包含一些程式碼中常見的屬性用法：

- 在 Web 服務中使用 `WebMethod` 屬性標示方法，以表示此方法應該可以透過 SOAP 通訊協定來呼叫。 如需詳細資訊，請參閱 <xref:System.Web.Services.WebMethodAttribute> 。
- 描述在與原生程式碼交互作用時，如何封送處理方法參數。 如需詳細資訊，請參閱 <xref:System.Runtime.InteropServices.MarshalAsAttribute> 。
- 描述適用於類別、方法和介面的 COM 屬性。
- 使用 <xref:System.Runtime.InteropServices.DllImportAttribute> 類別呼叫 Unmanaged 程式碼。
- 針對標題、版本、描述或商標等方面來描述您的組件。
- 描述要將類別的哪些成員序列化以取得持續性。
- 描述如何基於 XML 序列化目的，在類別成員與 XML 節點之間進行對應。
- 描述方法的安全性需求。
- 指定用來強制執行安全性的特性。
- 控制由 Just-In-Time (JIT) 編譯器所進行的最佳化，讓程式碼保持易於偵錯。
- 取得有關方法之呼叫端的資訊。

## <a name="related-sections"></a>相關章節

如需詳細資訊，請參閱：

- [建立自訂屬性 (C#)](creating-custom-attributes.md)  
- [使用反映存取屬性 (C#)](accessing-attributes-by-using-reflection.md)  
- [如何使用屬性建立 C/c + + 等位（c #）](how-to-create-a-c-cpp-union-by-using-attributes.md)  
- [常見屬性 (C#)](../../../language-reference/attributes/global.md)  
- [呼叫端資訊 (C#)](../../../language-reference/attributes/caller-information.md)  

## <a name="see-also"></a>另請參閱

- [C # 程式設計指南](../../index.md)
- [反映 (C#)](../reflection.md)
- [屬性](../../../../standard/attributes/index.md)
- [在 C 中使用屬性#](../../../tutorials/attributes.md)
