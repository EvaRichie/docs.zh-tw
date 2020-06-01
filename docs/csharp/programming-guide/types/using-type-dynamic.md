---
title: 使用 dynamic 類型 - C# 程式設計指南
ms.date: 07/20/2015
helpviewer_keywords:
- dynamic [C#], about dynamic type
- dynamic type [C#]
ms.assetid: 3828989d-c967-4a51-b948-857ebc8fdf26
ms.openlocfilehash: 24d48605e560038d70f1818611f339a94ecc2bba
ms.sourcegitcommit: a241301495a84cc8c64fe972330d16edd619868b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/01/2020
ms.locfileid: "84241964"
---
# <a name="using-type-dynamic-c-programming-guide"></a>使用 dynamic 類型 (C# 程式設計手冊)

C# 4 引進一種新型別 `dynamic`。 此類型是靜態類型，但 `dynamic` 類型的物件會略過靜態類型檢查。 在大多數情況下，其運作會像是具有 `object` 類型。 在編譯時期，會假設類型為 `dynamic` 的項目能夠支援所有作業。 因此，您無須考慮物件是從 COM API、動態語言 (例如 IronPython)、HTML 文件物件模型 (DOM)、反映或是程式其他地方取得其值。 不過，如果程式碼無效，則會在執行階段攔截到錯誤。

例如，如果下列程式碼中的執行個體方法 `exampleMethod1` 只有一個參數，則編譯器會將 `ec.exampleMethod1(10, 4)` 方法的第一個呼叫視為無效，因為它包含兩個引數。 呼叫會造成編譯器錯誤。 編譯器不會檢查 `dynamic_ec.exampleMethod1(10, 4)` 方法的第二個呼叫，因為 `dynamic_ec` 的類型為 `dynamic`。 因此，不會報告編譯器錯誤。 不過，這項錯誤並不是永遠不會被發現。 它會在執行階段被攔截，並造成執行階段例外狀況。

[!code-csharp[CsProgGuideTypes#50](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/usingdynamic.cs#50)]

[!code-csharp[CsProgGuideTypes#56](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/usingdynamic.cs#56)]

上述範例中的編譯器角色，就是將每個陳述式應該對類型為 `dynamic` 的物件或運算式所進行之動作的相關資訊封裝在一起。 在執行階段，會檢查這些預存資訊，如果有任何陳述式無效，便會造成執行階段例外狀況。

大多數動態作業的結果本身就是 `dynamic`。 例如，如果您在下列範例中將滑鼠指標停在 `testSum` 的使用用途上，IntelliSense 會顯示 **(區域變數) dynamic testSum** 類型。

[!code-csharp[CsProgGuideTypes#51](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/usingdynamic.cs#51)]

結果不是 `dynamic` 的作業包括：

* 從 `dynamic` 轉換成另一種類型。
* 包含 `dynamic` 類型引數的建構函式呼叫。

例如，下列宣告中 `testInstance` 的類型是 `ExampleClass`，而不是 `dynamic`：

[!code-csharp[CsProgGuideTypes#52](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/usingdynamic.cs#52)]

下一節＜轉換＞會顯示轉換範例。

## <a name="conversions"></a>轉換

動態物件和其他類型間的轉換很簡單。 因此，開發人員可以在動態和非動態行為之間進行切換。

所有物件都能隱含轉換成動態類型，如下列範例所示。

[!code-csharp[CsProgGuideTypes#53](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/usingdynamic.cs#53)]

相反地，隱含轉換可以動態套用至 `dynamic` 類型的任何運算式。

[!code-csharp[CsProgGuideTypes#54](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/usingdynamic.cs#54)]

## <a name="overload-resolution-with-arguments-of-type-dynamic"></a>dynamic 類型引數的多載解析

如果方法呼叫中有一或多個引數的類型為 `dynamic`，或如果方法呼叫的接收端類型為 `dynamic`，則會在執行階段 (而不是編譯時期) 發生多載解析。 在下列範例中，如果唯一可存取的 `exampleMethod2` 方法已定義為接受字串引數，則將 `d1` 作為引數傳送不會造成編譯器錯誤，但會造成執行階段例外狀況。 多載解析會在執行階段失敗，因為 `d1` 的執行階段類型為 `int`，而 `exampleMethod2` 需要字串。

[!code-csharp[CsProgGuideTypes#55](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/usingdynamic.cs#55)]

## <a name="dynamic-language-runtime"></a>Dynamic Language Runtime

動態語言執行時間（DLR）是在 .NET Framework 4 中引進的 API。 它提供的基礎結構支援 C# 中的 `dynamic` 類型，也支援實作 IronPython 和 IronRuby 之類的動態程式設計語言。 如需 DLR 的詳細資訊，請參閱 [Dynamic Language Runtime 概觀](../../../framework/reflection-and-codedom/dynamic-language-runtime-overview.md)。

## <a name="com-interop"></a>COM Interop

C# 4 包含幾項功能，可改善與 COM API (例如 Office Automation API) 相互操作的體驗。 這些改進包括使用 `dynamic` 類型，以及使用[具名和選擇性引數](../classes-and-structs/named-and-optional-arguments.md)。

許多 COM 方法允許針對引數類型和傳回型別進行變化，方法是將類型指定為 `object`。 這需要對值進行明確轉型，才能與 C# 中的強型別變數配合使用。 如果您使用[-link （c # 編譯器選項）](../../language-reference/compiler-options/link-compiler-option.md)選項進行編譯，則引入型別可 `dynamic` 讓您將 COM 簽章中的出現次數視為 `object` 型別 `dynamic` ，進而避免大部分的轉換。 例如，下列陳述式將比較使用 `dynamic` 類型和不使用 `dynamic` 類型存取 Microsoft Office Excel 試算表中儲存格的方式。

[!code-csharp[csOfficeWalkthrough#12](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csofficewalkthrough/cs/thisaddin.cs#12)]

[!code-csharp[csOfficeWalkthrough#13](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csofficewalkthrough/cs/thisaddin.cs#13)]

## <a name="related-topics"></a>相關主題

|Title|描述|
|-----------|-----------------|
|[動態](../../language-reference/builtin-types/reference-types.md)|說明如何使用 `dynamic` 關鍵字。|
|[動態語言執行時間總覽](../../../framework/reflection-and-codedom/dynamic-language-runtime-overview.md)|提供 DLR 概觀，DLR 是在 Common Language Runtime (CLR) 中新增一組動態語言服務的執行階段環境。|
|[逐步解說：建立和使用動態物件](walkthrough-creating-and-using-dynamic-objects.md)|針對建立自訂動態物件及建立存取 `IronPython` 程式庫的專案，提供逐步指示。|
|[如何使用 C# 功能存取 Office Interop 物件](../interop/how-to-access-office-onterop-objects.md)|示範如何建立使用具名和選擇性引數、`dynamic` 類型，以及其他可簡化 Office API 物件存取之增強功能的專案。|
